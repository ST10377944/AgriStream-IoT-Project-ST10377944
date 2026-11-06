# NewRepo
# AgriStream IoT - Real-Time Processing System

## 📌 Project Overview
AgriStream IoT is a cloud-based management web application designed for a company that provides smart monitoring solutions for large-scale commercial farms. The platform is built to reliably process massive surges of telemetry data from soil sensors alongside sudden bursts of high-resolution aerial imagery uploaded by field drones.

This project was developed as part of the **CLDV7112 Practicum** module.

## 🚀 Key Features
*   **Web Hosting:** Deployed via Azure App Service using ASP.NET Core MVC.
*   **User Management:** Secure storage of user accounts and system roles (Farmer, Agronomist, Admin) using Azure SQL Database.
*   **Cloud Storage (Data & Media):**
    *   **Azure Blob Storage:** Stores drone images and farm-related media uploaded via the web app.
    *   **Azure Table Storage:** Stores high-frequency, non-relational telemetry data (sensor readings).
*   **Serverless Data Pipeline:** An event-driven architecture using four Azure Functions:
    1.  **Blob-Trigger:** Logs upload details when a drone image is added to Blob Storage.
    2.  **HTTP GET:** Retrieves the latest telemetry data for the dashboard.
    3.  **HTTP POST:** Accepts irrigation commands and pushes them to a Queue.
    4.  **Queue-Trigger:** Processes irrigation commands from the queue.

## 🛠️ Technologies Used
*   **Framework:** ASP.NET Core MVC (.NET 8)
*   **Cloud Platform:** Microsoft Azure
*   **Database:** Azure SQL Database (Entity Framework Core)
*   **Serverless:** Azure Functions (Isolated Worker Model)
*   **Storage:** Azure Blob Storage & Azure Table Storage (Azure.Data.Tables SDK)
*   **Frontend:** HTML5, CSS3, Bootstrap 5, Razor Pages

## 📂 Repository Structure
*   `AgriStreamWebApp/` - The main MVC web application (Frontend + Database context).
*   `AgriStreamFunctions/` - The serverless Azure Functions project.

---

## 💻 How to Run the Application Locally

### Prerequisites
*   **Visual Studio 2022** (with the "ASP.NET and web development" and "Azure development" workloads installed).
*   **.NET 8.0 SDK**.
*   An active **Azure Subscription** (or Azure for Students).
*   **Azure Resources created:** App Service, Azure SQL Database, Storage Account, and Function App.

### Step 1: Clone and Open the Solution
1. Clone this repository to your local machine.
2. Open the `AgriStreamWebApp.sln` file in Visual Studio.

### Step 2: Configure Connection Strings (Crucial)
You must link the application to your Azure resources.
1. In the **`AgriStreamWebApp`** project, open `appsettings.json` and add your Azure SQL and Azure Storage connection strings:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=tcp:YOUR_SQL_SERVER.database.windows.net,1433;Initial Catalog=AgriStreamDB;User ID=sqladmin;Password=YOUR_PASSWORD;Encrypt=True;TrustServerCertificate=True;",
       "AzureStorage": "DefaultEndpointsProtocol=https;AccountName=YOUR_STORAGE_ACCOUNT;AccountKey=YOUR_KEY;EndpointSuffix=core.windows.net"
     }
   }

   In the AgriStreamFunctions project, open local.settings.json and add the same Storage connection string:

json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "DefaultEndpointsProtocol=https;AccountName=YOUR_STORAGE_ACCOUNT;AccountKey=YOUR_KEY;EndpointSuffix=core.windows.net",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
  }
}
Step 3: Apply Database Migrations
In Visual Studio, go to View > Other Windows > Package Manager Console.

Ensure the Default project dropdown is set to AgriStreamWebApp.

Run the following command to create the SQL tables in Azure:

powershell
Update-Database
Step 4: Run the Azure Functions (Backend)
In Solution Explorer, right-click the AgriStreamFunctions project and select Set as Startup Project.

Press F5 to run. A console window will open, showing the 4 functions are running locally. Keep this window open.

Step 5: Run the Web Application (Frontend)
In Solution Explorer, right-click the AgriStreamWebApp project and select Set as Startup Project.

Press F5 to run. Your browser will open to the local URL (e.g., https://localhost:7234).

You can now use the dashboard to register users, upload drone images, and view live sensor telemetry.

Developed by Sbonakaliso Madlopha - Student Number: ST10377944


