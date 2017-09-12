-- 45
SELECT s.sno, s.sname, c.cname, o.degree FROM score o INNER JOIN student s ON s.sno = o.sno INNER JOIN course c ON c.cno = o.cno WHERE c.cname = '计算机导论' AND s.ssex = '男';

-- 44
SELECT * FROM student t WHERE EXISTS (SELECT t2.sno FROM student t2 WHERE t2.sname = '李军' AND t2.ssex = t.ssex AND t2.class = t.class);
SELECT a.* FROM student a, student b WHERE a.ssex = b.ssex AND a.class = b.class AND b.sname = '李军';

-- 43
SELECT * FROM student WHERE ssex IN (SELECT ssex FROM student WHERE sname = '李军');
SELECT a.* FROM student a, student b WHERE a.ssex = b.ssex AND b.sname = '李军';

-- 42
SELECT t.* FROM score t WHERE NOT EXISTS (SELECT degree FROM score t1 WHERE t1.degree > t.degree);
SELECT * FROM score WHERE degree = (SELECT MAX(degree) FROM score);

-- 41
SELECT t.tno, t.tname, c.cno, c.cname FROM teacher t INNER JOIN course c ON c.tno = t.tno WHERE t.tsex = '男';

-- 40
SELECT * FROM student ORDER BY class DESC, sbirthday ASC;

-- 39 
SELECT * FROM student WHERE YEAR(sbirthday) = (SELECT YEAR(MAX(sbirthday)) FROM student)
UNION
SELECT * FROM student WHERE YEAR(sbirthday) = (SELECT YEAR(MIN(sbirthday)) FROM student);

-- 38 使用数据库的特殊函数解决特定的问题
SELECT sname 姓名, (YEAR(NOW()) - YEAR(sbirthday)) 年龄 FROM student;

-- 37
SELECT * FROM student WHERE sname NOT LIKE '王%';

-- 36 
SELECT t.class FROM student t WHERE t.ssex = '男' GROUP BY t.class HAVING COUNT(t.ssex) > 1;

-- 35
SELECT t.tname, t.depart FROM teacher t WHERE NOT EXISTS (SELECT c.tno FROM course c WHERE c.tno = t.tno);

-- 34
SELECT t.tname, t.depart FROM teacher t WHERE EXISTS (SELECT c.tno FROM course c WHERE c.tno = t.tno);

-- 33 
SELECT t.* FROM score t WHERE t.degree < (SELECT AVG(degree) FROM score t1 WHERE t1.cno = t.cno GROUP BY t1.cno);

-- 32 联合查询加上过滤
SELECT '学生' 分类, s.sname 姓名, s.ssex 性别, DATE_FORMAT(s.sbirthday, '%Y-%m-%d') 出生日期 FROM student s WHERE s.ssex = '女'
UNION ALL
SELECT '教师' 分类, t.tname 姓名, t.tsex 性别, DATE_FORMAT(t.tbirthday, '%Y-%m-%d') 出生日期 FROM teacher t	WHERE t.tsex = '女';

-- 31 联合查询
SELECT '学生' 分类, s.sname 姓名, s.ssex 性别, DATE_FORMAT(s.sbirthday, '%Y-%m-%d') 出生日期 FROM student s
UNION ALL
SELECT '教师' 分类, t.tname 姓名, t.tsex 性别, DATE_FORMAT(t.tbirthday, '%Y-%m-%d') 出生日期 FROM teacher t;

-- 30 
SELECT a.* FROM score a, score b WHERE a.sno = b.sno AND a.degree > b.degree AND a.cno = '3-105' AND b.cno = '3-245';
-- 29
SELECT a.* FROM score a, score b WHERE a.sno = b.sno AND a.degree > b.degree AND a.cno = '3-105' AND b.cno = '3-245' ORDER BY a.degree DESC;

-- 28 不同的系所有独有的职称
SELECT t.* FROM teacher t WHERE NOT EXISTS (SELECT prof FROM teacher t1 WHERE t1.depart <> t.depart AND t1.prof = t.prof);

-- 27
SELECT o.* FROM score o LEFT JOIN course c ON c.cno = o.cno LEFT JOIN teacher t ON t.tno = c.tno WHERE t.depart = '计算机系';

