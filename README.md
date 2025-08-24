# 📦 Sample Node.js Application with Docker Support

This repository contains a Node.js application packaged with Docker and managed via Docker Compose. It allows you to run the application in a containerized environment for easy setup and deployment.

## 📁 Project Structure
```
├── app
│   ├── public
│   │   └── styles
│   │       └── styles.css
│   ├── routes.js
│   └── server
│       └── views
│           └── index.ejs
├── app.js
├── docker-compose.yml
├── Dockerfile
├── Jenkinsfile
├── k8
│   ├── deployment.yaml
│   └── service.yaml
├── package-lock.json
├── package.json
└── readme.md
```


## 🚀 Getting Started

These instructions will get your application up and running using Docker.

### 🛠️ Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) (for local development)
- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/)

### 📦 Build and Run with Docker Compose

1. **Clone the repository**:

```bash
git clone https://github.com/acemilyalcin/sample-node-project.git
cd sample-node-project
```

2. **Start application**

```bash
docker-compose up --build
```

3. **Access the application**

Once the containers are up, you can access the app at: [http://localhost:3000](http://localhost:3000)