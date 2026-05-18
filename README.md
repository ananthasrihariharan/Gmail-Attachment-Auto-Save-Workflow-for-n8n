# Gmail-Attachment-Auto-Save-Workflow-for-n8n
Production-ready n8n workflow that automatically monitors Gmail inboxes, downloads email attachments in full size, prevents duplicate processing, extracts email content, and organizes files locally using sender-based folder structures.

## Overview

This n8n workflow automatically monitors a Gmail inbox, downloads new email attachments, extracts email content, and stores everything locally in an organized folder structure.

Designed for production usage such as:

- Printing press workflows
- ERP integrations
- Customer file collection
- Design studios
- Automated document intake systems
- Attachment archival systems

---

# Features

- Auto-check Gmail every minute
- Download full-size attachments safely
- Prevent duplicate email processing
- Skip host/sent emails automatically
- Extract HTML and text email body
- Save email metadata into text files
- Organize files by sender and timestamp
- Persistent processed-email tracking
- Works with large attachments
- Production-ready binary handling

---

# Workflow Architecture

```text
Schedule Trigger
        ↓
Get Emails (Gmail API)
        ↓
Process & Save Email
        ↓
Local File Storage
```

---

# Folder Structure

```text
/data/
 ├── sender@email.com/
 │     ├── 2026-05-18T10-45-22_Project_Files/
 │     │      ├── email.txt
 │     │      ├── artwork.pdf
 │     │      ├── logo.ai
 │     │      └── image.png
```

---

# Requirements

- n8n
- Gmail OAuth2 Credential
- Gmail API Enabled
- Persistent writable storage
- Docker recommended

---

# Installation

## 1. Import Workflow

Import the workflow JSON into n8n.

## 2. Configure Gmail Credential

Open the `Get Emails` node and attach your Gmail OAuth2 credential.

## 3. Enable Persistent Storage

Docker example:

```yaml
services:
  n8n:
    image: n8nio/n8n
    ports:
      - "5678:5678"
    volumes:
      - ./email-data:/data
```

## 4. Activate Workflow

Turn the workflow ON.

The system will start checking emails every minute.

---

# Gmail Permissions

Recommended scope:

```text
https://www.googleapis.com/auth/gmail.readonly
```

or

```text
https://www.googleapis.com/auth/gmail.modify
```

---

# Duplicate Prevention

Processed email IDs are stored in:

```text
/data/processed_ids.json
```

This prevents:

- Duplicate downloads
- Reprocessing
- Attachment duplication

---

# Attachment Handling

This workflow uses n8n binary storage APIs to safely download full-size attachments without truncation or corruption.

Supports:

- PDFs
- Images
- ZIP files
- AI/PSD files
- Office documents
- Large attachments

---

# Email Processing Features

## Automatically Skips

- Sent emails
- Already processed emails
- Invalid attachments
- Empty binary files

## Automatically Saves

- Email body
- Sender info
- Subject
- Date
- Attachments

---

# Technologies Used

- n8n
- Gmail API
- OAuth2
- Node.js File System APIs
- Docker Volumes

---

# Production Recommendations

- Use Docker volumes
- Backup `/data`
- Use dedicated Gmail accounts
- Restrict Gmail OAuth scopes
- Monitor disk usage for attachments

---

# Example Use Cases

## Printing Press

Automatically collect customer artwork files from email.

## ERP Intake

Receive invoices, POs, and documents automatically.

## Design Agencies

Collect client assets and revisions directly from Gmail.

---

# Future Improvements

Possible upgrades:

- Google Drive upload
- S3 integration
- OCR support
- Virus scanning
- Database logging
- ERP API integration
- WhatsApp notifications

---

# License

MIT License
