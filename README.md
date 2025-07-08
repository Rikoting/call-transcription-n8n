# 📞 Call Transcription Extractor (Regex-based)

This project is an n8n automation workflow that converts voice call audio into clean, structured data. It uses AssemblyAI for transcription and custom regex logic to extract information such as:

- Caller name
- Email address
- Department
- Purpose of the call
- Whether it's a follow-up
- Priority level
- Action requested

The data is then logged automatically into a connected Google Sheet.

---

## 🎯 Features

- ✅ Audio-to-text transcription with [AssemblyAI](https://www.assemblyai.com/)
- ✅ Regex-based data extraction using a Function node
- ✅ Google Sheets integration (Append Row)
- ✅ Duplicate and vague-purpose detection cleanup
- ✅ Basic email format validation (`emailValid`)
- ✅ Flags for follow-up and urgency (`followUp`, `priority`)
- ✅ Categorized action requests (`actionRequested`)

---

## 📦 Fields Captured

| Field            | Description                              |
|------------------|------------------------------------------|
| `name`           | Caller’s name (first + last only)        |
| `email`          | Email address (autocorrected if needed)  |
| `emailValid`     | Boolean (true/false) for format check     |
| `department`     | Extracted from phrases like “from the ___ department” |
| `purposes`       | List of reasons for the call              |
| `priority`       | `high` if urgent words detected (`asap`, `urgent`, etc.) |
| `followUp`       | True if user is following up              |
| `actionRequested`| ["status update", "confirmation", etc.]  |
| `transcript`     | Raw full transcription from the audio     |

---

## 🛠️ How to Use

1. Record an audio call and upload it to Google Drive
2. Generate a **direct download link** using this format:
https://drive.google.com/uc?export=download&id=FILE_ID
3. In the n8n workflow:
- Paste the link into the HTTP Request node (`audio_url`)
- Run the nodes in order:
  1. Submit Audio
  2. Check Status
  3. Function (Extract Info)
  4. Append Row
4. The results are logged into your Google Sheet.

---

## 📁 Example Files

| File                  | Description                                 |
|-----------------------|---------------------------------------------|
| `workflow.json`       | Full n8n export (import into new instance)  |
| `example-output.json` | Sample result from Function node            |
| `sample-transcript.txt` | Optional raw transcript from audio        |

---

## 🚀 Roadmap

- 🔜 AI-based parsing for better name/purpose/date extraction
- 🔜 Smart summarization and response generation using OpenAI or Hugging Face
- 🔜 Better handling of multiple action requests per call

---

## 👤 Author

Built by Riko Toh  
For Virtual Assistant, Executive Assistant, and automation workflows  
Made with 💻 and ☕ using n8n and AssemblyAI