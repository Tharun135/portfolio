# 🧠 Doc Scanner – AI-Powered Document Analysis

**Doc Scanner** is an intelligent web application that transforms how teams review and improve documentation.  
It allows users to upload documents in multiple formats — PDF, DOCX, Markdown, TXT, and more — then analyzes writing quality, grammar, and style using advanced NLP and AI models.  
The platform delivers **real-time, sentence-level feedback**, **AI-driven rewrites**, and **actionable insights** to help writers refine clarity and consistency.

---

## 🚀 Features Overview

- **Modern Web UI**: Responsive, intuitive interface with drag-and-drop uploads, dark mode, and live progress indicators.  
- **Multi-format Support**: Handles PDF, DOCX, Markdown, AsciiDoc, and plain text files, including batch uploads via ZIP.  
- **AI Writing Assistant**: Evaluates grammar, style, and readability, providing smart suggestions and metrics.  
- **Sentence-level Feedback**: Highlights issues in context, linking feedback directly to the corresponding sentence.  
- **AI Suggestions**: Offers contextual rewrites and explanations using Retrieval-Augmented Generation (RAG) and continuous learning.  
- **Batch Processing**: Supports multi-file and ZIP uploads with aggregated dashboards.  
- **User Feedback & History**: Tracks suggestion history and allows users to rate AI recommendations.

---

## 🏗 Architecture

### Frontend (index.html)

- **UI Frameworks**: Bootstrap 5, FontAwesome, Chart.js, Marked.js for Markdown rendering.  
- **Drag-and-Drop Upload**: Single or multiple file uploads with real-time progress and batch support.  
- **Document Analysis Dashboard**: Displays word and sentence counts, writing quality scores, detected issues, and insights.  
- **Sentence Highlighting**: Highlights sentences and links them to corresponding feedback.  
- **AI Feedback Tab**: Provides AI-generated suggestions, explanations, and source references.  
- **Export & History**: Export feedback as CSV and view previous suggestion history with ratings.

### Backend (Flask)

- **File Parsing**: Handles PDF, DOCX, Markdown, AsciiDoc, and TXT using `PyPDF2`, `python-docx`, `markdown`, and `BeautifulSoup`.  
- **Sentence Extraction**: Uses **spaCy** (if available) for robust segmentation, preserving HTML for accurate highlighting.  
- **Rule-based Analysis**: Custom rules for grammar, style, and readability; modular and extensible via Python modules.  
- **AI Suggestion Engine**: Combines rule-based feedback with LLM-powered suggestions (RAG, fallback deterministic rewrites).  
- **Real-time Progress**: WebSocket-based updates for uploads and analysis.  
- **Batch Processing**: Handles ZIP uploads and aggregates results.  
- **User Feedback & Learning**: Stores ratings to improve AI suggestions over time.

---

## 🔄 Example Workflow

1. **Upload Document** – Drag-and-drop or browse to select files (PDF, DOCX, MD, TXT, ZIP).  
2. **Real-time Analysis** – Progress bar shows stages: upload, parsing, sentence extraction, analysis, report generation.  
3. **Interactive Feedback** – Click highlighted sentences to view AI-powered suggestions and explanations.  
4. **Export & Review** – Export CSV feedback, review dashboards, and access suggestion history.

---

## 💻 Key Code Snippets

### Frontend: Drag-and-Drop Upload & Progress
```html
<!-- Dropzone for file upload -->
<div id="dropzone" class="dropzone"> ... </div>
<script>
// Handles drag-and-drop, file selection, and progress
</script>

## Backend: File Parsing & Sentence Extraction

def parse_file(file):
    # Determine file type and parse accordingly
    if extension == '.pdf':
        return parse_pdf(file)
    # Handle other formats...

def extract_sentences_with_html_preservation(html_content):
    # Uses spaCy if available, else regex-based splitting
    # Preserves HTML for sentence highlighting

## Backend: AI Suggestion Endpoint

@main.route('/ai_suggestion', methods=['POST'])
def ai_suggestion():
    # Receives sentence context and feedback
    # Returns AI-powered rewrite, explanation, and sources

🔐 Security & Best Practices

Validates and processes all file uploads securely.

Uses environment variables for configuration and API keys.

Modular rules for easy maintenance and extension.

Anonymized user feedback improves AI suggestions while preserving privacy.

🌟 Benefits

Automated, actionable feedback for writers and editors.

Context-aware AI suggestions to improve clarity and consistency.

Modern, intuitive interface for seamless document analysis.

Extensible and secure architecture ready for future enhancements.