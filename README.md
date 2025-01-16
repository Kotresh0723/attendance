#Attendance Database Reader:
This is a Python script that connects to an SQLite database called attendance.db, retrieves all records from the attendance table, and prints the retrieved data to the console.

#Purpose:
The script is designed to fetch and display all records from the attendance table in the attendance.db SQLite database. Each record is printed as a tuple, where each element in the tuple represents a field from the corresponding row in the database.

#Requirements:
-Python 3.x
-SQLite3 (comes with Python by default)

#Files:
-attendance.db: SQLite database containing the attendance table.
-attendance_reader.py: The Python script that connects to the SQLite database and prints the records.

#Installation:

1.Ensure that Python 3.x is installed on your machine. You can download Python from here.
2.Make sure the attendance.db file exists in the same directory as the Python script, or update the database file path in the script.
3.The attendance.db database should already contain an attendance table. If not, you need to create it and populate it with records.

#Usage:

1.Open a terminal or command prompt.
2.Navigate to the directory containing the script and the database file.

#Run the script using Python:

bash

python attendance_reader.py
The script will connect to the SQLite database, fetch all records from the attendance table, and print each record as a tuple.

#Example output:

arduino

(1, 'John Doe', '2025-01-16', 'Present')
(2, 'Jane Smith', '2025-01-16', 'Absent')

#Code Breakdown:

python
import sqlite3

# Connect to the SQLite database
conn = sqlite3.connect("attendance.db")
cursor = conn.cursor()

# Execute SQL query to select all records from the 'attendance' table
cursor.execute("SELECT * FROM attendance")

# Fetch all records
records = cursor.fetchall()

# Loop through and print each record
for record in records:
    print(record)

# Close the connection to the database
conn.close()
Step 1: The script imports the sqlite3 module to interact with the SQLite database.
Step 2: It connects to the attendance.db database using sqlite3.connect().
Step 3: It creates a cursor to execute SQL commands.
Step 4: The SELECT * FROM attendance SQL command fetches all records from the attendance table.
Step 5: fetchall() retrieves all records, and each record is printed as a tuple.
Step 6: Finally, the connection to the database is closed using conn.close().
Troubleshooting
Error: sqlite3.OperationalError: no such table: attendance:
This error occurs if the attendance table does not exist in the database. Make sure the attendance table is created and populated in the attendance.db file.
Error: sqlite3.DatabaseError: database disk image is malformed:
This error indicates that the database file might be corrupted. You may need to create a new database or restore a backup.
