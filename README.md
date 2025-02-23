# Pharmakart

Pharmakart is a comprehensive online pharmacy platform designed to facilitate the purchase of medications. It offers advanced features, including prescription-based medication management, seamless order processing, and automated refill reminders for recurring prescriptions. The platform is built on a microservices architecture, comprising the following core components:

- **Authentication Service (`authentication-svc`)**
- **Product Service (`product-svc`)**
- **Order Service (`order-svc`)**
- **Payment Service (`payment-svc`)**
- **Reminder Service (`reminder-svc`)**
- **API Gateway Service (`gateway-svc`)**
- **Frontend Service (`frontend-svc`)**

## Key Features
- **Prescription-Based Medication Management**: Enables users to securely upload and validate prescriptions for medication orders.
- **Order Processing**: Provides a streamlined interface for users to place and track medicine orders.
- **Product Management**: Enables adding, updating, deleting, and retrieving product details.
- **Order Management**: Handles order creation, retrieval, and status updates.
- **Inventory Integration**: Automatically updates product inventory when an order is created.
- **Payment Processing**: Secure transactions using Stripe, ensuring seamless checkout.
- **Automated Refill Reminders**: Sends timely notifications for recurring medications to ensure uninterrupted treatment.
- **Swagger API Documentation**: Comprehensive API documentation integrated via Swagger for seamless developer interaction.
- **Admin Dashboard**: A centralized administrative interface to manage and monitor application operations using dedicated admin credentials.

## Prerequisites
- Docker installed.
- `make` installed (for running automated script).
- `protoc` installed (for generating protobuf files).
- `npm` installed (for frontend dependencies).
- `stripe` CLI installed (optional, for local stripe tests)
- Visual Studio Code (optional, for development).
- Go installed.

## Getting Started

### 1. Clone the Main Repository
Clone the main repository:
```bash
git clone https://github.com/PharmaKart/pharmakart-web.git
cd pharmakart-web
```

### 2. Clone the Individual Services
Pharmakart is built using multiple services. Clone each service repository into the `pharmakart-web` folder:
```bash
git clone https://github.com/PharmaKart/gateway-svc.git
git clone https://github.com/PharmaKart/authentication-svc.git
git clone https://github.com/PharmaKart/product-svc.git
git clone https://github.com/PharmaKart/order-svc.git
git clone https://github.com/PharmaKart/payment-svc.git
git clone https://github.com/PharmaKart/reminder-svc.git
git clone https://github.com/PharmaKart/frontend-svc.git
git clone https://github.com/PharmaKart/cloud-config.git
```

#### Install protoc-gen-go packages for golang
```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```

#### Generate Protobuf Files
Run the following commands to generate protobuf files for the authentication, product, order, and payment services:

## (Windows)
**If prompted for file or directory, choose file by pressing "F".**
```cmd
cd authentication-svc
make win-proto
```

```cmd
cd ../product-svc
make win-proto
```

```cmd
cd ../order-svc
make win-proto
```

```cmd
cd ../payment-svc
make win-proto
```

```cmd
cd ../reminder-svc
make win-proto
```

## (Others)
```bash
cd authentication-svc
make proto
cd ../product-svc
make proto
cd ../order-svc
make proto
cd ../payment-svc
make proto
cd ../reminder-svc
make proto
```

### 3. Set Up the Services
#### Run `go mod tidy`
Before running the services, ensure dependencies are properly managed:
```bash
cd authentication-svc
go mod tidy
cd ../product-svc
go mod tidy
cd ../order-svc
go mod tidy
cd ../payment-svc
go mod tidy
cd ../reminder-svc
go mod tidy
cd ../gateway-svc
go mod tidy
cd ..
```

#### Install Frontend Dependencies
Navigate to the `frontend-svc` directory and install the required dependencies:
```bash
cd frontend-svc
npm install
cd ..
```

#### Start Stripe forwarder
```bash
stripe login
stripe listen --forward-to localhost:8080/api/v1/payment/webhook
```

### 4. Run the Application
Start the application using Docker Compose:
```bash
docker-compose up --build -d
```

### 5. Set Up the Database
Once the PostgreSQL container is running, execute the `database.sql` script to set up the database:
```bash
docker exec -i pharmakart_db psql -U postgres -d pharmakartdb < database.sql
```

### 6. Access the Application
- **Backend**: Access the backend API at `http://localhost:8080`.
- **Frontend**: Access the frontend application at `http://localhost:3000`.
- **Swagger**: Access the Swagger UI at `http://localhost:8080/swagger/index.html`. Use the following credentials:
  - **Username**: `admin`
  - **Password**: `password`

### 7. Admin Credentials
The admin account is created by the `database.sql` script. Use the following credentials to log in:
- **Username**: `admin`
- **Password**: `password`

### 8. Development Setup (Optional)
For developers using Visual Studio Code, a workspace file is provided to streamline development:
- Open the `pharmakart-workspace.code-workspace` file in Visual Studio Code.
- The workspace is preconfigured with all service folders and a `launch.json` file for debugging.

## Project Structure
- **`authentication-svc`**: Handles user authentication, authorization, and customer management.
- **`product-svc`**: Manages product catalog and inventory.
- **`order-svc`**: Handles order creation, retrieval, and status updates.
- **`payment-svc`**: Processes payments and verifies transactions.
- **`reminder-svc`**: Manages automated medication refill reminders.
- **`gateway-svc`**: Acts as an API gateway for routing requests.
- **`frontend-svc`**: The user interface for the application.
- **`docker-compose.yml`**: Docker Compose file to orchestrate the services.
- **`database.sql`**: SQL script to set up the database schema and admin user.
- **`pharmakart-workspace.code-workspace`**: Visual Studio Code workspace file for development.

## Troubleshooting
- Ensure all service repositories are cloned correctly into the `pharmakart-web` folder.
- Make sure Docker is running and has sufficient resources.
- Check logs for any errors in the Docker containers.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Happy coding! If you have any questions or issues, feel free to open an issue in the repository.

---

