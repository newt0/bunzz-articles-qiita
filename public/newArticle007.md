---
title: コントラクトをローカルにデプロイする際のプライベートキーのハッキングリスク
tags:
  - ブロックチェーン
  - DApps
  - Web3
  - DeFi
  - ノーコード
private: false
updated_at: '2024-05-15T17:48:13+09:00'
id: 3070c285f131c37c84f1
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---

:::note info
本記事は下記の翻訳となります。
[『The Hacking Risk of Private Keys When Deploying Contracts Locally』](https://blog.bunzz.dev/the-hacking-risk-of-private-keys-when-deploying-contracts-locally/)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/632917ee-a8c4-7982-712c-90cd8532f8b3.png)

## ETH Global Tokyo からの真実の物語

この物語は ETH Global Tokyo で展開されました。Bunzz Prize ハッカソンに参加した開発者が、プレゼン中に凍りつき、「攻撃を受けた！」と叫びました。何が起こったのか尋ねると、「私のウォレットがハッキングされ、資金が抜き取られました」と言いました。原因はすぐに明らかになりました。彼はローカルの開発環境を使用し、契約をデプロイするためにプライベートキーをローカルに保存していました。

残念ながら、このプライベートキーは、彼が開発していた DApp プログラムのコードで指定された保存場所が公開された GitHub リポジトリにプッシュされていました。要するに、彼のプライベートキーは世界中のどこからでも見える状態でした。

## ハッカソンの慌ただしい環境

以下は考えられる理論です。ハッカソンが開催されると、初心者を含む多くの開発者が参加し、通常よりもプレッシャーの中でコードを書くことがあります。締め切りが迫るにつれ、急いでコードを GitHub にアップロードすることになるかもしれません。世界のどこかで、悪意のある人物がハッカソンのスケジュールを把握し、新しいリポジトリが次々と作成されるのを待っているかもしれません。彼らはこの山のようなコードを見て、プライベートキーを見つけ出します。

これは考えられないシナリオではありません。なぜなら、私たちの被害者はコードの提出後すぐに資金が引き出されたからです。実際、特定のキーワードを使用して GitHub を検索すると（さらなる悪用を防ぐために明かしません）、プライベートキーが明示的にリストされているいくつかのリポジトリが見つかりました。

![](https://super-translator.inaridiy.workers.dev/assets/image/a7c1eeaa-3a26-4ca4-a56d-7b0429a22364)

開発者は、ローカル環境からデプロイする際に GitHub に機密キーを無意識にアップロードすることがあり、ハッカーの攻撃を受ける可能性があります。

恐ろしい事実は、Hardhat、Truffle、Foundry などのローカル開発環境を利用するユーザーなら誰にでも起こり得るということです。これらの環境では、プライベートキーをローカルに保存し、その場所をコードで指定する必要があります。

## 安全な Web3 開発環境の探求

このような事故を回避する方法は、ローカル環境の代わりに Remix のような IDE を使用することです。ただし、Remix を主要な開発環境として使用している開発者は少なく、安全な Web3 開発環境がまだ存在しない可能性があります。

このため、[Bunzz](https://bunzz.dev/)のデプロイプロセスは MetaMask を介して行われ、このようなリスクを軽減しています。また、私たちは開発インフラの一環として理想的な IDE の開発の可能性を継続的に探求しています。プライベートキーのセキュリティを向上させることは、Web3 の発展を確実に推進するでしょう。

---

---

:::note info
【Bunzz とは】
Bunzz はアジア最大級の DApps 開発インフラを運営する、web3×LLM におけるリーディングカンパニーです。「公共財としてのスマートコントラクト」の実現に向けて、各種 web3 インフラやサービスを開発・提供しております。

【Our Projects】

- **[Smart Contract Hub | スマートコントラクトの Github](https://www.bunzz.dev/)**
- **[DeCipher | "Read me" for All of Contracts](https://www.bunzz.dev/decipher)**
- **[Bunzz for Enterprise | Tier1 の技術リソースを日本企業に提供](https://enterprise.bunzz.dev/ja)**
- **[Bunzz Audit | 透明かつ持続的なコントラクト監査の仕組みを実現](hhttps://www.bunzz.dev/audit)**

【Social Links】

- [X(旧 Twitter))](https://twitter.com/BunzzDev)
- [Discord Community](https://t.co/6hHgssJdvW)
- [Youtube](https://www.youtube.com/@bunzzdev)
- [Instagram](https://www.instagram.com/bunzzdev/)

【お問合せ】
web3 開発・コンサルティングのご相談はこちらから 👉[Google Form](https://forms.gle/4tgQjWSw2MMMZW6E6)
:::

:::note info
Bunzz R&D エンジニア荒巻さんの著書[『スマートコントラクトの仕組みと法律』](https://amzn.to/3V03sNH)が好評発売中です 📕
<a href="https://amzn.to/3V03sNH" rel="nofollow" referrerpolicy="no-referrer-when-downgrade">
<img
    src="https://m.media-amazon.com/images/I/81wopoZ1K4L._SY522_.jpg"
    alt="『スマートコントラクトの仕組みと法律』（中央経済グループパブリッシング）"
    width="200px"
    height="auto"
    Style="border: 0px;"
  />
</a>
:::
