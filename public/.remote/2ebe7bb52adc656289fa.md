---
title: スマートコントラクトの将来を確保するために、EUの法律がキルスイッチの実装を義務付けています。
tags:
  - ブロックチェーン
  - DApps
  - Web3
  - DeFi
  - ノーコード
private: false
updated_at: '2024-05-15T17:29:03+09:00'
id: 2ebe7bb52adc656289fa
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---

:::note info
本記事は下記の翻訳となります。
[『Securing the Future of Smart Contracts: EU Legislation Mandates Kill Switch Implementation』](https://blog.bunzz.dev/securing-the-future-of-smart-contracts/)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/dd1455ca-abab-77de-c877-4d5e3c4f5f4b.png)

最近、スマートコントラクトのセキュリティと制御を向上させるための動きとして、欧州議会はすべてのスマートコントラクトにキルスイッチを含めることを義務付ける法律を可決しました。この動きは、ブロックチェーンと仮想通貨のコミュニティ内で多くの議論と話題を呼んでいます。

### **誰が法案を通過させ、いつ、そしてどのような目的で行われましたか？**

2023 年 3 月 10 日、欧州議会はこの法案を可決しました。この法案の目的は、ブロックチェーンベースのアプリケーションやデジタル資産のセキュリティと安定性を向上させることです。議員たちは、この措置によってユーザーがハッカーや悪意のある行為者による潜在的な搾取から保護されるだけでなく、スマートコントラクトに関する予期せぬ問題や紛争が発生した場合に規制上の保護策が提供されると信じています。

> "スマートコントラクトには、リセットや停止、中断の命令を行うことができる内部機能が含まれるべきです。[…]特に、非合意による終了や中断が許容されるべき条件の下で評価されるべきです。"

この法律は、スマートコントラクトが他の契約形態と同等の保護を受けることも認められました。

> "キルスイッチを含めることは、不変性の保証を損ない、キルスイッチの使用を管理するための担当者が必要となるため、障害点を導入します。[…]Uniswap などの多くのスマートコントラクトには、このキルスイッチの機能がありません。"

この法案は、賛成 500、反対 23、棄権 110 の多数で可決されました。議会のメンバーは、欧州連合の欧州評議会および各加盟国との間で法律の最終形態について協議することになります。

### **キルスイッチとは具体的に何であり、どのようなコードを実装する必要がありますか？**

キルスイッチは、特定の条件下でスマートコントラクトの終了または一時停止を可能にする組み込みのメカニズムです。これは、契約が侵害された場合や予期しない事態や法的紛争により実行を停止する必要がある場合に特に有用です。

新しい法律に準拠するために、開発者はスマートコントラクトのコードにキルスイッチを組み込む必要があります。これには、アクセス制御、緊急停止機能、指定された条件または特定の条件でトリガーされるタイムロックアクションの組み合わせが含まれる場合があります。具体的な実装方法は、ブロックチェーンプラットフォームとスマートコントラクトの性質によって異なる場合があります。

スマートコントラクトのキルスイッチは、スマートコントラクト内に組み込まれたメカニズムであり、特定の条件下での終了または一時停止を可能にします。この機能は、予期しない問題、紛争、ハッカーや悪意のある行為者による潜在的な悪用の場合に、スマートコントラクトのセキュリティと制御を向上させるために設計されています。キルスイッチは、指定された当事者または特定の事前定義条件によってトリガーされることがあります。これは、スマートコントラクトのコード内での実装方法によって異なります。

Solidity のスマートコントラクトでは、修飾子、関数、およびアクセス制御を組み合わせてキルスイッチを実装することができます。以下に、Solidity のスマートコントラクトで基本的なキルスイッチを実装する方法の例を示します。

```
pragma solidity ^0.8.0;
contract KillSwitchExample {
  address public owner;
  bool public isPaused;
  // Set the contract's owner as the deployer of the contract
  constructor() {
      owner = msg.sender;
  }
  // Modifier to check if the contract is paused
  modifier whenNotPaused() {
      require(!isPaused, "Contract is paused");
      _;
  }
  // Modifier to check if the caller is the owner
  modifier onlyOwner() {
      require(msg.sender == owner, "Caller is not the owner");
      _;
  }
  // Function to pause or unpause the contract
  function setPaused(bool _isPaused) public onlyOwner {
      isPaused = _isPaused;
  }
  // Example function that can only be called when the contract is not paused
  function doSomething() public whenNotPaused {
      // Your function logic here
  }
}
```

この例では、キルスイッチは isPaused という状態変数と whenNotPaused 修飾子を使用して実装されています。setPaused 関数は、コントラクトのオーナーがコントラクトを一時停止または再開することができるようにします。コントラクトが一時停止されている場合、whenNotPaused 修飾子を使用している関数は実行されず、スマートコントラクトの動作が一時停止されます。

これは単純な例であり、スマートコントラクトの複雑さに応じて、特定の要件に合わせてキルスイッチの実装をカスタマイズする必要がある場合があります。

### **この法案の成立によって、キルスイッチのない以前に展開された契約の使用が違法になりますか？**

新しい法律では、キルスイッチのない以前に展開されたスマートコントラクトの使用を違法にするわけではありません。ただし、欧州連合内でこれらのスマートコントラクトを引き続き使用する場合、開発者は既存のスマートコントラクトにキルスイッチを追加する必要があります。法律に違反した場合、非準拠のスマートコントラクトの開発者やユーザーには罰則やその他の法的な結果が生じる可能性があります。

### **キルスイッチのない契約を開発する企業や個人は、EU のユーザーにサービスを提供できなくなりますか？**

この法案の成立により、キルスイッチのないスマートコントラクトを開発する企業や個人は、ヨーロッパ連合内のユーザーにサービスを提供することができなくなります。サービスの提供を続けるためには、彼らは自身のスマートコントラクトが新しい法律に準拠していることを確認する必要があります。これには、コードの更新、潜在的な脆弱性のあるスマートコントラクトの監査、および新しい規制の範囲内で運営していることを確認するための法的助言の受け入れが必要になる場合があります。

### **結論**

まとめると、欧州議会の法律によるスマートコントラクトへのキルスイッチの組み込み要件は、ブロックチェーン技術とデジタルアセットの領域において重要な進展です。開発者や企業にはいくつかの課題をもたらすかもしれませんが、それはスマートコントラクトの全体的なセキュリティと安定性を向上させ、ユーザーの保護と EU におけるブロックチェーンベースのアプリケーションの成長のための安全な環境を提供する可能性もあります。

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
