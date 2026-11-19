# SmartFarm

**A Web-Based Smart Farming Application Using Laravel and React for Irrigation Prediction**

SmartFarm is a web-based application designed to support agricultural land management, environmental monitoring, and data-driven irrigation decisions. It combines a React frontend, Laravel backend, MySQL database, and a machine-learning prediction service.

The application is connected to the **Smart Agriculture Prediction System**, a related Machine Learning project that develops and evaluates the Random Forest and K-Means models used to support irrigation prediction and land-condition analysis.

## Project Overview

SmartFarm provides a centralized platform for farmers and administrators to manage agricultural information and access irrigation-related insights.

Farmers can manage their farmland and crop information, provide environmental parameters, and review irrigation prediction results. Administrators can manage farmer accounts and monitor agricultural data across the application.

The system is organized into three main parts:

1. **Frontend — React.js:** provides the user interface and communicates with the Laravel backend through HTTP API requests.
2. **Backend — Laravel:** handles application logic, API endpoints, authentication, authorization, request validation, and database operations.
3. **Data and prediction services — MySQL and FastAPI:** MySQL stores application data and prediction history, while FastAPI exposes the machine-learning prediction service. Laravel connects the frontend, database, and prediction service.

## Relationship with Smart Agriculture Prediction System

SmartFarm is the web application implementation related to the **Smart Agriculture Prediction System** Machine Learning project.

The two projects have different but complementary responsibilities:

| Component | Smart Agriculture Prediction System | SmartFarm |
|---|---|---|
| Main focus | Machine Learning development and evaluation | Web application development |
| Random Forest | Model training, tuning, and evaluation | Uses prediction output to provide irrigation recommendations |
| K-Means | Clustering and agricultural-condition analysis | Presents land microclimate zone information |
| Main technologies | Python, Pandas, NumPy, Scikit-learn | Laravel, React, MySQL |
| Prediction interface | Interactive demo deployed on Hugging Face Spaces | Prediction feature integrated into the SmartFarm application through FastAPI |
| Main output | Trained models and analytical results | Agricultural management features and stored prediction history |

The Machine Learning project covers data preprocessing, exploratory data analysis, Random Forest classification, model evaluation, feature importance analysis, and K-Means clustering. The SmartFarm application uses the prediction capability as part of its irrigation simulation and monitoring features.

### Prediction Integration Workflow

1. A farmer enters agricultural parameters in the Smart Irrigation Simulator in the React application.
2. React sends the input to the Laravel backend through an API request.
3. Laravel forwards the prediction request to the FastAPI machine-learning service.
4. FastAPI processes the input using the deployed Random Forest and K-Means models.
5. The prediction results are returned to Laravel.
6. Laravel stores the prediction output in MySQL, including the Random Forest and K-Means results in JSON format.
7. Laravel returns the response to React, which displays the irrigation status, recommendations, and microclimate zone information.

The Hugging Face Spaces demo belongs to the Machine Learning project and demonstrates the model's prediction functionality. It is separate from the FastAPI service used for SmartFarm integration.

## Main Features

### Farmer
- Login and access to the Farmer Dashboard.
- View an overview of farmland, crops, and irrigation status.
- Create, view, update, and delete farmland records.
- Manage crop information associated with farmland.
- View farmland details and environmental information.
- Run irrigation predictions using agricultural and environmental parameters.
- Review previous prediction results.

### Administrator
- Login and access to the Admin Dashboard.
- Manage farmer accounts.
- Monitor registered farmland.
- Review agricultural, sensor, and prediction information.
- View system activity records.

### Smart Irrigation and Land Monitoring
- Simulate irrigation requirements using Random Forest classification.
- Display microclimate zone information based on K-Means clustering.
- Store prediction results and prediction history.
- Present agricultural information through dashboard components and monitoring views.

## Machine Learning Models

SmartFarm integrates two models developed in the related Smart Agriculture Prediction System project.

### Random Forest Classification

Random Forest is used to classify irrigation requirements based on agricultural and environmental input.

The prediction input includes:

- Crop type
- Soil type
- Seedling stage
- Soil Moisture Index (MOI)
- Temperature
- Humidity

The application presents three irrigation outcome classes:

| Class | Interpretation |
|---|---|
| 0 | No Irrigation Required |
| 1 | Irrigation Required |
| 2 | Special Handling Required |

The related Machine Learning project reports the following Random Forest test results:

| Evaluation Metric | Result |
|---|---:|
| Accuracy | 98.44% |
| Macro Precision | 97.98% |
| Macro Recall | 93.51% |
| Macro F1-Score | 95.50% |

These are model evaluation results from the Machine Learning project, not measurements of overall SmartFarm application performance.

### K-Means Clustering

K-Means is used to group agricultural and environmental conditions into three clusters. SmartFarm uses the clustering output to present microclimate zone information in its land monitoring feature.

## Database Design

SmartFarm uses MySQL as its relational database management system. The database contains seven main tables:

