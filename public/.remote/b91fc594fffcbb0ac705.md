---
title: Bunzzで利用可能なスマートコントラクトのVerify機能
tags:
  - Ethereum
  - 仮想通貨
  - ブロックチェーン
  - DApps
  - Web3
private: false
updated_at: '2024-05-15T16:07:39+09:00'
id: b91fc594fffcbb0ac705
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---

:::note info
本記事は下記の翻訳となります。
[『Smart Contract Verification Feature Available in Bunzz』](https://medium.com/@bunzzdev/smart-contract-verification-feature-available-in-bunzz-e0a0eeac78c5)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/366dda46-7ba0-d4ff-b54a-e1c1f6ee6ddc.png)

Bunzz は引き続き多くの機能を提供し、今回はブロックチェーン開発者コミュニティから最も要望の多かったスマートコントラクトの Verify 機能をリリースしました。

Bunzz で展開するすべてのスマートコントラクトのソースコードを簡単に Verify できるようになりました。Etherscan や他のネットワークブロックエクスプローラでスマートコントラクトを Verify するために必要なすべての入力フィールドにコピーして入力するためのデータが手に入ります。

ソースコードの Verify により、スマートコントラクトとやり取りするユーザーに透明性が提供されます。ソースコードをブロックエクスプローラにアップロードすることで、コンパイルされたコードとブロックチェーン上のコードを照合することができます。

それでは、Bunzz を使用してスマートコントラクトを検証するために必要な手順を一つずつ見ていきましょう。

## DApp を作成する

1. DApp を作成します
   ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/15582e3f-4e2f-ba08-62e9-13f7ca1f0d4c.png)

2. DApp の名前を入力します
   ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/6ee497cc-61d7-008d-ef14-b7a3df206d8a.png)

3. デプロイするネットワークを選択します
   ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/cc643a94-edf6-6bcf-d00c-48eb78d47098.png)

4. デプロイしたいスマートコントラクトモジュールを選択して追加します
   ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/48e48f06-0a28-dacd-e4fa-cebff2a56a03.png)

5. 必要なパラメータ（この例では name, symbol, cap）を入力し、最後に「デプロイ」をクリックします
   ![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/b51f5604-cf56-76aa-cf74-3e7b3ebcb505.png)

6. 選択したネットワークにスマートコントラクトモジュールがデプロイされます！

## Verify 方法

モジュールがデプロイされたら、DApp のダッシュボードで検証機能にアクセスできます。 「Verify the contract」をクリックしてください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/9c4c14e9-ba50-ca03-22f5-a6f7a467ecb9.png)

次に、提供された以下のデータをコピーして、選択したネットワークブロックエクスプローラの検証フォームに入力してください。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/6814b9d8-f046-3252-c56a-33fa817b5ede.png)

例えば、モジュールが Goerli テストネットワークにデプロイされている場合は、コントラクトアドレスをコピーして Goerli テストネットワークのブロックエクスプローラの検索エンジンに貼り付けます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/4f94cea5-63ac-4fdb-8a4b-ebeb4e5b9390.png)

次に、*契約タブ*に移動し、「Verify and Publish」をクリックします。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/788c2293-6ad6-5351-e596-32cc81387d3b.png)

そして、Bunzz のダッシュボードに必要なすべてのデータをコピーして貼り付けるか、対応するデータフィールドを選択し、最後に「Verify and Publish」ボタンが表示されるまで続けます。

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/b0b75be5-058c-73d2-4784-204bc45e3f50.png)
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/04cefd37-feac-0743-b7c9-e54be448e0bc.png)

以上で、Bunzz に展開したスマートコントラクトモジュールが Verify されました！

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
