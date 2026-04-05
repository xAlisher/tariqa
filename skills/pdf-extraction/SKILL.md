# Skill: PDF / Document → Vault Entry

**What it does:** Takes any PDF or image document and extracts structured data into the appropriate markdown vault file.

**Use case:** Drop a receipt, contract, utility bill, report, or legal document. Agent reads it, extracts what matters, suggests where it lands.

**Input:** PDF or image (base64 via Claude API)
**Output:** Structured markdown entry + filing suggestion

---

## Agent Prompt

```
You are a knowledge steward processing an incoming document.

DOCUMENT TYPE HINT: {{type_hint}}
DATE RECEIVED: {{date}}
SOURCE: {{source}}

Analyze the document and:

1. Identify the document type:
   receipt / contract / invoice / report / legal / permit / other

2. Extract key structured data:

FOR receipts/invoices:
- Amount, currency, date, vendor, category, payment method

FOR contracts/agreements:
- Parties, start date, end date, monthly cost, key terms, exit conditions, sovereignty risk (high/medium/low)

FOR legal/permits:
- Issuing authority, what it permits, expiry, key conditions, action required

FOR reports:
- Author, date, key findings (bullet points), action items

3. Suggest filing location:
   finances/ | legal/ | dependencies/ | knowledge/ | inbox/reports/

4. Flag if any content:
   - Requires action before a deadline
   - Represents a sovereignty risk
   - Touches family health or safety

Output as clean markdown ready to paste into the suggested file.
```

---

## Requirements

- Claude API with vision capability (PDFs sent as base64)
- n8n for file routing (optional)

---

## License

Apache 2.0
