# 🍕 Mira Food Delivery Bot (FastAPI Webhook)

This project implements a conversational AI agent for a fictional restaurant, "Pandeyji's Eatery," allowing users to place, modify, and track food delivery orders directly through a website chatbot.

The solution is a full-stack integration: the frontend uses HTML/JS, the conversational layer is handled by Dialogflow ES, and the business logic and persistence are managed by a custom Python webhook connected to a MySQL database.

## 🚀 Key Features

  * **Conversational State Management:** Uses Python dictionaries (`inprogress_orders`) to track a user's order items and quantities across multiple conversational turns (Sessions).
  * **Database Integration (Read/Write):** Executes SQL transactions for order placement and status lookups.
  * **Order Fulfillment:** Handles order finalization by writing items, quantities, and a total price to the MySQL database.
  * **Real-time Tracking:** Fetches the current status of an existing order by ID from the database.
  * **Web Integration:** Connects the Dialogflow agent to a static HTML frontend using the Dialogflow Messenger component.

## 💻 Tech Stack & Dependencies

The project relies on the following core components:

| Component | Purpose | Installation Command |
| :--- | :--- | :--- |
| **Python 3.x** | Backend logic execution. | Required Installation |
| **PyCharm** | Development IDE (Recommended). | Required Installation |
| **MySQL Server** | Persistence layer for order history and tracking. | Required Installation |
| **Dialogflow ES** | Conversational AI Agent (Intents & Entities). | Required Installation |
| **FastAPI** | High-performance Python web framework (The Webhook). | `pip install fastapi` |
| **Uvicorn** | ASGI server to run the FastAPI application. | `pip install "uvicorn[standard]"` |
| **MySQL Connector** | Python driver for MySQL database connection. | `pip install mysql-connector-python` |

## 📁 Project Structure

| Folder/File | Purpose |
| :--- | :--- |
| `backend/` | Contains all Python business logic, database helpers, and the FastAPI application. |
| `frontend/` | Contains the static website files (`index.html`) and visual assets (`1.jpg`, etc.). |
| `.gitignore` | Excludes environment and sensitive files (`db_helper.py`, `.venv`). |
| `dialogflow_exports/` | Recommended location for the exported ZIP file of the Dialogflow agent. |

-----

## ⚙️ Installation and Setup Guide

### 1\. Database Setup

1.  Ensure **MySQL Server** is running.
2.  Open **MySQL Workbench** and create the database named: `pandeyji_eatery`.
3.  Create the necessary tables (e.g., `orders`, `order_items`, `order_tracking`, `food_items`). Ensure primary keys and foreign keys are defined for data integrity.

### 2\. Python Environment and Dependencies

1.  **Create Virtual Environment** (in your project directory):
    ```bash
    python -m venv .venv
    ```
2.  **Activate Environment (in PyCharm Terminal):**
    ```bash
    .\.venv\Scripts\Activate.ps1
    ```
3.  **Install Dependencies:**
    ```bash
    pip install fastapi uvicorn[standard] mysql-connector-python
    ```

### 3\. Configure Database Credentials (CRITICAL SECURITY STEP)

**⚠️ The `db_helper.py` file is ignored by Git for security.**

1.  Create a file named **`db_helper.py`** inside your `backend/` folder.
2.  Paste the connection code, replacing the placeholder password with your actual MySQL `root` password:

```python
# db_helper.py (Must be created locally with valid credentials)
import mysql.connector
from mysql.connector import Error

cnx = None
try:
    cnx = mysql.connector.connect(
        user="root",
        password="YOUR_ROOT_PASSWORD_HERE", # <--- UPDATE THIS
        host="localhost",
        database="pandeyji_eatery"
    )
    # Include all other functions (get_order_status, insert_order_item, etc.)
except Error as e:
    print(f"CRITICAL ERROR: Failed to connect to MySQL database: {e}")




