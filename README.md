This script implements a facial recognition-based attendance system using OpenCV, TensorFlow, and MySQL. Here's a step-by-step explanation of how the code works and how to set it up:

Steps to Set Up and Run the Script:

1. Install Required Libraries

You need to install the following Python libraries:
-opencv-python: For capturing video and image processing.
-tensorflow: For running the pre-trained model.
-mysql-connector: For interacting with the MySQL database.
-numpy: For numerical operations and image handling.
Use the following command to install them:
bash
pip install opencv-python tensorflow mysql-connector numpy

#importing libraries
import cv2
import numpy as np
import mysql.connector
from tensorflow.keras.models import load_model
import time


2. Prepare the Model and Label Files

-Ensure you have the keras_model.h5 (your trained model) and labels.txt (the list of labels, one per line) available in the same directory as the script.
-The model should be trained to recognize the faces you're working with.

# Load the model
model = load_model("keras_model.h5", compile=False)
# Load the labels
class_names = open("labels.txt", "r").readlines()


3. Set Up the MySQL Database
-Create a MySQL database called attendance_system.
-Create a table in the attendance_system database for storing attendance records. The table should look something like this:
sql:
CREATE TABLE attendance (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    status VARCHAR(50) NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
Ensure you replace the MySQL connection details (host, user, password, database) with your actual database credentials.


4. Adjust the Script

Update the database credentials in the script:
python
Copy code
conn = mysql.connector.connect(
    host="localhost",
    user="root",
    password="your_password",  # Replace with your MySQL root password
    database="attendance_system"
)
-Ensure that the camera index (0 or 1) corresponds to the correct camera on your system.


5. Understanding the Main Logic

-Model Loading: The script loads the pre-trained Keras model (keras_model.h5) and the labels from the labels.txt file.
-Database Connection: A connection to the MySQL database is established for recording attendance.
-Webcam Feed: The script opens a webcam feed using OpenCV. It processes each frame to make predictions about the recognized face.
-Face Recognition and Attendance: The model predicts the face and checks if the confidence score is above a threshold. If the person is recognized, their attendance is recorded in the database, and a cooldown timer ensures that attendance is only recorded once per session.
-Displaying the Feed: The script displays the live webcam feed with the recognized person's name overlayed on the screen.
-Exit Condition: Press the ESC key to stop the program.


6. Running the Script

-Open a terminal or command prompt and run the script:
bash
-python attendance_system.py


7. Working of Attendance Logging
-Once a face is recognized, the system will check if the person has already been marked present in the database.
-If not, the system will insert a new record with the person's name and status as "present".
-If the person’s attendance has already been marked, the script will not mark them again until the cooldown time has passed.


8. Exiting the Program
-Press the ESC key to terminate the webcam feed and close the program.
Notes:
-Model Training: Make sure the model is trained with the same input format (224x224) and class labels.
-Database: The script assumes that the attendance table contains a column for the name of the person and their status. You may want to extend it with additional information like timestamp or location.
