# 



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
