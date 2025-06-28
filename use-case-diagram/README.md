# 📘 Airbnb Clone – Use Case Diagram

## 🎯 What Is a Use Case Diagram?

A **Use Case Diagram** is a visual representation of the interactions between users (actors) and the system. It shows:
- The **features** the system provides
- The **users (roles)** that interact with those features
- The **goals/actions** those users want to achieve

It is a key part of UML (Unified Modeling Language) and is widely used in software engineering for:
- Clarifying system behavior
- Communicating requirements with stakeholders
- Laying a foundation for development (user stories, APIs, DB schema)

---

## 📌 Purpose of This Diagram

This use case diagram defines how different types of users interact with the **Airbnb Clone** backend system. It:
- Captures **who** does **what**
- Shows system **boundaries and behavior**
- Prepares us for writing **user stories**, developing **backend features**, and applying **role-based access control**

---

## 👥 Actors (System Users)

| Role   | Description                                  |
|--------|----------------------------------------------|
| Guest  | A visitor looking to explore or book a property |
| Host   | A user listing and managing properties       |
| Admin  | A privileged user who oversees the system    |

---

## 🧩 Use Cases and Actions

Below is a breakdown of each use case (system feature), who uses it, and what their action/goal is:

| Feature               | Role   | Action Description |
|-----------------------|--------|--------------------|
| **Search Properties** | Guest  | Find available properties based on location, date, etc. |
| **Sign Up**           | Guest  | Create an account to access full platform functionality |
| **Book Property**     | Guest  | Reserve a selected property for specific dates |
| **Leave Review**      | Guest  | Submit feedback after staying at a property |
| **Manage Listings**   | Host, Admin | Add, edit, or remove property listings |
| **Manage Bookings**   | Host, Admin | View and manage guest bookings (approve, cancel) |
| **Respond to Reviews**| Host, Admin | Reply to guest feedback on properties |
| **Process Payments**  | Admin  | Handle transactions and financial flows |
| **User Management**   | Admin  | Create, update, or deactivate user accounts |
| **Send Notifications**| System (automated) | Alert users about events like confirmations or cancellations |

---

## 🗂️ Files in This Directory

```bash
use-case-diagram/
├── use.drawio.png   # Use Case Diagram (image)
└── README.md        # This documentation file
