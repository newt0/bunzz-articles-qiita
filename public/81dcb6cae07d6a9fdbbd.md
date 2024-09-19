---
title: '[翻訳] MinimalForwarder【Bunzzスマートコントラクトモジュール】'
tags:
  - 仮想通貨
  - ブロックチェーン
  - DApps
  - Web3
  - DeFi
private: false
updated_at: '2024-07-10T16:54:36+09:00'
id: 81dcb6cae07d6a9fdbbd
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---

:::note info
本記事は下記の翻訳となります。
[『MinimalForwarder Smart Contract Module in Bunzz』](https://blog.bunzz.dev/minimalforwarder-smart-contract-module-in-bunzz/)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/43a88fe1-2e40-c46a-625d-adebb50b5518.png)

# MinimalForwarder Smart Contract Module in Bunzz - Blog on Bunzz, a DApp development platform

これは、[ERC2771](https://eips.ethereum.org/EIPS/eip-2771) 互換の契約と一緒に使用するためのシンプルな最小メタトランザクションフォワーダーです。

この MinimalForwarder モジュールは主にテスト用に作られており、本番環境で使用するためにはいくつかの機能が不足しています。したがって、この契約は、信頼性のあるフォワーディングシステムに必要なすべてのプロパティを持つことを意図していません。それには、[GSN](https://docs.opengsn.org/contracts/) プロジェクトのようなより複雑な要素が必要です。

このモジュールとコードには、[https://bit.ly/3U7lg7T](https://bit.ly/3U7lg7T) からアクセスできます。

### 使用方法

MinimalForwarder モジュールを使用するには、レシーバーコントラクトで[ERC2771Context](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/metatx/ERC2771Context.sol)を実装する必要があります。

- このコントラクトには、最初は所有者のいない白いフラグオブジェクトがメモリにあります
- 任意のユーザーは、契約の setFlagOwner メソッドを呼び出してフラグの所有権を主張し、好きな色でフラグを塗ることができます
- レシーバーコントラクトは、直接トランザクションとフォワードされたトランザクションの両方を処理できる必要があります。それらの違いは、msg.sender の値です
- フォワードされたトランザクションでは、**msg.sender**はフォワーダーコントラクトのアドレスです。したがって、この状況では、レシーバーコントラクトはトランザクションのペイロードから実際の msg.sender を取得する必要があります

> これは、「@openzeppelin/contracts/metatx/ERC2771Context.sol」契約を拡張することで実現されます。

- レシーバーコントラクトは ERC2771Context です。さらに、契約は信頼できるフォワーダー（トランザクションをフォワードするために有効化された唯一のフォワーダー）を指定してデプロイする必要があります

> Constructor(address trustedForwarder) ERC2771Context(trustedForwarder) {} そして、コントラクトコードでは、msg.sender を\_msgSender()メソッドで置き換える必要があります。

- function setFlagOwner(string memory \_color) external { address previousHolder = currentHolder; currentHolder = \_msgSender(); color = \_color; emit FlagCaptured(previousHolder, currentHolder, color); }

以下のコードでは、\_msgSender()メソッドが直接トランザクションとフォワードされたトランザクションの両方に対して意図されたメッセージ送信者を取得できる方法を示しています。

> function \_msgSender() internal view virtual override returns (address sender) { if (isTrustedForwarder(msg.sender)) { assembly { sender := shr(96, calldataload(sub(calldatasize(), 20))) } } else { return msg.sender; } }

同様のアプローチは、以下のような取引プロトコルでも使用されています。

[https://wyvernprotocol.com/docs](https://wyvernprotocol.com/docs)

[https://github.com/etherdelta/smart_contract](https://github.com/etherdelta/smart_contract)

[https://protocol.0x.org/en/latest/index.html](https://protocol.0x.org/en/latest/index.html)

[https://github.com/DexyProject/protocol](https://github.com/DexyProject/protocol)

実行例は、Vercel で次の URL で利用できます：[https://meta-transaction.vercel.app/](https://meta-transaction.vercel.app/)。

setFlagOwner メソッドをガス料金を支払わずに呼び出したいユーザー向けに、Web インターフェースが利用可能です。唯一の要件は、メタマスクプラグインがブラウザにインストールされていることです。ただし、ガス料金はまだリレーサーの仕事で支払われる必要があります。しかし、心配しないでください。ガス料金（もちろんテストネットのもの）はデモリレーサーサーバーによって支払われます。

### 関数

**#WRITE**

- transferOwnership
- execute
- renounceOwnership

**#READ**

- verify
- owner
- getNonce

このモジュールとコードには、[https://bit.ly/3U7lg7T](https://bit.ly/3U7lg7T) からアクセスできます。

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
