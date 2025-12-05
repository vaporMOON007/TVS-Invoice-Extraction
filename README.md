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
