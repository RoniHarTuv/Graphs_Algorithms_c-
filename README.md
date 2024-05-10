*מטלה 1 קורס תכנות מערכות 2:*

פרוייקט זה מציג את מחלקת "GRAPH" ומחלקת "ALGORITHMS" .
במחלקת GRAPH שדות הגרף הם כדלהלן:
1. מטריצת שכנויות (ווקטור דו מימדי) המייצגת את קודקודי וצלעות הגרף. צלע קיימת מקודקוד I לקודקוד J אמ"מ בתא ה [J][I] במטריצה מופיע מספר שאינו 0.
2. שדה בוליאני- האם הגרף מכוון.
3. שדה בוליאני- האם לגרף צלעות שליליות.
  
לגרף יש כמה ווריאציות בו הוא יכול להתקיים. להלן סוגי הגרפים וכיצד נקבעו:
גרף יהיה לא מכוון אם מטריצת השכנויות היא סימטרית.
גרף יהיה מכוון אם מטריצת השכנויות אינה סימטרית.
גרף יהיה ממושקל כל עוד ישנם צלעות שמשקלן שונה, אחרת, כשכל הצלעות בגרף באותו המשקל- גרף ייחשב כלא ממושקל.
בגרף ייתכנו צלעות שליליות(אם התא במטריצה מספר שלילי) וחיוביות.

במחלקת "Graph":

1.פונקציית loadGraph המקבלת את מטריצת השכנויות, מוודאת את תקינותה(שהמטריצה ריבועית, שבאלכסון יש רק אפסים..) וקובעת את שאר השדות.
2.פונקציית printGraph אחראית על ההדפסה של המטריצה יחד עם הנתונים של אותו הגרף- האם מכוון, כמה צלעות וכמה קודקודים בגרף, האם יש צלעות שליליות.
3.פונקציות get המחזירות את שדות האובייקט כיוון שהשדות הינם private.

מחלקת "Algorithms" :
המחזיקה מספר אלגוריתמים על גרפים. נפרט על אופן פעולת האלגוריתמים:

1.פונקציית "isConncted": מקבלת גרף ומחזירה true אם הגרף קשיר. גרף יהיה קשיר אמ"מ ניתן להגיע מכל קודקוד לכל קודקוד בגרף.
בגרף לא מכוון- נריץ את אלגוריתם BFS (פונקציית עזר) -במידה וכל הקודקודים "שחורים"\"בוקרו" לאחר איטרציה יחידה(לא משנה מהו קודקדו ההתחלה) - נדע שהגרף קשיר.
בגרף מכוון- נריץ BFS מכל קודקוד ונבצע את אותה הבדיקה עבור כל ריצה כזו. אם לאחר מעבר על כל קודקודי הגרף והרצת האלג' כולם החזירו true, הגרף קשיר.

2.פונקציית "shortestPath" : מקבלת גרף, נקודות התחלה וסוף- ומחזירה מחרוזת של המסלול הקצר ביותר בין 2 קודקודים אלו במידה וקיים.
בהנתן גרף- נבדוק האם יש לו צלעות שליליות. אם כן- נריץ את אלגוריתם BELLMAN-FORD (פונקציית עזר), אחרת נריץ את אלגוריתם DIJKSTRA (פונקציית עזר, יעיליה יותר)

3.פונקציית "isContainsCycle": המקבלת גרף ומחזירה האם קיים בו מעגל כלשהוא. אם קיימים כמה- מחזירה אחד מהם.
האסטרטגיה היא לעבור עך הגרף באמצעות אלגוריתם DFS , ולנסות למצוא BACK EDGES- צלעות אשר במהלך ריצת האלגוריתם DFS הקודקוד שלהם כבר היה צבוע באפור, וגם הוא אב קדמון של הקודקוד הנוכחי. אם יש צלעות כאלו- סימן שבגרף קיים מעגל.
על מנת לקבל את המסלול של המעגל עצמו נעזרתי בצ'אט GPT אשר הבדיל בין פונקציית DFS בגרף מכוון ובגרף לא מכוון. הדיוק הוא שבגרף לא מכוון נוסף פרמטר נוסף- והוא parent- קודקוד האב של הקודקוד הנוכחי בעץ שנוצר- משמש למניעת בלבול בהכרעת מעגל באמצעות הBACK EDGES.

