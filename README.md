
# Swagger Petstore API Automation Framework

## 1. Executive Summary
This repository contains a professional API automation suite for the **Swagger Petstore**, a RESTful web service. The project utilizes **Postman** for script development and **Newman** for headless execution, ensuring continuous validation of backend services.

The framework validates the integrity of data flow across critical modules (Pet, Store, and User), implementing dynamic data chaining and rigorous assertions for Status Codes, JSON Schema, and Response Time.

**Author:** Oynndrila Singh Purkayestha
**Role:** QA Automation Engineer
**Tools:** Postman, Newman, GitHub Actions
**Status:** Active Maintenance

---

## 2. Repository Artifacts
The following files are included in this repository to provide full traceability of the testing cycle:

* **Swagger Petstore.postman_collection.json**
    The core test suite containing sequenced API requests (GET, POST, PUT, DELETE) and JavaScript-based test scripts.

* **Swagger-Petstore.postman_environment.json**
    Configuration file managing dynamic environment variables (Base URL, Pet IDs, Order IDs) to isolate test data.


---

## 3. Test Scope & Functional Coverage
The automation suite verifies the End-to-End (E2E) lifecycle of store entities:

### 3.1 Pet Management (CRUD)
* **Add Pet (POST):** Creates a new pet entry with dynamic naming. Captures the generated \`petId\` for subsequent tests.
* **Find Pet (GET):** Retrieves pet details using the stored \`{{petId}}\`. Validates data accuracy against the creation payload.
* **Update Pet (PUT):** Modifies existing pet status (e.g., "available" to "sold"). Verifies data persistence.
* **Delete Pet (DELETE):** Removes the pet from the registry and confirms \`404 Not Found\` on subsequent retrieval.

### 3.2 Store & User Operations
* **Place Order (POST):** Validates inventory management by placing orders for specific pets.
* **User Management:** Covers user creation, login simulation, and session validation.

---

## 4. Technical Implementation

### 4.1 Dynamic Environment Chaining
Data is passed dynamically between requests to ensure test independence and reduce hard-coding:
* **Base URL:** Centralized endpoint configuration (e.g., \`https://petstore.swagger.io/v2\`).
* **Pet ID:** Runtime-generated ID extracted from the "Create Pet" response.
* **Username:** Dynamic username for user lifecycle testing.

### 4.2 Quality Assurance Assertions
Every request includes strict validation scripts:
* **Status Code:** Validates standard HTTP responses (200 OK, 404 Not Found, 405 Invalid Input).
* **Performance:** Ensures API latency is within acceptable limits (< 1500ms).
* **Schema Validation:** Verifies the JSON structure matches the Swagger specification.

---

## 5. Execution Guide

### 5.1 Manual Execution (Postman GUI)
1.  Import \`Swagger Petstore.postman_collection.json\` and \`Swagger-Petstore.postman_environment.json\`.
2.  Select the **Swagger-Petstore** environment from the top-right dropdown.
3.  Execute the collection using the **Runner**.

### 5.2 Automated Execution (Newman CLI)
To run the suite in a Continuous Integration (CI) environment, use the following commands:

\`\`\`bash
# Install Dependencies
npm install -g newman newman-reporter-htmlextra

# Run Test Suite
newman run "Swagger Petstore.postman_collection.json" -e "Swagger-Petstore.postman_environment.json" -r cli,htmlextra
\`\`\`

---

## 6. CI/CD Pipeline (GitHub Actions)
The repository is configured to run automated tests on every push to the \`main\` branch.
* **Workflow:** \`.github/workflows/petstore-ci.yml\`
* **Outcome:** Automatically installs Node.js/Newman, executes tests, and publishes an HTML Report artifact.

---

## 7. Author
**Oynndrila Singh Purkayestha**
