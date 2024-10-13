# one-traefik-multiple-project

Welcome to the **one-traefik-multiple-project** repository! This project demonstrates how to use a single Traefik Docker container as a reverse proxy for multiple projects, each with different domains. Instead of manually installing and configuring a reverse proxy for a server, you can deploy this pre-configured Traefik container and easily add as many projects with as many domains as you need.

```
root/
├── traefik/
│ ├── docker-compose.yml
├── project-1/
│ ├── docker-compose.yml
├── project-2/
│ ├── docker-compose.yml
├── README.md
└── ... (additional projects)
```

## Table of Contents

- [one-traefik-multiple-project](#one-traefik-multiple-project)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
  - [Getting Started](#getting-started)
    - [1. Clone the Repository](#1-clone-the-repository)
    - [2. Configure Environment Variables](#2-configure-environment-variables)
      - [Traefik Environment Variables](#traefik-environment-variables)
    - [3. Set Up Docker Networks](#3-set-up-docker-networks)
    - [4. Deploy Traefik](#4-deploy-traefik)
    - [5. Deploy Projects](#5-deploy-projects)
      - [Project 1](#project-1)
      - [Project 2](#project-2)
    - [6. Verify the Setup](#6-verify-the-setup)

## Features

- **Single Traefik Instance**: Manage multiple projects with a single Traefik reverse proxy.
- **Automatic HTTPS**: Leverage Let's Encrypt for automatic SSL certificate provisioning.
- **Easy Scalability**: Add as many projects and domains as needed without additional configuration.
- **Docker Compose**: Simplified deployment using Docker Compose for Traefik and each project.

## Prerequisites

Before getting started, ensure you have the following installed on your system:

- [Docker](https://docs.docker.com/get-docker/) (version 20.10.0 or higher)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.27.0 or higher)
- A registered domain name pointed to your server's IP address.
- Open ports `80` and `443` on your server.

## Getting Started

Follow these steps to set up the Traefik reverse proxy and deploy multiple projects.

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/traefik-multi-project-reverse-proxy.git
cd traefik-multi-project-reverse-proxy
```

### 2. Configure Environment Variables

Set up the necessary environment variables for Traefik and each project.

#### Traefik Environment Variables

Create a `.env` file inside the `traefik` directory:

```bash
cp .env.example .env
```

Edit the `.env` file to set your domain and other necessary variables.

```bash
USERNAME=your_admin_username
PASSWORD=your_admin_password
ROOT_DOMAIN=yourdomain.com
ACME_EMAIL=youremail@domain.com
```

**Note:** To generate and set the hashed password in one command for Traefik's HTTP Basic Auth, you can use the following command:

```bash
export HASHED_PASSWORD=$(openssl passwd -apr1 $PASSWORD)
```

For each project, create a `.env` file based on the provided examples.

```bash
ROOT_DOMAIN=yourdomain.com
```

### 3. Set Up Docker Networks

Traefik and the projects need to communicate over a shared Docker network.

```bash
docker network create traefik-network
```

### 4. Deploy Traefik

Navigate to the `traefik` directory and launch the Traefik service using Docker Compose.

```bash
cd traefik
docker compose up -d
```

### 5. Deploy Projects

For each project, navigate to the project directory and launch the service using Docker Compose.

#### Project 1

```bash
cd project-1
docker compose up -d
```

#### Project 2

```bash
cd project-2
docker compose up -d
```

### 6. Verify the Setup

Open your browser and navigate to the domains you've configured. You should see the projects running correctly.
