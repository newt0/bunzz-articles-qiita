---
title: Bunzzとの楽しいFunDityの構築：Salem Olaoyeへのインタビュー
tags:
  - 仮想通貨
  - ブロックチェーン
  - DApps
  - Web3
  - DeFi
private: false
updated_at: '2024-05-15T15:57:24+09:00'
id: e3bcc18fa87ff72b7fa3
organization_url_name: bunzzdev
slide: false
ignorePublish: false
---
:::note info
本記事は下記の翻訳となります。
[『Building FunDity with Bunzz: An Interview with Salem Olaoye』](https://blog.bunzz.dev/building-fundity-an-interview-with-salem-olaoye/)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/438597/f46353b6-26a8-0c4e-526a-2f54565b2f6e.png)

# Building FunDity with Bunzz: An Interview with Salem Olaoye

このブログ記事では、Web3Africa ハッカソンで Bunzz と提携して[FunDity](https://bunzz-fun-dity-5no1.vercel.app/)という募金 DApp を開発したスマートコントラクト開発者の[Salem Olaoye](https://twitter.com/Salthegeek1)さんへのインタビューについて詳しく掘り下げる特権を得ました。

Salem さんは、ハッカソンでの経験、彼のチームが FunDity を作った理由、そして開発プロセスで Bunzz がどのように使用されたかについて、魅力的な旅に連れて行ってくれます。

以下は私たちの会話のハイライトです：

**Q: 自己紹介をお願いします。**

Salem: 私の名前は Salem Olaoye です。スマートコントラクトの開発に 1 年半以上没頭しています。

**Q: ハッカソンで作成した dApp について詳細を教えていただけますか？**

Salem: 私が作成した dApp は、[FunDity](https://bunzz-fun-dity-5no1.vercel.app/)という分散型の募金プラットフォームです。FunDity は、起業に関連するプロジェクト、スタートアップ、非営利団体の資金調達における透明性などの課題に取り組んでいます。この dApp は、各キャンペーンのために Ethereum アドレスを自動作成することで、募金プロセスを簡素化します。ユーザーは dApp を通じて簡単にキャンペーンを作成し、キャンペーンアドレスを共有し、シームレスに資金を受け取ることができます。さらに、dApp 内での資金の透明な追跡を提供し、説明責任を確保します。

**Q: FunDity は GoFundMe と似ていますか？**

Salem: はい、GoFundMe と類似点があります。FunDity は、GoFundMe のブロックチェーン版です。

**Q: あなたの dApp のアイデアのインスピレーションは何ですか？**

Salem: この dApp のアイデアのインスピレーションは、お金が多くの人々の生活に重要な役割を果たしているという認識から生まれました。募金プロセスを簡素化し、スマートコントラクトベースのキャンペーンウェブサイトの作成を自動化することで、Web3 の初心者に対して、複雑な開発やウェブサイト作成の必要性を排除したアクセス可能なプラットフォームを提供することを目指しました。

**Q: 2 人のチームで作業したとお聞きしましたが、あなたはどの役割を担当し、主にバックエンドの開発を担当しましたか？**

Salem: はい、私は主にバックエンドの開発を担当しました。スマートコントラクトを構築し、包括的なテストを書き、デプロイプロセスを担当しました。

**Q: このプロジェクトで使用したテックスタックについての洞察を提供していただけますか？**

Salem: Solidity と Ethers.js などのツールを使用しました。さらに、特定の側面の整合性を確保するために Hardhat を組み込みました。また、このプロジェクトでは、スマートコントラクトのデプロイとの効率的な相互作用において特に優れたツールである[Bunzz](https://www.bunzz.dev/)を使用しました。

**Q: Bunzz を具体的にどのように使用しましたか？主にスマートコントラクトのデプロイに使用しましたか？**

Salem: Bunzz は、dApp とのシームレスな相互作用のためのモジュールの作成に重要な役割を果たしました。スマートコントラクトのデプロイと相互作用のプロセスを効率化し、煩雑なコーディングの必要性を排除しました。

Bunzz は、私たちの開発ワークフローを大幅に簡素化する貴重なツールでした。

**Q: このプロジェクトをさらに開発・拡大する予定はありますか？**

Salem: 絶対に、このプロジェクトをさらに開発する予定があります。GoFundMe などの既存のプラットフォームが存在する一方で、私の最初の焦点はプロジェクトやキャンペーンのクラウドファンディングを求める個人にあります。彼らのニーズに対応した簡単で安全なソリューションを提供することを目指しています。

**Q: この dApp の採用において何か課題を予測していますか？**

Salem: この dApp の採用には大きな障壁はないと確信しています。私たちはクラウドファンディングキャンペーンの作成プロセスを簡素化し、ブロックチェーン技術による資金の安全性を確保しています。ユーザーフレンドリーなインターフェース、キャンペーンごとに生成される一意の Ethereum アドレスの自動生成、学習コストの最小化により、スムーズな採用プロセスを予測しています。

**Q: どのブロックチェーンプラットフォームにこの dApp を展開する予定ですか？Ethereum が主な選択肢とおっしゃいましたが、それは正しいですか？**

Salem: はい、Ethereum は展開の主な選択肢ですが、Polygon などの代替案も検討しています。現在、テスト目的で Polygon のテストネットを利用しています。

**Q: ブロックチェーンの領域でどこまでキャリアを築きたいとお考えですか？**

Salem: 私はフルタイムのスマートコントラクト開発者になることを目指しており、この分野で私の目標に合致するチームの一員であることに幸運を感じています。私の究極の目標は、分散型技術の進歩に貢献し、ブロックチェーン業界の未来を形作ることです。

---

[Bunzz](https://www.bunzz.dev/)では、実際の問題を解決するためのブロックチェーンソリューションをサポートし、提供していることに興奮しています。Salem が FunDity を構築する過程での旅は、コミュニティの力、継続的な学習、革新的な思考の重要性を示しています。彼の分散型募金のための dApp は、ブロックチェーン空間内での資金調達に対する実用的で透明性のある安全なソリューションを紹介しています。

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
