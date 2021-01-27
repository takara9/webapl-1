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





