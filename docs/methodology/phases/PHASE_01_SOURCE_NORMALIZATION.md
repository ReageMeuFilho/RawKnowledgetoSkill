# Phase 1: Source Normalization

## Objective

Transform raw source materials into clean, timestamped, citable references that can be traced throughout the skill creation process.

---

## Inputs

- Raw videos (mp4, mov, etc.)
- Documents (PDF, DOCX, etc.)
- Interview recordings/notes
- Chat logs/conversations
- Existing SOPs/manuals

## Outputs

- `source_manifest.yaml` - Catalog of all sources
- Timestamped transcripts (JSON)
- Extracted markdown documents
- Indexed references

---

## Process

### Step 1: Inventory All Source Materials

Create a manifest listing every piece of source material:

```yaml
# 01-sources/manifest.yaml
sources:
  - id: VID-001
    type: video
    title: "Property Manager Training - Emergency Protocols"
    path: "videos/emergency-protocols.mp4"
    duration: "45:32"
    date: 2024-06-15
    sme: "Maria Santos"
    language: pt-BR
    
  - id: DOC-001
    type: document
    title: "Condo Bylaws v2.3"
    path: "documents/bylaws_v2.3.pdf"
    effective_date: 2024-01-01
    sections: 12
```

### Step 2: Transcribe Videos with Timestamps

Use Whisper or AssemblyAI for accurate timestamped transcription:

```bash
# Using Whisper
whisper videos/emergency-protocols.mp4 \
  --model large-v3 \
  --language pt \
  --output_format json \
  --output_dir transcripts/
```

Output format required:

```json
{
  "segments": [
    {
      "id": 0,
      "start": 0.0,
      "end": 4.5,
      "text": "Hoje vamos cobrir os protocolos de emergência para vazamentos."
    },
    {
      "id": 1,
      "start": 4.5,
      "end": 12.3,
      "text": "A primeira coisa que você precisa fazer é classificar a gravidade."
    }
  ]
}
```

### Step 3: Extract Documents to Markdown

Convert documents to citable markdown:

```markdown
<!-- 02-references/policies/leak-escalation-policy.md -->
# Leak Escalation Policy

**Source:** Condo Bylaws v2.3, Section 4.2
**Effective Date:** 2024-01-01
**Document ID:** DOC-001

## 4.2.1 Severity Classifications

### Emergency (Immediate Response Required)
- Standing water affecting multiple units
- Active flooding from burst pipe
- Water intrusion near electrical panels

### Urgent (Response within 2 hours)
- Active leak contained to single unit
- Water damage spreading to adjacent areas

### Routine (Response within 24 hours)
- Minor drip, no active spreading
- Cosmetic water damage only

---
*Extracted from DOC-001, pages 23-25*
```

### Step 4: Identify Procedures in Sources

Watch/read through sources and tag procedure locations:

```yaml
# In source manifest, add procedure identification
- id: VID-001
  procedures_identified:
    - name: "Leak Triage Protocol"
      timestamp_start: "12:34"
      timestamp_end: "15:22"
      description: "Main procedure for classifying and routing leak reports"
      
    - name: "After-Hours Escalation"
      timestamp_start: "28:10"
      timestamp_end: "32:45"
      description: "Special handling for issues outside business hours"
```

### Step 5: Capture Key Quotes

Extract exact wording for use in conversation examples:

```yaml
key_quotes:
  - source_id: VID-001
    timestamp: "13:45"
    speaker: "Maria Santos"
    quote: "A primeira coisa é sair do cômodo. Nunca toque em nada elétrico quando houver faíscas."
    relevance: "Emergency safety instruction - exact wording"
    
  - source_id: VID-001
    timestamp: "14:12"
    speaker: "Maria Santos"  
    quote: "Ligue 193 imediatamente. Depois me liga que eu mando o eletricista."
    relevance: "Emergency response protocol - exact wording"
```

---

## Quality Gate

Before proceeding to Phase 2, verify:

- [ ] All videos have timestamped transcripts
- [ ] All documents are extracted to markdown with section references
- [ ] Each source has a unique ID (VID-XXX, DOC-XXX, INT-XXX)
- [ ] Procedures are identified with locations
- [ ] Key quotes are captured with exact wording
- [ ] Source manifest is complete and validated
- [ ] No conflicting information between sources (or conflicts documented)

---

## Tools

### Transcription Options

| Tool | Best For | Output |
|------|----------|--------|
| Whisper (OpenAI) | High accuracy, local | JSON with timestamps |
| AssemblyAI | Real-time, speaker diarization | JSON with speakers |
| Rev.ai | Professional quality | SRT/VTT files |

### Document Extraction

| Tool | Best For | Output |
|------|----------|--------|
| PyMuPDF | PDFs with structure | Markdown |
| Pandoc | DOCX conversion | Markdown |
| Docling | Complex documents | Structured JSON |

---

## Common Issues

### Issue: Video has multiple speakers
**Solution:** Use AssemblyAI with speaker diarization, tag each speaker

### Issue: Document is scanned/image-based
**Solution:** Use OCR (Tesseract) before extraction, verify accuracy

### Issue: Source contains conflicting information
**Solution:** Document conflict in manifest, flag for SME clarification

### Issue: Audio quality is poor
**Solution:** Use larger Whisper model, or request cleaner recording

---

## Example Output

After Phase 1, your directory should look like:

```
01-sources/
├── manifest.yaml           # Complete source catalog
├── videos/
│   └── emergency-protocols.mp4
├── documents/
│   ├── bylaws_v2.3.pdf
│   └── vendor_sla.pdf
├── transcripts/
│   └── emergency-protocols.json
└── interviews/
    └── landlord_carlos_2024-01-04.md

02-references/
├── policies/
│   ├── leak-escalation-policy.md
│   └── expense-approval-policy.md
├── contacts/
│   └── vendor-list.md
└── procedures/
    └── after-hours-protocol.md
```

---

## Next Phase

Once all quality gates pass, proceed to [Phase 2: Knowledge Extraction](PHASE_02_KNOWLEDGE_EXTRACTION.md)

