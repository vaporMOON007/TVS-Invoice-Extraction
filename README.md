# TVS-Invoice-Extraction
This project is an AI-powered invoice extraction system that automatically processes invoice images, enhances them for OCR, sends them to IBM WatsonX LLM for structured data extraction, performs multi-level validation (GST, dates, IMEI, taxes), calculates final amounts, applies proportional adjustments, and exports results to Excel with tables.
It supports multi-line invoices, confidence scoring, error handling with retries, stamp/signature detection, and image preprocessing for maximum accuracy.

Core logic is implemented in Extractor.py and image enhancement is handled by image_processor.py 

📁 Project Structure
📦 Invoice-Extraction-System
│
├── Extractor.py                # Main engine for AI extraction, validations & Excel export
├── image_processor.py          # Image preprocessing (upscaling, denoising, thresholding)   
│
├── INPUT_IMAGES/               # Raw invoice images
├── PROCESSED_IMAGES/           # Enhanced images (auto-generated)
│
├── extraction_log.txt          # Runtime logs & warnings
│
├── output.xlsx                 # Final Excel file (Item Details + Invoice Summary)
│
└── README.md                   # Documentation (this file)

🚀 Features
🔍 1. Advanced Image Preprocessing (Implemented in image_processor.py 

Upscaling, denoising, grayscale conversion
Adaptive thresholding for OCR clarity
Automated folder processing

🤖 2. AI-Based Data Extraction (WatsonX)

Uses IBM WatsonX LLM (Llama-4 Maverick 17B) along with extremely detailed extraction prompt and ruleset
Extracts 40+ invoice fields including:
Invoice details (number, date, type) Supplier & customer data
GST, taxes, IMEI, serial numbers
Multi-row items table
Stamp, signature & hypothecation detection

🛡️ 3. Multi-Layer Validation Engine(Implemented in Extractor.py )

GST format verification
Date format validation
Phone number validation
IMEI validation
Tax percentage sanity checks
Cross-field cosistency checks
Auto-cleaning of invalid OCR outputs

📤 4. Clean Excel Output

Two sheets are generated:
Sheet 1 – Item_Details
Sheet 2 – Invoice_Summary

Logs all warnings and corrections to extraction_log.txt

⚙️ Setup & Installation
1. Install Python 3.9+
python --version

2. Install Required Libraries

Create a virtual environment (optional) then install dependencies:

pip install opencv-python numpy pandas openpyxl ibm-watsonx-ai
pip install futures

3. Configure Paths in Extractor.py

In Extractor.py update the folder paths:

RAW_IMAGES_DIR = r"PATH_TO_INPUT_IMAGES"
PREPROCESSED_DIR = r"PATH_TO_OUTPUT_IMAGES"
EXCEL_OUTPUT_PATH = r"PATH_TO_SAVE_EXCEL"


Also add your:

IBM WatsonX API key

Project ID

Model ID

5. Run the Main Extraction Script
python Extractor.py


The script will preprocess images extract data using WatsonX , validate calculate items , generate Excel and log issues
Invoice_Summary sheet → High-level report per invoice

extraction_log.txt → All corrections + validation logs


Great — here is your **GitHub-optimized README.md** with **badges, visuals, sections, and clean formatting**.
I have **not** added citations in this version because GitHub READMEs should not contain those markers.
(If you want citations kept, tell me and I’ll regenerate.)

---

# 📄 **AI-Powered Invoice Extraction System**

### *Automated Invoice Processing using IBM WatsonX, OCR Enhancement & Intelligent Validation*

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.9%2B-blue?logo=python" />
  <img src="https://img.shields.io/badge/IBM-WatsonX-orange?logo=ibm" />
  <img src="https://img.shields.io/badge/OCR-Enabled-green" />
  <img src="https://img.shields.io/badge/Automation-Multi--Threaded-purple" />
  <img src="https://img.shields.io/badge/Excel-Export-success?logo=microsoft-excel" />
</p>

---

# 🚀 **Overview**

This project is a complete **AI-driven invoice extraction pipeline** that:

✔ Enhances raw images for OCR
✔ Extracts structured fields using **IBM WatsonX LLM**
✔ Performs **high-accuracy validation** (GST, phone, IMEI, dates, tax %)
✔ Handles **multi-line invoices**, tax logic & amount corrections
✔ Generates **Excel reports** with Item-Details & Invoice-Summary
✔ Calculates **confidence scores** for audit reliability
✔ Applies **proportional adjustment** when extracted totals mismatch

It is built for real-world business use where invoices vary widely in format, clarity, and structure.

---

# 📁 **Project Structure**

```
📦 Invoice-Extraction-System
│
├── Extractor.py                # Main pipeline: OCR→LLM→Validation→Excel export
├── image_processor.py          # Image enhancement (upscale, denoise, threshold)
│
├── INPUT_IMAGES/               # Raw invoice images
├── PROCESSED_IMAGES/           # Automatically enhanced images
│
├── extraction_log.txt          # Logs: warnings, corrections, retries
├── output.xlsx                 # Final Excel output (auto-generated)
│
└── README.md                   # Project documentation
```

---

# ✨ **Features**

## 🔧 **1. Advanced Image Preprocessing**

✔ Upscaling for better DPI
✔ Noise removal
✔ Adaptive thresholding
✔ Batch processing support

Improves OCR accuracy significantly for low-quality invoices.

---

## 🤖 **2. AI Extraction using IBM WatsonX**

The LLM extracts **structured JSON** including:

### **Header Fields**

* Invoice Number (with handwritten/printed detection)
* Invoice Date
* Supplier & Customer details
* GSTIN (validated)
* Stamp & Signature detection

### **Item Table Extraction**

* Item numbers
* Description (cleaned + brand identification)
* IMEI / Serial Number extraction
* Quantity, Rate, Amount
* SGST / CGST / IGST %
* Tax calculation correctness rules

---

## 🧠 **3. Multi-Layer Validation Engine**

✔ GST format & state-code validation
✔ IMEI (15-digit) verification
✔ Phone number & date validation
✔ Tax % correctness checks
✔ Cross-field corrections with logging

---

## 📊 **4. Smart Amount Calculation Engine**

Handles:

* Tax-inclusive invoices
* Multi-item computations
* Difference tolerance checks
* Proportional adjustments
* Confidence scoring for extracted vs. calculated values

---

## ⚡ **5. Multi-Threaded Performance**

Processes multiple invoices using Python's `ThreadPoolExecutor`.

---

## 📤 **6. Clean Excel Reporting**

Exports 2 sheets:

### **Sheet 1 → Item_Details**

* One row per item
* All extracted + validated fields
* Excel table formatting

### **Sheet 2 → Invoice_Summary**

* One row per invoice
* Total amounts
* Confidence scores
* Stamp match score
* Tax-inclusive flag

---

# ⚙️ **Setup & Installation**

## 1️⃣ Install Python Packages

```sh
pip install opencv-python numpy pandas openpyxl ibm-watsonx-ai
```

---

## 2️⃣ Configure API & Paths

Inside `Extractor.py`, update:

```python
RAW_IMAGES_DIR = r".../INPUT_IMAGES"
PREPROCESSED_DIR = r".../PROCESSED_IMAGES"
EXCEL_OUTPUT_PATH = r".../output.xlsx"

API_KEY = "YOUR_API_KEY"
PROJECT_ID = "YOUR_PROJECT_ID"
MODEL_ID = "meta-llama/llama-4-maverick-17b-128e-instruct-fp8"
```

---

## 3️⃣ (Optional) Run Preprocessing Only

```sh
python image_processor.py
```

---

## 4️⃣ Run the Complete Extraction Pipeline

```sh
python Extractor.py
```

---

# 🧪 **Output**

### ✔ Excel file with:

* Item-level details
* Invoice summary
* Confidence scores

### ✔ Logs include:

* Invalid GST fixes
* Phone/date corrections
* Amount mismatches
* Retry attempts

---

# 🖼️ **Visual Workflow Diagram**

```
 Raw Images
      ↓
 Image Preprocessing (Upscale + Denoise + Threshold)
      ↓
   WatsonX LLM Extraction
      ↓
 Field Validations (GST, IMEI, Tax %, Dates)
      ↓
 Smart Amount Calculations + Adjustments
      ↓
 Confidence Scoring
      ↓
 Excel Export (2 sheets)
```

---

# 📌 **Future Enhancements**

* Web dashboard for uploads
* Automatic PDF → Image conversion
* Real-time API endpoint
* Multi-language invoice support
* Database integration

---

# 🤝 **Contributing**

Pull requests are welcome!
Please raise issues for bugs or feature requests.

---

# ❤️ **Made for high-accuracy compliance & audit workflows**

If you want a **PDF version** or want this README **uploaded into your repository automatically**, just tell me!
