# Dockerコンテナからrsyncで送受信

rsync に **--blocking-io -e 'docker exec -i'** というオプションをつければ [コンテナ]:[パス] でコンテナ内部を指定できる。

## debian-jessieで動作の確認

	cd debian-jessie

イメージの作成

	docker build -t debian-jessie-rsync-test .

コンテナの作成

	docker run --name rsync-test -d debian-jessie-rsync-test

## alpine での動作を確認

	cd alpine

イメージの作成

	docker build -t alpine-rsync-test .

コンテナの作成

	docker run --name rsync-test -d alpine-rsync-test

## rsyncでファイルのやりとり

**-rltDv** というオプションは、-a オプションの -rlptgoD から p(perms), g(group), o(owner)を抜いて -v を加えたもの

リモートの/etc をローカルにもってくる 

	rsync --blocking-io -e 'docker exec -i' -rltDv rsync-test:etc work/

空のファイルをつくってみる

	touch work/etc/hogehoge

ローカルの etc を リモートの /etc に上書き

	rsync --blocking-io -e 'docker exec -i' -rltDv work/etc rsync-test:/

etc/hogehoge がアップロードできたか確認

	docker exec rsync-test ls -al /etc/hogehoge

## コンテナに入る

	docker exec -it rsync-test /bin/sh

## 終了

コンテナの停止

	docker stop rsync-test

コンテナの削除

	docker rm rsync-test

## 参考情報
* [GitHub:`docker exec -i` as a transport for `rsync -e` #13660](https://github.com/docker/docker/issues/13660#issuecomment-192975035)

* [DEBIAN_FRONTEND=noninteractive ってなんだ](http://qiita.com/udzura/items/576c2c782adb241070bc)

