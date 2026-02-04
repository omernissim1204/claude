# 🎓 Course Automation Workflows

אוטומציה מלאה ליצירת תוכן לימודי מ-PDF: שאלות אמריקאיות + אינפוגרפיקות.

## 📁 קבצים בפרויקט

### 1. **Workflows**
- ⭐ `course-automation-v2.json` - **גרסה חדשה!** עם Langchain nodes (מומלץ!)
- `course-automation-simple.json` - גרסה ראשונה (HTTP requests)
- `course-automation-workflow.json` - ניסוי ראשוני (לא לשימוש)

### 2. **מדריכים**
- ⭐ `V2-SETUP-GUIDE.md` - **מדריך ל-v2** (התחל כאן!)
- `workflow-installation-guide.md` - מדריך ל-v1
- `n8n-mcp-setup.md` - הגדרת n8n-MCP עם Claude Desktop

---

## 🚀 התחלה מהירה

### צעד 1: הכן API Keys
אתה צריך:
- [ ] Telegram Bot Token ([צור כאן](https://t.me/botfather))
- [x] Claude API Key (יש לך!)
- [x] Supabase credentials (מוגדר!)
- [ ] Gemini API (אופציונלי - לאינפוגרפיקות)

### צעד 2: ייבא ל-n8n
1. פתח את n8n שלך: https://omern8n.cloud
2. **Workflows → Import from File**
3. בחר: `course-automation-simple.json`
4. הגדר credentials (ראה מדריך מפורט)
5. **Activate!**

### צעד 3: שלח PDF
1. פתח את הבוט שלך בטלגרם
2. שלח PDF **עם caption**: `/course שם_הקורס`

   או פשוט שלח PDF והבוט יזהה אוטומטית!

3. המתן 10-15 דקות
4. תקבל הודעה כשמוכן! ✅

---

## 🎯 מה ה-Workflow עושה?

```
📱 PDF בטלגרם
    ↓
🤖 Claude מנתח → 40-60 נושאים
    ↓
    ├─→ 50 שאלות אמריקאיות → 💾 Supabase
    └─→ פרומפטים לאינפוגרפיקות → 💾 קובץ
```

### פלט:
- ✅ **50 שאלות** בטבלה `quiz_questions`
- ✅ **40-60 פרומפטים** מוכנים ל-Gemini
- ✅ **קורס חדש** בטבלה `course_settings`

---

## 📊 טבלאות Supabase

### `quiz_questions`
```json
{
  "id": "uuid",
  "course_id": "text",
  "question": "text",
  "options": [
    {"id": "A", "text": "...", "isCorrect": true/false}
  ],
  "explanation": "text",
  "difficulty": "easy/medium/hard",
  "created_at": "timestamp"
}
```

### `course_settings`
```json
{
  "course_id": "text",
  "display_name": "text",
  "enabled": true/false,
  "updated_at": "timestamp"
}
```

---

## 💡 טיפים לשימוש

### שמות קורסים:
```
✅ טוב: psychopathology
✅ טוב: micro_bio
❌ לא טוב: Psychopathology 101
❌ לא טוב: קורס בפסיכופתולוגיה
```

### שליחת PDF:
```
/course psychopathology
[צרף PDF]

או פשוט:
[צרף PDF]  ← הבוט יזהה מהקובץ
```

### אם משהו תקוע:
1. בדוק **Executions** ב-n8n
2. בדוק את הטבלאות ב-Supabase
3. ראה: **פתרון בעיות** במדריך המפורט

---

## 📖 מדריכים מפורטים

- **התקנה מלאה**: קרא `workflow-installation-guide.md`
- **n8n-MCP setup**: קרא `n8n-mcp-setup.md`

---

## 🔧 טכנולוגיות

- **n8n** - Workflow automation
- **Claude API** - ניתוח PDF + יצירת תוכן
- **Supabase** - Database + Storage
- **Telegram** - Interface
- **Gemini** - יצירת אינפוגרפיקות (אופציונלי)

---

## 💰 עלויות משוערות

לכל קורס (PDF 50 עמודים):
- Claude API: ~$0.45
- Gemini: חינם (60 תמונות/דקה)
- Supabase: חינם (עד 1GB)
- Telegram: חינם

**סה"כ: ~$0.45 לקורס** 🎉

---

## ✅ Status

- [x] n8n-MCP מוגדר עם Claude Desktop
- [x] Workflow מוכן לייבוא
- [x] Supabase מחובר
- [x] Claude API מוכן
- [ ] Telegram Bot (צריך להגדיר)
- [ ] Gemini API (אופציונלי)

---

## 📞 תמיכה

יש בעיה? בדוק:
1. **n8n Executions** - לוגים מפורטים
2. **Supabase Table Editor** - מה נשמר?
3. **המדריך המפורט** - פתרון בעיות נפוצות

---

**נוצר עם ❤️ ב-Claude Code**

Session: https://claude.ai/code/session_01NtLE8pjCt3tpaDw98HWUYH
