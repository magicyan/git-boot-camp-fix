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

8.git reset --hard master
　コマンドの説明：git resetは、以前のコミットを取り消す時などにつかいます。
　　　　　　　　　「git reset --hard master」の意味は、　masterのHEADと同じ状態にまで、
　　　　　　　　　HEAD INDEX 作業ディレクトリの状態をもとに戻すという意味になります。
　　　　　　　　　使い所としては、ブランチを切って開発をしていたが、masterの開発が進んでブランチの開発の意味がなくなった場合などに使います。
　ハマるポイント：オプションが「--hard」「--soft」「--mixed」がありますので、その差が分かりづらいです。
　　　　　　　　　また、HEAD INDEX 作業ディレクトリの理解も必要です。
　オプションの意味：「--hard」HEAD INDEX 作業ディレクトリ全てが、指定したコミットやHEADの状態になります。→手元の作業ディレクトリの内容も含めて、指定した状態になってしまいます。
                 「--mixed」HEAD INDEXは指定したコミットやHEADの状態になりますが、作業ディレクトリはそのままです。（オプション指定しない場合のデフォルトはこれ）→直近のコミットと、git addでインデックスに加えた結果が取り消されます。
                 「--soft」HEAD は指定したコミットやHEADの状態になりますが、INDEXと作業ディレクトリには変更が加わりません。→直近のコミットを取り消し（git commit --amendと同じ結果）

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
