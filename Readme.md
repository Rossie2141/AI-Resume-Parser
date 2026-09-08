# 📄 AI Resume Parser

An AI-powered resume parser that converts **PDF resumes into structured JSON** using PDF layout extraction, section detection, LLM-based extraction, and validation.

## 🚀 Approach

### Initial Approach

The first version used a **single LLM prompt** to extract all resume information at once:

```text
PDF → Text → LLM → JSON
```

This worked for basic resumes but caused accuracy issues such as:

* Project names being detected as skills
* Responsibilities appearing in the skills list
* Incorrect URL classification
* Cross-section information leakage

### Optimized Approach

To improve accuracy, the pipeline was redesigned to be **section-aware**:

```text
PDF
 ↓
Text + Layout Extraction
 ↓
Section Detection
 ↓
┌─────────┬────────────┬──────────┬───────────┐
│ Skills  │ Experience │ Projects │ Education │
└─────────┴────────────┴──────────┴───────────┘
 ↓
Specialized Extraction
 ↓
Cleaning + Validation
 ↓
Structured JSON
```

Each section is processed independently, giving the LLM a much more focused task and reducing cross-section contamination.


## 🧠 Key Design Decisions

* **PyMuPDF** for PDF text and layout extraction
* **Qwen2.5-3B-Instruct** for semantic extraction
* **Section-specific prompts** for better accuracy
* **Regex-based extraction** for emails, phones, and URLs
* **Pydantic** for output validation
* Empty or unsupported fields are removed instead of hallucinating values

> **Core principle:** Extract only what is explicitly present in the resume.

## 🛠️ Tech Stack

| Technology          | Purpose                 |
| ------------------- | ----------------------- |
| Python              | Core development        |
| PyMuPDF             | PDF extraction          |
| Qwen2.5-3B-Instruct | LLM extraction          |
| PyTorch             | Model inference         |
| Pydantic            | Validation              |
| Streamlit           | User interface          |
| Google Colab        | Current experimentation |

## 📌 Current Status

🚧 **Prototype / Active Development**

The current focus is improving extraction accuracy across different resume formats.

Once accuracy is satisfactory, the project will be refactored into a modular production-ready Python architecture.

## 🔮 Future Improvements

* Better multi-column layout handling
* OCR for scanned resumes
* Skill normalization
* Confidence scoring
* Automated accuracy evaluation
* REST API and production deployment
