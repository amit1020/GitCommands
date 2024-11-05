
# התחנות (areas) שהקבצים יכולים להימצאות

![Git Summary](./Screenshot%202024-11-03%20at%2021.23.58.png)

## הגדרות ראשוניות

### הגדרת שם משתמש

```sh
git config --global user.name "<your user name>"
```


### הגדרת אימייל

```sh
git config --global user.email "<your email>"
```
<br/><br/>

> [!NOTE]
> It is important to configure these settings after running [git](url) for the first time.

<br/>

# פקודות בסיסיות

### git init 

מאתחל מאגר git חדש בתיקייה, יוצר קובץ git. נסתר
```sh
git init
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git status 
מציג את ממצב הקבצים במאגר, כולל קבצים בשלבים השונים וקבצים שנעשו בהם שינויים

```sh
git status
```

<br><br><br>
# ניהול גרסאות commit

### git add 

מוסיף קובץ ספציפי לשלב ה-staging area  או את כל הקבצים

```sh
git add <file.name>  #add specific file in stagin area

git add .  #add all files in staging area
```

> [!IMPORTANT]
> all areas explain at the top of the page

<br><br>

### commit 
יוצר קומיט הודעה מפורטת

```sh
git commit -m "<commit name>" #useing after user add  

git commit -am "<commit name>" #Marks and adds all changes to the tracking (no new files) and commits.
```
<br><br><br>

# היסטוריה גרסאות
### git log 
בעזרתו נוכל לצפות ברשימת הקומטים שבוצעו במאגר הנוכחי. כל שורת קומיט כוללת את ה-hash(מזהה) הייחודי לו, את השם הכותב, את תאריך ושעת הקומיט, ולעיתים הודעה שמסבירה גם את השינויים שבוצעו

```sh
git log #מציג את כל ההיסטוריה של הקומיטים בפורמט מלא

git log --author <user name> #על מנת לצפות בקומיטים שנוצרו ע״י משתמש מסויים

git log -n <number:int> #במידה ויהיה לנו המון קומיטים ונרצה לקבל רק מספר מסויים של קומיטים

git log --oneline #מציגת את היסטוריית הקומיטים בשורה אחת עבור כל קומיט.

git log --since="<date: 2023-01=01>" --until="<date: 2023-12-31>"

git log --grep="<name>" # חיפוש הודעות קומיט הכוללות מילה מוסיימת

git log -p # כדי לראות את השינויים בכל קומיט, כך קומיט יכיל גם את השינויים המלאים שבוצעו בו

git log --stat #מציכ תיאור כללי של שינויים(סטטיסטיקה בלבד, הפקודה תציג את מספר השורות ששונו בכל קובץ בכל בקומיט 

git log -- <path/to/file> # אם רוצים לראות היסטוריה של קובץ או תיקייה מסויים, יציג את כל הקומיטים שבהם הקובץ שונה

git log --oneline --graph --decorate --all #פקודה זו תציג את כל הקומיטים בכל הענפים, עם מזהי קומיט מקוצרים,גרף, ותצוגה גרפית של ראשי הענפים והתגיות

git log --shortstat # אפשר לראות כמה שורות נוספו או הוסרו בכל קומיט

git log <Branch1>..<Branch2> #מאפשר להשוות את הענף הנוכחי לענף אחר, יציג את הקומיטים שנמצאים בבראנצ 2 ולא נמצאים בבראנצ 1  

git log --decorate #הפקודה תציג כל קומיט עם פרטים על הבראנצ או התגית שקשורים אליו

```
> [!IMPORTANT]
> אם רוצים דוגמה מסויימת מומלץ להשתמש בchatgpt

<br><br>

### git diff

```sh
# 1. השוואה בין שינויים לא מסומנים (Unstaged Changes)
# פקודה זו מציגה את כל השינויים שבוצעו בקבצים אך טרם נוספו ל-stage (לא בוצע להם git add).
git diff

# 2. השוואה בין שינויים מסומנים (Staged Changes)
# פקודה זו מציגה את השינויים בקבצים שנוספו ל-stage בעזרת git add, אך טרם בוצע להם commit.
git diff --staged  # אפשר גם להשתמש ב --cached

# 3. השוואה בין קומיט קודם (commit) לגרסה הנוכחית
# הפקודה הבאה תשווה בין הקומיט האחרון לבין השינויים הקיימים בסביבת העבודה (working directory).
git diff HEAD

# 4. השוואה בין קומיטים ספציפיים
# אפשר לציין שני קומיטים לפי המזהה (hash) שלהם כדי לראות את ההבדלים ביניהם.
# נניח שאנחנו רוצים להשוות בין שני קומיטים עם ה-IDs abc1234 ו-def5678.
git diff abc1234 def5678

# 5. השוואה בין הענף הנוכחי לענף אחר
# כאן אנחנו משווים בין הענף הפעיל (למשל "feature-branch") לבין ענף אחר (כמו "main").
# שימושי כשצריך לראות מה השינויים בין שני הענפים.
git diff main feature-branch

# 6. הצגת השינויים בקובץ מסוים בלבד
# כדי לראות את ההבדלים בקובץ מסוים בסביבת העבודה, ניתן לציין את הנתיב שלו בסוף הפקודה.
git diff path/to/file.txt

# 7. הצגת שינויים עם הקשר נוסף (Context)
# `-U` (או `--unified`) מאפשר להגדיר כמה שורות של "הקשר" מסביב לכל שינוי יופיעו בפלט.
# למשל, נשתמש ב-3 שורות הקשר:
git diff -U3

# 8. הצגת שינויים בקובץ מסוים בין קומיטים
# אם רוצים לראות את השינויים בקובץ מסוים בין שני קומיטים, נשתמש בפקודה עם המזהים של הקומיטים ונתיב הקובץ.
git diff abc1234 def5678 -- path/to/file.txt

# 9. הצגת שינויים בקובץ בין הענף הנוכחי לענף אחר
# מציג את ההבדלים בקובץ מסוים בין הענף הפעיל לבין ענף אחר (למשל "main").
git diff main -- path/to/file.txt

# 10. הצגת תקציר של השינויים (קבצים בלבד, בלי פירוט מלא)
# פקודה זו תציג רק אילו קבצים השתנו, מבלי להראות את ההבדלים עצמם.
git diff --name-only

# 11. הצגת סטטיסטיקות של השינויים
# מציג את מספר השורות שנוספו ונמחקו בכל קובץ, ולא את התוכן עצמו.
git diff --stat

# 12. השוואה תוך התעלמות מהבדלים במרווחים (רווחים, טאב, רווחים בסוף השורות)
# שימושי אם רוצים לראות שינויים בתוכן בלבד, ולא שינויים הקשורים לעיצוב קוד.
git diff -w

```


# ניהול קבצים ושינויים

```sh

git rm <file_name> #מסיר קובץמהמיקום שלו ומוסיף את ההסרה ל 

```









# עבודה עם branch

###  git branch 
מציג את כל הברנצ׳ים הקיימים 
```
git branch 
```






### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```

### git clone 
משכפל מאגר מרוחק למחשב

```sh
git clone https://github.com.user/repo.git
```



