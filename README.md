# RoadVision
### Computer-Vision-Based Road Damage Detection and Reporting System

**RoadVision** is a computer-vision-based application designed to detect visible road damage from recorded road videos and convert detected damage into location-tagged reports.

The system uses a fine-tuned **YOLOv8 object detection model** to identify potential road damage from extracted video frames. Detected images are associated with approximate geographical coordinates using timestamp-based GPS matching.

After completing a journey, users can review the detected images, confirm or reject potential damage, and submit verified reports. These reports are stored in a database and displayed on an interactive public road-damage map.

The project aims to combine automated road damage detection, geographical reporting, and human verification to make road inspection and monitoring more accessible.

---

## 📌 Problem Statement

Road damage, including potholes and different types of cracks, can create unsafe driving conditions and contribute to vehicle damage and road accidents.

Traditional road inspection methods often depend on manual surveys and public complaints. These approaches can be time-consuming and may not provide an efficient way to document and visualise road damage.

RoadVision proposes a computer-vision-based approach that analyses road footage, identifies potential damage, associates detections with geographical locations, and enables users to submit verified reports.

---

## 🎯 Objectives

- Develop a computer-vision-based system for detecting visible road damage.
- Process recorded road videos by extracting individual image frames.
- Fine-tune a YOLOv8 model to identify selected road-damage categories.
- Associate detected damage with approximate geographical coordinates.
- Provide a post-journey interface for reviewing and verifying detections.
- Generate structured, location-tagged road-damage reports.
- Visualise submitted reports on an interactive geographical map.
- Identify potential duplicate detections and reports.
- Provide an administrator interface for managing submitted reports.
- Evaluate detection performance and overall application functionality.

---

## ✨ Key Features

The following features represent the planned functionality of RoadVision.

### 1. Video-Based Road Inspection
- Record road footage using a mobile device.
- Upload previously recorded road videos.
- Collect GPS coordinates periodically during recording.
- Associate recording sessions with timestamps.

### 2. Automated Road Damage Detection
- Extract individual frames from recorded videos using OpenCV.
- Process extracted frames using a fine-tuned YOLOv8 model.
- Detect selected road-damage categories.
- Generate bounding boxes and confidence scores.
- Save frames containing potential road damage.

### 3. GPS Synchronisation
- Collect geographical coordinates during video recording.
- Match detection timestamps with corresponding GPS samples.
- Associate detected damage with approximate geographical locations.
- Support manual location selection when GPS data is unavailable or unreliable.

### 4. Post-Journey Detection Verification
- Display detected road-damage images after a recording session.
- Show predicted categories, confidence scores, and approximate locations.
- Allow users to swipe right to confirm a detection.
- Allow users to swipe left to reject a detection.
- Provide alternative confirmation and rejection buttons.
- Retain user-confirmed detections for report submission.

### 5. Road Damage Reporting
- Generate reports from user-confirmed detections.
- Store photographs, damage categories, and geographical coordinates.
- Maintain detection and submission timestamps.
- Generate unique report IDs.
- Maintain report statuses.

### 6. Duplicate Detection
- Identify repeated detections across nearby video frames.
- Compare geographical coordinates of submitted reports.
- Flag potentially duplicated reports.
- Allow administrators to review possible duplicates.

### 7. Interactive Public Map
- Display submitted road-damage reports on a geographical map.
- Position markers using latitude and longitude.
- Display damage categories and report details.
- Show associated photographs.
- Support filtering by damage category and report status.

### 8. Administrator Dashboard
- View submitted road-damage reports.
- Review photographs and geographical locations.
- Verify or reject reports.
- Update report statuses.
- Mark reports as resolved.
- Review potential duplicate reports.

---

## ⚙️ System Architecture

RoadVision follows a modular architecture that connects video processing, object detection, geographical location tagging, report generation, and map visualisation.

```text
       MOBILE APPLICATION
                |
        Record / Upload Video
                |
        GPS Data Collection
                |
                v
        VIDEO PROCESSING
             OpenCV
                |
        Extract Video Frames
                |
                v
      ROAD DAMAGE DETECTION
           YOLOv8 + PyTorch
                |
        Detect Road Damage
                |
        Save Detected Frames
                |
                v
       GPS SYNCHRONISATION
                |
       Timestamp-Based Matching
                |
                v
       POST-JOURNEY REVIEW
                |
       User Confirms / Rejects
                |
                v
        REPORT GENERATION
                |
       Duplicate Identification
                |
                v
             DATABASE
                |
         +------+------+
         |             |
         v             v
      PUBLIC MAP   ADMIN DASHBOARD
```

---

## 🔄 Application Workflow