| Table | Description |
|---|---|
| `admins` | Administrator account information |
| `users` | Farmer account information |
| `lands` | Agricultural land information |
| `crops` | Crop information associated with farmland |
| `sensors` | Environmental readings, including MOI, temperature, and humidity |
| `predictions` | Random Forest and K-Means prediction results |
| `activities` | Records of important application activities |

The database uses foreign keys and Laravel Eloquent relationships to connect related records.

The main data structure follows the relationship between farmers, their farmland, crops, environmental readings, and prediction records. Activity records can also reference relevant administrators, users, lands, and predictions.

## Technology Stack

| Technology | Purpose |
|---|---|
| PHP 8.x | Backend runtime |
| Laravel 12 | Backend framework and API development |
| Laravel Eloquent ORM | Database models and relationships |
| Laravel Sanctum | API token authentication |
| React 19 | Frontend library |
| Vite 7 | Frontend development and build tool |
| Tailwind CSS | User interface styling |
| Axios | HTTP communication between React and Laravel |
| MySQL 8.x | Relational database |
| Python | Machine-learning service runtime |
| FastAPI | Machine-learning prediction API |
| Random Forest | Irrigation classification |
| K-Means | Agricultural-condition clustering |
| Git | Version control |

## Dataset and Project Scope

The application uses agricultural information based on the **Smart Agriculture Dataset from Kaggle**.

The related Machine Learning project reports that the original dataset contains 16,411 records and 7 columns. After removing 128 duplicate records, 16,283 records remained for analysis.

The SmartFarm application scope includes five crop types:

- Wheat (Gandum)
- Chili (Cabai)
- Tomato (Tomat)
- Potato (Kentang)
- Carrot (Wortel)

The application also supports seven soil types, as defined in the project scope.

SmartFarm focuses on agricultural information management, environmental data monitoring, irrigation prediction simulation, and decision support. It does not include direct integration with physical IoT devices such as real-time sensor hardware, irrigation valves, or pump actuators.

## Getting Started

### Prerequisites

Install the following software before setting up the project:

- PHP 8.x
- Composer
- Node.js 22 or later
- npm
- MySQL 8.x
- Python (for the FastAPI prediction service)
- Git

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-folder>
```

### 2. Install Backend Dependencies

Navigate to the Laravel backend directory:

```bash
composer install
```

Create the environment file:

```bash
cp .env.example .env
```

Configure the database connection in `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=smartfarm
DB_USERNAME=root
DB_PASSWORD=
```

Generate the application key:

```bash
php artisan key:generate
```

Run the database migrations and seeders:

```bash
php artisan migrate --seed
```

To create the database tables without inserting seed data, run:

```bash
php artisan migrate
```

### 3. Install Frontend Dependencies

Navigate to the React frontend directory:

```bash
npm install
```

### 4. Configure the Application Services

Make sure the Laravel backend is configured with the correct MySQL database connection and FastAPI service address.

Configure the frontend API base URL to point to the Laravel backend. Use the environment-variable names and values defined by the actual project source code.

### 5. Start the Laravel Backend

In the Laravel backend directory, run:

```bash
php artisan serve
```

### 6. Start the React Frontend

In the React frontend directory, run:

```bash
npm run dev
```

### 7. Start the FastAPI Prediction Service

Start the FastAPI service using the entry point and dependency configuration provided in the machine-learning service source code.

Make sure the FastAPI service is running and reachable from Laravel before using the irrigation prediction feature.

> The exact FastAPI startup command and environment-variable names depend on the service files and configuration in the repository.

### 8. Access the Application

Open the local URL displayed by Vite in your browser (commonly `http://localhost:5173`).

For the complete prediction workflow, ensure that MySQL, Laravel, React, and FastAPI are running and correctly configured.

## My Contributions

My contribution focused on backend development, database implementation, application security, and service integration.

- Designed the relational database structure and entity relationships using MySQL.
- Developed Laravel migrations, seeders, Eloquent models, and model relationships.
- Implemented authentication, role-based authorization, and middleware.
- Developed CRUD operations and backend request validation.
- Implemented session management for application authentication flows.
- Developed API resource controllers and configured API routes.
- Integrated the React frontend with the Laravel backend.
- Configured the Laravel backend to communicate with the FastAPI machine-learning prediction service.
- Implemented Laravel Sanctum authentication for API access.

## Related Machine Learning Project

The machine-learning models integrated into SmartFarm were developed in the related project:

**Smart Agriculture Prediction System**

The project includes data preprocessing, exploratory data analysis, Random Forest model development and evaluation, feature importance analysis, K-Means clustering, and an interactive prediction demo.

Additional project resources:

- [Crop Irrigation Predictor – Hugging Face Spaces](https://huggingface.co/spaces/Miemey/crop-irrigation-predictor)
- [Original Smart Agriculture Dataset – Kaggle](https://www.kaggle.com/datasets/chaitanyagopidesi/smart-agriculture-dataset)


## Project Information

**Project:** SmartFarm  
**Course:** Web Framework Programming  
**Academic Year:** 2025/2026  
**Study Program:** Information Systems  
**Institution:** Universitas Pendidikan Ganesha

---

*SmartFarm — Integrating Web Development and Machine Learning for Smarter Irrigation Management.*
