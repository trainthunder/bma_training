# 
## 📑 Table of Contents

- [ER diagram](#-introduction)
- [Connection](#-prerequisites)
- [Table Description](#-table-description)
- [Fields Description](#-configuration)
- [Decision Document](#-decision-document)
- [Migration Changelog](#-migration-changelog)


## ER diagram
![image](https://github.com/user-attachments/assets/bfe01214-9788-4e13-b373-abb9f46fe77e)

## 📂 Table Description

| Table Name             | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `courses`              | Contains records of individual courses offered, including details like title, duration, and associated department. |
| `course_categories`    | Stores categories or types of courses (e.g., online, lab-based, seminar).   |
| `departments`          | Contains academic departments responsible for courses and subjects.         |
| `registration_conditions` | Specifies conditions or prerequisites required to register for courses.  |
| `subjects`             | Represents subject areas covered within the curriculum (e.g., Math, Physics). |
| `course_subjects`      | Junction table linking courses to the subjects they cover.                  |
| `topics`               | Contains granular topics that fall under specific subjects.                 |
| `subjects_topic`       | Junction table linking subjects to their respective topics.                 |

## Fields Description

## 🏢 departments
- `department_id` - ID that refer to department
- `name_th` – Name of department in thai language
- `name_en` – Name of department in english language

---

## 🗂 course_categories
- `category_id` – ID that refer to category
- `name_th` – Name of course category in thai language
- `name_en` – Name of course category in english language
- `departments_id` – ID of department that relation with this course category

---

## 📚 courses
- `course_id` – ID that refer to course
- `name_th` – Name of course in thai language
- `name_en` – Name of course in english language
- `total_hours` – Total hours to learn this course
- `total_credits` – Total credits of this course
- `course_categories_id` – ID that refer to category
- `evaluation_criteria` – Criteria for evaluate

---

## ✅ registration_conditions
- `condition_id` – ID that refer to registration condition
- `course_id` – ID that refer to course id that relation with this registration condition
- `condition_type` – The condition type of this registration condition
- `description` – Description about this conditions

---

## 📖 subjects
- `subject_id` – ID that refer to subject
- `name_th` – Name of subject in thai language
- `name_en` – Name of subject in english language
- `hours` – Hour of this subject take
- `credits` – Credit of this subject

---

## 📌 topics
- `topic_id` – ID that refer to topic
- `name_th` – Name of topic in thai language
- `name_en` – Name of topic in english language
- `hours` – Hours to use in this topic
- `credits` – Credits of this topic

---

## 🔁 course_subjects
- `course_id` – ID of course that relation with this subject
- `subject_id` – ID of subject that relation with this course

---

## 🔁 subjects_topics
- `subject_id` – ID of subject that relation with this topic
- `topic_id` – ID of topic that relation with this subject

---

## Decision Document

---

**Decomposition for Flexibility:**

1. **Flexibility in Data Entry**: can be added or modified independently of the main course information.
2. **Reusability:** Subjects and topics can be reused across multiple courses.
3. **Scalability:** As the number of courses, subjects, or topics grows, the database can handle the increased data volume more efficiently
4. **UI Workflow Alignment:** The design allows the creation of a course record in the database before subjects and topics are defined. This separation simplifies the initial course creation process. The administrator doesn't need to provide subject and topic details when first creating the course, making the process more streamlined and user-friendly.
**Many-to-Many Relationships:** The `course_subjects` and `subject_topics` junction tables are essential for handling the many-to-many relationships. A course can have multiple subjects, and a subject can belong to multiple courses. Similarly, a subject can have multiple topics, and a topic can belong to multiple subjects.

## Tradeoff

1. Increased Complexity in Data Management
    1. More Complex Queries
    2. Data Integrity
    3. Transaction Management
       
![image](https://github.com/user-attachments/assets/6512ef02-7816-4325-97bb-d022642e4832)

## Migration Changelog

This changelog tracks all database migrations for the educational course management system. Each section describes the structure, relationships.


## 20250509120000_create_departments

**Table Created:** `departments`  
**Fields:**
- `name_th` (string, limit: 100) – department name in Thai
- `name_en` (string, limit: 100) – department name in English

**Relationships:**
- None

---

## 20250509120100_create_course_categories

**Table Created:** `course_categories`  
**Fields:**
- `name_th`, `name_en` – category names
- `department_id` – foreign key

**Relationships:**
- `belongs_to :department`

---

## 20250509120200_create_courses

**Table Created:** `courses`  
**Primary Key:** `course_id`  
**Fields:**
- `name_th`, `name_en`, `total_hours`, `total_credits`, `evaluation_criteria`
- `course_category_id` – foreign key

**Relationships:**
- `belongs_to :course_category`
