# medhistory-arc
high level architecture of medhistory
High-Level Architecture
The application comprises three layers:
Frontend: Mobile app for user interaction.
Tools: React Native or Flutter.
Features:
Upload documents (camera or gallery).
View extracted summaries.
Suggest medicines.
View medical history.
Backend: Python-based server handling logic and data processing.
Framework: Django (or Flask if you prefer a lightweight alternative).
Database: Storing user data, documents, summaries, and medical history.
Database: PostgreSQL for structured data or MongoDB for flexibility.
Cloud Services:
OCR, NLP, and APIs.
Hosting the backend and serving APIs.

Component-Wise Architecture
1. Frontend
Key APIs to Connect to Backend:
/upload-document: To send scanned images.
/generate-summary: To fetch summaries for documents.
/suggest-medicines: To display medicine recommendations.
/share-history: To retrieve sharable QR codes.

2. Backend
Tech Stack
Framework: Django or Flask.
Database ORM: Django ORM (if using Django) or SQLAlchemy.
Libraries:
pytesseract (OCR).
transformers or spaCy (text summarization).
qrcode (QR code generation).
requests (external API calls).
Key API Endpoints
Authentication
/register: Register a user.
/login: Authenticate user with JWT.
Document Management
/upload-document (POST):
Accepts user-uploaded images.
Performs OCR using Tesseract or Google Vision API.
Saves extracted text in the database.
/generate-summary (GET):
Fetches extracted text.
Processes text with NLP summarization models.
Stores and returns a summary.
Medicine Suggestions
/suggest-medicines (GET):
Uses external APIs to search for medicines.
Example API: PharmEasy or 1mg APIs.
Returns a list of medicines with links to purchase.
Medical History
/get-medical-history (GET):
Retrieves and formats user’s medical history.
/share-history (GET):
Generates a QR code for sharing medical history.

3. Database Schema
User Table
id: Unique identifier.
name, email, password: User credentials.
created_at, updated_at: Timestamps.
Documents Table
id: Unique identifier.
user_id: Foreign key linking to user.
image_url: Path to uploaded image.
extracted_text: Text extracted from the document.
summary: Summarized text.
Medical History Table
id: Unique identifier.
user_id: Foreign key linking to user.
details: JSON field storing historical data.
created_at: Timestamp.

4. Cloud Services
OCR:
Option 1: Local OCR using pytesseract.
Option 2: Cloud OCR via Google Vision API or AWS Textract for higher accuracy.
NLP:
Summarize text with Hugging Face Transformers (e.g., BERT).
Use spaCy for lightweight NLP tasks.
Hosting:
Host backend on AWS Elastic Beanstalk, Azure App Service, or Heroku.
Use S3 (or equivalent) for image storage.
QR Code Sharing:
Use qrcode to generate QR codes.
Encrypt sensitive data before encoding.

System Flow
Document Processing:
User uploads an image via the app.
Backend processes the image with OCR to extract text.
Extracted text is summarized and saved.
Medicine Suggestions:
Backend fetches relevant medicines via APIs.
Results are displayed in the app.
Medical History Sharing:
User requests medical history via the app.
Backend retrieves data, generates a QR code, and sends it to the user.
Data Security:
Sensitive data is encrypted before storage.
Access to APIs and data is token-based.

