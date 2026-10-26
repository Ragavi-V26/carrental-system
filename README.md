# 🚗 APEX DRIVE — CAR RENTAL MANAGEMENT SYSTEM

> **Full-Stack Enterprise College Project**  
> Built with **Java 21**, **Spring Boot 3.3.4**, **Spring Data JPA / Hibernate**, **MySQL 8.0**, and **Modern Responsive Frontend (HTML5, CSS3, JavaScript, Bootstrap 5)**.

---

## 🌟 Project Overview

**Apex Drive** is a production-grade, full-stack Car Rental Management System developed as a college capstone project. It implements a complete end-to-end rental lifecycle:
1. **User Authentication & Authorization**: Secure customer and admin registration/login with BCrypt password hashing and role-based access control (RBAC).
2. **Dynamic Fleet Catalog**: Explore cars with category filters (Hatchback, Sedan, SUV, Luxury), real-time search, sorting, and availability indicators.
3. **Smart Booking Engine**: Prevents double-booking / date overlaps, calculates duration and pricing strictly on the server, and persists transactions in MySQL.
4. **My Bookings & Vehicle Drop-off**: View reservation status, return active vehicles with drop-off notes, and automatically update fleet availability.
5. **Java I/O Reporting**: Download formatted rental invoices and administrative CSV audit reports generated via Java I/O streams (`BufferedWriter`, `ByteArrayOutputStream`).
6. **Administrator Console**: Manage vehicle inventory (Full CRUD), inspect all customer bookings, update rental statuses, and monitor real-time business KPIs.

---

## 🛠️ Technology Stack

| Layer | Technologies |
| :--- | :--- |
| **Backend Language** | **Java 21 LTS** |
| **Framework** | **Spring Boot 3.3.4** (`spring-boot-starter-web`, `data-jpa`, `security`, `validation`) |
| **ORM / Persistence** | **Hibernate / Spring Data JPA** |
| **Database** | **MySQL 8.0+** (`carrental_db`) via `mysql-connector-j` |
| **Password Security**| **BCrypt Password Encoder** |
| **Reporting / I/O**   | **Core Java I/O** (`BufferedWriter`, `OutputStreamWriter`, `ByteArrayOutputStream`) |
| **Frontend**         | **HTML5**, **Modern Automotive CSS3**, **Vanilla JavaScript (ES6+)**, **Bootstrap 5.3**, **Bootstrap Icons** |
| **Build Tool**       | **Maven 3.9+ / Maven Wrapper (`mvnw.cmd`)** |

---

## 🎨 Design System & Theme

Inspired by modern luxury automotive brands:
- **Primary Navy**: `#0B132B` & `#1C2541`
- **Surface Cards**: `#162447` with glassmorphic subtle borders
- **Racing Accent**: `#E63946` (Crimson Red) & `#D62828`
- **Text & Badges**: `#FFFFFF` high-contrast typography, emerald green for available status, amber for active rentals.

---

## 📂 Project Architecture & Package Structure

