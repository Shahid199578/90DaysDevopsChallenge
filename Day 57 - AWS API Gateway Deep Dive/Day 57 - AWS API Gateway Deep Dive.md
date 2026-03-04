# Day 57 - AWS API Gateway Deep Dive

Welcome to **Day 57** of the DevOps 90-Day Challenge!
Today, we dive deep into **Amazon API Gateway**, the front door for your serverless applications. It allows you to create robust REST and HTTP APIs that expose your Lambda functions to the world.

[![](https://img.youtube.com/vi/placeholder/0.jpg)](https://www.youtube.com)

[Watch the video (Link Pending)]()

---

## Objective

By the end of this session, you will:

* Understand the difference between **REST** vs **HTTP** APIs in AWS.
* Create an API that triggers a Lambda function.
* Implement **Query Parameters** and **Path Variables**.
* secure your API using **API Keys** or **Throttling**.

---

## Tools Used

* **Amazon API Gateway**
* **AWS Lambda**
* **Postman** or **Curl** (for testing)

---

## Key Concepts

### 1. Types of APIs
*   **REST API**: Feature-rich. Supports complex validation, transformation, WAF, and private endpoints.
*   **HTTP API**: Newer, faster, and cheaper. Good for simple proxying to Lambda.
*   **WebSocket API**: For persistent, real-time 2-way communication (chat apps).

### 2. Integration Request/Response
API Gateway is a proxy.
*   **Method Request**: Client sends data (GET /users?id=123).
*   **Integration Request**: Gateway maps this data to what Lambda expects (JSON event).
*   **Lambda Processing**: Business logic.
*   **Integration Response**: Lambda returns data.
*   **Method Response**: Gateway formats it for the client (Status 200 OK).

### 3. Deployment Stages
You can't call an API until it's **Deployed**.
You deploy APIs to **Stages** (e.g., `dev`, `test`, `prod`). This allows you to manage different versions of your API simultaneously.

---

## Key Concepts Applied

| Concept | Example Used |
| :--- | :--- |
| **Resources & Methods** | Creating a `/hello` resource and a `GET` method. |
| **Lambda Proxy Integration** | Passing the raw HTTP request directly to Lambda as a JSON object. |
| **CORS** | Enabling Cross-Origin Resource Sharing so your frontend can call the API. |

---

## Bonus (Extra Learning)

*   Set up a **Usage Plan** and **API Key** to limit how many requests a user can make.
*   Import an API definition using **OpenAPI (Swagger)** spec.

---

## Congratulations!

You have successfully exposed your backend code as a web API! You can now build frontends, mobile apps, or command-line tools that interact with your cloud logic.

---

## Try These Next

*   Build a simple **Calculator API** (GET /add?a=5&b=10).
*   Enable **Access Logging** for your API Gateway stage to debug traffic.
