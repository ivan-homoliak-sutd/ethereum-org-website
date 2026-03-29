---
title: "トークンをレイヤー2にブリッジする方法"
description: "ブリッジを使用してイーサリアムからレイヤー2にトークンを移動させる方法。"
lang: ja
---

# トークンをレイヤー2にブリッジする方法 {#how-to-bridge-tokens-to-layer-2}

イーサリアムの取引量が多くなると、手数料が高騰する場合があります。 これに対する1つの解決方法は新しい"レイヤー"をつくることです。すなわち、イーサリアムそのものと同じような方法で機能する別のネットワークをつくることです。 これらは、いわゆるレイヤー2と呼ばれ、低い手数料でより多くのトランザクションを処理し、定期的に結果をイーサリアムに保存するだけなのでイーサリアムの混雑とコストを減らすのに役立ちます。 そのためトランザクションの速度が向上し、コストが削減できます。 これらの長所によって、多くの人気のあるクリプトプロジェクトはレイヤー2に移行しています。 トークンをイーサリアムからレイヤー2へ移動する最も簡単な方法としては、ブリッジを使うことです。

**前提条件:**

- 暗号通貨ウォレットが必要です。— お持ちでない場合は、このガイド[イーサリアムアカウントを作成する](/guides/how-to-create-an-ethereum-account/)に従ってください。
- ウォレットに資金を追加する

## 1. 使用したいレイヤー2ネットワークを決定する {#1-determine-which-layer-2-network-you-want-to-use}

当サイトの[レイヤー2ページ](/layer-2/)で、さまざまなプロジェクトや重要なリンクについて詳しく知ることができます。

## 2. 選択したブリッジへ行く {#2-go-to-the-selected-bridge}

人気のあるレイヤー2ネットワークをいくつか挙げます。

- [Arbitrumブリッジ](https://portal.arbitrum.io/bridge?l2ChainId=42161)
- [Optimismブリッジ](https://app.optimism.io/bridge/deposit)
- [Bobaネットワークブリッジ](https://hub.boba.network/)

## 3. ウォレットをブリッジに接続する {#3-connect-to-the-bridge-with-your-wallet}

ウォレットがイーサリアムのメインネットネットワークに接続されていることを確認します。 接続されていない場合、ネットワークを切り替えるように、ウェブサイトが自動的に要求します。

![トークンをブリッジするための共通インターフェース](./bridge1.png)

## 4. 金額を指定して資金を移動する {#4-specify-the-amount-and-move-the-funds}

思わぬ事態を防ぐために、レイヤー2ネットワークに入る金額と、それにかかる手数料を確認してください。

![トークンをブリッジするための共通インターフェース](./bridge2.png)

## 5. ウォレットのトランザクションを確認する {#5-confirm-the-transaction-in-your-wallet}

トランザクションを処理するために、ETHの形で手数料([ガス](/glossary/#gas)と呼ばれる)を支払う必要があります。

![トークンをブリッジするための共通インターフェース](./bridge3.png)

## 6. 資金が移動されるのを待つ {#6-wait-for-your-funds-to-be-moved}

このプロセスに10分以上かかることはありません。

## 7. 選択したレイヤー2ネットワークをウォレットに追加する (オプション) {#7-add-the-selected-layer-2-network-to-your-wallet-optional}

ネットワークのRPC詳細は、[chainlist.org](http://chainlist.org)で確認できます。 ネットワークの追加およびトランザクションの完了により、トークンがウォレットに表示されるはずです。 <br />

<Alert variant="update">
<AlertEmoji text=":eyes:"/>
<AlertContent className="justify-between flex-row items-center">
  <div>さらに詳しく知りたいですか？</div>
  <ButtonLink href="/guides/">
    他のガイドを見る
  </ButtonLink>
</AlertContent>
</Alert>

## よくある質問 {#frequently-asked-questions}

### 取引所に資金がある場合はどうなりますか? {#what-if-i-have-funds-on-an-exchange}

取引所から直接、一部のレイヤー2へ引き出しできる場合があります。 詳細については、[レイヤー2ページ](/layer-2/)の「レイヤー2への資金移動」セクションをご覧ください。

### トークンをL2にブリッジした後、イーサリアムメインネットに戻すことはできますか？ {#can-i-go-back-to-ethereum-mainnet-after-i-bridge-my-tokens-to-l2}

はい、同じブリッジを使用していつでも資金をメインネットに戻すことができます。
