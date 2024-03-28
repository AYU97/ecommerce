# ecommerce-microservice

- Utilizing an API gateway as a central point of entry, the application seamlessly integrates all services, consolidating endpoints for the `auth`, `order`, and `product` microservices.
- Docker images serve as the deployment mechanism for each microservice, the API gateway, and RabbitMQ, ensuring portability and ease of deployment across various environments.
- Communication between the `product` service and `order` service occurs through RabbitMQ, facilitated by two dedicated queues: `orders` and `products`, streamlining data exchange and enhancing scalability.
- Within the architecture, the `product` service initiates communication by publishing data to the orders queue, subsequently consumed and processed by the `order` service for collation and further action.
- Following the `order` processing, the `order` service publishes relevant details to the `product` queue, enabling the `product` service to retrieve and finalize `order` information, ensuring seamless transaction flow.
- Automated through GitHub Actions, the CI workflow (`test.yml`) orchestrates testing procedures for the auth and product services, ensuring robust code quality and functionality validation upon every push or pull request event.

Tech Stack: Node.js, Express, MongoDB, Docker, RabbitMQ, Mocha, Chai

## Prerequisites

- Have [npm](https://www.npmjs.com) and [Node.js](https://nodejs.dev/en/) on your machine
- Have [Docker](https://www.docker.com) installed
- Have [RabbitMQ](https://www.rabbitmq.com) installed
- Set up your own [MongoDB](https://www.mongodb.com) collection with appropriate security/credential settings

## Steps to run

### On Docker

1. Create a .env file following the format specified in the `/auth/env.example`, `order/env.example` and `product/env.example` directories, following the format specified in each microservice directory
2. Run `docker-compose build`
3. Run `docker-compose up`. Now you can test the APIs from localhost:3003

### On localhost

1. Create a .env file following the format specified in the `/auth/env.example`, `order/env.example` and `product/env.example` directories, following the format specified in each microservice directory
2. Run `npm install` in the `/auth`, `/product`, `/order` and `/api-gateway` directories
3. Run `npm start` on all four directories mentioned in the step above. Now you can test the APIs from localhost:3003
