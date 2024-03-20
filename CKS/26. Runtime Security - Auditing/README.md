# [Kubernetes Audit](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

Each request can be recorded with an associated stage. The defined **stages** are:

- **RequestReceived** - The stage for events generated as soon as the audit handler receives the request, and before it is delegated down the handler chain.
- **ResponseStarted** - Once the response headers are sent, but before the response body is sent. This stage is only generated for long-running requests (e.g. watch).
- **ResponseComplete** - The response body has been completed and no more bytes will be sent.
- **Panic** - Events generated when a panic occurred.

The defined **audit levels** are:

- **None** - don't log events that match this rule.
- **Metadata** - log request metadata (requesting user, timestamp, resource, verb, etc.) but not request or response body.
- **Request** - log event metadata and request body but not response body. This does not apply for non-resource requests.
- **RequestResponse** - log event metadata, request and response bodies. This does not apply for non-resource requests.

![Stage and Levels](stage_and_levels.png)
