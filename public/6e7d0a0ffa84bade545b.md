---
title: '[スレッド] Berachefコントラクトの詳細解説 [Berachain翻訳]'
tags:
  - Blockchain
  - Ethereum
  - Web3
  - Berachain
  - SunriseLayer
private: false
updated_at: '2024-09-11T17:11:46+09:00'
id: 6e7d0a0ffa84bade545b
organization_url_name: sunriselayer
slide: false
ignorePublish: false
---
:::note info
本記事は下記の翻訳となります。
[『[Thread] Berachef contract walk-through』](https://blog.berachain.com/blog/thread-berachef-contract-walk-through-2)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/db659569-f7de-5ce5-2165-af5b58d07f0a.png)

https://x.com/camiinthisthang/status/1818739046358888862

> Berachain では、バリデーターはブロック構築の報酬を Rewards Vaults を通じて dapps に直接配分しなければなりません。バリデーターは「カッティングボード」を通じて、どの vaults にどの比率で報酬を配分するかを選択します。
> スマートコントラクトレベルでこの仕組みがどのように機能するか、詳しく見ていきましょう 👇

https://x.com/camiinthisthang/status/1818739104580092241

> バリデーターは BGT ステーションでこの仕組みを裏で使用し、BGT の配分方法を設定します。円グラフをイメージしてください。各セクションが全体に対する割合を表し、それぞれのセクションが報酬の vault に対応しています。
> 例はこちらでご覧いただけます - https://t.co/dwtNiS0CHy pic.twitter.com/yyexXzn4Iz

https://x.com/camiinthisthang/status/1818739165330391552

> カッティングボードを更新するには、queueNewCuttingBoard 関数が呼び出されます。これにより、新しいカッティングボードが有効になるまでの遅延が設定されます。
> これにより、バリデーターの設定があまり頻繁に変更されないようになり、より予測可能性が高まります。 pic.twitter.com/Q2DQP4XikF

https://x.com/camiinthisthang/status/1818739225174622310

> また、カッティングボードを表す CuttingBoard 構造体があります。これには、このカッティングボードが有効になるブロックと、先ほど見た Weights 構造体の配列が含まれています。 pic.twitter.com/8aANqbQX2j

https://x.com/camiinthisthang/status/1818739685281481008

> 読者の皆様へ：報酬 vaults がゲージと呼ばれているのをご覧になったかもしれません。近々、より分かりやすくするために、ドキュメントと UI を更新して報酬 vaults という表現に統一する予定です。

> Proof of Liquidity のコントラクトについて詳しくは、このスレッドをチェックしてください！

---

---

:::note info
【Sunrise とは】
Sunrise は Proof of Liquidity(PoL)と Fee Abstraction（手数料抽象化）を備えたデータ可用性レイヤーです。 私たちは DA の体験を再構築し、多様なエコシステムからのモジュラー型流動性を活用してロールアップを立ち上げています。

- [Sunrise - Specialized DA Layer for Proof of Liquidity](https://sunriselayer.io/)
- [Sunrise / Gluon Docs](https://docs.sunriselayer.io/)

【Social Links】

- [X(旧 Twitter)[英語])](https://twitter.com/SunriseLayer)
- [X(旧 Twitter)[日本語])](https://twitter.com/SunriseLayer)
- [Discord Community](https://discord.com/invite/sunrise)
- [Medium](https://sunriselayer.medium.com/)
- [Github](https://github.com/sunriselayer)
- [Linkedin](https://www.linkedin.com/company/sunriselayer)

【お問合せ】
Sunrise へのお問い合わせはこちらから 👉 [Google Form](https://forms.gle/h8RVahxRtXUvYwnv6)

![1080x360.jpeg](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3839047/8971d83b-3331-4757-dc72-320d28618735.jpeg)

:::
