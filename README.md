# 📰 Print Media Size Automation (PDF-Guided Estimation)

## 📌 Overview

This project aims to automate the estimation of **real-world print sizes (length × width in cm)** for large volumes of newspaper and print media clips.

In typical agency workflows, teams receive **thousands of print clips** (images) packed in ZIP folders and manually calculate their sizes by visually inspecting each clip and entering measurements into Excel. This process is **slow, error-prone, mentally exhausting, and not scalable**.

This repository explores and implements a **structured, rule-based automation approach**, inspired by how humans estimate print sizes using **newspaper column logic**, rather than unreliable pixel-only or black-box ML methods.

---

## 🎯 Core Problem

### Manual Workflow Today
- Open each print clip image  
- Visually estimate length and width  
- Enter values into Excel  
- Repeat for ~2000 clips per batch  

### Pain Points
- Extremely time-consuming  
- Mentally exhausting  
- Inconsistent measurements across analysts  
- Not scalable for large datasets  

### Goal of This Project
Reduce manual effort by **automating print clip size estimation with ~80–90% accuracy**, while keeping the logic **transparent, explainable, and aligned with real agency practices**.

---

## 🛠 Tools & Technologies Used

- **Python 3**
- **Google Colab** – execution environment  
- **OpenCV (cv2)** – image reading & pixel analysis  
- **Pillow (PIL)** – image handling  
- **pandas** – structured data handling & Excel output  
- **NumPy** – numeric computations  
- **PyMuPDF / pdfplumber** – PDF parsing for reference understanding  
- **zipfile** – ZIP upload & processing  
- **openpyxl** – Excel file writing  

---

## 🧠 How the System Works (High-Level Logic)

### Conceptual Analogy (Used Throughout Development)

- **PDF = TV**  
- **Code = Child**  
- **Human = Teacher**  

The system is **not meant to visually guess sizes**.  
It is meant to **learn the measurement logic a human uses** and apply it consistently.

---

## 📐 Final Adopted Approach: Column-Based Structural Measurement

Instead of unreliable pixel similarity or ML guessing, the system follows **print media structural rules**.

### Reference Understanding (Training Phase)

A reference PDF or publication standard defines:
- Page width & height  
- Column count  
- Column width (in cm)  

This step teaches the system **how size measurement works**, not how images look.

### Prediction Phase (Real Work)

- User uploads a ZIP folder containing print clip images  
- For each image:
  - Pixel width & height are extracted  
  - Ratios are calculated against page structure  
  - Real-world size is inferred using column rules  

### Output

A single Excel file is generated with the following columns:
1. Folder Path  
2. File Name  
3. Publication Name  
4. City  
5. Date  
6. Page Number  
7. Length (cm)  
8. Width (cm)  

---

## 📊 Output Format (Excel)

The system always produces **one Excel file**, overwriting previous results:

Print_Media_Automation/

└── Output_Excel/

└── Print_Analysis_Result.xlsx


No images, ZIPs, or temporary folders are saved.

---

## ⚠️ Key Challenges Faced

### 1. Pixel ≠ Physical Size
- Same physical print size can have wildly different pixel dimensions  
- Caused by DPI variation, compression, screenshots, cropping, etc.  

### 2. PDF “Visual Learning” Limitation
- PDFs with sample images and sizes cannot reliably teach size by appearance  
- They can only teach **measurement rules**  

### 3. ML & NLP Unsuitability
- No consistent labels  
- No reliable scale normalization  
- High variance across publications  

---

## 🧪 Error Handling & Edge Cases

The system includes handling for:
- Unreadable or corrupted images  
- Unsupported file formats  
- Missing metadata (date or page number)  
- Unexpected folder structures  

Skipped images are reported as:

X clips were skipped due to <error_reason>

---

## 👥 Intended Users

This repository is ideal for:
- Media monitoring agencies  
- PR analytics teams  
- Print media analysts  
- Operations teams handling large clip volumes  
- Developers building newsroom automation tools  

Not intended for:
- Fully automated computer-vision sizing without human logic  
- Arbitrary image size estimation without publication standards  

---

## 📈 Accuracy & Limitations

### Current Accuracy
Approximately **80–90%** when:
- Publication layout rules are known  
- Clips are reasonably cropped  
- Column structure is consistent  

### Known Limitations
Accuracy drops if:
- Publication layout changes drastically  
- Clips are heavily cropped without page context  
- DPI varies within the same batch  

This approach requires **discipline in input standards**.

---

## 📌 Assumptions & Constraints

- Newspaper layouts follow consistent column structures  
- Column widths are constant per publication  
- Input ZIP contains only print clip images  
- Folder paths encode city/location information  
- File names encode publication, date, and page number  

---

## 🚀 Future Improvements

- Publication-wise configuration files (JSON/YAML)  
- Semi-assisted UI for manual correction of edge cases  
- Confidence scoring per measurement  
- Batch comparison against historical measurements  
- Optional OCR for column boundary detection  
- Support for multilingual publication name parsing  

---

## 🧾 How to Clone & Run

git clone https://github.com/Jyotihirdhani/Image-Analysis-Project.git

cd Image-Analysis-Project

1. Open the notebook in **Google Colab**  
2. Mount Google Drive  
3. Ensure project root structure exists:
   /content/drive/MyDrive/Print_Media_Automation/
4. Run cells sequentially  
5. Upload ZIP when prompted  
6. Download Excel output from `Output_Excel`

---

## 🏁 Final Note

This project intentionally avoids **black-box guessing**.

It reflects how **real humans measure print clips**, translated into **deterministic, explainable automation**.

Accuracy here comes not from more data —  
but from **respecting print media structure**.
