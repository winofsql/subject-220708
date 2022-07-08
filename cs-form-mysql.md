### 社員マスタの読み込み
```cs
using System.Data.Odbc;
using System.Diagnostics;

namespace WinFormsApp3
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {

            OdbcConnectionStringBuilder builder = new OdbcConnectionStringBuilder();

            builder.Driver = "MySQL ODBC 8.0 Unicode Driver";

            // 接続用のパラメータを追加
            builder.Add("server", "localhost");
            builder.Add("database", "lightbox");
            builder.Add("uid", "root");
            builder.Add("pwd", "");

            // 接続の作成
            OdbcConnection myCon = new OdbcConnection();

            // MySQL の接続準備完了
            myCon.ConnectionString = builder.ConnectionString;

            // MySQL に接続
            myCon.Open();

            // SQL
            string myQuery =
                @$"SELECT
                    社員マスタ.*,
                    DATE_FORMAT(生年月日,'%Y-%m-%d') as 誕生日
                    from 社員マスタ where 社員コード = '{this.textBox1.Text}'";

            // MessageBox.Show(myQuery);

            // SQL実行用のオブジェクトを作成
            OdbcCommand myCommand = new OdbcCommand();

            // 実行用オブジェクトに必要な情報を与える
            myCommand.CommandText = myQuery;    // SQL
            myCommand.Connection = myCon;       // 接続

            // 次でする、データベースの値をもらう為のオブジェクトの変数の定義
            OdbcDataReader myReader;
            // SELECT を実行した結果を取得
            myReader = myCommand.ExecuteReader();

            // myReader からデータが読みだされる間ずっとループ
            if (myReader.Read())
            {
                // 列名より列番号を取得
                int index = myReader.GetOrdinal("氏名");
                // 列番号で、値を取得して文字列化
                string text;
                text = myReader.GetValue(index).ToString();
                // コンソールに出力
                Debug.Write(text + " : ");

                this.textBox3.Text = text;

            }

            myReader.Close();
            myCon.Close();

        }
    }
}
```
