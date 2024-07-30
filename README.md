# Automating Java Web Application Deployment with Ansible

## Table of Contents

- [Introduction](#introduction)
- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Steps Involved in Automation](#steps-involved-in-automation)
  - [User and Directory Setup](#user-and-directory-setup)
  - [Database and Dependencies](#database-and-dependencies)
  - [Application and Proxy Setup](#application-and-proxy-setup)
  - [Logging Configuration](#logging-configuration)
- [Deployment Instructions](#deployment-instructions)


## Introduction

This project demonstrates the automation of deploying a Java Spring Boot web application using Ansible. The automation process includes setting up the necessary environment, installing dependencies, configuring the application, setting up a reverse proxy, and managing logs.

## Project Overview

This Ansible project automates the deployment and configuration of a Java Spring Boot web application with PostgreSQL and Nginx on a remote Ubuntu 22.04 server. The playbook handles:

- User and directory setup
- Dependency installation
- Database configuration
- Application deployment
- Nginx reverse proxy setup
- Logging configuration

## Prerequisites

To get started with this project, ensure you have the following:

- Ansible 2.9+
- A remote Ubuntu 22.04 server
- Java 11+
- Maven 3.6+
- PostgreSQL 12+
- Nginx 1.26+
- Git


## Steps Involved in Automation

### User and Directory Setup

The first step involves setting up a dedicated user and directory for the application. The playbook:

- Creates a user named `hng` with sudo privileges.
- Clones the `devops` branch of your repository into the `/opt` directory on the remote server.
- Ensures the directory is owned by the `hng` user.

### Database and Dependencies

Next, the playbook handles the installation and configuration of the database and other dependencies:

- Installs PostgreSQL and creates the required database and user.
- Saves the admin credentials in a secure location.
- Installs necessary dependencies like Java, Maven, and any messaging queues required by the application.

### Application and Proxy Setup

The application is then configured and deployed:

- Ensures the Spring Boot application is built and runs on `127.0.0.1:3000`.
- Installs and configures Nginx to reverse proxy requests from port `80` to the application, ensuring it is accessible externally.

### Logging Configuration

Finally, the playbook sets up logging to capture application logs:

- Creates a directory for log files.
- Configures stderr logs to be saved in `/var/log/stage_5b/error.log` and stdout logs in `/var/log/stage_5b/out.log`.
- Ensures both log files are owned by the `hng` user.

## Deployment Instructions

1. **Clone the repository:**

   ```sh
   git clone https://github.com/yourusername/ansible_project.git
   cd ansible_project
   ```

2. **Create a `innventory.cfg` file:**

   Create a `innventory.cfg` file in the root directory of the project.
     ```
    [hng] # host groups
    0.0.0.0 #server ip. can be more than one
   ```

4. **Run the Ansible playbook:**

   ```sh
    ansible-playbook -i inventory.cfg main.yml -b
   ```

## Troubleshooting

If you encounter any issues during deployment, increase the verbosity of the Ansible playbook execution by using the `-vvv` option:

```sh
ansible-playbook -i inventory.cfg main.yml -b -vvv
```

Refer to the error messages and logs for more details on resolving issues.

