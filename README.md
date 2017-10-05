# git_boot_camp
git boot camp

1.git add ファイル名
git add コマンドは追加されたファイルなどをバージョン管理の対象として追加するコマンド。
オプションに「.」を指定して、ファイルをまとめてコマンドを実行することもできる。


2.git commit
　コマンドの説明：ファイルやディレクトリの追加・変更を、リポジトリに記録するときに使う操作です。
　ハマるポイント：1.の「git add」をしていないと、ファイルを変更していても記録されません。
　便利なオプション：「git commit -m コミットメッセージ 」で、直接コミットメッセージを入力できます

5. git branch fix/42

git branch <branch_name>

ローカルのリポジトリに対して、ブランチ <branch_name> を作成します。
ブランチを作成しますが、HEAD は移動しません。
ブランチに切り替えるには、git checkout <branch_name> を実行する必要があります。

git status を実行して、今どのブランチ上にいるかを確認してから作業を行いましょう。

----------------
$ git status
On branch id/14
.....
----------------

git branch 自体は、branchの作成、リスト、削除が行えるコマンドで、オプションも大量にあります。

6.git checkout -b fix/42; git commit
7.git checkout -b fix/42
・git checkout -b fix/42
    現在のブランチから新規ブランチ(fix/42)を作成する
    新規ブランチの作成後、現在のブランチを新規ブランチに切り替える (-b)
・git commit
    現在のブランチの修正をリポジトリに反映させる
