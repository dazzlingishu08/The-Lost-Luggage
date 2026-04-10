# The-Lost-Luggage
# 🚂 Railway Parcel Tracking System

> *"If I know the parcel number, I should find it in 10 seconds — not 10 minutes."*

A console-based **Parcel Tracking System** built using **Core Java** and **MySQL**, connected via **JDBC**. Developed as part of the DBMS Java Assessment — IEM | UEM Kolkata, April 2026.

---

## 📖 Project Overview

A railway parcel office in Howrah handles hundreds of parcels daily. Parcels are labelled by hand, claim slips are issued on paper, and unclaimed parcels pile up in corners. When a passenger arrives to claim their parcel, staff spend 20+ minutes searching through dusty rows.

This system digitizes the entire parcel management workflow — from registration to status tracking — in a simple console application.

---

## 🛠️ Tech Stack

| Component     | Technology                     |
|---------------|-------------------------------|
| Language      | Core Java (Console Application)|
| Database      | MySQL                          |
| Connectivity  | JDBC (Java Database Connectivity) |
| Input         | Scanner-based console input    |

---

## 📁 Project Structure

```
RailwayParcelTracker/
│
├── src/
│   ├── Main.java           # Menu-driven main application
│   └── DB_Connection.java  # JDBC connection handler
│
├── sql/
│   └── schema.sql          # Database and table creation scripts
│
├── screenshot.png          # Terminal output screenshot
└── README.md               # Project documentation
```

---

## 🗄️ Database Schema

**Database:** `LUGGAGE`

```sql
CREATE DATABASE LUGGAGE;
USE LUGGAGE;

CREATE TABLE parcels (
    parcel_id   INT PRIMARY KEY AUTO_INCREMENT,
    sender      VARCHAR(100),
    receiver    VARCHAR(100),
    destination VARCHAR(100),
    weight_kg   DECIMAL(5,2),
    booked_on   DATETIME DEFAULT CURRENT_TIMESTAMP,
    status      ENUM('booked', 'in transit', 'arrived', 'claimed') DEFAULT 'booked'
);
```

---

## ⚙️ Features

| # | Feature              | Description                                                    |
|---|----------------------|----------------------------------------------------------------|
| 1 | **Register Parcel**  | Add a new parcel with sender, receiver, destination, and weight |
| 2 | **Update Status**    | Change parcel status: `booked → in_transit → arrived → claimed` |
| 3 | **Search Parcel**    | Look up a parcel by ID and view its full details               |
| 4 | **Unclaimed List**   | View all parcels that arrived 3+ days ago and are still unclaimed |
| 5 | **Exit**             | Safely close the application                                   |

---

## 🚀 Getting Started

### Prerequisites

- Java JDK 8 or higher
- MySQL Server (running locally)
- MySQL JDBC Driver (`mysql-connector-java.jar`)

### Setup Instructions

**1. Clone or download the project**

```bash
git clone https://github.com/your-username/railway-parcel-tracker.git
cd railway-parcel-tracker
```

**2. Set up the database**

Open your MySQL client and run:

```bash
mysql -u root -p < sql/schema.sql
```

**3. Configure DB credentials**

Open `src/DB_Connection.java` and update your credentials:

```java
private static final String URL      = "jdbc:mysql://localhost:3306/LUGGAGE";
private static final String USER     = "root";
private static final String PASSWORD = "your_password_here";
```

**4. Compile the project**

```bash
javac -cp .;path/to/mysql-connector-java.jar src/*.java
```

**5. Run the application**

```bash
java -cp .;path/to/mysql-connector-java.jar Main
```

> On Linux/macOS, replace `;` with `:` in the classpath.

---

## 💻 Sample Console Interaction

```
======== PARCEL TRACKER ========
press 1: register parcel
press 2: update status
press 3: search parcel
press 4: view unclaimed (3+ days)
press 5: Exit

Enter your choice: 3
Enter the ID of parcel to Search: 108

SEARCH RESULT...
SENDER: Ram Yadav | RECEIVER: Sita Devi | DEST: Patna | DATE: 2026-03-05 | weight: 3.50 | Status: arrived
```

---

## 🔑 Key Implementation Details

- **PreparedStatement** used for all SQL operations — prevents SQL injection.
- **try-catch** blocks handle all SQL exceptions gracefully.
- **RETURN_GENERATED_KEYS** used after INSERT to display the auto-generated parcel ID.
- Unclaimed parcel query filters using `CURRENT_DATE - INTERVAL 3 DAY` for accurate date comparison.
- All operations are menu-driven with a continuous `while(true)` loop until the user exits.

---

## 📋 Submission Checklist

- [x] `DB_Connection.java` — JDBC connection class
- [x] `Main.java` — Menu-driven main program
- [x] `schema.sql` — CREATE DATABASE + TABLE statements
- [x] `screenshot.png` — Terminal output showing features working
- [x] `README.md` — Project documentation

---

## 📌 Constraints Followed

- ✅ Core Java only — no Spring, Hibernate, or web frameworks
- ✅ JDBC used for MySQL connectivity — no JPA / ORM
- ✅ All operations are menu-driven via console
- ✅ No GUI — Scanner-based input
- ✅ SQL exceptions handled with try-catch
- ✅ PreparedStatement used for all SQL queries

---

## 👨‍💻 Author

**MCA Student — IEM | UEM Kolkata**
DBMS Java Assessment | April 2026
Domain: Transport | Set No: 6

---

> *"A database is not just data. It is the memory of your application. Make it reliable."*
