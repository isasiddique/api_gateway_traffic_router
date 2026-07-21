📘 Code Explainer: API Gateway Payload Screening & Traffic Router

This document breaks down the cloud backend load-balancing and routing logic line-by-line for non-technical stakeholders.

1. Ingesting Asynchronous Cloud Traffic
- payload_templates = [...]: This maps out our simulated web socket interface, replicating raw endpoint transactions hitting an enterprise system—tracking sizes, payload string formatting (JSON vs. Malformed XML), and authentication header integrity.
  
- random.choice(payload_templates): This mimics a highly transactional live cloud microservices application processing traffic spikes from around the globe.

2. Algorithmic Traffic Slicing (The Gateway Architecture)
- is_oversized = payload_size > 1000: This line serves as our infrastructure protection gate. It flags any payload over 1 Megabyte to prevent a Distributed Denial of Service (DDoS) attack or an intentional memory overflow payload from hitting internal microservices.

- if is_oversized or is_invalid_format or is_unauthenticated:: This is our structural switch routing matrix. If a request breaches any parameter, the gateway drops its standard destination and dynamically routes it to QUARANTINE_ISOLATION_SERVER with an HTTP 400 Bad Request code, preventing downstream service outages.
