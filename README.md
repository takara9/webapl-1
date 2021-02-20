# webapl-1
Simple Web Application 




## ビルド方法

{dockerhub_userid}の部分は、自分のDocker Hub のIdで置き換えてくださいね。

~~~
docker build -t {dockerhub_userid}/webapl1:1.0 .
~~~

## ローカル環境でのテストやデバッグ

~~~
docker run -it -p 3000:3000 --rm --name test {dockerhub_userid}/webapl1:1.0
~~~


## Docker Hubへの登録

~~~
docker login
docker push
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

ローカルだけではんく、パブリックGitHubへ変更を反映するには、old-origin へプッシュすれば良い

~~~
git push -u old-origin

git remote -v
old-origin	https://github.com/takara9/webapl-1 (fetch)
old-origin	https://github.com/takara9/webapl-1 (push)
origin	ssh://git@gitlab.labo.local:2224/tkr/webapl-1.git (fetch)
origin	ssh://git@gitlab.labo.local:2224/tkr/webapl-1.git (push)
~~~


