# UdaPeople Project

Welcome to the UdaPeople project, a revolutionary Human Resources concept aimed at helping small businesses better care for their most valuable resource: their people.

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [CI/CD Pipeline](#cicd-pipeline)
- [Built With](#built-with)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The UdaPeople project is built to provide an efficient and user-friendly platform for managing human resources within small businesses. This README file aims to guide you through the project setup, installation, and usage.

## Getting Started

To get started with the UdaPeople project, follow these steps:

1. Clone the repository:
   ```
   git clone <repository-url>
   ```

2. Navigate to the project directory:
   ```
   cd UdaPeople
   ```

3. Set up your environment configuration by copying `config-sample.yml` to `config.yml` and modifying the values as needed.

## Project Structure

The UdaPeople project is organized as follows:

- `backend`: Backend application source code and configurations.
- `frontend`: Frontend application source code and configurations.
- `.circleci`: CircleCI configuration files and Ansible scripts for deployment and server setup.

## Installation

### Backend Installation

1. Navigate to the `backend` directory:
   ```
   cd backend
   ```

2. Install dependencies:
   ```
   npm install
   ```

### Frontend Installation

1. Navigate to the `frontend` directory:
   ```
   cd frontend
   ```

2. Install dependencies:
   ```
   npm install
   ```

## Usage

### Running the Application

1. Start the backend server:
   ```
   cd backend
   npm start
   ```

2. Start the frontend application:
   ```
   cd frontend
   npm start
   ```

## CI/CD Pipeline

The UdaPeople project's CI/CD pipeline is orchestrated through CircleCI. It automates various stages of building, testing, deployment, and infrastructure management. The following is an overview of the pipeline stages and their corresponding jobs:

1. **Build Frontend and Backend**:
   - **Job**: `build-frontend` and `build-backend`
   - **Purpose**: Install dependencies and build the frontend and backend applications respectively.
   - **Dependencies**: None

2. **Test Frontend and Backend**:
   - **Job**: `test-frontend` and `test-backend`
   - **Purpose**: Run tests on the frontend and backend applications.
   - **Dependencies**: `build-frontend`, `build-backend`

3. **Scan Frontend and Backend**:
   - **Job**: `scan-frontend` and `scan-backend`
   - **Purpose**: Perform security scans on the frontend and backend applications.
   - **Dependencies**: `build-frontend`, `build-backend`

4. **Deploy Infrastructure**:
   - **Job**: `deploy-infrastructure`
   - **Purpose**: Deploy backend and frontend infrastructure using AWS CloudFormation templates.
   - **Dependencies**: `test-frontend`, `test-backend`, `scan-frontend`, `scan-backend`

5. **Configure Infrastructure**:
   - **Job**: `configure-infrastructure`
   - **Purpose**: Configure server instances with necessary dependencies using Ansible.
   - **Dependencies**: `deploy-infrastructure`

6. **Run Migrations**:
   - **Job**: `run-migrations`
   - **Purpose**: Run migrations on the backend application.
   - **Dependencies**: `configure-infrastructure`

7. **Deploy Frontend**:
   - **Job**: `deploy-frontend`
   - **Purpose**: Build and deploy the frontend application to an S3 bucket.
   - **Dependencies**: `run-migrations`

8. **Deploy Backend**:
   - **Job**: `deploy-backend`
   - **Purpose**: Build and deploy the backend application to a remote server.
   - **Dependencies**: `run-migrations`

9. **Smoke Test**:
   - **Job**: `smoke-test`
   - **Purpose**: Conduct smoke tests on both frontend and backend applications to ensure successful deployment.
   - **Dependencies**: `deploy-backend`, `deploy-frontend`

10. **CloudFront Update**:
    - **Job**: `cloudfront-update`
    - **Purpose**: Update the CloudFront distribution to reflect the latest deployment.
    - **Dependencies**: `smoke-test`

11. **Cleanup**:
    - **Job**: `cleanup`
    - **Purpose**: Remove old stacks and resources associated with previous deployments.
    - **Dependencies**: `cloudfront-update`

Each job performs specific tasks, contributing to the overall automation of the project's development lifecycle. The pipeline ensures efficient and consistent development, testing, and deployment processes for the UdaPeople project.

Please note that this is a high-level overview, and the details of each job's execution can be found in the provided configuration file.

The pipeline includes:
- Linting and testing of backend and frontend applications.
- Deployment of backend and frontend applications using Ansible scripts.

## Built With

- [Circle CI](www.circleci.com) - Cloud-based CI/CD service
- [Amazon AWS](https://aws.amazon.com/) - Cloud services
- [AWS CLI](https://aws.amazon.com/cli/) - Command-line tool for AWS
- [CloudFormation](https://aws.amazon.com/cloudformation/) - Infrastrcuture as code
- [Ansible](https://www.ansible.com/) - Configuration management tool
- [Prometheus](https://prometheus.io/) - Monitoring tool

## Contributing

Contributions to the UdaPeople project are welcome! Please follow these guidelines when contributing:
- Fork the repository and create a new branch for your feature/fix.
- Commit your changes with clear and descriptive messages.
- Create a pull request, explaining your changes and the problem they solve.

## License

This project is licensed under the [MIT License](LICENSE.md).
