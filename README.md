# WolkeSieben Tiervermittlung

<!-- ## Load Balancing and Custom Domains

1. Reserve static address via VPC network > Reserve static address
2. Create a load balancer via Network services > Load balancing > Create load balancer:

- From Internet to My VMs
- Backend configuration > Backend services > Create a backend service
  - Backend type > Serverless network endpoint group
  - Backends > New network endpoint group > -->

## Motivation & Idea [Savina]

- Tiervermittlung.de is crap
- Screenshots of UI (choose singlar + remaining in appendix)
- Why leverage cloud computing? Comparison to alternative hosting methods

## Architecture Overview [Arne]

- DDD / Strategy Pattern
- Microservices allow for independent component development by different teams
  - Swagger documentation available for each service
- Architecture diagram with component explanation, i.e. separation of concerns

## Frontend [Klaus]

- Deployment target: Cloud CDN
  - Comparison to other hosting methods (pro/con)
- Ionic/Angular Stack > ready for mobile
  - Easy-to-use WebSocket adapter
- Google OAuth login flow

## App Microservice [Arne]

- Deployment target: Cloud Run
- Framework: Django
  - SQL abstraction via built-in ORM
  - Includes DB migrations/admin panel/REST browser
  - Built in concepts for hardening / production mode
- Database: CloudSQL (MySQL) + Storage Bucket
  - No official Google Storage emulator (more complicated testing)
- REST API for basic features and user management
- Google OAuth verification and exchange to custom JWT

## Like & Chat Microservice [Nik]

- Framework: NestJS (Node.JS) > comparison to Django
- Monorepo setup with separate deployment targets
- Authentication through app microservice > should use public key cryptography in future to avoid unnecessary REST calls

### Like

- Deployment target: App Engine > comparison to Cloud Run
- Storage: BigTable (emulator available but not fully usable)

### Chat

- Deployment target: Cloud Run
- Storage: Firestore (emulator available)
- WebSocket authentication > not usable in upgrade request due to limited browser WebSocket API

## Recommender Cloud Function [Savina]

- Deployment target: Cloud Functions > benefits? when is it most cost efficient (high/low traffic)?
- Concept of using a dedicated DB view (vs. implementation of REST call [time-constraints])
- Trigger via PubSub > benefit to other trigger methods?
  - Explain publishing via Google PubSub client form App Microservice
- Async nature of recommendation (not time critical or required to synchronous response when creating a new offer)
- Service token authentication (B2B communication)

## Security [Savina]

- Use table of attack vectors and detail how a protection mechanism was implemented

## Scaling [Klaus]

- Load Balancer setup with serverless network endpoint groups > enables individual scaling
- Services and buckets may be deployed to multiple regions > LB decides which is the closets
  - Some cloud resources must be in the same region in order to communicate > implications?
- Message broker for Chat microservice [Nik]
- Stateless REST enables horizontal scaling

## Continuous Integration / Continuous Delivery [Arne/Nik]

- Docker-native development > couples code with deployment image
- GitHub Actions
- Deployment specification via service YAMLs
- Problem: no SSH session to containers

## Cost Analysis [Klaus]

- Cost per month in relation to requests / users per month

## Appendix

- Swager Docs (JSON export / links to production)
- Screenshots
- Larger architecture diagrams
- Individual service diagrams
- [Google Cloud specific deployment diagram](https://cloud.google.com/icons)