```
CarRentalManagementSystem/
├── carrental_schema.sql                       # Complete MySQL schema & initial seed data
├── pom.xml                                    # Maven configuration & dependencies
├── mvnw / mvnw.cmd / .mvn/                    # Portable Maven Wrapper
├── README.md                                  # Setup & execution guide
├── JAVA_CONCEPTS_AND_VIVA_GUIDE.md           # In-depth viva questions & OOP concept mapping
└── src/
    ├── main/
    │   ├── java/com/carrental/
    │   │   ├── CarRentalApplication.java      # Application Main Entry Point
    │   │   ├── config/
    │   │   │   ├── SecurityConfig.java        # Security filter chain & BCrypt encoder
    │   │   │   └── DataInitializer.java       # Automatic DB seed on startup (Admin, User, Cars)
    │   │   ├── controller/
    │   │   │   ├── AuthController.java        # Register, Login, Logout, Session check
    │   │   │   ├── CarController.java         # Public car catalog, category filters, search
    │   │   │   ├── BookingController.java     # Booking creation, user history, return, receipts
    │   │   │   └── AdminController.java       # Admin CRUD on fleet, bookings, stats, CSV export
    │   │   ├── dto/
    │   │   │   ├── ApiResponse.java           # Standardized generic JSON response wrapper
    │   │   │   ├── AuthResponse.java          # Authentication payload
    │   │   │   ├── LoginRequest.java          # Input validation for login
    │   │   │   ├── RegisterRequest.java       # JSR-303 input validation for registration
    │   │   │   ├── BookingRequest.java        # Car ID & date inputs with validation
    │   │   │   ├── CarDto.java                # Admin car creation & update DTO
    │   │   │   └── DashboardStatsDto.java     # Admin business KPI metrics
    │   │   ├── entity/
    │   │   │   ├── BaseEntity.java            # Abstract class (OOP Abstraction & Inheritance)
    │   │   │   ├── User.java                  # User entity (Encapsulation, Single-Table inheritance)
    │   │   │   ├── Admin.java                 # Admin entity (Inherits User, demonstrates Polymorphism)
    │   │   │   ├── Car.java                   # Vehicle specifications & inventory entity
    │   │   │   └── Booking.java               # Rental transaction record
    │   │   ├── enums/
    │   │   │   ├── Role.java                  # ROLE_USER, ROLE_ADMIN
    │   │   │   ├── CarCategory.java           # HATCHBACK, SEDAN, SUV, LUXURY
    │   │   │   └── BookingStatus.java         # CONFIRMED, COMPLETED, CANCELLED
    │   │   ├── exception/
    │   │   │   ├── ResourceNotFoundException.java
    │   │   │   ├── BookingConflictException.java
    │   │   │   ├── InvalidBookingDateException.java
    │   │   │   ├── UnauthorizedException.java
    │   │   │   └── GlobalExceptionHandler.java# Centralized @RestControllerAdvice
    │   │   ├── repository/
    │   │   │   ├── UserRepository.java        # Spring Data JPA queries
    │   │   │   ├── CarRepository.java         # Dynamic filter & search JPQL
    │   │   │   └── BookingRepository.java     # Overlapping date detection query
    │   │   └── service/
    │   │       ├── UserService.java           # Interface (Service Abstraction)
    │   │       ├── CarService.java            # Interface
    │   │       ├── BookingService.java        # Interface
    │   │       ├── ReportService.java         # Interface for Java I/O operations
    │   │       └── impl/
    │   │           ├── UserServiceImpl.java   # Implements UserService
    │   │           ├── CarServiceImpl.java    # Implements CarService
    │   │           ├── BookingServiceImpl.java# Implements BookingService
    │   │           └── ReportServiceImpl.java # Java I/O Report generation (Receipt & CSV)
    │   └── resources/
    │       ├── application.properties         # Main configuration
    │       ├── application-local.properties   # Local DB credentials (Gitignored)
    │       └── static/                        # Frontend Web Assets
    │           ├── index.html                 # Hero landing page & showcase
    │           ├── login.html                 # Login page with Quick Demo autofill
    │           ├── register.html              # Account creation page with validation
    │           ├── dashboard.html             # User Dashboard (4 core workflow cards)
    │           ├── cars.html                  # Fleet catalog, category filter, Rent modal
    │           ├── bookings.html              # My Bookings, Return Car dialog, Receipt download
    │           ├── admin.html                 # Admin Console (Fleet CRUD, Bookings, CSV export)
    │           ├── css/
    │           │   └── style.css              # Custom Dark Navy & Red automotive styling
    │           └── js/
    │               └── app.js                 # Global utilities, session state, navigation
```

---

## ⚡ Quick Start & Run Instructions

### Prerequisites
- **Java 21** installed (`java -version`).
- **MySQL Server 8.0+** running on `localhost:3306`.

### Database Configuration
1. The application automatically creates and initializes the `carrental_db` database if not present.
2. Credentials can be passed via environment variables or in `src/main/resources/application-local.properties`:
   ```properties
   spring.datasource.username=root
   spring.datasource.password=YOUR_PASSWORD
   ```

### Running the Application

Using the included Maven wrapper:
```powershell
# Windows
.\mvnw.cmd spring-boot:run
```

Or run the pre-built standalone executable JAR:
```powershell
java -jar target\car-rental-system-1.0.0.jar
```

### Accessing the Web Application
Open your browser and navigate to:
```
http://localhost:8080
```

---

## 🔑 Demo Credentials (Ready for Viva & Testing)
🔑 Demo Login

The application provides demo login options for testing and project demonstration.

Open the login page.
Use the Quick Demo Credentials buttons to fill in the demo login details.
Log in to explore the customer and administrator features.

Security note: Demo credentials are intended for local testing. Do not publish real passwords or sensitive database credentials in this repository.

## 🚀 Verification & Automated Testing

A complete automated test suite is provided in `scratch/test_suite.ps1`.
To re-run all 11 test suites against the live application:
```powershell
powershell -ExecutionPolicy Bypass -File .\scratch\test_suite.ps1
```
Tests verified:
- `Page Availability`: `index.html`, `cars.html`, `login.html`, `register.html`, `dashboard.html`, `admin.html`.
- `Database Connectivity`: MySQL 8.0 queries via Spring Data JPA.
- `Category Filters`: Dynamic filtering across Hatchbacks, Sedans, SUVs, and Luxury.
- `Registration & Login`: BCrypt password hashing & session authentication.
- `Reservation Engine`: Duration & pricing calculated on server.
- `Double-Booking Prevention`: Server rejects conflicting overlapping dates with HTTP 409.
- `Vehicle Return Flow`: Booking status turns COMPLETED, car availability is restored to inventory.
- `Java I/O Verification`: Generated formatted text receipts and CSV spreadsheets.
