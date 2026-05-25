
# AI-Based Classroom Attendance System using Face Recognition

## Aim
The aim of this project is to develop a fully functional AI-based classroom attendance system that can automatically detect and recognize student faces from a classroom image or live camera feed. The system marks students as **Present or Absent**, stores attendance records in a database, and provides a teacher dashboard for managing and exporting attendance reports.

---

## Project Description
This system uses **Face Recognition technology** to automate classroom attendance. It eliminates manual attendance marking and reduces time and errors. The system includes:

- Student face registration
- Face detection and recognition
- Automatic attendance marking
- Database storage of attendance records
- Teacher dashboard for viewing and editing attendance
- Export attendance report as CSV file

---

## Technologies Used
- Python
- OpenCV
- Face Recognition Library (dlib / face_recognition)
- NumPy
- Pandas
- SQLite / MySQL (Database)
- Flask (for dashboard - optional)

---

##  System Architecture
1. **Input Module** – Captures classroom image or video feed  
2. **Face Detection Module** – Detects faces using OpenCV  
3. **Face Recognition Module** – Matches faces with trained dataset  
4. **Attendance Module** – Marks present/absent students  
5. **Database Module** – Stores attendance records  
6. **Dashboard Module** – Displays and manages attendance  

---

##  How the System Works
1. Register student faces into the system  
2. Train the model with collected face data  
3. Capture classroom image or start live camera  
4. System detects and recognizes faces  
5. Attendance is automatically marked  
6. Data is stored in database and shown on dashboard  

---

# Program
```
!pip install opencv-python opencv-contrib-python numpy pandas flask pillow
import pandas as pd
print("Pandas installed successfully!")
import cv2
import os
import numpy as np
import pandas as pd
import sqlite3
from datetime import datetime
from IPython.display import display, clear_output
from PIL import Image
conn = sqlite3.connect("attendance.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT
)
""")

cursor.execute("""
CREATE TABLE IF NOT EXISTS attendance (
    name TEXT,
    date TEXT,
    status TEXT
)
""")

conn.commit()
print("Database ready!")
dataset_path = "dataset"

faces = []
labels = []
names = {}
label_id = 0

for person in os.listdir(dataset_path):
    person_path = os.path.join(dataset_path, person)
    
    names[label_id] = person
    
    for img_name in os.listdir(person_path):
        img_path = os.path.join(person_path, img_name)
        img = cv2.imread(img_path, cv2.IMREAD_GRAYSCALE)
        
        if img is not None:
            faces.append(img)
            labels.append(label_id)
    
    label_id += 1

recognizer = cv2.face.LBPHFaceRecognizer_create()
recognizer.train(faces, np.array(labels))

print("Model trained!")
cap = cv2.VideoCapture(0)

attendance = {}

face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)

print("Click Stop (⏹) to end")

while True:
    ret, frame = cap.read()
    if not ret:
        break

    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    faces_detected = face_cascade.detectMultiScale(gray, 1.3, 5)

    for (x, y, w, h) in faces_detected:
        face = gray[y:y+h, x:x+w]

        try:
            label, confidence = recognizer.predict(face)

            if confidence < 100:
                name = names[label]
                attendance[name] = "Present"

                cv2.putText(frame, name, (x, y-10),
                            cv2.FONT_HERSHEY_SIMPLEX, 1, (0,255,0), 2)
        except:
            pass

        cv2.rectangle(frame, (x,y), (x+w,y+h), (255,0,0), 2)

    img = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    img = Image.fromarray(img)

    clear_output(wait=True)
    display(img)

img = cv2.imread(image_path)

if img is None:
    print("❌ Image not found! Check path")
else:
    print("✅ Image loaded successfully")
    
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    print("✅ Converted to grayscale")

face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)

faces_detected = face_cascade.detectMultiScale(gray, 1.3, 5)

attendance = {}

for (x, y, w, h) in faces_detected:
    face = gray[y:y+h, x:x+w]

    try:
        label, confidence = recognizer.predict(face)

        if confidence < 100:
            name = names[label]
            attendance[name] = "Present"

            cv2.putText(img, name, (x, y-10),
                        cv2.FONT_HERSHEY_SIMPLEX, 1, (0,255,0), 2)
    except:
        pass

    cv2.rectangle(img, (x,y), (x+w,y+h), (255,0,0), 2)

display(Image.fromarray(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)))
all_students = list(names.values())

for student in all_students:
    if student not in attendance:
        attendance[student] = "Absent"

date = datetime.now().strftime("%Y-%m-%d")

for name, status in attendance.items():
    cursor.execute("INSERT INTO attendance VALUES (?, ?, ?)", (name, date, status))

conn.commit()

df = pd.DataFrame(list(attendance.items()), columns=["Name", "Status"])
df["Date"] = date

df.to_csv("attendance.csv", index=False)

print(df)
```

## Program Output
<img width="421" height="637" alt="image" src="https://github.com/user-attachments/assets/06b8b75d-bff7-4df1-b2bc-b05b902bf889" />

<img width="392" height="593" alt="image" src="https://github.com/user-attachments/assets/a47c8b12-7850-4221-9039-9ff2a3408563" />

<img width="848" height="176" alt="image" src="https://github.com/user-attachments/assets/a5c62b27-9ba3-44b7-9171-9357e520e762" />

### Result
The AI-based classroom attendance system was successfully developed and tested. The system accurately detects and recognizes student faces from both images and live camera feeds and automatically marks attendance as Present or Absent.
