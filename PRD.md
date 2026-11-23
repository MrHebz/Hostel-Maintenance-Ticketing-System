# Product Requirements Document (PRD)

Project Title: Hostel Facility & Maintenance Ticketing System  
Course: BU-COS 209  
Group: 9 [Navy Croc]  
Version: 1.0

---

## 1. Problem Statement & Overview

### 1.1 The Problem
Maintenance issues in campus hostels (faulty ceiling fans, leaking pipes, shocking sockets, broken door locks) are currently reported verbally to hall porters or hall senators, or written in physical logbooks at the desk. This causes:
- **Lost Requests:** Verbal complaints get forgotten during shift changes or busy periods.
- **No Tracking:** Students have no idea if their issue has been logged or when a technician will arrive.
- **Duplicate Complaints:** Roommates often report the same fault separately to different porters or senators.

### 1.2 Who Has This Problem
- **Students:** Live with broken facilities for days and waste time following up at the lodge.
- **Porters & Hall Senators:** Handle day to day hall welfare and operations, struggling to keep track of scattered verbal/WhatsApp complaints across hundreds of rooms.
- **Maintenance Technicians:** Lack a clear, prioritized task list with accurate room details.

---

## 2. Surveys and Interviews

### 2.1 Survey Statistics
- **Total People Interviewed:** 16 students
- **Average Wait Time for Repairs:** 14.5 days (ranging from 2 days for resolved plumbing to 4 weeks for unresolved electrical issues)
- **Percentage of Unresolved/Delayed Issues:** 50% (8 out of 16 students still waiting after 3 to 4 weeks)

### 2.2 Interview Notes
- **Student 1:** Stated that the plumber came 2 days after he complained and was impressed with the speed of repairs.
- **Student 2:** Stated that no action has been taken since he complained about the electrical issues in his room.
- **Porter / Hall Senator:** A porter stated that with the large volume of complaints across the hostel, getting repairs completed takes time.

### 2.3 Why Current Solutions Fall Short
- **Paper Logbooks at the Lodge:** Can get misplaced, hard to search, and give zero feedback to students.
- **Verbal / WhatsApp Reports to Senators:** Informal messages get buried under other hall announcements and lack accountability.

---

## 3. Proposed Solution & MVP Scope

A simple backend ticketing system that tracks every hostel maintenance request from the moment a student reports it until a technician fixes it and the student confirms it is done.

### Core Features
1. **Simple Ticket Creation:** Students log a complaint for their room by picking a category (**Electrical**, **Plumbing**, **Carpentry**, **Other**), adding a short description, and setting urgency (**Normal** or **Urgent**).
2. **Duplicate Prevention:** If an open ticket already exists for the same room and issue category, the system blocks duplicate entries and shows the existing ticket's progress instead.
3. **Clear 4-Step Pipeline:** Every ticket moves through four simple stages:
  - **1. Pending:** Student has submitted the complaint.
  - **2. Assigned:** A Porter or Hall Senator has verified the issue and assigned it to a technician.
  - **3. Fixed:** The technician has completed the repair.
  - **4. Closed:** The student confirms the repair works properly.

---

## 4. User Roles & What They Can Do

Instead of complex permission tables, the system has three straightforward roles:

- **Student:**
  - Can submit a new maintenance ticket for their own room.
  - Can view the current stage of their room's tickets.
  - Can mark a **Fixed** ticket as **Closed** once they verify the work is done.

- **Porter / Hall Senator:**
  - Can see all tickets submitted across their assigned hostel.
  - Can verify complaints and assign them to the right technician.
  - Can flag urgent issues or close tickets if a student forgets to confirm after 48 hours.

- **Maintenance Technician:**
  - Can only view tickets assigned directly to them.
  - Can update a ticket's stage from **Assigned** to **Fixed** once the repair is completed.

---

## 5. Backend Logic & Data Design (Language-Agnostic)

### 5.1 What Data It Store
- **Users:** ID, Matric/Staff Number, Full Name, Role (**Student**, **Porter_Senator**, **Technician**), Hostel, Room Number
- **Tickets:** Ticket ID, Student ID, Hostel, Room Number, Category, Urgency, Description, Stage (**Pending**, **Assigned**, **Fixed**, **Closed**), Assigned Technician ID, Date Created
- **History Logs:** Log ID, Ticket ID, Updated By, Previous Stage, New Stage, Timestamp

### 5.2 Key Rules the Backend Enforces
- **No Skipping Stages:** A ticket must follow the order (**Pending** -> **Assigned** -> **Fixed** -> **Closed**). A technician cannot mark a ticket **Fixed** before a Porter or Senator assigns it.
- **No Double-Assignment:** If a Porter and a Hall Senator try to assign the same ticket at the exact same second, the system accepts the first one and notifies the second person that it is already assigned.
- **Auto-Close Timer:** If a student doesn't confirm a **Fixed** ticket within 48 hours, the system automatically moves it to **Closed**.

---

## 6. Benefits
- Faster assignment of reported issues compared to paper logbooks.
- Zero lost maintenance requests across hostel shift changes.