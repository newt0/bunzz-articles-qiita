---
title: "Goldsky \U0001F9EEによるBerachainのデータのインデックスとクエリ [Berachain翻訳]"
tags:
  - Blockchain
  - Ethereum
  - Web3
  - cosmos
  - Berachain
private: false
updated_at: '2024-09-09T15:50:47+09:00'
id: 0d7aee0215eb67ebbfc6
organization_url_name: sunriselayer
slide: false
ignorePublish: false
---
:::note info
本記事は下記の翻訳となります。
[『Index & Query Berachain Data with Goldsky 🧮』](https://blog.berachain.com/blog/index-query-berachain-data-with-goldsky)
:::

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1926720/b5e53715-cfce-054a-c991-77e117479f62.png)

## Goldsky とは何か、なぜインデックス化に関心を持つ必要があるのか？

[Goldsky](https://goldsky.com/?ref=berachain.ghost.io)は、開発者がブロックチェーンからデータを格納してクエリする[GraphQL](https://graphql.org/?ref=berachain.ghost.io) API を構築することができます。このデータは高度にカスタマイズ可能であり、トークン供給の成長などのトレンドを明らかにするために使用したり、ユーザーのトークン残高などの瞬時のデータを取得したりすることができます。

サブグラフには、ブロックチェーンからデータをインデックス化し、生データを変換して簡単にクエリできる形式で格納するためのロジックが含まれています。

このチュートリアルでは、[**Berachain**](https://www.berachain.com/?ref=berachain.ghost.io)ネットワーク上のユーザーの ERC20 残高をクエリするサブグラフの開発方法を学びます。

### 必要要件 📋

- Nodejs `v20.11.0`以上
- pnpm
- IDE（例：VSCode、Replit など）

既に[The Graph](https://thegraph.com/?ref=berachain.ghost.io)に展開されているサブグラフを Berchain/Goldsky に展開したい場合は、「Goldsky でのセットアップ」セクションに進んでください。Goldsky と The Graph のサブグラフは完全な互換性があります！

### サブグラフの構築 🛠️

まず、ターミナルに入力してください：

```terminal
mkdir goldsky-subgraph;
cd goldsky-subgraph;

pnpm init;

pnpm install @graphprotocol/graph-cli @graphprotocol/graph-ts;

# Accept all of the defaults, hitting enter when prompted

# name: (project-name) project-name
# version: (0.0.0) 0.0.1
# description: The Project Description
# entry point: //leave empty
# test command: //leave empty
# git repository: //the repositories url
# keywords: //leave empty
# author: // your name
# license: N/A

# @graphprotocol dependencies provide subgraph development tooling
```

プロジェクトのルートに、以下のプロジェクト構造を作成してください（空のファイルでも構いません）:

```text
# FROM: ./goldsky-subgraph;

.
├── abis
│   └── Erc20.json
├── package.json
├── schema.graphql
├── src
│   ├── mapping.ts
│   ├── utils.ts
└── subgraph.yaml
```

`./abis/Erc20.json` に以下の内容を貼り付けて、ERC20 コントラクトのインターフェースを定義します:

```json
[
  {
    "constant": true,
    "inputs": [],
    "name": "name",
    "outputs": [{ "name": "", "type": "string" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      { "name": "_spender", "type": "address" },
      { "name": "_value", "type": "uint256" }
    ],
    "name": "approve",
    "outputs": [{ "name": "", "type": "bool" }],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "totalSupply",
    "outputs": [{ "name": "", "type": "uint256" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      { "name": "_from", "type": "address" },
      { "name": "_to", "type": "address" },
      { "name": "_value", "type": "uint256" }
    ],
    "name": "transferFrom",
    "outputs": [{ "name": "", "type": "bool" }],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "decimals",
    "outputs": [{ "name": "", "type": "uint8" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [{ "name": "_owner", "type": "address" }],
    "name": "balanceOf",
    "outputs": [{ "name": "balance", "type": "uint256" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [],
    "name": "symbol",
    "outputs": [{ "name": "", "type": "string" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  {
    "constant": false,
    "inputs": [
      { "name": "_to", "type": "address" },
      { "name": "_value", "type": "uint256" }
    ],
    "name": "transfer",
    "outputs": [{ "name": "", "type": "bool" }],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
  },
  {
    "constant": true,
    "inputs": [
      { "name": "_owner", "type": "address" },
      { "name": "_spender", "type": "address" }
    ],
    "name": "allowance",
    "outputs": [{ "name": "", "type": "uint256" }],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
  },
  { "payable": true, "stateMutability": "payable", "type": "fallback" },
  {
    "anonymous": false,
    "inputs": [
      { "indexed": true, "name": "owner", "type": "address" },
      { "indexed": true, "name": "spender", "type": "address" },
      { "indexed": false, "name": "value", "type": "uint256" }
    ],
    "name": "Approval",
    "type": "event"
  },
  {
    "anonymous": false,
    "inputs": [
      { "indexed": true, "name": "from", "type": "address" },
      { "indexed": true, "name": "to", "type": "address" },
      { "indexed": false, "name": "value", "type": "uint256" }
    ],
    "name": "Transfer",
    "type": "event"
  }
]
```

### サブグラフの設定

サブグラフを作成する最初のステップは、データソースとデータ構造（エンティティ）を定義することです。これは、`subgraph.yaml`またはサブグラフマニフェストで行います。

`./subgraph.yaml`に以下を貼り付けてください：

```yaml
specVersion: 0.0.4
description: ERC-20 subgraph with event handlers & entities
schema:
  file: ./schema.graphql
dataSources:
  - kind: ethereum/contract
    name: Erc20
    network: berachain-bartio
    source:
      address: "0x1306D3c36eC7E38dd2c128fBe3097C2C2449af64"
      abi: Erc20
      startBlock: 88948
    mapping:
      kind: ethereum/events
      apiVersion: 0.0.7
      language: wasm/assemblyscript
      entities:
        - Token
        - Account
        - TokenBalance
      abis:
        - name: Erc20
          file: ./abis/Erc20.json
      eventHandlers:
        - event: Transfer(indexed address,indexed address,uint256)
          handler: handleTransfer
      file: ./src/mapping.ts
```

このマニフェストでは、いくつかのポイントがあります：

1. `source`: アドレスは[bHONEY トークン](https://bartio.beratrail.io/address/0x1306D3c36eC7E38dd2c128fBe3097C2C2449af64?ref=berachain.ghost.io)であり、`Erc20`インターフェースを使用して、デプロイされた`startBlock`からインデックスされます
2. `entities`は、クエリ可能な JavaScript オブジェクトと考えることができます。エンティティはお互いに関連付けられることがあり、GraphQL スキーマで定義されます（以下参照）
3. `eventHandlers`: トークンの`Transfer`イベントが発生するたびに、`./src/mapping.ts`の`handleTransfer`メソッドが呼び出され、インデックスロジックが実行されます

### スキーマの作成

`./schema.graphql` では、サブグラフ内に存在するさまざまなエンティティのプロパティと関係を定義します。

```graphql
# Token details
type Token @entity {
  id: ID!
  #token name
  name: String!
  #token symbol
  symbol: String!
  #decimals used
  decimals: BigDecimal!
}

# account details
type Account @entity {
  #account address
  id: ID!
  #balances
  balances: [TokenBalance!]! @derivedFrom(field: "account")
}

# token balance details
type TokenBalance @entity {
  id: ID!
  #token
  token: Token!
  #account
  account: Account!
  #amount
  amount: BigDecimal!
}
```

`Token`エンティティは、ERC20 トークンのよく知られたプロパティを含んでいます。

`Account`エンティティには、ウォレットアドレスの`id`と興味深いことに、`TokenBalance`タイプの`balances`リストが含まれています。`@derivedFrom`ディレクティブは、アカウントの`balances`プロパティが、`TokenBalance`エンティティの`account`プロパティに基づいて逆引きで定義されることを意味します。

`TokenBalance`は、`Account`エンティティと`Token`エンティティの両方を活用して、各ユーザーのトークン残高を定義しています。

このチュートリアルでは、`Token`エンティティと`TokenBalance`エンティティの両方を持つ必要はありませんでした。ユーザーの MIM 残高は、単に`Account`エンティティにキャプチャすることも考えられます。ただし、この設計により、複数のトークン残高をキャプチャするためにサブグラフを拡張することが可能になります。

### マッピングの作成

マッピングファイルは、すべてが一緒になる場所です ✨ ブロックチェーンのデータは、スキーマで定義したエンティティと関連付けられます。以下では、`handleTransfer` イベントハンドラが呼び出されたときに発生する相互作用を定義しています。

`./src/mapping.ts` に以下のコードを追加してください:

```ts
//import event class from generated files
import { Transfer } from "../generated/Erc20/Erc20";
//import the functions defined in utils.ts
import { fetchTokenDetails, fetchAccount, updateTokenBalance } from "./utils";
//import datatype
import { BigInt } from "@graphprotocol/graph-ts";

export function handleTransfer(event: Transfer): void {
  // 1. Get token details
  let token = fetchTokenDetails(event);
  if (!token) {
    return;
  }

  // 2. Get account details
  let fromAddress = event.params.from.toHex();
  let toAddress = event.params.to.toHex();

  let fromAccount = fetchAccount(fromAddress);
  let toAccount = fetchAccount(toAddress);

  if (!fromAccount || !toAccount) {
    return;
  }

  // 3. Update the token balances
  // Setting the token balance of the 'from' account
  updateTokenBalance(
    token,
    fromAccount,
    BigInt.fromI32(0).minus(event.params.value)
  );

  // Setting the token balance of the 'to' account
  updateTokenBalance(token, toAccount, event.params.value);
}
```

`handleTransfer` は `Transfer` イベントをパラメータとして受け取り、情報 `(fromAddress, toAddress, transferAmount)` を含んでいます。この情報を使用して、ハンドラは次の機能を実行することができます:

1. トークンの詳細を取得する
2. アカウントの詳細を取得する
3. アカウントの残高を更新する

高レベルでは、このハンドラのコードは、`Transfer` イベントが発生するたびに、ERC20 アカウントの残高を忠実に更新します。

#### **エンティティの操作**

`mapping.ts`のコードは非常にシンプルですが、エンティティとのやり取りの重要な部分はユーティリティファイルに抽象化されています。では、サブグラフのエンティティとの操作の基本を見ていきましょう。

`./src/utils.ts`に以下のコードを追加してください：

```ts
//import smart contract class from generated files
import { Erc20 } from "../generated/Erc20/Erc20";
//import entities
import { Account, Token, TokenBalance } from "../generated/schema";
//import datatypes
import { BigDecimal, ethereum, BigInt } from "@graphprotocol/graph-ts";

const ZERO_ADDRESS = "0x0000000000000000000000000000000000000000";

// Fetch token details
export function fetchTokenDetails(event: ethereum.Event): Token | null {
  //check if token details are already saved
  let token = Token.load(event.address.toHex());
  if (!token) {
    //if token details are not available
    //create a new token
    token = new Token(event.address.toHex());

    //set some default values
    token.name = "N/A";
    token.symbol = "N/A";
    token.decimals = BigDecimal.fromString("0");

    //bind the contract
    let erc20 = Erc20.bind(event.address);

    //fetch name
    let tokenName = erc20.try_name();
    if (!tokenName.reverted) {
      token.name = tokenName.value;
    }

    //fetch symbol
    let tokenSymbol = erc20.try_symbol();
    if (!tokenSymbol.reverted) {
      token.symbol = tokenSymbol.value;
    }

    //fetch decimals
    let tokenDecimal = erc20.try_decimals();
    if (!tokenDecimal.reverted) {
      token.decimals = BigDecimal.fromString(tokenDecimal.value.toString());
    }

    //save the details
    token.save();
  }
  return token;
}

// Fetch account details
export function fetchAccount(address: string): Account | null {
  //check if account details are already saved
  let account = Account.load(address);
  if (!account) {
    //if account details are not available
    //create new account
    account = new Account(address);
    account.save();
  }
  return account;
}

export function updateTokenBalance(
  token: Token,
  account: Account,
  amount: BigInt
): void {
  // Don't update zero address
  if (ZERO_ADDRESS == account.id) return;

  // Get existing account balance or create a new one
  let accountBalance = getOrCreateAccountBalance(account, token);
  let balance = accountBalance.amount.plus(bigIntToBigDecimal(amount));

  // Update the account balance
  accountBalance.amount = balance;
  accountBalance.save();
}

function getOrCreateAccountBalance(
  account: Account,
  token: Token
): TokenBalance {
  let id = token.id + "-" + account.id;
  let tokenBalance = TokenBalance.load(id);

  // If balance is not already saved
  // create a new TokenBalance instance
  if (!tokenBalance) {
    tokenBalance = new TokenBalance(id);
    tokenBalance.account = account.id;
    tokenBalance.token = token.id;
    tokenBalance.amount = BigDecimal.fromString("0");

    tokenBalance.save();
  }

  return tokenBalance;
}

function bigIntToBigDecimal(quantity: BigInt, decimals: i32 = 18): BigDecimal {
  return quantity.divDecimal(
    BigInt.fromI32(10)
      .pow(decimals as u8)
      .toBigDecimal()
  );
}
```

- `fetchAccount()`は`Account`エンティティを返します。まず、渡された`address`を持つ`Account`エンティティが存在するかどうかを確認します。存在しない場合は新しいエンティティを作成します。
- `fetchTokenDetails()`は`Token`エンティティを返します。`Token`が存在しない場合、トークンアドレスを`ERC20`インターフェースにバインドして新しいインスタンスを作成します。これにより、トークンコントラクトから公開された読み取り関数にアクセスできるようになります。これにより、名前、シンボル、小数点以下の桁数などのトークンのプロパティを取得および設定できます。

- `updateTokenBalance()`はおそらく最も重要な関数であり、各転送ごとにユーザーの`TokenBalance`エンティティを更新します。`mapping.ts`ファイルに戻ってみると、この関数は`Transfer`イベントごとに 2 回呼び出されます。転送元の場合は負の`amount`が渡され、トークン残高の減少を示し、逆に受信者の場合は正の`amount`が渡されます。これにより、トークン残高の正確な会計が維持されます。

#### サブグラフのビルド

プロジェクトディレクトリのルートで、ターミナルで次のコマンドを実行します:

```terminal
# FROM: ./goldsky-subgraph;

pnpm codegen;
pnpm build;
```

これらのコマンドは、コントラクトの ABI から TypeScript クラスファイルを生成し、コードをコンパイルし、`/build`ディレクトリにビルド出力を作成します。

デプロイする前に、Goldsky での設定が必要です。

### Goldsky での設定方法

Goldsky は、サブグラフをホストし、必要なインデックス作業を行います。以下の手順に従ってアカウントを設定してください：

1. [app.goldsky.com](https://app.goldsky.com/?ref=berachain.ghost.io)でアカウントを作成します。
2. [設定ページ](https://app.goldsky.com/dashboard/settings?ref=berachain.ghost.io)で API キーを作成します。
3. Goldsky CLI をインストールします：

```terminal
curl https://goldsky.com | sh
```

4\. Log in with the API key created earlier:

```
goldsky login
```

#### サブグラフをデプロイする 🚀

プロジェクトのルートで、次のコマンドを実行します：

```
# FROM: ./goldsky-subgraph;

goldsky subgraph deploy erc20-subgraph/1.0.0 --path .
```

デプロイが成功したら、[デプロイされたサブグラフを表示](https://app.goldsky.com/dashboard/subgraphs?ref=berachain.ghost.io)します。ただし、すぐに使用することはできません。インデックス作成プロセスでは、トークンの残高を更新するためにすべてのブロックを処理する必要があります。

![](https://super-translator.inaridiy.workers.dev/assets/image/ca554c3c-3be4-4e99-a242-eeb8854ae1a7)
_Goldsky Subgraph Dashboard_

#### データのクエリ

ダッシュボードでは、「パブリック GraphQL リンク」という項目が表示されます。これを使用してクエリを作成することができます。新しいサブグラフを使って次のクエリを試してみましょう。

```graphql
{
  accounts {
    id
    balances {
      id
      token {
        id
        name
        symbol
        decimals
      }
      amount
    }
  }
}
```

一緒に試すための例が必要な場合は、この[ライブサブグラフ](https://api.goldsky.com/api/public/project_clteviu2hajla01r51uil7cp5/subgraphs/erc20-subgraph/1.0.0/gn?ref=berachain.ghost.io)を使用してください。

ユーザーの MIM 残高を Berachain の[ブロックエクスプローラ](https://artio.beratrail.io/address/0x000000000746a93872fecf15c2f22b998131df94?ref=berachain.ghost.io)と照合すると、サブグラフが正確にユーザーのトークン残高をインデックス化していることがわかります ✅

![](https://super-translator.inaridiy.workers.dev/assets/image/59c3e726-a19d-4161-9e04-a5b2f15f3277)
_Comparison of Subgraph and Block Explorer Token Balances_

## まとめ

これが Berachain ウォレットのトークン残高をインデックス化するために Goldsky サブグラフを使用する方法です。Goldsky は、開発者が簡単にカスタマイズされたブロックチェーンデータを保存およびクエリするためのデータ可用性プラットフォームです。

---

#### 🐻 Full Code Repository

最終的なコードを確認したり、他のガイドを見たりするには、[**_Berachain Goldsky Guide Code_**](https://github.com/berachain/guides/tree/main/apps/goldsky-subgraph?ref=berachain.ghost.io)をチェックしてください。

##### 🛠️ もっと作りたいですか？

Berachain でさらに多くのものを構築し、さらに多くの例を見たい場合は、[**_Berachain GitHub Guides Repo_**](https://github.com/berachain/guides?ref=berachain.ghost.io)をご覧ください。NextJS、Hardhat、Viem、Foundry など、さまざまな実装があります。

#### 開発者サポートをお探しですか？

質問をするために、[**_Berachain Discord_**](https://discord.com/invite/berachain?ref=berachain.ghost.io)サーバーに参加し、開発者チャンネルをチェックしてください。

❤️ この記事に対して愛を示すのを忘れないでください 👏🏼

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