4.פונקציית "isBipartite" : המקבלת גרף, ומחזירה האם הגרף הוא דו צדדי. גרף ייקרא דו צדדי אמ"מ ניתן לחק את כל קודקודי הגרף ל2 קבוצות, אשר צלעות הגרף נמצאות רק בין 2 הקבוצות ולא בתוך הקבוצות. אחת השיטות הידועות למציאת גרף דו צדדי היא האלגוריתם אשר צובע את קודקודי הגרף ב2 צבעים שונים. אם ניתן לצבוע אותו בצורה כזו שכל קודקוד אינו סמוך(צלע) לקודקוד בצבע זהה לשלו- אזי הגרף הוא דו צדדי. הפונקציה מחזירה את 2 קבוצות הקודקודים במידה והגרף דו צדדי.
נתחיל ביצירת מערך בו כל הקודקודים אינם צבועים. נעבור על כל קודקודי בגרף ונקרא לפונקציית עזר "colorCheck" אשר מקבלת את הגרף וקודקוד התחלה.היא  משתמשת במחסנית- ועוברת קודקוד קודקוד(החל מההתחלתי) ובודקת האם כאשר היא צובעת את שכניו(הקודקודים שיש אליהם צלע) יש כבר שכן שצבוע באותו הצבע.(נקלח מאתר Geeks For Geeks). הפונקציה תחזיר true אם מקודקוד התחלה ניתן לצבוע את הגרף ב2 צבעים. הפונקצייה תריץ את פונקציית העזר עבור כל אחד מקודקודי הגרף בתור קודקוד ההתחלה. לסיום, ניקח את המערך עם הקודקודים הצבועים ונחלק אותו ל2 סטים A,B אשר ייצגו את 2 הקבוצות השונות , ונדפיס אותם כמחרוזת.

5.פונקציית "negativeCycle" :המקבלת גרף ומחזירה מסלול של מעגל שלילי במידה וקיים. מעגל שלילי הינו מעגל בגרף בו סכום הצלעות קטן מ0.
קודם כל נעזר בפונקציית "isContainsCycle" , שכן אם לא קיים מעגל בגרף כלל אין צורך לחפש מעגל שלילי. כמו כן נעזר בשדה האם יש צלעות שליליות בגרף, כי אם אין אזי אין מעגל שלילי.
האלגוריתם בו נשתמש על מנת לאתר את המעגל השלילי הוא אלגוריתם BELLMAN FORD.
בגרף לא מכוון- נריץ את האלגוריתם פעם אחת מקודקוד התחלה כלשהוא על מנת לאתר מעגל שלילי. כידוע, אלגוריתם זה מבצע את פעולת RELAX שהיא פעולה ה
מכנסת" קודקוד -קובעת את המרחק הכי קצר מקודקוד לכל שאר קודודי הגרף ע"י מעבר על מטריצת השכנויות. במידה ויש קודקוד שהמסלול אליו בפעם הN התקצר- סימן שיש מעגל שלילי תו"כ המסלול.
בגרף מכוון- נצטרך לבצע את אותה הפעולה- רק מכל קודקוד בגרף כיוון שהצלעות אינן דו כיווניות וייתכנו כיוונים שונים. בדרך זו נאתר מעגל שלילי.


במחלקת "Test":
ישנם 50 טסטים אשר עוברים על כל הפונקציות ועל כל מקרי הקצה של הגרפים העלולים להתקיים.

מחלקת "Demo":
מחלקה זו מציגה 10 גרפים אשר כל אחד שונה בתכונותיו . התוכנית תריץ את כל אחת מהפונקציות על אותו הגרף ותראה בצורה ויזואלית אז תוצאות הפונקציות.
   

   

