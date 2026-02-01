# Image-Analysis-Project
## Print Media Size Automation (PDF-Guided Estimation)

### Overview
- This project aims to automate the estimation of real-world print sizes (length × width in cm) for large volumes of newspaper and print media clips.
- In typical agency workflows, teams receive thousands of print clips (images) in ZIP folders and manually calculate their sizes by visually inspecting each clip and entering measurements into Excel — a slow, error-prone, and exhausting process.
- This repository explores and implements a structured, rule-based automation approach inspired by how humans estimate print sizes using newspaper column logic.

### Core Problem

#### Manual workflow today:
- Open each print clip image
- Visually estimate length and width
- Enter values into Excel
- Repeat for ~2000 clips per batch

#### Pain points:
- Extremely time-consuming
- Mentally exhausting
- Inconsistent measurements across analysts
- Not scalable
  
### Goal of this project:
  Reduce manual effort by automating print clip size estimation with 80–90% accuracy, while keeping the logic explainable and aligned with real agency
  practices.


### Tools & Technologies Used
- Python 3 
- Google Colab (execution environment)
- OpenCV (cv2) – image reading & pixel analysis
- Pillow (PIL) – image handling
- pandas – structured data handling & Excel output
- NumPy – numeric computations
- PyMuPDF / pdfplumber – PDF parsing (reference analysis)
- zipfile – ZIP upload & processing
- openpyxl – Excel file writing

### How the System Works (High-Level Logic)
#### Conceptual Analogy (Used Throughout Development)
  - PDF = TV
  - Code = Child
  - Human = Teacher
    
The system is not meant to “guess” sizes visually. It is meant to learn the measurement logic a human uses.


### Final Adopted Approach: Column-Based Structural Measurement
#### Instead of unreliable pixel-based similarity or ML guessing, the system follows print media structural rules:
1.	Reference Understanding (Training Phase)
- A reference PDF or publication standard defines:
    - Page width & height
    - Column count
    - Column width (cm)
- This teaches the system how measurement works, not what each image looks like.
2.	Prediction Phase (Real Work)
- User uploads a ZIP folder containing print clip images
  - For each image:
    - Pixel width & height are extracted
    - Ratios are calculated against page structure
    - Real-world size is inferred using column rules
3.	Output
- A single Excel file is generated with standardized columns:
    - Folder Path
    - File Name
    - Publication Name
    - City
    - Date
    - Page Number
    - Length (cm)
    - Width (cm)





