### SQL 結合
```sql
SELECT
    社員マスタ.社員コード,
    社員マスタ.氏名,
    社員マスタ.フリガナ,
    社員マスタ.所属,
    コード名称マスタ.名称 as 所属名,
    CASE
        社員マスタ.性別
        WHEN 1 THEN '男'
        WHEN 0 THEN '女'
    END AS 性別,
    DATE_FORMAT(社員マスタ.作成日, '%Y/%m/%d') AS 作成日,
    DATE_FORMAT(社員マスタ.更新日, '%Y/%m/%d') AS 更新日,
    社員マスタ.給与,
    社員マスタ.手当,
    社員マスタ.管理者,
    DATE_FORMAT(社員マスタ.生年月日, '%Y/%m/%d') AS 生年月日
FROM
    社員マスタ
    LEFT OUTER JOIN コード名称マスタ ON 社員マスタ.所属 = コード名称マスタ.コード
    AND 2 = コード名称マスタ.区分
ORDER BY
    社員マスタ.社員コード;
```
![image](https://user-images.githubusercontent.com/1501327/177923000-efed069a-9296-456d-b5e8-b2f8843abd1a.png)

```sql
SELECT
    *
FROM
    社員マスタ;

SELECT
    A.社員コード,
    A.氏名,
    A.フリガナ,
    A.所属,
    コード名称マスタ.名称 as 所属名,
    CASE
        A.性別
        WHEN 1 THEN '男'
        WHEN 0 THEN '女'
    END AS 性別,
    DATE_FORMAT(A.作成日, '%Y/%m/%d') AS 作成日,
    DATE_FORMAT(A.更新日, '%Y/%m/%d') AS 更新日,
    A.給与,
    A.手当,
    A.管理者,
    B.氏名 as 管理者名,
    DATE_FORMAT(A.生年月日, '%Y/%m/%d') AS 生年月日
FROM
    社員マスタ A
    LEFT OUTER JOIN コード名称マスタ
    ON 
        A.所属 = コード名称マスタ.コード
        AND 2 = コード名称マスタ.区分
    LEFT OUTER JOIN 社員マスタ B
    ON
        A.管理者 = B.社員コード
ORDER BY
    A.社員コード
```
