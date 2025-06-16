# 🏥 Patient Management API

A **FastAPI**-based RESTful web service to manage patient records. The application allows you to **create**, **retrieve**, **update**, **delete**, and **sort** patient data, including dynamically computed **BMI** and health **verdict**.

## 🚀 Features

* 📄 Add new patients with validations
* 🔍 View all patients or a specific one
* 🔁 Update patient details with automatic BMI and verdict recalculation
* ❌ Delete a patient
* 📊 Sort patients by height, weight, or BMI
* 🧠 Computed fields like BMI and health verdict

---

## 📦 Requirements

* Python 3.8+
* FastAPI
* Uvicorn
* Pydantic

Install dependencies using:

```bash
pip install fastapi uvicorn
```

---

## 📁 Project Structure

```
├── main.py                # FastAPI application
├── patients.json          # JSON file to store patient data
└── README.md              # Project documentation
```

---

## 📌 API Endpoints

### 🏠 Root & Info

#### `GET /`

Returns a welcome message.

#### `GET /about`

Basic information about the API.

---

### 👁️ View Operations

#### `GET /view`

Returns all patient records.

#### `GET /patient/{patient_id}`

Returns data for a specific patient.

* **Path Param**: `patient_id` (e.g., `P001`)

---

### 🔁 Sorting

#### `GET /sort?sort_by=bmi&order=desc`

Returns sorted patient list based on:

* `sort_by`: `height`, `weight`, or `bmi`
* `order`: `asc` (default) or `desc`

Example:

```http
GET /sort?sort_by=height&order=asc
```

---

### ➕ Create Patient

#### `POST /create`

Creates a new patient entry.

**Request Body**:

```json
{
  "id": "P001",
  "name": "John Doe",
  "city": "Mumbai",
  "age": 30,
  "gender": "male",
  "height": 1.75,
  "weight": 70
}
```

Returns: Patient created confirmation.

---

### ✏️ Update Patient

#### `PUT /edit/{patient_id}`

Updates fields for a specific patient.

**Request Body** (partial update allowed):

```json
{
  "age": 35,
  "weight": 75
}
```

Automatically recalculates BMI and verdict.

---

### 🗑️ Delete Patient

#### `DELETE /delete/{patient_id}`

Deletes the patient entry if exists.

---

## 🧠 Data Model

### Patient

| Field   | Type  | Constraints                                     |
| ------- | ----- | ----------------------------------------------- |
| id      | str   | Required, unique                                |
| name    | str   | Required                                        |
| city    | str   | Required                                        |
| age     | int   | >0 and <120                                     |
| gender  | str   | one of `male`, `female`, `others`               |
| height  | float | >0, in meters                                   |
| weight  | float | >0, in kilograms                                |
| bmi     | float | **Computed**                                    |
| verdict | str   | **Computed** (`Underweight`, `Normal`, `Obese`) |

---

## 💡 Notes

* All patient records are stored in a JSON file `patients.json`.
* Computed fields (`bmi`, `verdict`) are derived dynamically using `@computed_field`.
* Duplicate creation using same `id` is restricted.
* Sorting supports missing values gracefully using default 0.

---

## ⚙️ Running the Server

```bash
uvicorn main:app --reload
```

API will be accessible at:
📍 [http://127.0.0.1:8000](http://127.0.0.1:8000)

Interactive docs:
📘 Swagger UI: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
📗 Redoc: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 🛠️ To-Do / Improvements

* [ ] Integrate persistent database (e.g., SQLite, PostgreSQL)
* [ ] Add authentication and authorization
* [ ] Implement pagination for large datasets
* [ ] Add filtering capabilities (e.g., by city, gender)

---

## 👨‍⚕️ Author

**Rahul Khichar**

