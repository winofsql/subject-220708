# subject-220708

### プロシージャ用デバッグテーブル
```sql
create table proc_debug (
	data1 number,
	data2 number,
	data3 varchar2(100),
	data4 varchar2(100),
	data5 date,
	data6 date
)
```
```sql
insert into proc_debug values(null,null,null,null,null,null)
```

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

### [【Oracle】PL/SQL入門](https://qiita.com/nkojima/items/93a9c01741965f11bb8c)

### プローシージャサンプル
```sql
create or replace procedure TEST1
(
    code     IN   varchar2
)
AS
    CURSOR cur1 IS
        SELECT 氏名,フリガナ FROM 社員マスタ
        WHERE 社員コード = code;

    syain_rec cur1%ROWTYPE;

BEGIN
    OPEN cur1;
        FETCH cur1 INTO syain_rec;
    CLOSE cur1;

    update PROC_DEBUG set DATA3 = syain_rec.氏名, DATA4 = syain_rec.フリガナ;

END;
```
```sql
DECLARE
BEGIN
    TEST1('0001');
END;
```

- ### ディレクトリオブジェクト
	- 権限( SYSTEM でログイン )
	```sql
	grant 
		CREATE ANY DIRECTORY 
		,DROP ANY DIRECTORY 
	to LIGHTBOX00
	```
	- 権限の確認
	```sql
	select * from USER_SYS_PRIVS where PRIVILEGE like '%DIR%'
	```
