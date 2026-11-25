# Product Requirements Document (PRD)

Project Title: Hostel Facility & Maintenance Ticketing System  
Course: BU-COS 209  
Group: 9 [Navy Croc]  
Version: 1.0

---

## 1. Product Overview
- **What is the product?:** A centralized backend ticketing web application designed for campus hostels to log, track, assign, and resolve student maintenance complaints (such as electrical faults, plumbing leaks, and broken bed frames).
- **Core Purpose:** To replace informal paper logbooks and scattered verbal or WhatsApp chats with an accountable and structured digital pipeline.

---

## 2. Problem Statement
- **What problem are we solving?:** Maintenance issues in campus hostels suffer from severe tracking failures. Students face long unacknowledged delays (averaging 14.5 days based on 16 student interviews, with 50% of issues left unresolved for weeks, particularly electrical faults). Verbal reporting leads to lost requests during shift changes, lack of student visibility, and duplicate complaints for the same room.

---

## 3. Business Objectives
- **What does the business want?:** 
  - Eliminate lost maintenance requests and miscommunications in campus hostels.
  - Improve operational accountability and reduce average repair resolution time for university Dorms.
  - Provide real-time operational data and metrics on maintenance backlogs for hall management.

---

## 4. Target Users
- **Who will use the product?:**
  - **Students:** Room occupants who log tickets and verify completed repairs.
  - **Porters & Hall Senators:** Hall welfare managers who verify incoming complaints, prevent duplicates, and assign tasks to technicians.
  - **Maintenance Technicians:** Works & Physical Planning staff who receive tasks and execute physical repairs.

---

## 5. Stakeholders
- **Who is involved or affected?:**
  - Hostel Management and Student Senators 
  - Dorm Residents
 

---

## 6. User Stories
- **What do users want to accomplish?:**
  - **Student 1:**I would like to be able to file complains and see the process of it being attended to instead of being told to wait all the time.
  - **Student 2:** I want to be able to visibly see when a technician is coming to hae peace of mind over the faulty things in my room. 
  - **Porter / Hall Senator:** A porter stated that with the large volume of complaints across the hostel, getting repairs completed takes time and wants to combat this with a better system.
  
---

## 7. Functional Requirements
- **What must the system do?:**
  - **User Authentication & Role Management:** Secure login distinguishing between **Student**, **Porter_Senator**, and **Technician** roles.
  - **Ticket Logging & Management:** Allow students to create tickets specifying room number, category (**Electrical**, **Plumbing**, **Carpentry**, **Other**), description, and urgency (**Normal** or **Urgent**).
  - **Duplicate Prevention Engine:** Automatically check if an open ticket already exists for the same room and category to block redundant submissions.
  - **Pipeline State Machine:** Enforce sequential stage transitions (**Pending** -> **Assigned** -> **Fixed** -> **Closed**) without skipping states.
  - **Automated Auto-Close Timer:** Move a **Fixed** ticket automatically to **Closed** if the student fails to confirm within 48 hours.

---

## 8. Non-Functional Requirements
- **How well must it operate?:**
  - **Reliability:** Backend data integrity must ensure zero race conditions or double-assignments when multiple porters attempt to assign overlapping tickets.
  - **Usability:** Simple, responsive interface optimized for quick mobile and desktop access across campus.
  - **Security:** Role-based access control preventing students from accessing administrative assignment features or viewing other rooms' private tickets.

---

## 9. Scope and Priorities
- **What is included in the MVP?:**
  - **In-Scope (MVP):** User roles, single-room ticket creation, duplicate blocking, 4-step pipeline tracking (**Pending**, **Assigned**, **Fixed**, **Closed**), manual assignment by porters/senators, and 48-hour auto-close.
  - **Out-of-Scope (Future Releases):** Push notifications via SMS/email, automated technician performance analytics dashboards, and multi-campus hostel scaling.

---

## 10. Acceptance Criteria
- **How do we verify features?:**
  - **Duplicate Check:** Submitting a second identical ticket for an active room and category returns a validation error and directs the user to the existing ticket.
  - **Pipeline Flow:** A technician cannot transition a ticket status to **Fixed** until a **Porter/Senator** has successfully moved it to **Assigned**.
  - **Auto-Close:** A ticket sitting in the **Fixed** stage for over 48 hours without student confirmation automatically switches status to **Closed**.

---

## 11. Assumptions and Open Questions
- **What remains unconfirmed?:**
  - **Assumptions:** Students have stable internet/network access on campus to log and check ticket statuses
