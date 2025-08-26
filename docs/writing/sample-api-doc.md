# API reference: Document analysis API

This API enables automated analysis of documents for style, readability, and consistency. It is designed for integration with documentation tools, CI/CD pipelines, and content quality dashboards.

---

## Authentication

All endpoints require an API key in the `Authorization` header:

```
Authorization: Bearer YOUR_API_KEY
```

---

## Endpoints

### POST /analyze

Analyze a document for style, grammar, and readability issues.

**Request:**

- Method: `POST`
- URL: `/analyze`
- Headers:
	- `Authorization: Bearer YOUR_API_KEY`
	- `Content-Type: application/json`
- Body:
	- `text` (string, required): The document content to analyze.

**Example Request:**

```bash
curl -X POST https://api.example.com/analyze \
	-H "Authorization: Bearer YOUR_API_KEY" \
	-H "Content-Type: application/json" \
	-d '{"text": "Your document text here."}'
```

**Response:**

```json
{
	"sentences": [
		{"text": "This is a sentence.", "issues": ["Passive voice"]},
		{"text": "Another sentence.", "issues": []}
	],
	"readability": 72.5,
	"quality_score": 88
}
```

**Error Responses:**

- `401 Unauthorized`: Invalid or missing API key.
- `400 Bad Request`: Malformed input (e.g., missing `text` field).
- `500 Internal Server Error`: Unexpected server error.

---

## Error Codes

| Code | Description                |
|------|----------------------------|
| 400  | Bad Request                |
| 401  | Unauthorized               |
| 422  | Unprocessable Entity       |
| 500  | Internal Server Error      |

---

## Example Use Case

Integrate this API into your CI pipeline to automatically review documentation for style and clarity before merging changes.
