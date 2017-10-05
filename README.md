# git_boot_camp
git boot camp

1.git add ファイル名
git add コマンドは追加されたファイルなどをバージョン管理の対象として追加するコマンド。
オプションに「.」を指定して、ファイルをまとめてコマンドを実行することもできる。


2.git commit
　コマンドの説明：ファイルやディレクトリの追加・変更を、リポジトリに記録するときに使う操作です。
　ハマるポイント：1.の「git add」をしていないと、ファイルを変更していても記録されません。
　便利なオプション：「git commit -m コミットメッセージ 」で、直接コミットメッセージを入力できます

3.git commit -a
git commit -a
git add と git commit を一辺にするためのコマンド。


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

<<<<<<< HEAD
13.git rebase master
　複数のブランチを切って作業しているとマージがあちらこちらで行われるため、入り組んで見にくくなります。
　こういう時に役立つのが、git rebase です。
　メリットは以下です。
　・git rebase masterで、現在のブランチのコミットをすべてmasterに適応できる。
　・コミットを一つずつ適応するため、一度に解決すべき競合が少なくなる。
　・また、履歴が一本化できるため後から見直したときにわかりやすい履歴になる。 
　途中で競合が起きた場合はそこでいったん停止するため、
　競合を解決し、git addしてからgit rebase --continueを実行してください。
　また、git rebase --abortコマンドを実行することで、いつでもrebaseを終了できます。　
　例：
　Masterのコミットm1 m2 m3 m4があるとします。
　さらに、m2から派生したbranch_Aのm2-a1 m2-a2 m2-a3と、
　m2-a1から派生したbranch_Bのm2-a1-b1 m2-a1-b2があるとします。
　このようなときに、branch_Bをチェックアウトしてる状態でgit rebase masterをすることで、
　m4の後にm2-a1、m2-a1-b1、m2-a1-b2を順番にもう一度コミットを行います。



=======
18 git pull
 git fetch と git merageの両方をするためのコマンド
 競合が発生した場合は、該当部分を手動で直してマージし直す必要があります。

21. git cherry pick 2
    現在選択中のブランチに、2のコミット(別のブランチに存在)のみを反映する。
    一旦反映したいブランチ上のコミットをログを含め確認したのちに、反映したいブランチに移動後に
    行うようにした方がよい
```
git checkout feature/test
git log
．．．．
git checkout master
git cherry-pick 2
```
    ブランチでの作業中に不具合等が発覚して修正したのちに、不具合修正部分のみをメインブランチに反映するのに有用らしい。
>>>>>>> 531fd9bfe35b470642820bab915c7288104ba750
