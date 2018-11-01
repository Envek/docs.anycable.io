# Architecture

![](./assets/images/scheme.png)

AnyCable **WebSocket server** (1) is responsible for handling clients, or sockets. That includes:
- low-level connections (sockets) management
- subscriptions management
- broadcasting messages to clients

WebSocket server should include gRPC client built from AnyCable [`rpc.proto`](https://github.com/anycable/anycable/blob/master/protos/rpc.proto).

**RPC server** (2) is a connector between Ruby application (e.g. Rails) and WebSocket server. It’s an instance of your application with a [gRPC](https://grpc.io) endpoint which implements `rpc.proto`.

This server is a part of the [`anycable` gem](./anycable_gem.md).

We use a **Pub/Sub service** (3) to send messages from the application to the WS server, which then broadcasts the messages to clients.

Currently, only Redis is supported as Pub/Sub service.