-- 26
SELECT c.* FROM course c WHERE EXISTS (SELECT cno FROM score o WHERE o.cno = c.cno AND o.degree > 85);

SELECT DISTINCT c.* FROM course c INNER JOIN score o ON o.cno = c.cno WHERE o.degree > 85;

SELECT c.cno, c.cname, c.tno FROM course c INNER JOIN score o ON o.cno = c.cno WHERE o.degree > 85 GROUP BY c.cno, c.cname, c.tno;

-- 25
SELECT * FROM student WHERE class IN ('95033', '95031');

-- 24 
SELECT t.tname FROM score o INNER JOIN course c ON c.cno = o.cno INNER JOIN teacher t ON t.tno = c.tno GROUP BY o.cno HAVING COUNT(o.sno) > 5;

-- 23 关联查询
SELECT o.sno, o.degree, c.cname FROM score o LEFT JOIN course c ON c.cno = o.cno LEFT JOIN teacher t ON t.tno = c.tno WHERE t.tname = '张旭';

-- 22 mysql的日期转换函数
SELECT sno, sname, sbirthday FROM student WHERE YEAR(sbirthday) = (SELECT YEAR(sbirthday) FROM student WHERE sno = '108');

-- 21 子查询 参考19题答案
SELECT a.* FROM score a, score b WHERE a.degree > b.degree AND b.sno = '109' AND b.cno = '3-105';

-- 20 嵌套查询和子查询
SELECT * FROM score WHERE degree < (SELECT MAX(o.degree) FROM score o) AND sno IN (SELECT sno FROM score GROUP BY sno HAVING COUNT(cno) > 1) ORDER BY degree;

-- 19 
-- 子查询
SELECT o.* FROM score o WHERE o.cno = '3-105' AND o.degree > ALL (SELECT IFNULL(degree, 0) FROM score WHERE cno = '3-105' AND sno = '109');
-- FULL JOIN 生成两个表的最大笛卡儿积，再过滤
SELECT a.* FROM score a, score b WHERE a.cno = '3-105' AND a.degree > b.degree AND b.cno = '3-105' AND b.sno = '109';

-- 18 score和grade表直接进行笛卡儿积，然后过滤
SELECT s.sno, s.cno, s.degree, g.rank FROM score s, grade g WHERE g.low <= s.degree AND g.upp >= s.degree;

-- 17 
SELECT AVG(o.degree) FROM score o INNER JOIN student s ON s.sno = o.sno WHERE s.class = '95033';

-- 16
SELECT s.sno, c.cname, o.degree FROM student s LEFT JOIN score o ON s.sno = o.sno LEFT JOIN course c ON c.cno = o.cno;

-- 15
SELECT s.sno, s.sname, o.cname, o.cno, c.degree FROM student s LEFT JOIN score c ON c.sno = s.sno LEFT JOIN course o ON o.cno = c.cno;

-- 14
SELECT student.sno, student.`sname`, score.cno, score.degree FROM student LEFT JOIN score ON student.sno = score.sno;

-- 13
SELECT sno FROM score GROUP BY sno HAVING MIN(degree) > 70 AND MAX(degree) < 90;

-- 12
SELECT cno, AVG(degree) FROM score WHERE cno LIKE '3%' GROUP BY cno HAVING COUNT(sno) >= 5;

-- 11
SELECT AVG(degree) FROM score WHERE cno = '3-105';

-- 10 子查询、最大值去重复
SELECT * FROM score WHERE degree = (SELECT max(degree) FROM score);

-- 9
SELECT COUNT(*) FROM student WHERE class = '95031';

-- 8
SELECT * FROM score ORDER BY cno ASC, degree DESC;

-- 7 
SELECT * FROM student ORDER BY class DESC;

-- 6
SELECT * FROM student WHERE class = '95031' OR ssex = '女';

-- 5
SELECT * FROM score WHERE degree IN (85, 86, 88);

-- 4
SELECT * FROM score WHERE degree BETWEEN 60 AND 80;

-- 3
SELECT * FROM student;

-- 2
SELECT DISTINCT depart FROM teacher;

-- 1
SELECT sname, ssex, class FROM student;

