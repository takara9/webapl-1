# webapl-1
Simple Web Application 




## ビルド方法

~~~
docker build -t webapl1:1.0 .
~~~

## ローカル環境でのテストやデバッグ

~~~
docker run -it -p 3000:3000 --rm --name test webapl1:1.0
~~~


## Harbor のコンテナレジストリへ登録

harborレジストリへのdocker login は、毎回実施する必要は無いので、省略可能できます。
docker imagesコマンドも、対象となるイメージの存在を確認するためなので、省略可能です。
タグの付与は、登録対象のレジストリごとに必要です。

~~~
docker login -u tkr harbor.labo.local
docker images
docker tag webapl1:1.0 harbor.labo.local/tkr/webapl1:1.0
docker push harbor.labo.local/tkr/webapl1:1.0
~~~

## Docker Hub レジストリサービスへ登録

Docker Hubへ登録するときは、サーバー名は省略可能で、ユーザー名だけで指定できます。
もちろん、アカウントを持っていなければなりません。

~~~
docker tag webapl1:1.0 maho/webapl1:1.0
docker push maho/webapl1:1.0
~~~




## パブリック GitHub からクローンして、プライベート GitLab へプッシュする方法

git コマンドで、ローカルのGitLabにアクセスできる設定を実施しておく。
それから、以下を実施することで、ローカルのGitLabを利用できる。

~~~
git clone https://github.com/takara9/webapl-1
cd webapl-1

git remote -v
origin	ssh://git@github.com/takara9/webapl-1 (fetch)
origin	ssh://git@github.com/takara9/webapl-1 (push)

git remote rename origin old-origin
git remote -v
old-origin	ssh://git@github.com/takara9/webapl-1 (fetch)
old-origin	ssh://git@github.com/takara9/webapl-1 (push)

git remote add origin ssh://git@gitlab.labo.local:2224/tkr/webapl-1.git
git push -u origin --all
~~~


## パブリック GitHub へもPushする方法

ローカルだけではなく、パブリックGitHubへ変更を反映するには、old-origin へプッシュすれば良い

~~~
git push -u old-origin

git remote -v
old-origin	https://github.com/takara9/webapl-1 (fetch)
old-origin	https://github.com/takara9/webapl-1 (push)
origin	ssh://git@gitlab.labo.local:2224/tkr/webapl-1.git (fetch)
origin	ssh://git@gitlab.labo.local:2224/tkr/webapl-1.git (push)
~~~


## 全てに反映させる場合

~~~
cd webapl-1
git status
git add README.md 
git commit -m "update "
git push -u origin --all
git push -u old-origin --all
~~~


