# 더미 데이터 생성
```sql
DELIMITER $$
DROP PROCEDURE IF EXISTS dataInsert$$

CREATE PROCEDURE dataInsert()
BEGIN
	DECLARE i INT DEFAULT 1;
    WHILE i <= 500 DO
		INSERT INTO study.posts(title, contents, userId)
        VALUES (concat('title',i), concat('contents',i), 1);
		SET i = i + 1;
	END WHILE;
END$$
DELIMITER $$

CALL dataInsert;
```