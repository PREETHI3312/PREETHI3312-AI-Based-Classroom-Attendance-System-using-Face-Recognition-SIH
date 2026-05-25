
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

## Program Output
<img width="421" height="637" alt="image" src="https://github.com/user-attachments/assets/06b8b75d-bff7-4df1-b2bc-b05b902bf889" />

<img width="392" height="593" alt="image" src="https://github.com/user-attachments/assets/a47c8b12-7850-4221-9039-9ff2a3408563" />

<img width="848" height="176" alt="image" src="https://github.com/user-attachments/assets/a5c62b27-9ba3-44b7-9171-9357e520e762" />

### Result
The AI-based classroom attendance system was successfully developed and tested. The system accurately detects and recognizes student faces from both images and live camera feeds and automatically marks attendance as Present or Absent.
