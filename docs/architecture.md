# Architecture

## Product Choice

**Telegram** — [https://telegram.org](https://telegram.org)

Telegram is a cloud-based messaging platform that supports text messages, media sharing, group chats, channels, and bots. It is known for its speed, cross-platform availability, and security features like end-to-end encrypted secret chats.

## Main components

![Telegram Component Diagram](./diagrams/out/telegram/component-diagram/Component%20Diagram.svg)

[PlantUML source](./diagrams/src/telegram/component-diagram.puml)

I selected the following 6 components from the diagram:

1. **MTProto Gateway (DC Entry)** — the entry point for all client connections. It accepts encrypted MTProto traffic from mobile, desktop, and web apps, terminates the protocol, and routes RPC calls to the appropriate core service inside the data center.

2. **Message Handling Service** — responsible for processing and persisting all messages. It writes messages to the Sharded Chat DB, updates sequence counters in the State Cache, and publishes events to the Event Bus so other services (like Push) can react.

3. **Media & File Service** — handles uploading, storing, and retrieving media files (photos, videos, documents). It streams file chunks to the Distributed File System (DFS) and saves file metadata in the database.

4. **Auth & Session Service** — manages user login and session validation. It verifies sessions on every request, handles phone-number-based login via SMS codes from external providers, and stores session state in the cache and DB.

5. **Notification/Updates Service** — delivers push notifications to users who are offline. It subscribes to new-message events from the Event Bus, looks up device tokens in the cache, and sends notifications through FCM (Android) or APNs (iOS).

6. **Channel/Broadcast Service** — handles fan-out for channels and large groups. It persists posts to the Sharded Chat DB, updates caches, and publishes events so that potentially millions of subscribers can be notified.

## Data flow

![Telegram Sequence Diagram](./diagrams/out/telegram/sequence-diagram/Sequence%20Diagram.svg)

[PlantUML source](./diagrams/src/telegram/sequence-diagram.puml)

I'll describe the "Send Message (with File Ref)" group from the sequence diagram. This is what happens after Alice has already uploaded a photo and now sends it as a message to Bob:

1. The **Mobile App** sends an RPC call `sendMessage(peer=Bob, input_file=file_id_A)` to the **MTProto Gateway**.
2. The **Gateway** forwards the request to the **Auth Service** to validate Alice's session. The Auth Service responds with OK.
3. The **Gateway** then passes the message request to the **Message Service**.
4. The **Message Service** persists the message (both inbox and outbox copies) in the **Sharded Chat DB** and increments the sequence counter (`pts`) in the **State Cache**.
5. The **Message Service** returns a message ID to the **Gateway**, which sends an RPC response back to the app.
6. The **App** updates Alice's UI with a single tick (message sent).

The key data exchanged: the client sends message content + file reference, the Auth Service exchanges session tokens, and the Message Service writes message records to the DB and counter updates to the cache.

## Deployment

![Telegram Deployment Diagram](./diagrams/out/telegram/deployment-diagram/Deployment%20Diagram.svg)

[PlantUML source](./diagrams/src/telegram/deployment-diagram.puml)

Telegram runs its own global infrastructure across multiple data centers. The components are deployed as follows:

- **Client devices** — Telegram apps run on user smartphones (iOS/Android), desktop computers, and web browsers. All clients connect to the backend via the MTProto protocol over TCP or WebSocket.
- **Edge / Connection Layer** — MTProto Gateways and the Bot API Frontend run at the edge of each DC. They handle connection management, protocol termination, and request routing.
- **Compute Cluster** — core services (Auth, Message, Channel, Media, Push) are deployed in containers within a compute cluster, communicating via internal RPC (TL-Schema).
- **Event Bus Cluster** — Kafka (or an internal equivalent) runs on dedicated nodes for async event propagation between services.
- **In-Memory Cluster** — Redis instances hold session state, sequence counters, and frequently accessed data.
- **Storage Cluster** — the Sharded Chat DB (a custom database engine) stores messages and metadata. The Distributed File System stores media files on separate storage nodes.
- **External services** — SMS providers (like Twilio) deliver auth codes, FCM/APNs deliver push notifications, and third-party bot servers connect via HTTPS through the Bot API Frontend.

## Assumptions

- I assumed Telegram uses Kafka or a similar distributed message broker for internal event propagation. The actual implementation might be a custom in-house solution, but the async event-driven pattern likely holds given the scale.
- I assumed media files are stored in a separate distributed file system from the message database. This makes sense for scalability (text and binary data have very different access patterns), but Telegram might use a more unified storage layer internally.

## Open questions

- How does the data flow look like in secret chats? Since secret chats use end-to-end encryption and messages are not stored on the server, the Message Service and DB must handle them very differently from cloud chats.
- How does Telegram handle data center failover and cross-DC replication? If a user's assigned DC goes down, how quickly are they rerouted, and how is message ordering and consistency maintained?
