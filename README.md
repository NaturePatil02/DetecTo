DeteTo Project: Planning and Development Report
Introduction
Project Overview
DeteTo is a learning-focused project designed to analyze ice hockey gameplay videos and automatically detect key events such as goals, penalties, fights, saves, and other significant occurrences. Additionally, the system will identify the players involved in these events, potentially through jersey number recognition, player tracking, or other identifiers. As a single-developer project in the early planning phase, the emphasis is on building a functional prototype using accessible tools and technologies to gain hands-on experience in computer vision, machine learning, and software development.
The core input will be video files (e.g., MP4 recordings of ice hockey games), and the output could include annotated videos, event timelines, or reports highlighting detected events and players. This project draws from fields like video analysis, object detection, and event classification, making it an excellent opportunity to learn AI/ML integration.
Objectives

Primary: Develop an end-to-end system to detect and classify ice hockey events from videos.
Secondary: Identify players involved in events; provide user-friendly outputs for review.
Learning Goals: Gain proficiency in Python, computer vision libraries (e.g., OpenCV), ML frameworks (e.g., TensorFlow or PyTorch), and project management as a solo developer.
Scope Limitations: Start with a minimum viable product (MVP) focusing on 3-5 key events (e.g., goals, penalties, shots on goal). Expand later if time allows. Assume publicly available videos for testing; no real-time streaming in MVP.

Requirements Gathering
Functional Requirements

Video Input Handling: Upload or select video files; support common formats like MP4, AVI.
Event Detection: Identify events such as:
Goals (e.g., puck crossing goal line).
Penalties (e.g., player entering penalty box, referee signals).
Shots on goal, saves, fights, or icing.

Player Identification: Detect and track players; recognize jersey numbers or team colors to identify individuals.
Output Generation: Generate timelines, annotated frames/videos, or JSON reports with event timestamps and player details.
User Interface: Simple CLI or web-based UI for input/output (e.g., via Streamlit for quick prototyping).

Non-Functional Requirements

Performance: Process a 5-10 minute video clip in under 30 minutes on standard hardware.
Accuracy: Aim for 70-80% event detection accuracy in MVP (improve iteratively).
Scalability: Handle videos up to 60 minutes; modular design for future enhancements.
Security/Privacy: No user data storage; local processing only.
Usability: Easy setup with documentation; error handling for invalid inputs.

User Stories (As a Solo Developer/User)

As a user, I want to upload a video so that the system can analyze it.
As a user, I want to see detected events with timestamps so I can review game highlights.
As a user, I want player names or numbers listed for each event to understand involvement.

System Architecture
High-Level Design
DeteTo will follow a pipeline architecture:

Input Layer: Video loader and preprocessor.
Processing Layer: Computer vision for frame extraction and analysis; ML models for detection.
Output Layer: Post-processing and visualization.
Storage: Temporary file handling; optional database for event logs (e.g., SQLite).

Components:

Video Preprocessor: Extract frames, resize, normalize.
Object Detector: Use models like YOLO for detecting pucks, players, goals.
Event Classifier: Custom or pre-trained model to classify sequences (e.g., RNN/LSTM for temporal analysis).
Player Tracker: Optical flow or tracking algorithms (e.g., SORT) combined with OCR for jersey numbers.
Integrator: Combine detections into coherent events.

Data Flow

Video → Frame Extraction → Object Detection → Tracking → Event Classification → Output Report.

Technology Stack

Programming Language: Python (versatile for ML and scripting).
Computer Vision: OpenCV for video handling and basic processing.
ML Frameworks: PyTorch or TensorFlow (PyTorch preferred for flexibility in prototyping).
Object Detection: Pre-trained YOLOv8 (from Ultralytics) for players/puck; fine-tune for hockey specifics.
Player Recognition: Tesseract OCR for jersey numbers; MediaPipe for pose estimation if needed.
Video Analysis: MoviePy for editing/annotating outputs.
UI: Streamlit for a simple web app; or Flask if more control is needed.
Data Management: Pandas for reports; SQLite for storing detections.
Version Control: Git (host on GitHub for backups).
Environment: Virtualenv or Conda; Google Colab for heavy ML training.
Datasets: Public ice hockey videos from YouTube/NHL archives; annotations from open sources like HockeyDataset or custom labeling via LabelStudio.

Development Phases and Workflow
As a single developer, adopt an agile approach: Break into sprints (2-4 weeks each), with daily/weekly progress checks. Use tools like Trello or Notion for task tracking. Each phase includes planning, implementation, testing, and review.
Phase 1: Setup and Research (Weeks 1-2)

