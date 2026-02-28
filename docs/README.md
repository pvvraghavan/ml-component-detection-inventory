# 🔌 ML-Powered Electrical Component Detection & Inventory Management

> **Final Year Industry-Sponsored Project** — DY Patil International University  
> **Industry Sponsor:** Kristl Seibt Engineers Pvt. Ltd., Pune, India  
> **Duration:** September 2024 – May 2025

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![YOLOv8](https://img.shields.io/badge/YOLOv8-Object%20Detection-FF6F00?style=flat)
![PyQt6](https://img.shields.io/badge/PyQt6-GUI-41CD52?style=flat&logo=qt&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-ML%20Framework-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-4169E1?style=flat&logo=postgresql&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)

---

## 📌 About the Project

This project automates the interpretation of **electrical design diagrams** using computer vision and machine learning. The system detects and classifies electrical components in real time, validates their connections, and feeds the results into a live desktop dashboard for inventory management and automated BOM (Bill of Materials) generation — replacing what was previously a manual, error-prone engineering process.

Built as a full-stack desktop application using **PyQt6**, the system integrates a fine-tuned **YOLOv8s** detection model with a **PostgreSQL** backend, giving engineers a seamless workflow from image input to exportable BOM output.

The system was developed under a sponsored engagement with **Kristl Seibt Engineers Pvt. Ltd.**, a firm specialising in electrical design automation.

> ⚠️ **Note:** Source code and trained model weights are proprietary to Kristl Seibt Engineers Pvt. Ltd. and cannot be made publicly available. This repository documents the system architecture, design decisions, and outcomes.

---

## 🏗️ System Architecture

![System Flow Diagram](docs/Flow_diagram_Project.png)

The application follows a structured flow from user authentication through ML inference to BOM generation and inventory management. See [`docs/architecture_notes.md`](docs/architecture_notes.md) for a full written breakdown of every module.

---

## 🖥️ Application Screenshots

### Login Window
> Secure user authentication with Sign Up support for new users.

![Login Window](docs/screenshots/Login_Window.jpeg)

---

### View Project Window
> Searchable list of all projects with Windows/Desktop view toggle.

![View Project Window](docs/screenshots/View_Project_Window.jpeg)

---

### View Inventory Dashboard
> Master inventory table aggregating component data across all projects and BOMs. Supports direct in-table editing, CSV export, and live DB sync.

![View Inventory Window](docs/screenshots/View_Inventory_Window.jpeg)

---

## ✨ Key Features

- **Real-time component detection** using a fine-tuned YOLOv8s model trained on electrical design diagrams
- **Connection validation** to verify wiring correctness and flag design inconsistencies
- **Full user authentication** — login, sign up, session management
- **Project management** — create, view, and search projects with multi-BOM support
- **Live PyQt6 dashboard** — inventory master view with direct table editing
- **Automated BOM generation** with component name, part number, and quantity
- **CSV export** for BOMs and inventory data
- **PostgreSQL integration** for structured storage, aggregation, and real-time updates
- **Automated reporting** to support manufacturing and procurement workflows

---

## 🔄 Application Flow (Summary)

```
User Login / Sign Up
      ↓
  Main Window
  ┌──────────────────────────────────────────┐
  │  Create Project  │  View Project          │
  │  View Inventory  │  Logout                │
  └──────────────────────────────────────────┘
      ↓                     ↓                      ↓
Create Project         View Project          View Inventory
  → Input images        → Browse BOMs         → Master component list
  → Run YOLOv8s         → Open BOM details    → Edit & update in-table
  → Generate BOM        → Export CSV          → Export CSV
  → Save to DB          → Update records      → Sync to PostgreSQL DB
```

---

## 📂 Repository Structure

```
ml-component-detection/
│
├── docs/
│   ├── Flow_diagram_Project.png      # Full system flow diagram
│   ├── architecture_notes.md         # Detailed module & design documentation
│   └── screenshots/
│       ├── Login_Window.jpeg
│       ├── View_Project_Window.jpeg
│       └── View_Inventory_Window.jpeg
│
├── requirements.txt                  # Python dependencies
└── README.md
```

> Source code is proprietary. The structure above reflects the actual layout of the private codebase.

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| **ML / Computer Vision** | YOLOv8s (Ultralytics), PyTorch, Scikit-Learn |
| **Data Processing** | Python, Pandas, NumPy |
| **GUI / Dashboard** | PyQt6 |
| **Database** | PostgreSQL, SQL |
| **Visualisation** | Matplotlib, Seaborn |
| **Version Control** | Git |

---

## 📊 Outcomes

- Automated detection and classification of multiple electrical component types from engineering diagrams
- Connection validation reduced manual design interpretation errors
- Automated BOM generation eliminated manual component counting in manufacturing preparation
- Inventory dashboard provided engineers with a real-time, editable master view across all projects
- CSV export enabled direct integration with downstream procurement workflows

---

## 📄 Publication

This work contributed to a research paper accepted at an international conference:

> **"[Paper Title]"**  
> *Vaishnaw G. Kale, Vaishnav V. Prasad*  
> Second International Conference on Artificial Intelligence, Computation, Communication, and Network Security **(AICCoNS 2026)**  
> University of Wollongong in Dubai — Hybrid, April 2026

---

## 👤 Author

**Vaishnav Veeraraghavan Prasad**  
MSc Computing Science — University of Glasgow  
📧 raghavanprasad2003@gmail.com  
🔗 [GitHub Profile](https://github.com/pvvraghavan)

---

## 🏢 Industry Sponsor

**Kristl Seibt Engineers Pvt. Ltd.**  
Pune, India — Specialising in Electrical Design Automation

---

*This project was completed as part of the final year undergraduate programme at DY Patil International University, under industry sponsorship.*
