# git_boot_camp
git boot camp

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


10. git rebase -i A〜E

git rebase -i A を実行すると、A 以降にコミットされたリビジョンの編集を行えます。
この場合、B,C,D,E が対象となります。


実際に試してみました。
同一のファイルにA,B,C,D,E を追記していき、都度コミットして5つのコミットを作成しました。
その後、git log を実行して、A をコミットした時のリビジョンを取得しておきます。

commit 021935c4f8a7424f4e1059efb447065fde23380d
Author: Masatoshi Yanase <magicyan@gmail.com>
Date:   Thu Oct 5 14:17:44 2017 +0900

    iA

git rebase -i 021935c4f8a7424f4e1059efb447065fde23380d を実行すると、以下のようなコミットログ画面？が表示されます。

pick b5dba87 B
pick 4f125ab C
pick d61570c D
pick 23ef596 E

これを、以下のように編集して、

d b5dba87 B
pick 4f125ab C
s d61570c D
s 23ef596 E

コミットログ画面を終了すると.....

error: could not apply 4f125ab... C

残念、エラーになりました。

恐らく、同じファイルに対して追記を繰り返したため、Bを消すとC以降がうまく反映できないためだと思われます。


さて、問題はここからです。
この状態で、git log を実行すると、なんと A 以降のコミットが消えてしまっています...orz
これでは、せっかくの仕事が水の泡です。

が、エラーメッセージをよく読むと、
To check out the original branch and stop rebasing, run "git rebase --abort".
とあったので、これを実行することでEまでのコミットがgit log で再び見えるようになりました。

ふぅ。

これで、失敗しても元に戻せることがわかったので、何度でもトライすることが出来ます。

※ちなみに、先生の説明によると、フィルの中間部分などへの変更であれば、同一ファイルであってもうまく行くのではないか、ということでした。
※実際、ファイルの中間であれば、うまく行きました。
