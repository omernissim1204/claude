# מדריך התקנת Workflow - אוטומציה מלאה מ-PDF לשאלות ואינפוגרפיקות

## 📋 תוכן עניינים
1. [סקירה כללית](#סקירה-כללית)
2. [דרישות מקדימות](#דרישות-מקדימות)
3. [הגדרת Telegram Bot](#הגדרת-telegram-bot)
4. [הגדרת Credentials ב-n8n](#הגדרת-credentials-בn8n)
5. [ייבוא ה-Workflow](#ייבוא-הworkflow)
6. [בדיקה והרצה](#בדיקה-והרצה)
7. [פתרון בעיות](#פתרון-בעיות)

---

## 🎯 סקירה כללית

### מה ה-Workflow עושה?

1. **מקבל PDF דרך Telegram** 📱
2. **שואל את שם הקורס**
3. **מנתח את הסיכום עם Claude** ומוציא 40-60 נושאים לאינפוגרפיקות
4. **במקביל:**
   - יוצר **50 שאלות אמריקאיות** ושומר ב-Supabase
   - יוצר **פרומפטים לאינפוגרפיקות** → Gemini יוצר תמונות → שומר ב-Supabase Storage
5. **מעדכן אותך בטלגרם** כשהכל מוכן! ✅

### זמן ריצה משוער
- ניתוח ראשוני: ~1-2 דקות
- יצירת שאלות: ~2-3 דקות
- יצירת אינפוגרפיקות (40-60): ~10-15 דקות
- **סה"כ: 13-20 דקות** לקורס מלא

---

## ✅ דרישות מקדימות

### 1. **Telegram Bot**
- [ ] צריך ליצור bot חדש דרך [@BotFather](https://t.me/botfather)
- [ ] תקבל **Bot Token** (שמור אותו!)

### 2. **API Keys שכבר יש לך:**
- [x] Claude API Key: `sk-ant-api03-NFXT...` ✓
- [x] Supabase URL + Service Role Key ✓
- [ ] **Gemini API Key** - יש לך? (צריך לבדוק)

### 3. **n8n פועל ומחובר:**
- [x] n8n רץ ב-Hostinger ✓
- [x] יש גישה לממשק n8n ✓

---

## 🤖 הגדרת Telegram Bot

### צעד 1: יצירת Bot
1. פתח את Telegram ושלח הודעה ל-[@BotFather](https://t.me/botfather)
2. שלח: `/newbot`
3. בחר שם לבוט, למשל: `Course Automation Bot`
4. בחר username, למשל: `omer_course_bot`
5. **שמור את ה-Token שתקבל!** משהו כמו:
   ```
   123456789:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

### צעד 2: הגדרות נוספות (אופציונלי)
```
/setdescription - בוט לעיבוד אוטומטי של סיכומי קורסים
/setabouttext - ממיר PDF לשאלות ואינפוגרפיקות
```

---

## 🔑 הגדרת Credentials ב-n8n

### 1. **Telegram API**
1. ב-n8n: Settings → Credentials → Add Credential
2. בחר: **Telegram API**
3. הכנס:
   - **Access Token**: ה-token מ-BotFather
4. שמור בשם: `Telegram Bot`

### 2. **Claude (Anthropic) API**
1. Credentials → Add Credential
2. בחר: **Anthropic API** (או צור HTTP Header Authentication)
3. הכנס:
   - **API Key**: `YOUR_CLAUDE_API_KEY` (מהקובץ הצדדי שקיבלת)
4. שמור בשם: `Claude API`

### 3. **Supabase API**
1. Credentials → Add Credential
2. בחר: **Supabase API**
3. הכנס:
   - **Host**: `YOUR_SUPABASE_URL`
   - **Service Role Key**: `YOUR_SUPABASE_SERVICE_ROLE_KEY`
4. שמור בשם: `Supabase`

### 4. **Gemini API**
1. Credentials → Add Credential
2. בחר: **Google AI (Gemini) API**
3. הכנס:
   - **API Key**: [צריך לבדוק אם יש]
4. שמור בשם: `Gemini API`

> **שים לב:** אם אין Gemini API key, אפשר להשיג אחד חינם ב-[Google AI Studio](https://makersuite.google.com/app/apikey)

---

## 📥 ייבוא ה-Workflow

### גרסה מפושטת - ללא Gemini (רק שאלות)

אם אין לך Gemini API, אפשר להתחיל עם workflow פשוט שרק יוצר שאלות:

1. ב-n8n: **Workflows → Add Workflow**
2. שם: `Course Automation - Questions Only`
3. לחץ על **Import from File**
4. העלה את הקובץ: `course-automation-workflow-simple.json`

### גרסה מלאה - עם Gemini

1. ודא שיש לך Gemini API key מוגדר
2. ב-n8n: **Workflows → Add Workflow**
3. שם: `Course Automation - Full`
4. לחץ על **Import from File**
5. העלה את הקובץ: `course-automation-workflow.json`

### לאחר הייבוא:

1. **עדכן Credentials בכל node:**
   - פתח כל node שמסומן באדום (שגיאת credentials)
   - בחר את ה-credential המתאים מהרשימה
   - שמור

2. **הפעל את ה-Workflow:**
   - בפינה הימנית עליונה: **Inactive → Active**

---

## 🧪 בדיקה והרצה

### בדיקה ראשונית:

1. **שלח הודעה לבוט שלך בטלגרם**
   - פתח את הבוט (@your_bot_username)
   - שלח: `/start`
   - הבוט אמור להגיב (אם לא, בדוק שה-workflow פעיל)

2. **העלה PDF לבדיקה:**
   - שלח קובץ PDF קטן (5-10 עמודים) לבוט
   - הבוט ישאל: "מה שם הקורס?"
   - הקלד שם, למשל: `test_course`
   - המתן לתוצאות!

3. **עקוב אחרי הביצוע:**
   - ב-n8n: **Executions** → תראה את הריצה החיה
   - בטלגרם: תקבל עדכוני progress
   - ב-Supabase: בדוק שהשאלות נכנסו לטבלה

### מה אמור לקרות:

```
📱 "קיבלתי את הקובץ! מה שם הקורס?"
   ↓ (אתה משיב)
⚙️ "מעולה! מתחיל לעבוד על הקורס..."
   ↓ (1-2 דקות)
✅ "ניתוח הסיכום הושלם! מתחיל ליצור שאלות ואינפוגרפיקות..."
   ↓ (10-15 דקות)
🎉 "הושלם! 50 שאלות נוספו, 45 אינפוגרפיקות נוצרו"
```

---

## 🔧 פתרון בעיות

### ❌ הבוט לא מגיב בטלגרם

**פתרונות:**
1. בדוק שה-workflow **Active** (ירוק)
2. בדוק את ה-Telegram Credential
3. ב-n8n: **Executions** → בדוק אם יש שגיאות
4. נסה: **Deactivate → Save → Activate** שוב

### ❌ שגיאה בהעלאת PDF

**אפשרויות:**
1. הקובץ גדול מדי? נסה קובץ קטן יותר (<10MB)
2. זה באמת PDF? לא Word/תמונה
3. ב-n8n executions - בדוק את השגיאה המדויקת

### ❌ Claude מחזיר שגיאת 401/403

**פתרון:**
- API Key לא תקין או פג תוקף
- בדוק את ה-Claude Credential
- נסה API key חדש

### ❌ השאלות לא נכנסות ל-Supabase

**בדוק:**
1. ה-Supabase Credential נכון?
2. יש RLS (Row Level Security) על הטבלה? כבה אותו או הוסף policy
3. המבנה של הטבלה תואם?
   ```sql
   -- Structure should be:
   CREATE TABLE quiz_questions (
     id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
     course_id TEXT NOT NULL,
     question TEXT NOT NULL,
     options JSONB NOT NULL,
     explanation TEXT,
     difficulty TEXT,
     created_at TIMESTAMPTZ DEFAULT NOW()
   );
   ```

### ❌ Gemini לא יוצר תמונות

**אפשרויות:**
1. אין Gemini API key מוגדר
2. חרגת מה-quota החינמי של Gemini
3. הפרומפט ארוך מדי - בדוק ב-executions

**פתרון זמני:** השתמש ב-workflow הפשוט (שאלות בלבד) ויצור את האינפוגרפיקות ידנית אחר כך

### ❌ הכל תקוע/לוקח המון זמן

**זה נורמלי אם:**
- יש 50+ אינפוגרפיקות ליצור
- Claude מעבד PDF גדול (100+ עמודים)

**טיפים:**
- תן לזה לרוץ, אל תבטל
- יש timeout ב-n8n? הגדל אותו ב-Settings
- אפשר לפצל ל-2 workflows נפרדים (שאלות + אינפוגרפיקות)

---

## 📊 סטטיסטיקות ועלויות

### עלויות משוערות לקורס:

**Claude API:**
- ניתוח PDF (50 עמודים): ~$0.10
- יצירת 50 שאלות: ~$0.20
- יצירת 50 פרומפטים: ~$0.15
- **סה"כ Claude: ~$0.45**

**Gemini API:**
- יצירת 50 תמונות: חינם (עד 60/דקה)
- אם חרגת: ~$0.10-0.20

**Supabase:**
- Storage: חינם (עד 1GB)
- Database: חינם (עד 500MB)

**סה"כ לקורס: ~$0.45-0.65** 💰

---

## 🎓 טיפים לשימוש

### להפיק את המקסימום:

1. **PDFs איכותיים:**
   - וודא שה-PDF ברור וקריא
   - אם יש גרפים חשובים, וודא שהם ברזולוציה טובה

2. **שמות קורסים:**
   - השתמש בשמות קצרים ועקביים
   - אנגלית בלי רווחים (למשל: `micro_bio` במקום `Microbiology 101`)

3. **ניהול קורסים:**
   - שמור רשימה של course_ids שיצרת
   - אפשר להריץ שוב על אותו קורס - יתווספו שאלות חדשות

4. **אינפוגרפיקות:**
   - אם לא מרוצה מאינפוגרפיקה, אפשר ליצור מחדש רק אותה
   - שמור את הפרומפטים שקיבלת - הם שימושיים!

---

## 📞 תמיכה

### אם משהו לא עובד:

1. **בדוק את ה-Executions ב-n8n** - יש שם לוג מפורט
2. **בדוק את הטבלאות ב-Supabase** - מה נכנס ומה לא
3. **בדוק את התשובות של Claude** - האם הן בפורמט הנכון?

### לוגים חשובים:
- n8n: **Executions → בחר ריצה → View Details**
- Supabase: **Table Editor → quiz_questions**
- Telegram: הודעות מהבוט

---

## 🚀 שלב הבא

### רעיונות לשיפור:

1. **תזמון אוטומטי:**
   - הוסף node שמקשיב לתיקייה ב-Google Drive
   - כל PDF חדש עובר אוטומטית

2. **דוחות:**
   - הוסף node ששולח דוח מסכם במייל
   - עם קישורים לשאלות והאינפוגרפיקות

3. **בחירת רמת קושי:**
   - תן לסוכן לקבוע difficulty (easy/medium/hard) לכל שאלה
   - לפי מורכבות המושג

4. **ולידציה:**
   - הוסף node שבודק שכל שאלה תקינה לפני הכניסה ל-DB
   - מונע שאלות broken

---

**בהצלחה! 🎉**

אם יש בעיות - אני כאן לעזור! 😊
