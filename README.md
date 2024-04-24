# 3-tier-Application-IA-2

This repository contains the code for a three-tier application built using Docker, with a multi-container setup. The application includes a frontend developed with React, a backend powered by Spring Boot, and a MongoDB database.

In this i used My already built project of Advanced Web Technoloy.

## Technologies Used

- Frontend: React
- Backend: Spring Boot
- Database: MongoDB
- Docker

## Docker Setup

### Step 1: Setting up the GitHub Repository

To get started, create a new GitHub repository to host the project. Follow these steps:

1. Sign in to GitHub and navigate to your dashboard.
2. Click on the "New" button to create a new repository.
3. Choose a name for your repository (e.g., "3-tier-Application-IA-2") and add an optional description.
4. Select "Public" or "Private" as per your preference.
5. Check the box to initialize the repository with a README.
6. Click on the "Create repository" button to finalize.

Once the repository is created, clone it to your local machine using the `git clone` command.

### Step 2: Designing the Architecture

Before proceeding with Docker, design the architecture of your application. We'll have three containers:

1. Presentation Tier (Frontend): React
2. Application Tier (Backend): Spring Boot
3. Data Tier (Database): MongoDB

### Step 3: Creating Dockerfiles

Next, create Dockerfiles for each tier to define the environment and dependencies. Use the following Dockerfile templates as a starting point:

**Frontend (React):**
```Dockerfile
# Frontend Dockerfile
```

**Backend (Spring Boot):**
```Dockerfile
# Backend Dockerfile
```

**Database (MongoDB):**
```Dockerfile
# Database Dockerfile
```

Ensure to install the necessary dependencies and configure the environment in each Dockerfile.

### Step 4: Building Docker Images

Build Docker images for each tier using the `docker build` command. Don't forget to tag the images with appropriate names, including your roll number.

### Step 5: Deploying the Application

Deploy the application using Docker by following these steps:

1. **Frontend Container:**
   - Run the following command to build and run the frontend container:
     ```bash
     docker run -d --name frontend-container -p 3000:3000 <frontend_image_name>
     ```
   - Replace `<frontend_image_name>` with the name of your frontend Docker image.

2. **Backend Container:**
   - Run the following command to build and run the backend container:
     ```bash
     docker run -d --name backend-container -p 8080:8080 <backend_image_name>
     ```
   - Replace `<backend_image_name>` with the name of your backend Docker image.

3. **Database Container:**
   - Run the following command to build and run the database container:
     ```bash
     docker run -d --name db-container -p 27017:27017 <database_image_name>
     ```
   - Replace `<database_image_name>` with the name of your database Docker image.

Now, your three-tier application is up and running! You can access the frontend at `http://localhost:3000`.

## Conclusion

Congratulations on setting up a three-tier application using Docker! This architecture provides a scalable and efficient way to develop and deploy applications. Feel free to explore and customize the application further according to your requirements.

Stay tuned for more tutorials and happy coding!
