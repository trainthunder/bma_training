# 
## 📑 Table of Contents

- [ER diagram](#-introduction)
- [Connection](#-prerequisites)
- [Table Description](#-table-description)
- [Fields Description](#-configuration)
- [Database Design Decision](#-connecting-to-postgresql)
- [Migration Changelog](#-example-usage)


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

# Decision Document

---

**Decomposition for Flexibility:**

1. **Flexibility in Data Entry**: can be added or modified independently of the main course information.
2. **Reusability:** Subjects and topics can be reused across multiple courses.
3. **Scalability:** As the number of courses, subjects, or topics grows, the database can handle the increased data volume more efficiently

**Many-to-Many Relationships:** The `course_subjects` and `subject_topics` junction tables are essential for handling the many-to-many relationships. A course can have multiple subjects, and a subject can belong to multiple courses. Similarly, a subject can have multiple topics, and a topic can belong to multiple subjects.

## Tradeoff

1. Increased Complexity in Data Management
    1. More Complex Queries
    2. Data Integrity
    3. Transaction Management
