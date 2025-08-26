
# Doc Scanner – Advanced Document Analysis

This project showcases an advanced AI-powered document scanner web application. It enables users to upload documents (PDF, DOCX, Markdown, TXT, etc.), analyzes their content for writing quality, grammar, and style, and provides actionable feedback and AI-powered suggestions for improvement.

---

## Features Overview

- **Modern Web UI**: Responsive, visually appealing interface with drag-and-drop upload, dark mode, and real-time progress.
- **Multi-format Support**: Accepts PDF, DOCX, Markdown, AsciiDoc, and plain text files, including batch uploads via ZIP.
- **AI Writing Assistant**: Analyzes writing quality, grammar, and style, and provides smart suggestions and metrics.
- **Sentence-level Feedback**: Highlights issues in context and links feedback to specific sentences.
- **AI Suggestions**: Offers AI-powered rewrites and explanations for detected issues, with RAG (Retrieval-Augmented Generation) and user learning.
- **Batch Processing**: Supports multi-file and ZIP uploads with summary dashboards.
- **User Feedback & History**: Tracks suggestion history and allows users to rate and provide feedback on AI suggestions.

---

## Architecture

### Frontend (index.html)

- **UI Frameworks**: Bootstrap 5, FontAwesome, Chart.js for charts, and Marked.js for Markdown rendering.
- **Drag-and-drop Upload**: Users can upload single or multiple files, with real-time progress and batch support.
- **Document Analysis Dashboard**: Displays word/sentence counts, writing quality score, detected issues, and smart insights.
- **Sentence Highlighting**: Sentences are highlighted in the document view and linked to feedback.
- **AI Feedback Tab**: Users can request AI-powered suggestions for each issue, view explanations, and see knowledge sources.
- **Export & History**: Export feedback as CSV and view suggestion history with ratings.

### Backend (Flask)

- **File Parsing**: Handles PDF, DOCX, Markdown, AsciiDoc, and TXT using PyPDF2, python-docx, markdown, and BeautifulSoup.
- **Sentence Extraction**: Uses spaCy (if available) for robust sentence segmentation, with HTML preservation for accurate highlighting.
- **Rule-based Analysis**: Applies custom rules for grammar, style, and readability (modular, extensible via Python modules).
- **AI Suggestion Engine**: Combines rule-based feedback with LLM-powered suggestions (RAG, fallback to deterministic rewrite).
- **Real-time Progress**: WebSocket-based progress updates for uploads and analysis.
- **Batch Processing**: Handles ZIP uploads, processes each file, and aggregates results.
- **User Feedback & Learning**: Stores user ratings and feedback to improve future suggestions.

---

## Example Workflow

1. **Upload Document**: Drag and drop or browse to select files (PDF, DOCX, MD, TXT, ZIP).
2. **Real-time Analysis**: Progress bar and stage indicators show upload, parsing, sentence extraction, analysis, and report generation.
3. **Interactive Feedback**: View document with sentence-level highlights. Click on issues to get AI-powered suggestions and explanations.
4. **Export & Review**: Export feedback as CSV, review analysis charts, and access suggestion history.

---

## Key Code Snippets

### Frontend: Drag-and-Drop Upload & Progress

```html
<!-- Dropzone for file upload -->
<div id="dropzone" class="dropzone"> ... </div>
<script>
// Drag-and-drop, file selection, and progress logic
// ... (see index.html for full implementation)
</script>
```

### Backend: File Parsing & Sentence Extraction

```python
# Parse uploaded file and extract sentences with HTML preservation
def parse_file(file):
	# ... (see backend code)
	if extension == '.pdf':
		return parse_pdf(file)
	# ...

def extract_sentences_with_html_preservation(html_content):
	# Uses spaCy if available, else regex splitting
	# ...
```

### Backend: AI Suggestion Endpoint

```python
@main.route('/ai_suggestion', methods=['POST'])
def ai_suggestion():
	# Receives feedback and sentence context
	# Returns AI-powered rewrite, explanation, and sources
	# ...
```

---

## Security & Best Practices

- All file uploads are validated and processed securely.
- Environment variables are used for configuration and API keys.
- Modular rule system for easy extension and maintenance.
- User feedback is anonymized and used to improve AI suggestions.

---

## Benefits

- **Automated, actionable feedback** for writers and editors.
- **AI-powered suggestions** tailored to document context and user goals.
- **Modern, user-friendly interface** for document analysis and improvement.
- **Extensible and secure** architecture for future enhancements.