1. The user starts a road-recording session.
2. The mobile application records road footage and collects GPS coordinates with timestamps.
3. The user ends the recording session.
4. OpenCV extracts individual frames from the recorded video at predefined intervals.
5. Extracted frames are passed to the fine-tuned YOLOv8 model.
6. The model identifies potential road damage and generates bounding boxes with confidence scores.
7. Frames containing potential damage are saved with their timestamps.
8. The system matches detection timestamps with the collected GPS history.
9. Repeated detections from nearby frames are grouped.
10. The user receives a post-journey detection summary.
11. The user reviews and confirms or rejects each detection.
12. Confirmed detections are converted into structured road-damage reports.
13. The system checks for potential duplicate reports.
14. Reports are stored in the database.
15. Submitted reports are displayed on the public road-damage map.
16. Administrators can review, verify, reject, or resolve reports.

---

## 🛠️ Technology Stack

 Programming Language - Python 
 Object Detection - Ultralytics YOLOv8n 
 Deep Learning Framework - PyTorch 
 Image and Video Processing - OpenCV 
 Model Training - Google Colab 
 Mobile Application - React Native with Expo 
 Backend / API - FastAPI 
 Database - SQLite 
 Map Visualisation - OpenStreetMap 
 GPS and Location - Device Location API 
 Duplicate Identification - GPS Distance Comparison 

*The technology stack represents the proposed implementation and may be adjusted based on integration requirements.*

---

## 🤖 Machine Learning Approach

RoadVision uses a pretrained YOLOv8 model as its starting point and fine-tunes it using a labelled road-damage dataset.

### Dataset

**Road Damage Dataset 2022 (RDD2022)**

The dataset provides road images with annotations for different categories of road damage.

Dataset reference: [RDD2022 – Road Damage Detector](https://github.com/sekilab/RoadDamageDetector)

### Target Detection Categories

- Potholes
- Longitudinal cracks
- Transverse cracks
- Alligator cracks

### Model Training Pipeline

1. Obtain and inspect the labelled road-damage dataset.
2. Identify relevant damage categories.
3. Prepare images and annotations in YOLO-compatible format.
4. Divide the dataset into training, validation, and testing sets.
5. Load a pretrained YOLOv8n model.
6. Fine-tune the model using the prepared dataset.
7. Evaluate the model on a held-out test set.
8. Integrate the trained model into the application.

### Evaluation Metrics

The detection model will be evaluated using:

- **Precision:** Measures how many predicted detections are correct.
- **Recall:** Measures how many actual damage instances are detected.
- **F1-score:** Represents the balance between precision and recall.
- **mAP:** Measures object-detection performance across confidence and IoU thresholds.
- **Inference Time:** Measures the time required to process an image.

---

## 📦 Project Modules

### Modules and responsibility-

 Video Recording and Input - Records or accepts road videos
 Video-to-Frame Conversion - Extracts individual frames 
 Detection Engine - Identifies road damage using YOLOv8 
 GPS Synchronisation - Associates detections with approximate locations 
 Detection Verification - Allows users to confirm or reject detections 
 Report Submission - Generates and stores road-damage reports 
 Duplicate Identification - Identifies potentially repeated reports 
 Public Road-Damage Map - Geographically visualises submitted reports 
 Administrator Dashboard - Manages and verifies reports 

---

## 📍 GPS Location Accuracy

RoadVision uses timestamp-based GPS synchronisation to associate detected road damage with geographical coordinates.

However, the GPS position of a mobile device may not represent the exact physical position of a pothole visible ahead of a moving vehicle.

Therefore, the application treats the associated coordinates as approximate locations rather than guaranteed exact positions.

---

## 🔮 Future Enhancements

Potential improvements include:

- Improving detection accuracy under different lighting and weather conditions.
- Implementing advanced image-similarity-based duplicate detection.
- Improving geographical localisation accuracy.
- Supporting additional road-damage categories.
- Optimising the detection model for edge devices.
- Investigating false detections caused by shadows and dark road patches.

---

## ⚠️ Limitations and Scope

The initial project focuses on detecting visible road damage and generating location-tagged reports.

The following are outside the initial project scope:

- Pothole depth measurement.
- Accident prediction.
- Continuous city-wide road surveillance.
- Vehicle-mounted hardware deployment.
- Automatic submission of reports to government authorities.
- Integration with municipal road-maintenance systems.
- Guaranteed detection of every pothole or crack.

RoadVision provides potential road-damage detections and user-verified reports. It does not independently verify physical road conditions or guarantee that a reported issue will be repaired.

---

## 📚 References

1. Road Damage Dataset 2022 (RDD2022).
2. [Ultralytics YOLO Documentation](https://docs.ultralytics.com/)
3. [OpenCV Documentation](https://docs.opencv.org/)
4. [PyTorch Documentation](https://pytorch.org/docs/)
5. POT-YOLO – *Real-Time Road Potholes Detection Using Edge Segmentation-Based YOLOv8 Network*, IEEE Sensors Journal, 2024.

---

<p align="center">

**RoadVision — Making Roads Safer Through Computer Vision.** 🚧

</p>
