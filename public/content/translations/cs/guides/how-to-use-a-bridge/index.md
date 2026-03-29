---
title: Jak propojit tokeny do 2. vrstvy
description: "Návod vysvětlující, jak přesunout tokeny z Etherea do 2. vrstvy pomocí mostu."
lang: cs
---

# Jak propojit tokeny do 2. vrstvy {#how-to-bridge-tokens-to-layer-2}

Pokud je na Ethereu velký provoz, může se to prodražit. Jedním z řešení je vytvoření nových „vrstev“: tj. různých sítí, které fungují podobně jako samotné Ethereum. Tyto takzvané 2. vrstvy pomáhají snižovat přetížení a náklady na Ethereum tím, že zpracovávají mnohem více transakcí za nižší poplatky a jejich výsledek ukládají na Ethereum pouze jednou za čas. Tyto 2. vrstvy nám tak umožňují provádět transakce s vyšší rychlostí a nižšími náklady. Mnoho populárních krypto projektů přechází na 2. vrstvu právě kvůli těmto výhodám. Nejjednodušší způsob, jak přesunout tokeny z Etherea do 2. vrstvy, je použít most.

**Předpoklady:**

- mít kryptoměnovou peněženku – pokud ji nemáte, řiďte se tímto návodem a [vytvořte si účet na Ethereu](/guides/how-to-create-an-ethereum-account/)
- mít v peněžence prostředky

## 1. Určete, kterou síť 2. vrstvy chcete použít {#1-determine-which-layer-2-network-you-want-to-use}

Více informací o různých projektech a důležitých odkazech najdete na naší [stránce o druhé vrstvě](/layer-2/).

## 2. Otevřete si vybraný most {#2-go-to-the-selected-bridge}

Mezi populární 2. vrstvy patří:

- [Přemostění Arbitrum](https://portal.arbitrum.io/bridge?l2ChainId=42161)
- [Přemostění Optimism](https://app.optimism.io/bridge/deposit)
- [Přemostění sítě Boba](https://hub.boba.network/)

## 3. Připojte se k mostu pomocí vaší peněženky {#3-connect-to-the-bridge-with-your-wallet}

Ujistěte se, že je vaše peněženka připojena k síti hlavní síti Etherea. Pokud není, webová stránka vás automaticky vyzve k přepnutí sítě.

![Společné rozhraní pro přemosťování tokenů](./bridge1.png)

## 4. Zadejte částku a přesuňte prostředky {#4-specify-the-amount-and-move-the-funds}

Zkontrolujte si částku, kterou získáte na oplátku v síti 2. vrstvy, a poplatky, abyste se vyhnuli nepříjemným překvapením.

![Společné rozhraní pro přemosťování tokenů](./bridge2.png)

## 5. Potvrďte tuto transakci ve své peněžence {#5-confirm-the-transaction-in-your-wallet}

Za zpracování transakce budete muset zaplatit poplatek (nazývaný [palivo](/glossary/#gas)) ve formě ETH.

![Společné rozhraní pro přemosťování tokenů](./bridge3.png)

## 6. Počkejte, až budou vaše prostředky převedeny {#6-wait-for-your-funds-to-be-moved}

Tento proces by neměl trvat déle než 10 minut.

## 7. Přidejte vybranou síť 2. vrstvy do své peněženky (volitelné) {#7-add-the-selected-layer-2-network-to-your-wallet-optional}

Podrobnosti o síti RPC můžete zjistit pomocí [chainlist.org](http://chainlist.org). Po přidání sítě a dokončení transakce byste měli tokeny vidět ve své peněžence. <br />

<Alert variant="update">
<AlertEmoji text=":eyes:"/>
<AlertContent className="justify-between flex-row items-center">
  <div>Chcete se dozvědět více?</div>
  <ButtonLink href="/guides/">
    Podívejte se na naše další návody
  </ButtonLink>
</AlertContent>
</Alert>

## Často kladené dotazy {#frequently-asked-questions}

### Co když mám prostředky na burze? {#what-if-i-have-funds-on-an-exchange}

Možná budete moci vybírat na některé 2. vrstvě přímo z burzy. Další informace naleznete v části „Přejít na druhou vrstvu“ na naší [stránce o druhé vrstvě](/layer-2/).

### Mohu se po přesunu svých tokenů na 2. vrstvu vrátit zpět do hlavní sítě Etherea? {#can-i-go-back-to-ethereum-mainnet-after-i-bridge-my-tokens-to-l2}

Ano, své prostředky můžete kdykoli přesunout zpět do hlavní sítě pomocí stejného mostu.
