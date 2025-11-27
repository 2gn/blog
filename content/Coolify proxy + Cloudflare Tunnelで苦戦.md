
Coolifyを使って、Cloudflare Tunnel経由でご家庭サーバーを運用している。Coolifyのドキュメントはとても親切なので、[公式のガイド](https://coolify.io/docs/knowledge-base/cloudflare/tunnels/all-resource)を用意してくれている。ところが、このセットアップを完成させるのが結構大変だった。

完成図はこんな感じ(公式サイトより)。
![[image-cloudflare.png]]

# 


# なぜか80番ポート以外を見つけてくれないtraefik

とあるサービスは8080番ポートでWebインターフェースを出していたのだが、これを自動で見付けてプロキシしてくれるはずのcoolify-proxy(traefik)が、全然見つけてくれなかった。

WebUIの走るポート(だいたいdocker-compose.ymlで設定できる)を80番ポートに変えると、機嫌よく動きだすようになった。