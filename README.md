# 🚀 Vanilla PHP + MariaDB + OracleDB (with Docker)

This project provides a complete development environment using Docker, featuring:

- **PHP** (vanilla, no frameworks)
- **MariaDB** (relational database)
- **OracleDB** (optional second database)

It is designed as a **GitHub template** to quickly start new projects using PHP, CSS, and JavaScript without worrying about local environment setup.

---

## 📦 Requirements

Before starting, make sure you have installed:

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

No prior Docker experience is required!

---

## 🧩 Project Structure

```plaintext
/PHP-vanilla/
│
├── docker/
│   ├── apache-php/
│   │   └── Dockerfile      # PHP + Apache configuration
│   ├── mariadb/
│   └── oracle/
│
├── src/                    # Public files (PHP, CSS, JS)
│   └── index.php
│
├── .env                    # Environment variables (optional)
├── docker-compose.yml      # Docker Compose configuration
└── README.md                # Documentation
```

---

## ⚡ Fast Installation (Step-by-Step)

### 1. Clone this repository

```bash
git clone https://github.com/Sergio-Colque-Ponce/PHP-vanilla.git
cd PHP-vanilla
```

If you are using this project as a template, click **"Use this template"** on GitHub instead of cloning.

---

### 2. Build and start the containers

```bash
docker compose up --build
```

The first build may take several minutes as Docker downloads images.

> If you have an error at any port, you can change the port in .env 
---

### 3. Access your PHP application

Open your browser and navigate to:

```plaintext
http://localhost:8080
```

You should see the PHP application running.

---

## 🛠️ Services and Ports

| Service        | URL/Port          | Description                         |
|----------------|-------------------|-------------------------------------|
| PHP + Apache   | `localhost:8080`  | Main application                    |
| MariaDB        | `localhost:3306`  | MariaDB database server (optional)  |
| OracleDB       | `localhost:1521`  | OracleDB server (optional)          |

---

## 🔄 Live Reloading

- The `/src` folder is mounted into the container.
- Any changes saved (`Ctrl + S`) in the `src/` directory will be **immediately reflected** in your browser.
- No need to rebuild containers for code changes.

---

## 🗄️ Data Persistence

- **MariaDB** uses a named volume (`mariadb_data`) to persist your database information.
- **OracleDB** maintains its own internal data by default.

Data is not lost when you stop containers unless you explicitly remove volumes.

---

## 🧠 Important Notes

### Modifying Docker Configuration

If you make changes to:

- `docker-compose.yml`
- `Dockerfile` (inside `docker/apache-php/`)

You **must** rebuild the containers:

```bash
docker compose up --build
```

---

### Adding PHP Extensions

To add new PHP extensions (e.g., `gd`, `mbstring`, `pdo`):

1. Open `docker/apache-php/Dockerfile`.
2. Add the extension:

```dockerfile
RUN docker-php-ext-install <extension_name>
```

Example:

```dockerfile
RUN docker-php-ext-install mysqli pdo pdo_mysql
```

3. Rebuild the containers:

```bash
docker compose up --build
```

---

### Changing Database Credentials

You can configure database credentials:

1. Modify the `.env` file.
2. Or update the `docker-compose.yml` environment variables.

Example `.env` file:

```dotenv
# MariaDB settings
MARIADB_ROOT_PASSWORD=rootpassword # <-- this is for the root user
MARIADB_DATABASE=mydatabase
MARIADB_USER=myuser
MARIADB_PASSWORD=mypassword
MARIADB_PORT=3306 # <-- CHANGE THIS if you have an error for port
# OracleDB settings
ORACLE_PASSWORD=oraclepassword
ORACLE_PORT=1522 # <-- CHANGE THIS if you have an error for port
```

**Important:** Never push your real `.env` to GitHub.

---

### Stopping the Containers

To stop all running containers:

```bash
docker compose down
```

---

### Cleaning Everything

To stop containers **and** remove all volumes (database data):

```bash
docker compose down --volumes
docker compose up --build
```

---

## 🚀 How to Use this Template for New Projects

1. Click **"Use this template"** button on GitHub.
2. Create a new repository from the template.
3. Clone your new repository:

```bash
git clone https://github.com/your-username/your-new-project.git
cd your-new-project
```

4. Run Docker as usual:

```bash
docker compose up --build
```

5. Start coding in the `/src` folder!

---

## 📜 .gitignore

```gitignore
# Ignore node_modules if using npm
node_modules/

# Ignore environment files
.env

# Ignore Docker volumes
mariadb_data/

# Ignore PHP caches
*.log
*.cache

# Ignore system files
.DS_Store
Thumbs.db
```
