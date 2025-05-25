
# 🧠 Grok PDF Summarizer

This project allows you to extract and summarize content from PDF documents using xAI's **Grok 3** and **Grok 3 Mini** models via the official API.

---

## 🚀 Features

* ✅ Upload any PDF file
* 🧠 Uses **Grok 3** for high-quality summarization
* 🧾 Outputs concise summaries of long documents
* 💼 Suitable for legal docs, research papers, resumes, etc.

---

## 🔧 Requirements

* Python 3.8+
* [xAI API Access](https://console.x.ai)
* Valid billing with credits (required to avoid 403 errors)

---

## 💰 Pricing (as per xAI)

| Model            | Text Input (\$/M tokens) | Text Output (\$/M tokens) | Rate Limit | Notes               |
| ---------------- | ------------------------ | ------------------------- | ---------- | ------------------- |
| grok-3           | \$3.00                   | \$15.00                   | 10 rps     | High accuracy       |
| grok-3-mini      | \$0.30                   | \$0.50                    | 10 rps     | Cheaper alternative |
| grok-3-fast      | \$5.00                   | \$25.00                   | 10 rps     | Faster response     |
| grok-3-mini-fast | \$0.60                   | \$4.00                    | 10 rps     | Balanced option     |

---

## 📈 Model Performance (Highlights)

| Benchmark | Grok 3 Beta (Think) | Grok 3 Mini Beta |
| --------- | ------------------- | ---------------- |
| AIME’24   | 95.8                | 90.8             |
| GPQA      | 84.6                | 84.0             |
| LCB       | 80.4                | 79.4             |
| MMLU      | 78.0                | —                |

---

## 🛠️ Installation

```bash
pip install openai PyMuPDF
```

---

## 📄 Example Code

```python
import fitz  # PyMuPDF
from openai import OpenAI

# Initialize client
client = OpenAI(
    api_key="your_xai_api_key",
    base_url="https://api.x.ai/v1"
)

def extract_pdf_text(pdf_path):
    with fitz.open(pdf_path) as doc:
        return "\n".join(page.get_text() for page in doc)

def summarize_with_grok(text):
    response = client.chat.completions.create(
        model="grok-3",  # Or "grok-3-mini"
        messages=[
            {"role": "user", "content": f"Summarize the following:\n{text}"}
        ]
    )
    return response.choices[0].message.content

# Usage
pdf_text = extract_pdf_text("your_file.pdf")
summary = summarize_with_grok(pdf_text)
print("Summary:", summary)
```

---


