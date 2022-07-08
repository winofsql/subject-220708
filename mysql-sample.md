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
![image](https://user-images.githubusercontent.com/1501327/177922909-6dd55881-db30-46f3-9e7a-79db4e6568f4.png)
