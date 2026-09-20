# Restful Booker API Test Automation Suite

Automated End-to-End (E2E) API testing suite for the [Restful Booker API](https://restful-booker.herokuapp.com/), built using **Postman**, **Newman CLI**, and **htmlextra** reporter.

## 📌 Project Overview
This project validates the authentication and CRUD lifecycle of the Restful Booker booking management system. It automatically extracts session tokens and dynamically passes booking IDs across requests to ensure seamless E2E integration verification.

## 🛠️ Tech Stack & Tools
* **Postman**: API Request design, dynamic test script creation, and assertions.
* **Newman**: Command-line runner for Postman collections.
* **newman-reporter-htmlextra**: Detailed, interactive HTML reporting tool.
* **Node.js**: Environment runtime.

## 📊 Data-Driven Testing (DDT)
This suite leverages dynamic data decoupling via external JSON data sources (`booking_data.json`).
* **Multi-Iteration Coverage**: Runs the full suite against multiple user profiles (e.g., `Sherif`, `Esraa`) without duplicating request logic.
* **Dynamic Placeholders**: Request bodies utilize Postman environment variables (`{{firstname}}`, `{{lastname}}`, etc.) populated automatically per iteration.

## 🧪 Test Scenarios Covered

### 🟢 Positive Scenarios (Happy Path & CRUD)
* **Authentication**: Generate dynamic access tokens (`/auth`).
* **Create Booking**: Create new booking records and extract `bookingid` dynamically.
* **Get Booking**: Fetch details using path variables (`/booking/:id`).
* **Update Booking**: Full update of booking details (`PUT`).
* **Partial Update**: Partial modification of booking properties (`PATCH`).
* **Delete Booking**: Purge booking records (`DELETE`).

### 🔴 Negative Scenarios (Edge Cases & Authorization)
* **Partial Update with Invalid Token**: Verify `403 Forbidden` response when modifying data without valid credentials (`PATCH`).
* **Delete Booking with Invalid Token**: Verify authorization rules deny deletion attempts using corrupted/missing tokens (`DELETE`).

## 🚀 How to Run the Suite

### Prerequisites
* Node.js installed on your machine.
* Newman & htmlextra installed globally:
```bash
  npm install -g newman newman-reporter-htmlextra
### Execution Steps

 **Clone the repository:**
```bash
npm install -g newman newman-reporter-htmlextra
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
npx newman run "Restful Booker E2E Testing.postman_collection.json" -e "Restful Booker Env.postman_environment.json" -d "booking_data.json" -r cli,htmlextra