Goals: Establish project foundation.
Tasks:
Set up Git repository and development environment.
Research ice hockey rules/events for accurate detection (e.g., what visual cues indicate a penalty?).
Collect sample data: Download 5-10 short hockey video clips (e.g., via YouTube-DL).
Label a small dataset manually (e.g., 100 frames) using LabelStudio.

Milestone: Working environment with sample video loaded and frames extracted.
Time Estimate: 10-20 hours.

Phase 2: Core Feature Development - Video Preprocessing (Weeks 3-4)

Feature Workflow:
Planning: Define input formats; decide on frame rate (e.g., process every 5th frame to optimize speed).
Development: Write scripts to load videos, extract frames, apply filters (e.g., edge detection for rink boundaries).
Integration: Use OpenCV functions like cv2.VideoCapture and cv2.imwrite.
Testing: Unit tests for frame count accuracy; manual review of extracted frames.

Milestone: Script that preprocesses a video and saves frames.
Time Estimate: 15-25 hours.

Phase 3: Object Detection and Tracking (Weeks 5-8)

Feature Workflow (Object Detection):
Planning: Identify objects to detect (players, puck, goal posts, referees).
Development: Install YOLOv8; fine-tune on hockey-specific dataset (use transfer learning to avoid heavy training).
Integration: Feed preprocessed frames into model; output bounding boxes.
Testing: Evaluate on sample videos; metrics like mAP (mean Average Precision).

Feature Workflow (Player Tracking):
Planning: Decide on tracking method (e.g., track players across frames).
Development: Implement SORT (Simple Online Realtime Tracking) or DeepSORT.
Integration: Combine with detection; add OCR for jersey numbers using Tesseract.
Testing: Track accuracy in crowded scenes; handle occlusions.

Milestone: Detect and track players/puck in a video clip.
Time Estimate: 30-50 hours (ML training can be time-intensive; use pre-trained weights).

Phase 4: Event Classification (Weeks 9-12)

Feature Workflow:
Planning: Define event signatures (e.g., goal: puck near net + crowd reaction; penalty: referee arm raise + player to box).
Development: Build a sequence model (e.g., LSTM on top of detection features) to classify event windows (e.g., 5-10 second clips).
Integration: Process tracked data to flag events; associate players.
Testing: Confusion matrix for event types; end-to-end video run.

Milestone: Detect 3-5 events with player IDs in sample videos.
Time Estimate: 25-40 hours.

Phase 5: Output and UI Integration (Weeks 13-14)

Feature Workflow (Output Generation):
Planning: Design report format (e.g., JSON with timestamps, event types, players).
Development: Use MoviePy to annotate videos (draw boxes, add text).
Integration: Generate timelines using Pandas.

Feature Workflow (UI):
Planning: Simple interface for video upload and result viewing.
Development: Build with Streamlit; pages for input, processing status, outputs.
Testing: User flow tests; handle large files.

Milestone: Full prototype with UI.
Time Estimate: 15-25 hours.

Phase 6: Testing, Optimization, and Deployment (Weeks 15-16)

Testing:
Unit/Integration: Pytest for code.
System: Run on unseen videos; measure accuracy/speed.
Edge Cases: Low-quality videos, different camera angles.

Optimization: Profile code (e.g., with cProfile); reduce processing time via batching or lighter models.
Deployment: Package as a Docker container or standalone app; host locally or on free platforms like Heroku.
Milestone: Deployed MVP with documentation.
Time Estimate: 10-20 hours.

Timeline and Milestones

Total Duration: 4 months (assuming 10-15 hours/week).
Milestones:
End of Month 1: Setup complete, preprocessing working.
End of Month 2: Detection and tracking functional.
End of Month 3: Event classification integrated.
End of Month 4: Full prototype tested and deployed.

Tracking: Weekly logs in a project journal; adjust based on progress.

Risks and Mitigations

Risk: ML model accuracy low due to limited data. Mitigation: Use pre-trained models; augment data with flips/rotations.
Risk: Hardware limitations for training. Mitigation: Use cloud (Colab) or downsample videos.
Risk: Scope creep (adding too many events). Mitigation: Stick to MVP; prioritize core features.
Risk: Burnout as solo dev. Mitigation: Break tasks into small wins; take breaks.
Risk: Data availability. Mitigation: Source from public domains; create synthetic data if needed.

Conclusion
This report provides a structured, end-to-end plan for developing DeteTo as a solo project. It emphasizes iterative development, leveraging open-source tools to keep things manageable. Start with Phase 1, and refine as you go—remember, this is for learning, so document challenges and solutions along the way. If you encounter roadblocks (e.g., specific library issues), iterate on the plan. Good luck with DeteTo; it sounds like a fun and educational endeavor! If you need code snippets or adjustments, let me know.
