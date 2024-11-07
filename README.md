
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
> It is important to configure these settings after running [git](https://git-scm.com) for the first time.
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
# מעבר בין areas
#### add stash 

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
> [!IMPORTANT]
> אם רוצים דוגמה מסויימת מומלץ להשתמש בchatgpt

<br><br>
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

### git show
מאפשרת להציג מידע מפורט על קומיט ספציפי. זה כולל את מזהה הקומיט, מחבר הקומיט, תאריך הקומיט, ההודעה וכן את השינויים שבוצעו בקבצים. אפשר להגיד שזה שילוב של גיט לוג וגיט דיף

```sh
# הצגת commit ספציפי
git show <commit_hash>

#שימוש בדגלים להצגת מידע נוסף:


git show --pretty=oneline <commit_hash>     # הצגת commit בשורה אחת
git show --pretty=short <commit_hash>        # פורמט קצר של commit
git show --pretty=full <commit_hash>         # פורמט מלא עם פרטים נוספים
git show --pretty=format:"%h %an %s" <commit_hash>  # פורמט מותאם אישית

# הצגת שמות הקבצים בלבד
git show --name-only <commit_hash>

# הצגת שמות הקבצים עם סטטוס (A - הוספה, D - מחיקה)
git show --name-status <commit_hash>

# הצגת סיכום סטטיסטי של השינויים
git show --stat <commit_hash>

# הצגת כל הפאץ' (ברירת המחדל)
git show -p <commit_hash>

# הצגת תוכן קובץ מסוים מענף מסוים
git show main:README.md

# הצגת מידע על תגית
git show <tag_name>

# צמצום הבדלים לנתיב מסוים
git show --relative=<path> <commit_hash>

# הצגת commit בלי השינויים בקוד (רק הכותרת והמטא-דאטה)
git show --no-patch <commit_hash>
```

### git reflog
הפקודה ```git reflog``` מציגה את ההיסטוריה של השינויים ב-HEAD. זה כולל לא רק את ה-commits, אלא גם את השינויים בענפים (branches), פעולות מיזוג (merges) ושימוש בפקודות כמו git reset. הפקודה מהווה כלי שימושי במיוחד למעקב אחרי שינויים שנעשו ב-HEAD, גם כאשר נעשו פעולות מורכבות שעלולות להשפיע על ההיסטוריה של המאגר.
 
```sh
# הצגת היסטוריית ה-HEAD (ברירת המחדל)
git reflog

# הצגת היסטוריית הפניות של branch מסוים (כגון main)
git reflog show main

# הצגת מספר מוגבל של ערכים אחרונים (לדוגמה, 5 ערכים)
git reflog -n 5

# שימוש בפורמט מותאם אישית להצגת ההיסטוריה
git reflog --pretty=oneline
git reflog --pretty=format:"%h %gd %gs"

# הצגת ההיסטוריה עם נתוני תאריך בפורמטים שונים
git reflog --date=iso
git reflog --date=relative

# מחיקת ערכי reflog ישנים (נדרשת זהירות!)
git reflog expire --expire=now --all

# שחזור commit שנמצא ב-reflog באמצעות reset
git reset --hard HEAD@{2}

# הצגת היסטוריית ההפניות של תגית (tag) מסוימת
git reflog show <tag_name>

# הצגת היסטוריית הפניות של אובייקט מסוים (למשל HEAD)
git reflog show HEAD
```

<br>

### git blame
הפקודה ```git blame``` משמשת למעקב אחרי היסטוריית השינויים בכל שורת קוד בקובץ ספציפי. הפקודה מציגה מי המחבר של כל שורה ומתי השורה נערכה בפעם האחרונה. זהו כלי שימושי להבנת מי שינה חלקים מסוימים בקוד, באיזה commit השינוי נעשה ומתי זה קרה.

```sh
# שימוש בסיסי להצגת היסטוריית שינויים של קובץ
git blame <filename>

# הצגת blame עבור טווח שורות מסוים (לדוגמה, שורות 10 עד 20)
git blame -L 10,20 <filename>

# הצגת blame עם תאריך בפורמט יחסי (כגון "5 days ago")
git blame --date=relative <filename>

# הצגת blame עם תאריך בפורמט ISO סטנדרטי
git blame --date=iso <filename>

# הצגת כתובת האימייל של המחבר במקום שם המחבר
git blame --show-email <filename>

# הצגת blame עבור commit ספציפי
git blame <commit_hash> -- <filename>

# הצגת blame תוך התעלמות מ-commits מסוימים (למשל, תהליך refactoring)
git blame --ignore-rev <commit_hash> <filename>

# הצגת blame עם התעלמות מ-commits מרובים (נוח לתהליכי refactoring גדולים)
git blame --ignore-revs-file=<file_with_commit_hashes> <filename>

# הצגת blame תוך דילוג על מרווחי רווח לבנים (whitespace changes)
git blame -w <filename>

# הצגת blame עם מידע נוסף כמו שם הקובץ המקורי (useful for renaming)
git blame --root <filename>

```



# ניהול קבצים ושינויים
### git rm 
הפקודה ```git rm``` משמשת למחיקת קבצים מתוך מאגר Git. היא מסירה את הקובץ גם ממערכת הקבצים שלך וגם ממצב הסטייג'ינג של Git, כך שב-commit הבא הקובץ לא ייכלל במאגר


```sh
# 1. מחיקת קובץ מהמאגרים ומהמחשב
git rm <filename>
# דוגמה:
git rm old_file.txt

# 2. הסרת קובץ מהמאגרים אך לא מהמחשב (שמור את הקובץ בתיקיית העבודה)
git rm --cached <filename>

# 3. מחיקת תיקייה ורוב קבצי משנה בתוכה (רקורסיבית)
git rm -r <directory>

# 4. מחיקת קבצים בכפייה אם הם כבר שונו בסטייג'ינג
git rm -f <filename>

# 5. מחיקת קבצים ומודעות על מחיקת קבצים שלא נמצאים במעקב (כמו קבצים חדשים)
git rm -n <filename>

# 6. מחיקת קבצים עם דגל -r (רקורסיבי) וגם עם חיפוש סיומות מסוימות
git rm -r '*.log'
```


### git reset 
הפקודה ```git reset``` ב-Git משמשת לשינוי מצבו של ה-HEAD (הנקודה בה אתה נמצא בגרסה הנוכחית של המאגר) ולביצוע שינויים בסטייג'ינג וב-working directory. עם ```git reset``` אפשר לנוע אחורה בהיסטוריה של הקומיטים או לבטל שינויים שבוצעו לאחר מכן.


```sh
# 1. git reset --soft <commit>
# Reset to a specific commit and keep changes in the staging area (changes are ready to be committed)
git reset --soft <commit>

# 2. git reset --mixed <commit>
# Reset to a specific commit and keep changes only in the Working Directory (not in the staging area)
git reset --mixed <commit>

# 3. git reset --hard <commit>
# Reset to a specific commit and remove all changes (both in the Working Directory and the staging area)
git reset --hard <commit>

# 4. git reset --merge <commit>
# Reset to a specific commit while keeping changes without creating conflicts (useful during merges)
git reset --merge <commit>

# 5. git reset --keep <commit>
# Reset to a specific commit while keeping changes in the Working Directory if they don't cause conflicts
git reset --keep <commit>

# 6. git reset <commit> (default, equivalent to --mixed)
# Reset to a specific commit while keeping changes in the Working Directory but not in the staging area
git reset <commit>

# 7. git reset --hard
# Reset to the initial state of the repository, removing all changes (nothing left in the Working Directory)
git reset --hard

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



