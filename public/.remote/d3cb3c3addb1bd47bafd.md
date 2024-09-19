---
title: '[翻訳] ERC1155D【Bunzzスマートコントラクトモジュール】'
tags:
  - Ethereum
  - 仮想通貨
  - ブロックチェーン
  - DApps
  - Web3
private: false
updated_at: '2024-07-10T16:56:20+09:00'
id: d3cb3c3addb1bd47bafd
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---
:::note info
本記事は下記の翻訳となります。
[『ERC1155D Smart Contract Module in Bunzz』](https://blog.bunzz.dev/erc1155d-smart-contract-module-in-bunzz/)
:::
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/faa6573e-3dd7-9850-488f-09701c8f3806.png)

ERC1155D モジュールは、ガス効率の良い NFT コントラクトであり、ERC721 の代替となります。これは 1/1 の NFT（供給数が 1）にのみ使用することを意図しており、供給数が 1 より大きいトークンはサポートしていません。

このモジュールは、ERC1155 と完全に後方互換性があり、仕様に従う場合に高いガスコストの問題はありません。ERC1155 トークンをスワップする中央集権的または非中央集権的な取引所を壊すことはありません。

その利点の中には、次のものがあります：

仕様に干渉せずに ERC1155 プロトコルを拡張するための有用な関数があります。
OpenZeppelin の ERC1155 よりもマイニングと転送のガスコストが低いです。
完全に非代替可能であり、ERC721 およびその派生バージョンの適切な代替品です。
ERC721 slim や ERC721A などの高度に最適化されたものを含め、他のどのコントラクトよりもガス効率が優れています。
このモジュールとコードには、こちらからアクセスできます：https://bit.ly/42gmxwN

### 使用方法

プロジェクトで ERC1155D スマートコントラクトモジュールを使用するには、contracts/ERC1155D.sol をプロジェクトにコピーします。

次に、それをインポートし、コントラクトを ERC1155 として拡張する実装を書きます。

注意：ERC1155D は tokenID の列挙を維持しません。コントラクト内でカウンターを実装する必要があります。

## 関数

### #書き込み

- safeBatchTransferFrom
- safeTransferFrom
- setApprovalForAll

### #読み取り

- MAX_SUPPLY
- balanceOf
- balanceOfBatch
- getERC721BalanceOffChain
- getOwnershipRecordOffChain
- isApprovedForAll
- ownerOfERC721Like
- supportsInterface
- uri
  このモジュールとコードには、こちらからアクセスできます：https://bit.ly/42gmxwN

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
Bunzz R&D エンジニア荒牧さんの著書[『スマートコントラクトの仕組みと法律』](https://amzn.to/3V03sNH)が好評発売中です 📕
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
