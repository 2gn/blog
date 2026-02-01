

Rust製のHomebrewの代替ユーティリティ。uvと同じような仕組みで動いている。
ちょっと前から気になっていたので使ってみた。
# なぜ速いのか

> Why is it faster?
> - Content-addressable store: packages are stored by sha256 hash (at /opt/zerobrew/store/{sha256}/). Reinstalls are instant if the store entry exists.
> - APFS clonefile: materializing from store uses copy-on-write (zero disk overhead).
> - Parallel downloads: deduplicates in-flight requests, races across CDN connections.
> - Streaming execution: downloads, extractions, and linking happen concurrently.

- ダウンロードされたパッケージはハッシュ値とともに格納されるので、再インストールが爆速
- バイナリを複製せず、共有することによって複製にかかる時間を短縮
- 並列ダウンロードするので、ダウンロードが他のダウンロードにブロックされない
- ダウンロード、展開、リンクが同時に行われる

# インストール

以下を実行

```sh
curl -sSL https://raw.githubusercontent.com/lucasgelfond/zerobrew/main/install.sh | bash
```

# Homebrewからの移行

```sh
zb migrate
```

が全てをやってくれる。しかし、Homebrewのクリーンアップ時にアルファベット順に上からパッケージをアンインストールするので、依存関係が複雑なパッケージのアンインストールに失敗する。二周目が必要。また、Homebrewのパスがハードコードされている設定ファイルとかはぶっ壊れる(starship 壊れる)。

# 現状

- tapはサポートされていない [#100](https://github.com/lucasgelfond/zerobrew/issues/100)
	- つまりhomebrew/caskは入らない
	- ここら辺は需要が高いのですぐ実装されると思う