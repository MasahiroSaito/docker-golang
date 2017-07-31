# docker-golang

Golang 用の Docker イメージを Alpine を使って作成し、時刻を日本時間に設定してあります。Goプロジェクト配下に *docker-compose.yml* を作成し `docker-compose up -d` を叩くと、プロジェクトを `go get -t && go build` して生成されたバイナリを `./app` で実行します。

## Examples

実際に使っているプロジェクト

- [slack-logger](https://github.com/MasahiroSaito/slack-logger)
- [go-redis](https://github.com/MasahiroSaito/go-redis)

### docker-compose

コンテナ側の */go* の中身を保持しておくことで `go get -t` で依存パッケージをダウンロードしてくる時間を短縮できます。この時、自身が置かれている `/go/src/app` フォルダも保持することになりますが中身を再度保持することはありません。

```
app:
  image: masahirosaito/golang
  volumes:
    - ".:/go/src/app"
    - "./go:/go"
```
