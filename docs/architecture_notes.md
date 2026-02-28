# Architecture Notes

## System Overview

The application is a **desktop-based ML pipeline and inventory management system** built with PyQt6. It combines a YOLOv8s computer vision backend with a structured GUI frontend, backed by a PostgreSQL database. The system is designed to automate electrical component detection from design diagrams and manage the resulting Bills of Materials (BOMs).

---

## Application Flow

The full user journey is documented in the flow diagram (`docs/flow_diagram.png`). Here is a written breakdown:

### 1. Authentication Layer
- On launch, the user is presented with a **Login Window**
- **New users** can register via the Sign Up flow → once account is created, they are redirected back to login
- **Existing users** log in directly
- A **Login Status** check is performed:
  - `False` → Error message is shown, user retries
  - `True` → User proceeds to the Main Window
- Users can **Logout** from the Main Window, which returns them to the Login screen

### 2. Main Window
The central hub of the application with four primary actions:

| Action | Description |
|---|---|
| **Create Project** | Start a new project and trigger the ML detection pipeline |
| **View Project** | Browse and open previously created projects and their BOMs |
| **View Inventory** | See a master inventory list across all projects |
| **Logout** | Return to the login screen |

---

## Module Breakdown

### Create Project Flow
1. User fills in:
   - Project Name
   - Project Creation Date
   - Path to the folder containing input images
2. Clicks **Next** → navigates to the **BOM Generation Window**
3. BOM Generation Window:
   - Fetches project details from PostgreSQL DB
   - User inputs a BOM Name
   - Clicks **Generate BOM** → triggers the **Detection Engine** (YOLOv8s)
   - Detection Engine outputs:
     - **Final Bill** — structured component list
     - **Detection Engine Output** — raw model results
   - BOM is saved back to the DB
4. Additional options: **View Images**, **Export CSV**, **Back to Main Window**
5. Project details can be updated at any time, syncing changes to the DB

### View Project Flow
1. Displays a **searchable table** of all projects created by the user
2. Supports filtering by **Windows / Desktop** view toggle
3. User selects a project → opens **BOM List View Window**:
   - Shows all BOMs associated with the selected project
4. User selects a BOM → opens **BOM View Window**:
   - Displays component name, part number, and quantity
   - Options: **Download CSV**, **Update BOM**, **Back**

### View Inventory Flow
1. Opens the **Inventory Dashboard**
2. Displays a master-list of all components and their quantities across all BOMs/projects
3. Table columns: BOM Name, Project Name, Created On, Priority, Status
4. Bills can be **edited directly in the table view**
5. Clicking **Update** saves changes to the PostgreSQL DB
6. **CSV export** is available — the bill is downloaded by the user
7. Options: **Update**, **Back**, **Refresh**

---

## Database Design

**Database:** PostgreSQL

The application uses PostgreSQL for persistent storage of all project, BOM, and inventory data. Key data entities:

- **Users** — authentication credentials
- **Projects** — project metadata (name, date, image folder path)
- **BOMs** — bill of materials linked to projects (BOM name, creation date, status, priority)
- **BOM Items** — individual component entries (component name, part number, quantity)

All CRUD operations are performed via SQL queries through Python's database adapter. The inventory dashboard aggregates data across all projects in a single master view.

---

## ML Detection Engine

- **Model:** YOLOv8s (fine-tuned on electrical component diagrams)
- **Framework:** PyTorch (via Ultralytics)
- **Input:** Folder of electrical design diagram images
- **Output:**
  - Detected component classes and bounding boxes
  - Confidence scores per detection
  - Aggregated component counts → used to populate BOM

### Pipeline Steps
1. Images are loaded from the user-specified folder path
2. YOLOv8s runs inference on each image
3. Connection validation logic checks for wiring consistency
4. Detection results are aggregated into component counts
5. BOM is generated from the aggregated data and stored in PostgreSQL

---

## Tech Stack Summary

| Layer | Technology |
|---|---|
| GUI Framework | PyQt6 |
| ML Model | YOLOv8s (Ultralytics) |
| Deep Learning | PyTorch |
| Data Processing | Python, Pandas, NumPy |
| Database | PostgreSQL |
| Visualisation | Matplotlib, Seaborn |
| Version Control | Git |

---

## Key Design Decisions

**Why PyQt6 for the GUI?**
PyQt6 provides a native desktop experience with rich table and form widgets, making it well-suited for an engineering tool that requires real-time data display and direct table editing without a web server.

**Why YOLOv8s?**
The `s` (small) variant of YOLOv8 offers a strong balance between detection accuracy and inference speed, which was important for processing multiple diagram images efficiently on standard hardware.

**Why PostgreSQL?**
Structured relational storage was chosen over flat files to support multi-project, multi-BOM queries, inventory aggregation across projects, and direct in-place record updates from the dashboard.

---

*This document reflects the architecture of the system as implemented during the sponsored project engagement with Kristl Seibt Engineers Pvt. Ltd., September 2024 – May 2025.*
