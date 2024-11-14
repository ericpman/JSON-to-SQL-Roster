# JSON-to-SQL-Roster Database

This script processes JSON data to populate an SQLite database for managing user-course relationships with roles. It creates tables for `User`, `Course`, and `Member` entities and establishes relationships between them, while allowing flexible role assignments. Finally, it generates a `UserCourseRole` table to store a joined view of user-course-role information.

## Requirements

- **Python 3**: This script uses Python's `sqlite3` and `json` modules, both of which are included in Python's standard library.
- **SQLite Database**: The database (`rosterdb.sqlite`) will be created automatically if it does not exist.
- **JSON Data File**: A JSON file (default: `roster_data.json`) that contains an array of user-course-role entries in the format `["user_name", "course_title", role]`.

## How It Works

1. **Database Setup**: The script drops existing tables (if any) and recreates the `User`, `Course`, `Member`, and `UserCourseRole` tables.

![Screenshot 2024-11-14 160110](https://github.com/user-attachments/assets/5b28990b-e67c-419b-a681-3909c7cee51c)


2. **Data Insertion**: It reads data from a JSON file and populates the `User`, `Course`, and `Member` tables, using:
   - `User` table for storing unique users.
 
  ![Screenshot 2024-11-14 160029](https://github.com/user-attachments/assets/33ada737-c936-4c82-b1fe-ed9952d9b908)

   - `Course` table for storing unique courses.
     
  ![Screenshot 2024-11-14 160050](https://github.com/user-attachments/assets/ba307df8-0daa-49be-9b98-238d67fa3ea4)


   - `Member` table to represent relationships between users and courses with a specific role.
     
  ![Screenshot 2024-11-14 160038](https://github.com/user-attachments/assets/8d67c991-b405-4584-ad5a-9b2ffeec9a9d)


3. **Joined Data Output**: The script retrieves all user-course-role relationships from the joined tables and inserts this data into the `UserCourseRole` table.


![Screenshot 2024-11-14 160058](https://github.com/user-attachments/assets/30b00d86-d9b2-4efc-82fc-c22973ccf838)



## Database Schema

The database schema includes the following tables:

- **User**: Stores unique users with an `id` and `name`.
- **Course**: Stores unique courses with an `id` and `title`.
- **Member**: Stores relationships between users and courses with `user_id`, `course_id`, and `role`.
- **UserCourseRole**: Final table containing joined results of `user_name`, `course_title`, and `role`.

## Running the Script

1. Save your JSON data in a file (default filename: `roster_data.json`).
2. The JSON file should contain data in the following format:
```
[
    ["Alice", "Math", 1],
    ["Bob", "Science", 0],
    ["Alice", "Science", 1]
]
```
  - The first element is the user name.
  - The second element is the course title.
  - The third element is the role (e.g., 1 for instructor, 0 for student).
    
3. Run the script and when prompted, leave the field blank and press Enter to use the default roster_data.json filename.

![Screenshot 2024-11-14 155357](https://github.com/user-attachments/assets/90b257db-0864-4ee9-8f06-ce245c71bbbd)



## Output
The UserCourseRole table is populated with the results of joining the User, Course, and Member tables, displaying each user's role for each course.

## Notes
SQL Injection Protection: The script uses parameterized SQL queries to prevent SQL injection.
Error Handling: Make sure to handle any errors or exceptions if the JSON data format is inconsistent.
