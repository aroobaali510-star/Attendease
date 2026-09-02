# Attendease
AttendEase - Attendance Management System
# AttendEase — Student Attendance Tracker

A full-stack Android application built with Java, Android Studio, and Firebase.

---

## 🚀 Setup Instructions

### Step 1: Firebase Project Setup

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click **Add Project** → name it `AttendEase`
3. Enable **Google Analytics** (optional)

### Step 2: Add Android App to Firebase

1. In Firebase Console → Project Settings → **Add App** → Android
2. Package name: `com.attendease`
3. Download `google-services.json`
4. **Replace** the placeholder `app/google-services.json` with your downloaded file

### Step 3: Enable Firebase Services

#### Authentication
- Firebase Console → **Authentication** → Get Started
- Enable **Email/Password** provider

#### Realtime Database
- Firebase Console → **Realtime Database** → Create Database
- Start in **Test mode** (then apply rules below)
- Copy your database URL (e.g. 

https://github.com/user-attachments/assets/f22fbb46-23d3-4568-bc97-3d5ca3a43353

`https://attendease-default-rtdb.firebaseio.com/`)

#### Update Database URL in FirebaseHelper.java
Open `app/src/main/java/com/attendease/utils/FirebaseHelper.java` and update:
```java
private static final String DB_URL = "https://YOUR-PROJECT-ID-default-rtdb.firebaseio.com/";
```

### Step 4: Apply Database Security Rules

In Firebase Console → Realtime Database → Rules, paste:
```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read":  "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
```

### Step 5: Open in Android Studio

1. Open Android Studio → **Open** → select the `AttendEase` folder
2. Let Gradle sync complete
3. Run on **emulator** (API 24+) or **physical device**

---

## 📱 Features

| Feature | Description |
|---|---|
| 🔐 Auth | Email/password login & register via Firebase |
| 📚 Subjects | Add/delete subjects with live tracking |
| ✅ Attendance | Mark Present/Absent per day (one entry per day enforced) |
| 📊 Stats | Live % per subject + overall dashboard |
| ⚠️ Warnings | Danger alerts when attendance drops below 75% |
| 🧮 Bunk Calc | Shows how many classes can be missed or must be attended |
| 📅 History | Full day-by-day log with delete support |
| 🌑 Dark Theme | Full dark UI with cyan accent |

---

## 🏗 Architecture

```
com.attendease/
├── activities/
│   ├── SplashActivity.java
│   ├── LoginActivity.java
│   ├── RegisterActivity.java
│   ├── MainActivity.java          ← Dashboard
│   ├── AddSubjectActivity.java
│   ├── SubjectDetailActivity.java ← Mark attendance + bunk calc
│   ├── AttendanceHistoryActivity.java
│   └── ProfileActivity.java
├── adapters/
│   ├── SubjectAdapter.java
│   └── AttendanceAdapter.java
├── models/
│   ├── Subject.java
│   └── AttendanceRecord.java
└── utils/
    ├── FirebaseHelper.java
    └── DateUtils.java
```

## 🗃 Firebase Data Structure

```
users/
  {uid}/
    name: "Student Name"
    email: "student@email.com"
    subjects/
      {subjectId}/
        name: "Physics"
        totalClasses: 20
        presentClasses: 17
        createdAt: 1234567890
    attendance/
      {subjectId}/
        {yyyy-MM-dd}/
          date: "2025-04-10"
          present: true
          timestamp: 1234567890
```

---

## 🛠 Tech Stack

- **Language**: Java
- **IDE**: Android Studio (Iguana / Hedgehog+)
- **Min SDK**: 24 (Android 7.0)
- **Target SDK**: 34 (Android 14)
- **Backend**: Firebase Auth + Realtime Database
- **UI**: Material Components 3, ConstraintLayout, RecyclerView, CardView
- **Build**: Gradle 8.2, Google Services plugin 4.4

