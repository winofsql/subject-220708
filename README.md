# subject-220708

### [簡易PL/SQLビルダー](https://winofsql.jp/download/easy_plsql_builder.zip)
![image](https://user-images.githubusercontent.com/1501327/177899102-df81f461-0c06-4b1f-bb00-b5b415f7d97f.png)
```sql
CREATE OR REPLACE FUNCTION GET_CNAME
(
    /* 文字列引数の定義 */
    PM_STRING IN VARCHAR2
)
/* 戻り値の定義 */
RETURN VARCHAR2

/**********************************************************/
/* 変数の定義 */
/**********************************************************/
AS
    RET_VALUE	VARCHAR2(2000);
    WK_VALUE	VARCHAR2(2000) := '初期値の設定';

/**********************************************************/
/* 処理開始 */
/**********************************************************/
BEGIN

    /* 代入 */
    RET_VALUE := PM_STRING;

    IF RET_VALUE is NULL THEN 
        RET_VALUE := '該当者は存在しません';
    ELSE 
        SELECT 氏名 INTO WK_VALUE from 社員マスタ
            WHERE 社員コード = RET_VALUE;
        RET_VALUE := WK_VALUE;
    END IF; 

    /* 戻り値 */
    RETURN RET_VALUE;

END;
```

### [Oracle】PL/SQL入門](https://qiita.com/nkojima/items/93a9c01741965f11bb8c)
