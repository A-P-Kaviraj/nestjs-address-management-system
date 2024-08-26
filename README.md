# Address Management System

## Overview

This project is a microservice-based address management system built using NestJS. It includes three microservices:

-   **User Service:** Provides user data.
-   **Address Management Service:** Manages addresses and communicates with the user & email service.
-   **Email Service:** Sends email notifications.

The services communicate with each other using RabbitMQ as the message broker.

## Getting Started

Follow these steps to set up and run the project:

### Prerequisites

-   Node.js (v14 or later)
-   Docker
-   RabbitMQ

### Installation

1.  **Clone the with Submodules:**
   
    To clone the repository with all its submodules, use the following command:
    ```
    git clone --recurse-submodules https://github.com/A-P-Kaviraj/nestjs-address-management-system.git
    ```
    
3.  **Install Dependencies:**
    
    Navigate to each microservice's folder and install the dependencies:
    
    ```
    cd nestjs-address-management-system-address-service
    npm install
    ```
    ```
    cd nestjs-address-management-system-user-service
    npm install
    ```
    ```
    cd nestjs-address-management-system-email-service
    npm install
    ```
4.  **Set Up Email Credentials:**
    
    In the `email.service.ts` file of the email service, configure your email credentials directly:
    ```
    import * as nodemailer from 'nodemailer;
    
    @Injectable()
    export class EmailService {
      async sendEmail(email: string, message: string) {
        const transporter = nodemailer.createTransport({
          service: 'gmail',
          auth: {
            user: 'your-email@example.com',
            pass: 'your-password',
          },
        });
    
        await transporter.sendMail({
          from: '"NestJS App" <your-email@example.com>',
          to: email,
          subject: 'Address Added',
          text: message,
        });
    
        console.log(`Email sent to ${email}`);
      }
    }
   
    
5.  **Start RabbitMQ:**
    
    Use Docker to run RabbitMQ:
    
	   ```
	   docker run -d --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:management
	  ```
    
6.  **Run the Microservices:**
    
    For each microservice, run:
    
    ```
    npm run start
    ```
## Usage

### Address Management Service

To add an address, send a POST request to:

```
POST http://localhost:3000/address/add
Content-Type: application/json

{
  "userId": 1,
  "address": "Give any address you want"
}
```
## Testing Requests

You can use the provided `request.http` file to test the Address Management Service.
Create a `request.http` file:

```
POST http://localhost:3000/address/add
Content-Type: application/json

{
  "userId": 1,
  "address": "Give any address you want"
}
```

### Using VS Code REST Client Extension:

1.  Install the REST Client extension in Visual Studio Code.
2.  Open the `request.http` file and click "Send Request" to execute it.

### Alternative:

You can use Postman to send the POST request by configuring the URL, method, and body as specified above.

## Dependencies

The following dependencies are used in this project:

-   **NestJS:** Framework for building efficient, scalable Node.js server-side applications.
-   **RabbitMQ:** Message broker for communication between microservices.
-   **Nodemailer:** Email sending library for Node.js.
-   **dotenv:** Module for loading environment variables from a `.env` file (if used).

## Notes

-   Make sure RabbitMQ is running and accessible at `localhost:5672`.
-   Ensure that email credentials are correctly configured in `email.service.ts` & `user.service.ts` to enable email functionality.
