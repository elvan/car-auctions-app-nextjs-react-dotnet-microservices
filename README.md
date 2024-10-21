# Car Auctions App - Microservices Architecture

## Description

Car Auctions App is a microservices-based platform that facilitates the creation and management of online car auctions. It is designed to be highly scalable, secure, and capable of handling real-time bids using a modern tech stack. The platform is built using multiple microservices, each responsible for distinct functions such as auction management, bidding, user authentication, and search functionality. The application leverages Kubernetes (K8S) for orchestration, Docker for containerization, and gRPC for efficient inter-service communication.

## Features

- **Auction Management**

  - Allows users to create, update, and delete auctions with real-time updates.
  - Provides a detailed view for each auction, enabling the seller to manage bids and auction settings.
  - Integrated with MongoDB for persistence, ensuring scalable data handling.

- **Bidding Service**

  - Enables users to place bids on active auctions.
  - Includes real-time bid updates via SignalR, ensuring users are promptly notified of new bids and auction status changes.
  - Includes gRPC-based communication between services for bid validation and processing.

- **Real-Time Notifications**

  - Implemented with SignalR and RabbitMQ for real-time messaging.
  - Includes toast notifications to alert users of auction activity, bids, and auction conclusions.

- **Search Functionality**

  - Provides advanced filtering options for searching auctions by car make, model, and date.
  - Implements MongoDB for fast and flexible searching of auction items.

- **Authentication and Authorization**

  - Built on IdentityServer4, the platform uses JWT tokens for secure, role-based authentication.
  - Integrated with NextAuth for managing login, logout, and session handling on the frontend.
  - Provides authorization checks for auction actions, ensuring only authenticated users can perform specific tasks.

- **Kubernetes & Docker Integration**

  - Fully containerized using Docker for each microservice with `docker-compose` orchestration.
  - Deployed on Kubernetes with services configured for cluster IP, load balancing, and secure communication via TLS.
  - PersistentVolumeClaims (PVC) are used for managing databases such as PostgreSQL, MongoDB, and RabbitMQ.
  - Let’s Encrypt integration for automatic TLS certificate management in production.

#### Technology Stack

- **Frontend**: Next.js, React, TailwindCSS, Zustand, Flowbite React
- **Backend**: .NET 8.0, ASP.NET Core, gRPC, SignalR, MassTransit
- **Database**: PostgreSQL, MongoDB
- **Messaging**: RabbitMQ, SignalR
- **Containerization**: Docker, Docker Compose
- **Orchestration**: Kubernetes (K8S)
- **Authentication**: IdentityServer4, NextAuth.js
- **Testing**: xUnit, Mongo2Go, MassTransit Test Harness

## Installation

### Prerequisites

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Kubernetes: [Install Kubernetes](https://kubernetes.io/docs/setup/)
- Node.js: [Install Node.js](https://nodejs.org/)

### Environment Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/elvan/car-auctions-app-nextjs-react-dotnet-microservices.git
   cd car-auctions-app-nextjs-react-dotnet-microservices
   ```

2. **Set up environment variables:**

   - Copy the example environment files for each service:
     ```bash
     cp infra/dev-k8s/dev-secrets.yml.example infra/dev-k8s/dev-secrets.yml
     cp appsettings.json.example src/IdentityService/appsettings.json
     ```

3. **Install Dependencies:**

   For Node.js services:

   ```bash
   cd src/WebApp
   npm install
   ```

   For .NET microservices:

   ```bash
   cd src/AuctionService
   dotnet restore
   ```

### Installation Commands

1. **Run Docker Compose for Development:**

   ```bash
   docker-compose -f infra/dev-k8s/docker-compose.yml up --build
   ```

2. **Deploy to Kubernetes:**

   Apply the Kubernetes manifests:

   ```bash
   kubectl apply -f infra/K8S/
   ```

3. **Set up TLS certificates for production:**

   ```bash
   kubectl apply -f infra/prod-k8s/staging-le.yml
   kubectl apply -f infra/prod-k8s/prod-le.yml
   ```

## Usage

Once the application is installed and running, you can interact with the various microservices as follows:

1. **Access the frontend:**

   - Open the browser and navigate to the web app (`http://localhost:3000` for development or the domain set up in production).

2. **Creating Auctions:**

   - Log in to the application.
   - Navigate to the auction creation form, fill in the required details, and submit.
   - Auctions will appear in the listings, and users can place bids in real-time.

3. **Placing Bids:**

   - Select any auction from the list and use the bid form to place a bid.
   - Users will receive real-time notifications of bids and auction status changes.

4. **Monitoring Auctions:**

   - Use the search and filtering features to find auctions based on specific criteria like car make and model.
   - Auction details pages provide real-time updates of the current highest bid, countdown timer, and bid history.
