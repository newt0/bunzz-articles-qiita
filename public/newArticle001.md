---
title: EIP 4844の理解：初心者ガイド
tags:
  - ブロックチェーン
  - DApps
  - Web3
  - DeFi
  - ノーコード
private: false
updated_at: '2024-05-15T17:25:58+09:00'
id: b6aeaafb27187b841569
organization_url_name: null
slide: false
ignorePublish: false
---

:::note info
本記事は下記の翻訳となります。
[『Understanding EIP 4844: A Beginner Guide』](https://blog.bunzz.dev/understanding-eip-4844/)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/beace851-c249-d1e2-e3e1-76f85e78887b.png)

## **イントロダクション：**

ブロックチェーン技術の世界では、Ethereum は拡大するユーザーベースに対応し、トランザクションのスループットを向上させ、コストを削減するためのソリューションに積極的に取り組んできました。長期的なスケーラビリティを実現するために、Ethereum はデータシャーディングのコンセプトを取り入れています。完全なシャーディングに向けたこの旅の一環として、Ethereum Improvement Proposal 4844（EIP-4844）が導入されました。この提案は、セキュリティと分散化を維持しながら、約 10 万トランザクション/秒（TPS）の高いスループットを実現するために、Ethereum を準備することを目指した過渡的なステップとして機能します。

## **EIP 規格と EIP-4844 の重要性の理解：**

Ethereum Improvement Proposals（EIP）は、Ethereum プロトコルの改善、新機能、または変更を概説する公式文書です。これらは、Ethereum コミュニティのメンバーが潜在的な改善策を提案し、議論する手段として機能します。

EIP-4844 は、具体的には Ethereum ネットワーク内でのシャードブロブトランザクションの統合に焦点を当てています。シャーディングは、データベースをより小さなパーティション（シャード）に分割して効率とパフォーマンスを向上させることを意味します。シャードブロブトランザクションを実装することで、Ethereum はトランザクションコストを向上させ、全体的なスループットを増加させることを目指しています。EIP-4844 は完全なシャーディングの解決策ではありませんが、より広範な採用のために必要なスケーラビリティとコスト効率を実現するための重要な一歩となります。

## **この記事から期待できること：**

この記事では、EIP-4844 の詳細と Ethereum のスケーラビリティへの影響について詳しく説明します。シャーディングの概念を説明し、EIP 規格の役割について洞察を提供し、Ethereum エコシステム内でのシャードブロブトランザクションの重要性を明らかにします。さらに、EIP-4844 によって導入された主な機能とメカニズム、ブロブを運ぶトランザクション、ガスの計算、EIP-4844 と完全なシャーディングの関係などを探求します。この記事の最後まで読むことで、EIP-4844 の包括的な理解を得ることができ、Ethereum のスケーラビリティの向上とトランザクションコストの削減に対する取り組みにどのように貢献しているかを理解することができます。

この探求を通じて、以下の洞察を得ることができます：

1. Ethereum のスケーラビリティを向上させるためのシャーディングの概念とその重要性。
2. 完全なシャーディングに向けた中間ステップとしての EIP-4844 の役割。
3. ブロブを運ぶトランザクションやガスの計算など、EIP-4844 によって導入された機能とメカニズム。
4. EIP-4844 が Ethereum のスケーラビリティとコスト削減のロードマップとどのように一致しているか。
5. EIP-4844 の実装によって期待されるユーザーの利点には、より高速なトランザクションと低い手数料が含まれます。

この記事の最後まで読むことで、EIP-4844 の重要性と Ethereum のスケーラビリティと大規模な採用に対する影響を理解し、それについて十分な知識を持つことができるでしょう。

## **EIP-4844 とは何ですか？**

EIP-4844 は、具体的には Ethereum ネットワーク内でのシャードブロブトランザクションの統合に焦点を当てています。シャーディングは、データベースをより小さなパーティション（シャード）に分割して効率とパフォーマンスを向上させることを意味します。Ethereum の文脈では、シャーディングはトランザクションコストを改善し、スループットを増加させることを目指しています。Ethereum は、dank sharding と呼ばれる特定のタイプのシャーディングを実装する予定であり、これにより Ethereum の TPS が約 10 万に大幅に増加することが期待されています。

Danksharding は、以前の Ethereum および非 Ethereum のシャーディング提案と比較して、いくつかの革新を導入しています。それはトランザクションではなくデータのブロブにより多くのスペースを提供することに焦点を当てています。さらに、danksharding は、各シャードが独自の提案者を持つ必要がないように、1 つの提案者がすべてのシャードのトランザクションを選択するマージドフィーマーケットを実装しています。最大抽出可能価値（MEV）の問題に対処するために、提案者/ビルダーの分離方法も導入されています。

### EIP-4844（Proto-Danksharding）

EIP-4844、または proto-dank sharding としても知られるものは、完全な dank sharding に向けた中間ステップとして機能します。これは、TPS を約 1,000 に増やし、「blob-carrying transactions」と呼ばれる新しいトランザクションタイプを導入することを目指しています。これらのトランザクションには、完全な danksharding を実現するための重要な要素である「blob」が含まれています。EIP-4844 の実装は 2023 年の後半に予定されていますが、遅延が発生する可能性もあります。

## **EIP-4844 はどのように機能するのか？**

EIP-4844 は、通常のトランザクションに似ていますが、「blob」と呼ばれるバイナリラージオブジェクトが追加された「blob-carrying transactions」を導入します。これにより、ブロックには blob が添付され、blob を運ぶブロックのデータ容量が増加します。なお、blob の含まれることは、単にブロックサイズを増やすこととは異なります。Ethereum は、中央集権化や計算要件に関する懸念から、ブロックサイズの増加を避けています。

blob はブロックとは異なる特性を持っています。ブロックは無期限に保存され、Ethereum 仮想マシン（EVM）に表示されますが、blob は有限の寿命を持ち、EVM には表示されません。blob は Ethereum のコンセンサスレイヤーに存在し、実行レイヤーではないため、より安価なストレージコストが発生します。EIP-4844 には、将来の完全な danksharding に必要な実行レイヤーロジック、検証ルール、多次元の手数料市場、その他のシステム変更も含まれています。

EIP-4844 は実際のシャーディングを実装していませんが、必要なスケーラビリティとコストレベルを広範な採用に向けて Ethereum をより近づける役割を果たします。完全な danksharding を達成しないにしても、EIP-4844 はスケーラビリティとコスト削減の利点を提供します。

## **EIP-4844 はユーザーにどのような利益をもたらすのか？**

EIP-4844 は、Ethereum のロールアップ中心のロードマップに沿ったプロトコルのアップグレードです。その実装の準備は急速に進んでおり、すでに開発ネットが稼働しており、アップグレードの仕様も最終段階に近づいています。

EIP-4844 の実装後、ユーザーはトランザクションの高速化と手数料の削減という形で明らかな改善を期待することができます。成功した実装は、Ethereum の暗号通貨市場における競争力も向上させます。

削除された古い blob データにアクセスすることに関心を持つユーザーにとって重要なのは、blob は数週間後に削除されますが、そのデータは Ethereum のコンセンサスレイヤーによって長期間保持されるストレージで利用可能であるということです。

## **Blob トランザクション**

EIP-4844 は、EIP-2718 標準に基づいた新しいトランザクションタイプ「blob transaction」を導入します。blob トランザクションの TransactionType は BLOB_TX_TYPE であり、TransactionPayload は TransactionPayloadBody の RLP シリアル化です。TransactionPayloadBody には、chain_id、nonce、max_priority_fee_per_gas、max_fee_per_gas、gas_limit、to、value、data、access_list、max_fee_per_data_gas、blob_versioned_hashes、y_parity、r、s などのさまざまなフィールドが含まれています。

blob トランザクションは通常の作成トランザクションとは異なり、「to」フィールドは 20 バイトのアドレスを表し、nil にすることはできません。

blob トランザクションの EIP-2718 ReceiptPayload は、status、cumulative_transaction_gas_used、logs_bloom、logs を RLP でエンコードしたものです。

Blob トランザクションの形式：

|                    |                                          |
| ------------------ | ---------------------------------------- |
| フィールド         | 説明                                     |
| TransactionType    | BLOB_TX_TYPE                             |
| TransactionPayload | TransactionPayloadBody の RLP シリアル化 |

## **署名**

blob トランザクションの署名値 y_parity、r、s は、特定のダイジェスト上で secp256k1 署名を構築することによって計算されます。ダイジェストは、BLOB_TX_TYPE と chain_id、nonce、max_priority_fee_per_gas、max_fee_per_gas、gas_limit、to、value、data、access_list、max_fee_per_data_gas、blob_versioned_hashes の RLP シリアル化の連結を keccak256 ハッシュアルゴリズムを使用してハッシュ化したものです。

署名の計算：

```
digest = keccak256(BLOB_TX_TYPE || rlp([chain_id, nonce, max_priority_fee_per_gas, max_fee_per_gas, gas_limit, to, value, data, access_list, max_fee_per_data_gas, blob_versioned_hashes]))

signature = secp256k1_sign(digest, private_key)

y_parity, r, s = extract_signature_parts(signature)
```

## **ヘッダー拡張**

EIP-4844 は、2 つの新しい 64 ビット符号なし整数フィールド（data_gas_used および excess_data_gas）を導入することで、現在のヘッダーエンコーディングを拡張します。data_gas_used フィールドは、ブロック内のトランザクションによって消費されるデータガスの総量を表します。excess_data_gas フィールドは、ターゲットを上回って消費されるデータガスの累積トータルを 0 で制限したものを追跡します。ターゲットデータガス消費を超えるブロックは、excess_data_gas の値を増加させ、ターゲットを下回るブロックはその値を減少させます。

ヘッダーエンコーディング：

|                 |                                                                  |
| --------------- | ---------------------------------------------------------------- |
| フィールド      | 説明                                                             |
| data_gas_used   | ブロック内のトランザクションによって消費されるデータガスの総量   |
| excess_data_gas | ブロックの前に消費された余剰データガスの累積トータル（0 で制限） |

## **バージョン付きハッシュを取得するためのオペコード**

EIP-4844 は、バージョン付きハッシュを取得するための新しいオペコードである BLOBHASH（オペコード HASH_OPCODE_BYTE を使用）を導入します。このオペコードは、スタックからビッグエンディアンの uint256 としてインデックスを読み取り、インデックスが blob_versioned_hashes リストの範囲内であれば、tx.blob_versioned_hashes[index]でそれを置き換えます。それ以外の場合は、インデックスをゼロ化された bytes32 の値で置き換えます。このオペコードには、HASH_OPCODE_GAS で定義されたガスコストがかかります。

BLOBHASH オペコード：

|            |                                                                                      |
| ---------- | ------------------------------------------------------------------------------------ |
| オペコード | 説明                                                                                 |
| BLOBHASH   | インデックスをスタックから読み取り、対応するバージョン付きハッシュでそれを置き換える |

## ポイント評価プリコンパイル

POINT_EVALUATION_PRECOMPILE_ADDRESS に位置する新しいプリコンパイルが導入され、KZG プルーフを検証します。このプルーフは、コミットメントによって表されるブロブが特定のポイントで与えられた値に評価されることを示しています。POINT_EVALUATION_PRECOMPILE_GAS のコストで実行されるプリコンパイルは、提供された versioned_hash とコミットメント、ポイント、およびプルーフの値を使用して、コミットメントの関連付けと KZG プルーフの妥当性を検証します。

ポイント評価プリコンパイル：

```
def point_evaluation_precompile(input: Bytes) -> Bytes:
    versioned_hash = input[:32]
    z = input[32:64]
    y = input[64:96]
    commitment = input[96:144]
    proof = input[144:192]

    assert kzg_to_versioned_hash(commitment) == versioned_hash
    assert verify_kzg_proof(commitment, z, y, proof)

    return Bytes(U256(FIELD_ELEMENTS_PER_BLOB).to_be_bytes32() + U256(BLS_MODULUS).to_be_bytes32())
```

## ガスアカウンティング

EIP-4844 は、通常のガスとは独立した新しいタイプとしてデータガスを導入します。EIP-1559 と同様に、データガスも独自のターゲティングルールに従います。excess_data_gas ヘッダーフィールドには、データガス価格を計算するために必要な永続的なデータが格納されます。現在、データガスで価格設定されているのはブロブのみです。

ガスアカウンティングの式：

```
data_fee = calc_data_fee(header, tx)
total_data_gas = get_total_data_gas(tx)
data_gasprice = get_data_gasprice(header)

calc_data_fee(header, tx) = get_total_data_gas(tx) * get_data_gasprice(header)

get_total_data_gas(tx) = DATA_GAS_PER_BLOB * len(tx.blob_versioned_hashes)
get_data_gasprice(header) = fake_exponential(MIN_DATA_GASPRICE, header.excess_data_gas, DATA_GASPRICE_UPDATE_FRACTION)
```

## コンセンサスレイヤーの検証

コンセンサスレイヤーでは、ブロブはビーコンブロック本体に完全にエンコードされず、代わりに「サイドカー」として伝播されます。コンセンサスレイヤーは、ブロブの可用性を確保し、更新されたビーコンブロックの処理、ビーコンブロックタイプと新しいブロブサイドカーのゴシップと同期、および関連するブロブサイドカーを持つビーコンブロックの生成を処理します。

## 実行レイヤーの検証

実行レイヤーでは、ブロックの妥当性条件を強制します。これには、excess_data_gas の更新、ブロブトランザクションの十分な残高、少なくとも 1 つのブロブの存在、バージョン付きブロブハッシュの検証、現在のデータガス価格の確認、総データガスの追跡、およびブロックごとの最大データガスの制限が含まれます。

## ネットワーキング

ブロブトランザクションには、PooledTransactions と BlockBodies の 2 つのネットワーク表現があります。PooledTransactions は、EIP-2718 TransactionPayload、ブロブ、コミットメント、およびプルーフを含むラップ形式を使用します。これらの要素は、ブロブトランザクションの検証に必要なデータをカプセル化しています。ブロックボディの取得応答に使用される BlockBodies は、標準の EIP-2718 ブロブトランザクション TransactionPayload 形式に従います。

ノードはブロブトランザクションを自動的にピアにブロードキャストしません。代わりに、これらのトランザクションは NewPooledTransactionHashes メッセージを使用してアナウンスされ、GetPooledTransactions を使用して手動でリクエストできます。

## 結論

EIP-4844 は、Ethereum の目標であるロールアップの一時的なスケーリングリリーフを提供するための完全なシャーディングへの重要なステップです。EIP-4844 は、最終的なシャーディング仕様の予想される形式でのブロブトランザクションの導入により、ロールアップをスロットあたり 0.375 MB までスケーリングすることを可能にします。システムの限定的な使用時に手数料を低く保つために、別個の手数料市場を確立します。

EIP-4844 の設計は、即時の結果の達成と将来の開発負担の最小化の間の実装の努力をバランスさせています。これには、新しいトランザクションタイプ、実行レイヤーロジック、コンセンサスの相互検証、ビーコンブロックロジック、およびブロブのための自己調整型独立ガス価格など、完全なシャーディングに必要な作業が大幅に進んでいます。

完全なシャーディングに向けたさらなる作業には、2D サンプリングの拡張、データ可用性サンプリングの実装、提案者/ビルダーの分離、およびバリデータの託管要件が含まれます。

EIP-4844 はまた、将来のプロトコルの改善やクリーンアップへの道を開くものであり、そのガス価格の更新ルールを主要なベース手数料の計算に適用することがあります。

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
