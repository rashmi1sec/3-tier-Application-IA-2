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

First Pull Mongdb images

**Database Image (MongoDB):**

```Pull Image
docker pull mongo:latest
```

```Check Image
docker images
```


![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/9e5315c6-9d63-45d9-bf5f-7b3bbe21337b)

```Run Container
docker run -d -p 27017:27017 --name rashmi-mongo mongo:latest
```

```Check Running Status
docker ps
```
![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/88c9dd72-a546-4013-aacf-7c72f9c68f3e)


**Backend(SpringBoot):**
```.yaml file
# Backend Connectivity with Mongo Docker Container
spring:
  data:
    mongodb:
      database: test
      host: rashmi-mongo
      port: 27017
```

```Modify pom.xml file
# Give FInal Name
<finalName>hotelAPI</finalName>
```

Pick maven Jar and applicatoin will be install as mongodb propeties with Mongodb container



![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/451b800f-6659-43f7-b654-043c4e176f6b)

After Above Steps in Target folder jar will be genrated.

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/552fef27-a535-4677-9a2a-4a28cc71102e)


### Step 3: Creating Dockerfiles

Next, create Dockerfiles for each tier to define the environment and dependencies. Use the following Dockerfile templates as a starting point:

**Frontend (React):**
```Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```
**Backend (Springboot):**
```Dockerfile
FROM openjdk:21
ADD target/hotelAPI.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```




Ensure to install the necessary dependencies and configure the environment in each Dockerfile.

### Step 4: Building Docker Images

Build Docker images for each tier using the `docker build` command. Don't forget to tag the images with appropriate names, including your roll number.

Build Backend Dockerfile


**Backend (Springboot):**
```cmd
# Build Sprignboot Image
 docker build -t staynfeast .

```
**Frontend (React):**
```cmd
# Build React Image
  docker build .


```

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/336510b7-c538-4db1-93b6-d53ab4f94ced)

After done give them name

```cmd
# Give Tag name to React Image
docker tag 109b13ad4ba0 staynfeast-front:latest

```

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/a9eac2f2-46b0-4f3b-ad06-ff42503b343b)

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/be9be744-8acc-4c7c-a11e-f743f6f2e19b)


![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/0acbe247-c84a-4572-9e57-1a1be322943e)


### Step 5: Deploying the Application

Deploy the application using Docker by following these steps:


  


1. **Database Container:**
   - Run the following command to build and run the database container:
     ```bash
     docker run -d -p 27017:27017 --name <database_image_name> mongo:latest
     docker run -d -p 27017:27017 --name rashmi-mongo mongo:latest
     ```
   - Replace `<database_image_name>` with the name of your database Docker image.
  
![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/e3193b89-57b6-47da-bbf2-38a01b386ceb)


2. **Backend Container:**
   - Run the following command to build and run the backend container:
     ```bash
     docker run -p 8080:8080 --name <container_name> --link rashmi-mongo:mongo <backend_image_name>
     docker run -p 8080:8080 --name staynfeast --link rashmi-mongo:mongo staynfeast:1.0
     ```
   - Replace `<backend_image_name>` with the name of your backend Docker image.

3. **Frontend Container:**
   - Run the following command to build and run the frontend container:
     ```bash
     docker run -d --name frontend-container -p 3000:3000 
     docker run -p 3000:3000 --name <conatainer_name> --link staynfeast -d <frontend_image_name>
     docker run -p 3000:3000 --name staynfeast-front --link staynfeast -d staynfeast-front:latest
     ```
   - Replace `<frontend_image_name>` with the name of your frontend Docker image.
  

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/8a8ccbf6-9101-4723-99f2-3737aea9622f)


![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/cf4d34a5-e80e-49ed-9578-541cbb866cd9)


Now, your three-tier application is up and running! You can access the frontend at `http://localhost:3000`.

![image](https://github.com/rashmi1sec/3-tier-Application-IA-2/assets/167959995/69137988-de06-471e-8351-58d61a026eb1)


## Conclusion

Congratulations on setting up a three-tier application using Docker! This architecture provides a scalable and efficient way to develop and deploy applications. Feel free to explore and customize the application further according to your requirements.

Stay tuned for more tutorials and happy coding!
