# הגדרת n8n-MCP להוסטינגר שלך ✅

## מה עשיתי?

הגדרתי את n8n-MCP כך שתוכל להשתמש ב-1,084 nodes של n8n ישירות מ-Claude!

## הגדרות שהוגדרו

**API URL שלך:** `https://omern8n.cloud`
**קובץ הגדרות:** `~/.config/Claude/claude_desktop_config.json`

### מה נמצא בקובץ ההגדרות?

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "https://omern8n.cloud",
        "N8N_API_KEY": "[המפתח שלך]",
        "N8N_MCP_TELEMETRY_DISABLED": "true"
      }
    }
  }
}
```

## איך להשתמש?

### 1️⃣ אתחל את Claude Desktop
אם אתה משתמש ב-Claude Desktop, אתחל אותו מחדש כדי שההגדרות ייכנסו לתוקף.

### 2️⃣ התחל לעבוד עם n8n
עכשיו אתה יכול לבקש מ-Claude:

**דוגמאות:**
- "הראה לי את כל ה-workflows שלי ב-n8n"
- "צור workflow חדש ששולח מייל כשמתקבלת הודעה חדשה"
- "חפש לי nodes שקשורים ל-Slack"
- "הסבר לי איך עובד ה-HTTP Request node"
- "הפעל את workflow מספר 123"

### 3️⃣ בדיקה מהירה
אתה יכול לבדוק שהכל עובד על ידי:

```bash
npx n8n-mcp --version
```

## 🎯 מה המערכת יכולה לעשות?

✅ **גישה לכל 1,084 nodes של n8n**
- חיפוש ב-nodes לפי קטגוריה
- קבלת תיעוד מפורט על כל node
- דוגמאות שימוש

✅ **ניהול workflows**
- רשימת workflows
- יצירת workflows חדשים
- עדכון workflows קיימים
- הפעלה של workflows

✅ **ניהול credentials**
- רשימת credentials
- יצירה ועדכון

## ⚠️ אזהרות חשובות

1. **אל תערוך workflows בפרודקשן ישירות** - תמיד צור עותק לפני עריכה
2. **בדוק שינויים** - תמיד בדוק ב-dev environment לפני production
3. **גיבוי** - שמור גיבויים של workflows חשובים

## 🔧 פתרון בעיות

### אם n8n-MCP לא עובד:

1. **בדוק שNode.js מותקן:**
```bash
node --version
npm --version
```

2. **בדוק את קובץ ההגדרות:**
```bash
cat ~/.config/Claude/claude_desktop_config.json
```

3. **הפעל ידנית:**
```bash
npx n8n-mcp
```

### אם יש שגיאת אימות (401/403):

ייתכן שה-API key פג תוקף. צור API key חדש ב-n8n:
1. היכנס ל-https://omern8n.cloud
2. לך ל-Settings → API
3. צור API key חדש
4. עדכן את הקובץ `~/.config/Claude/claude_desktop_config.json`

## 📝 הערות נוספות

- **טלמטריה כבויה** - לא נאסף מידע על השימוש שלך
- **ההתקנה דרך NPX** - לא דורשת התקנה קבועה, npx מוריד את החבילה בפעם הראשונה
- **עובד עם כל n8n** - לא משנה איפה ה-n8n רץ (Hostinger, Docker, Cloud, וכו')

---

## 🚀 מוכן לעבודה!

עכשיו תוכל לעבוד עם n8n ישירות מהשיחה עם Claude. פשוט תבקש ממנו לעשות משהו והוא ישתמש ב-n8n-MCP מאחורי הקלעים.

**צריך עזרה?** פשוט שאל אותי מה אתה רוצה לעשות עם n8n ואני אעזור לך! 😊
