# SolarX — AI-Based Solar Panel Detection and Analysis

SolarX is an AI-powered web application designed to automate the detection, counting, and surface area analysis of rooftop solar panels from high-resolution satellite and aerial imagery. The platform leverages a custom-trained **YOLOv8** object detection model and provides an interactive web dashboard for real-time inference and database logging.

---

## 🚀 Key Features

- **Real-Time AI Detection**: Upload satellite/aerial images and instantly detect solar panels using a custom-trained YOLOv8 model.
- **Rooftop Area Approximation**: Calculates individual and cumulative surface area (in pixels) of detected panels based on bounding box dimensions.
- **Inference Visualization**: Automatically draws bounding boxes with detection confidence percentages and overlays them on the output image.
- **Database Logging**: Integrates with a MySQL database via Flask-SQLAlchemy to record detection metadata (filename, output path, panel count, and calculated area) with timestamps.
- **Minimalist Frontend**: Features a simple, responsive web interface for uploading imagery and viewing comparative results.

---

## 🛠️ Technology Stack

- **Backend AI Server**: Python, Flask, Flask-SQLAlchemy, OpenCV
- **AI/ML Frameworks**: PyTorch, Ultralytics YOLOv8
- **Frontend**: HTML5, CSS3, JavaScript (AJAX-based upload & rendering)
- **Database**: MySQL (using the `pymysql` driver)

---

## 📁 Project Structure

```text
SolarX/
│
├── models/
│   └── best.pt            # Custom-trained YOLOv8 weights
│
├── static/
│   ├── uploads/           # Directory for user-uploaded satellite images
│   └── results/           # Processed output images with bounding box overlays
│
├── templates/
│   └── index.html         # Frontend dashboard interface
│
├── app.py                 # Core Flask backend, database model, & YOLO pipeline
├── README.md              # Project documentation
└── requirements.txt       # Python dependency list (optional)
```

---

## ⚙️ Installation and Local Setup

### 1. Prerequisites
Ensure you have the following installed on your machine:
- **Python 3.8+**
- **MySQL Server**
- **pip** (Python Package Installer)

### 2. Clone the Repository
```bash
git clone https://github.com/HasanAli-07/Reverse-SolarDetectionApp.git
cd Reverse-SolarDetectionApp
```

### 3. Create a Virtual Environment
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 4. Install Dependencies
Install the required packages using pip:
```bash
pip install Flask opencv-python-headless ultralytics Flask-SQLAlchemy PyMySQL torch torchvision
```

### 5. Database Configuration
1. Start your local MySQL server.
2. Create a new database named `solar_detection`:
   ```sql
   CREATE DATABASE solar_detection;
   ```
3. Update the database URI connection string in `app.py` (lines 14–15) with your MySQL username and password:
   ```python
   # Connection format: mysql+pymysql://<username>:<password>@localhost/solar_detection
   app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql+pymysql://root@localhost/solar_detection'
   ```
   *Note: On running the server, the app automatically initializes the database tables (using `db.create_all()`).*

### 6. Run the Application
Start the local Flask development server:
```bash
python app.py
```
The server will start at `http://127.0.5.1:5000/`.

---

## 💡 How to Use

1. Open your web browser and navigate to `http://127.0.0.1:5000/`.
2. Click the **Upload Image** button and select a satellite image of rooftops.
3. The image is processed through the YOLOv8 pipeline in the backend.
4. View the results on the dashboard:
   - **Annotated Image**: Green boxes outlining each detected panel.
   - **Solar Panel Count**: Total number of panels identified.
   - **Cumulative Surface Area**: Approximate total area calculated.
5. The upload metadata and result path are automatically saved to your MySQL database for future analytics.