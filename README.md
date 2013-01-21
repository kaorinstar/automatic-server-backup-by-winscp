#automatic-server-backup-by-winscp

Automatic Server Backup by WinSCPは、  
WinSCPとWindowsのタスク機能を使用して自動的にサーバーのバックアップを行います。

## 目次
1. 注意
2. インストール
3. アンインストール
4. 設定
5. 使い方
6. ライセンス

## 1. 注意
このプログラムでサーバーのバックアップを実行する前に  
必ず手動でバックアップを行なってください。

また、このプログラムは、以下の動作をします。

1. WinSCPを実行し、使用者が指定したサーバーに接続します。
2. 使用者が指定したフォルダーにサーバーのデーターをダウンロードします。
3. ダウンロードしたデーターを複製または削除を行います。
4. 7-Zipを実行し、ダウンロードしたデーターの圧縮または解凍を行います。

## 2. インストール
1. ダウンロードします。

2. 「backup.bat.txt」ファイル、「bin」フォルダー、「conf」フォルダーを任意のフォルダーに設置します。

3. 「backup.bat.txt」ファイルをメモ帳または、任意のテキストエディターで開き、  
   設定を自身の環境に合わせて変更し、保存します。  
   (設定については、「4. 設定 > ・バックアップ環境変数」を参照)

4. 「backup.bat.txt」ファイルのファイル名の.txt部分を削除します。(例：backup.bat)

5. Windowsのタスクに「backup.bat」ファイルを登録します。  
   ※タスクの登録方法は下記を参照してください。
     * [Windows XP][LINK-WINXP-ADDTASK]
     * [Windows Vista][LINK-WINVISTA-ADDTASK]
     * [Windows 7][LINK-WIN7-ADDTASK]  

   ※Windows Vista以降で「ユーザー・アカウント制御（UAC）」を有効にしている場合は、  
     「セキュリティ オプション」の「最上位の特権で実行する」にチェックを入れてください。

###圧縮モードを使用する
圧縮モードとは、ダウンロードしたデーターを7-Zipを利用して自動的に圧縮する機能です。  
(圧縮モードを使用しない場合はこの手順は不要です) 

1. 7-Zipの[サイト][LINK-7ZIP]から、「7-Zip コマンドラインバージョン」をダウンロードし、  
   「bin」フォルダー内に設置します。  
   ※ライセンスの問題で同梱しておりません。

2. 「backup.bat」ファイルをメモ帳または、任意のテキストエディターで開き、  
   以下の環境変数を自身の環境に合わせて変更し、保存します。  
   (設定については、「4. 設定 > ・バックアップ環境変数」を参照)
   * SEVEN_ZIP_PATH  
   * COMPRESSION_MODE  
   * COMPRESSION_TYPE

## 3. アンインストール
1. Windowsのタスクから「backup.bat」ファイルの実行タスクを削除します。

2. 「backup.bat」ファイル、「bin」フォルダー、「conf」フォルダーを削除します。

## 4. 設定
###バックアップ環境変数
   
   * CONF_DIR(必須)  
   サーバーの設定ファイルを保存するフォルダーのパスを指定します。  
   例)%~dp0conf
   
   * WINSCP_PATH(必須)  
   WinSCPの実行ファイルのパスを指定します。  
   例)%~dp0bin\winscp\WinSCP.exe
   
   * TIMEOUT_MESSAGE(必須)  
   WinSCPのタイムアウトメッセージを指定します。  
   例)タイムアウトしました
   
   * SEVEN_ZIP_PATH  
   7-Zipの実行ファイルのパスを指定します。  
   例)%~dp0bin\7za\7za.exe
   
   * COMPRESSION_MODE  
   圧縮モードを有効・無効を指定します。(y：有効/n：無効)  
   例)y
   
   * COMPRESSION_TYPE  
   圧縮のタイプを指定します。(zip/7z)  
   例)7z
   
   * COMPRESSION_LEVEL  
   圧縮のレベルを指定します。(0/1/3/5/7/9)  
   例)7

###サーバー環境変数
   
   * BACKUP_DIR_PATH(必須)  
   バックアップするフォルダーのパスを指定します。  
   例)C:\path\to\backup\foo
   
   * REMOTE_DIR_PATH(必須)  
   サーバー側のフォルダーのパスを指定します。  
   例)/path/to/remote/bar
   
   * PROTOCOL(必須)  
   プロトコルを指定します。(sftp/scp/ftp/ftps)  
   例)ftp
   
   * PORT_NUMBER(必須)  
   ポート番号を指定します。  
   例)21
   
   * HOST_NAME(必須)  
   ホスト名を指定します。  
   例)my.host.name
   
   * USER_NAME(必須)  
   ユーザー名を指定します。  
   例)username
   
   * PASSWORD(必須)  
   パスワードを指定します。  
   例)password
   
   * HOST_KEY  
   SSHサーバーのホストキーを指定します。(SFTPとSCPプロトコルを使用する場合)  
   例)ssh-rsa 1024 xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx
   
   * CERTIFICATE  
   SSL/TLS証明書を指定します。(FTPSプロトコルを使用する場合)  
   例)xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx
   
   * PRIVATE_KEY  
   秘密鍵のパスを指定します。(SCPプロトコルを使用する場合)  
   例)C:\my_private_key.ppk
   
   * MAX_SYNC_RETRIES(必須)  
   サーバー接続のリトライ回数を指定します。  
   例)5
   
   * MAX_BACKUP(必須)  
   データーのバックアップ個数を指定します。  
   例)20

## 5. 使い方
###サーバーのバックアップを開始する
   1. 「conf」フォルダー内にある「sample_conf.ini.txt」ファイルを同じフォルダーに複製します。

   2. 複製したファイルをメモ帳または、任意のテキストエディターで開き、  
      バックアップしたいサーバーの情報を設定し、保存します。  
      (設定については、「4. 設定 > ・サーバー環境変数」を参照)

   3. 複製したファイルをお好きなファイル名に変更し、.txt部分を削除します。(例：mybackup.ini)

   4. 完了です。

###サーバーのバックアップを停止する
   1. 「conf」フォルダー内にあるバックアップを停止したいサーバーの設定ファイルを削除します。  
      ※バックアップされているデーターも不要であれば削除します。

   2. 完了です。

## 6. ライセンス
Copyright &copy; 2012 Kaoru Ishikura.  
Licensed under the [GPL Version 3 licenses][GPL].

[LINK-WINXP-ADDTASK]: http://support.microsoft.com/kb/881869/ja
[LINK-WINVISTA-ADDTASK]: http://windows.microsoft.com/ja-JP/windows-vista/Schedule-a-task
[LINK-WIN7-ADDTASK]: http://windows.microsoft.com/ja-JP/windows7/Schedule-a-task
[LINK-7ZIP]: http://sevenzip.sourceforge.jp/download.html
[GPL]: http://www.gnu.org/licenses/gpl.html
