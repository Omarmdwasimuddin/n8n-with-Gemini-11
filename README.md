# 🤖 n8n — Gemini AI Integration Guide

> n8n এ Google Gemini AI সংযুক্ত করে Webhook দিয়ে AI-powered Email Automation তৈরির গাইড।

---

## 📊 Workflow Overview

```
index.html (Frontend)
      │  POST Request
      ▼
Webhook Node
      │
      ▼
Google Gemini (AI Response)
      │
      ▼
Gmail: Send a message
      │
      ▼
Respond to Webhook (Frontend এ Reply পাঠাও)
```

---

## ⚙️ Webhook সেটআপ

### ✅ ধাপ ১ — Webhook Node যোগ করো ও URL কপি করো

- **"Add first step"** এ ক্লিক করো
- **"Webhook"** সার্চ করো এবং ক্লিক করো
- **HTTP Method:** `POST` সিলেক্ট করো
- **POST URL** কপি করো
- `index.html` ফাইলে **Scroll** করে নিচে `WEBHOOK_URL` এর জায়গায় কপি করা URL **Paste** করো

![Webhook Setup](https://imgur.com/1m0j0Jc.png)

---

### ✅ ধাপ ২ — CORS Enable করো

n8n বন্ধ করো এবং CORS সহ আবার চালু করো:

**Step 1:** n8n বন্ধ করো
```
Ctrl + C
```

**Step 2:** CORS Enable করে n8n চালু করো
```powershell
$env:N8N_CORS_ALLOWED_ORIGINS="*"; n8n
```

> ⚠️ **কেন CORS দরকার?** `index.html` থেকে n8n এ Request পাঠাতে CORS Allow করতে হয়। না করলে Browser Request Block করবে।

---

## 🤖 Google Gemini সেটআপ

### ✅ ধাপ ৩ — Gemini Node যোগ করো

- **Webhook** এর **`+`** বাটনে ক্লিক করো
- **"Google Gemini"** সার্চ করো এবং ক্লিক করো
- **"Message a model"** সিলেক্ট করো
- **"Set up credential"** এ ক্লিক করো

---

### ✅ ধাপ ৪ — Gemini API Key নাও

নতুন Browser Tab ওপেন করো এবং নিচের ধাপগুলো করো:

```
Google AI Studio সার্চ করো
        │
        ▼
"Get started" এ ক্লিক করো
        │
        ▼
"Get API key" এ ক্লিক করো
        │
        ▼
API Key কপি করো
```

---

### ✅ ধাপ ৫ — API Key সংযুক্ত করো

- **Set up credential** এর **API Key** Field এ Paste করো
- **Save** বাটনে ক্লিক করো
- ট্যাব বন্ধ করো
- Gemini Node এ বাকি **Value** সেট করো

![Gemini Credential](https://imgur.com/znayjyY.png)
![Gemini Value Setup](https://imgur.com/2DohqCm.png)
![Gemini Model Config](https://imgur.com/O1YOiQp.png)

---

## ✉️ Gmail Node সেটআপ

### ✅ ধাপ ৬ — Gmail Node যোগ করো

- **Message a model** এর **`+`** বাটনে ক্লিক করো
- **"Gmail"** সার্চ করো → **"Send a message"** সিলেক্ট করো
- **Value** সেট করো *(Gemini এর Response কে Email Body হিসেবে ব্যবহার করো)*

![Gmail Send Message](https://imgur.com/pCm2BBA.png)

---

## 🔁 Respond to Webhook সেটআপ

### ✅ ধাপ ৭ — Respond to Webhook Node যোগ করো

- **Send a message** এর **`+`** বাটনে ক্লিক করো
- **"Respond to Webhook"** সার্চ করো এবং ক্লিক করো
- **Value** সেট করো *(Gemini এর Response Frontend এ পাঠাও)*

> 💡 **কেন দরকার?** `index.html` এ User যে Prompt দিয়েছে তার AI Response Browser এ দেখানোর জন্য।

![Respond to Webhook](https://imgur.com/JBkNSOX.png)

---

## 🔗 Final সেটআপ ও Publish

### ✅ ধাপ ৮ — Webhook আপডেট ও Publish করো

- **Webhook Node** ওপেন করো
- **Respond** সেটিং আপডেট করো
- **Production URL** কপি করো
- `index.html` এ **Paste** করো
- **Publish** বাটনে ক্লিক করো

![Webhook Update & Publish](https://imgur.com/BHkSrVs.png)

---

### ✅ ধাপ ৯ — Prompt দিয়ে Test করো

`index.html` ওপেন করো এবং Prompt দিয়ে Test করো।

![Prompt Test](https://imgur.com/D0CiQrU.png)

> ✔️ সফল হলে:
> - Gemini AI Prompt এর উত্তর তৈরি করবে
> - Gmail এ Email চলে যাবে
> - Browser এ AI Response দেখা যাবে

---

## 📚 এই Workflow এ কী কী হচ্ছে?

```
১. User → index.html এ Prompt লিখলো
          │
          ▼
২. Webhook → POST Request পেলো
          │
          ▼
৩. Gemini → Prompt পড়ে AI Response তৈরি করলো
          │
          ▼
৪. Gmail → AI Response সহ Email পাঠালো
          │
          ▼
৫. Respond to Webhook → Browser এ Response দেখালো
```

---

## 📋 Quick Reference

| ধাপ | Node | কাজ |
|-----|------|-----|
| ১ | Webhook | POST URL তৈরি করো ও index.html এ দাও |
| ২ | — | CORS Enable করে n8n Restart করো |
| ৩–৫ | Google Gemini | API Key নিয়ে Credential সেটআপ করো |
| ৬ | Gmail | AI Response সহ Email পাঠাও |
| ৭ | Respond to Webhook | Browser এ Response দেখাও |
| ৮ | — | Webhook Update করে Publish করো |
| ৯ | — | Prompt দিয়ে Test করো |

### গুরুত্বপূর্ণ মনে রাখো:

| বিষয় | বিস্তারিত |
|-------|-----------|
| **CORS** | n8n Restart এর সময় অবশ্যই দিতে হবে |
| **Test URL** | Testing এর সময় ব্যবহার করো |
| **Production URL** | Publish এর পর index.html এ দাও |
| **Respond to Webhook** | Frontend এ Response পাঠাতে দরকার |

---

*Gemini AI এর সাথে n8n সংযুক্ত করলে যেকোনো Form বা Chat Interface কে AI-Powered বানানো সম্ভব।*
