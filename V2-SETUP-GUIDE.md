# 🚀 Course Automation v2 - מדריך התקנה

## ✨ מה חדש ב-v2?

### שיפורים מרכזיים:
✅ **Langchain Anthropic nodes** - עובד ישירות עם binary, בלי base64 ידני!
✅ **Upsert במקום הנכון** - מיד אחרי Extract Course Info
✅ **3 Anthropic nodes** - כולם משתמשים ב-Langchain
✅ **פשוט יותר** - פחות nodes, פחות שגיאות
✅ **יציב יותר** - binary handling מובנה

---

## 📥 התקנה מהירה

### 1️⃣ ייבוא ל-n8n

1. פתח n8n: `https://omern8n.cloud`
2. **Workflows → Import from File**
3. בחר: `course-automation-v2.json`
4. הקובץ ייטען!

---

### 2️⃣ הגדרת Credentials

אתה צריך להגדיר **3 credentials**:

#### **A. Telegram Bot**
```
Type: Telegram API
Access Token: [מ-@BotFather]
Name: Telegram Bot
```

#### **B. Anthropic API**
```
Type: Anthropic API
API Key: YOUR_CLAUDE_API_KEY
Name: Anthropic account
```

#### **C. Supabase** (בקבצים שלך)
פשוט החלף בכל ה-nodes:
- `YOUR_SUPABASE_SERVICE_ROLE_KEY`

---

### 3️⃣ התאמת ה-Workflow

**ב-3 nodes של Anthropic:**
1. `Analyze PDF for Topics`
2. `Generate Questions`
3. `Generate Infographic Prompts`

**בכל אחד:**
- לחץ על ה-node
- בחר **Credentials** → בחר את ה-Anthropic credential שיצרת
- שמור

**ב-2 nodes של Supabase:**
1. `Upsert Course Settings`
2. `Insert Questions`

**בכל אחד:**
- פתח את ה-Headers
- החלף `YOUR_SUPABASE_SERVICE_ROLE_KEY` עם:
  ```
  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InN5enhlZGJjYXBjeW56amxwamNnIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc2Njc2NDg1NywiZXhwIjoyMDgyMzQwODU3fQ.Nlj_OO8PO4DZeEDYNj8vnqXMf0N0S7lhyxDwPFn3gks
  ```

---

## 🎯 זרימת העבודה

```
📱 PDF מטלגרם
    ↓
✅ בדיקה שזה PDF
    ↓
📝 חילוץ שם קורס
    ↓
💾 שמירת קורס ב-Supabase
    ↓
💬 הודעה: "מתחיל..."
    ↓
📥 הורדת PDF
    ↓
🤖 ניתוח ל-40-60 נושאים (Anthropic Langchain)
    ↓
📋 שמירת קונטקסט
    ↓
💬 הודעה: "יוצר שאלות..."
    ↓
    ├─→ 🤖 50 שאלות (Anthropic) → Parse → Supabase
    └─→ 🤖 פרומפטים (Anthropic) → Split
    ↓
🎉 הודעה: "הושלם!"
```

---

## 🔧 הבדלים מ-v1

| תכונה | v1 | v2 |
|-------|----|----|
| PDF handling | HTTP Request + base64 ידני | Langchain - אוטומטי |
| Anthropic nodes | HTTP Request | Langchain (מובנה) |
| Upsert timing | מאוחר מדי | מיד אחרי Extract |
| Code nodes | 1 (base64 conversion) | 2 (parse only) |
| יציבות | בעייתי | יציב |

---

## ✅ בדיקה

### שלח PDF לבוט:

**אופציה 1: עם שם**
```
/course test_course
[צרף PDF]
```

**אופציה 2: בלי שם**
```
[צרף PDF]
```
הבוט יזהה אוטומטית מהקובץ.

---

## 📊 פלט צפוי

אחרי 10-15 דקות:
```
🎉 הושלם!

✅ 50 שאלות נוספו
✅ 45 פרומפטים נוצרו

📚 קורס: test_course

הכל מוכן!
```

---

## 🐛 פתרון בעיות

### שגיאה: "Could not find credential"
**פתרון:** לך לכל Anthropic node והגדר מחדש את ה-credential.

### שגיאה: "PDF cannot be empty"
**פתרון:** בדוק ש-"Download PDF" רץ בהצלחה. הסתכל ב-Binary tab.

### Supabase 401/403
**פתרון:** בדוק את ה-Service Role Key בשני ה-nodes.

### אין פלט מ-Anthropic
**פתרון:** הגדל `maxTokens` ל-16000 בכל ה-nodes.

---

## 💰 עלויות

### לכל קורס (PDF 50 עמודים):
- **Analyze Topics**: ~$0.15 (8K tokens)
- **Generate Questions**: ~$0.25 (16K tokens)
- **Generate Prompts**: ~$0.15 (16K tokens)

**סה"כ: ~$0.55 לקורס** 🎉

---

## 🔐 אבטחה

הקובץ מכיל placeholders בלבד:
- `YOUR_SUPABASE_SERVICE_ROLE_KEY`
- `YOUR_CLAUDE_API_KEY`
- `ANTHROPIC_CREDENTIAL_ID`

**ה-credentials האמיתיים ב:** `.credentials.txt`

---

## 📝 הערות

1. **maxTokens**: כל ה-Anthropic nodes מוגדרים ל-8K-16K
2. **Model**: כולם משתמשים ב-`claude-sonnet-4-5-20250929`
3. **Binary**: אוטומטי - Langchain מטפל בהכל
4. **Parallel**: שאלות ופרומפטים נוצרים במקביל

---

## 🎓 טיפים

1. **PDFs קטנים**: התחל עם 10-20 עמודים לבדיקה
2. **שמות קורסים**: השתמש באנגלית ללא רווחים
3. **Monitoring**: עקוב אחרי Executions ב-n8n
4. **Supabase**: בדוק את הטבלאות אחרי ריצה

---

**בהצלחה! 🚀**

יש בעיות? בדוק את ה-Executions ב-n8n - יש שם לוגים מפורטים.
