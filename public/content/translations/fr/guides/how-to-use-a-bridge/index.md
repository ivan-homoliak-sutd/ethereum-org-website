---
title: "Comment transférer des jetons aux réseaux de seconde couche"
description: "Un guide expliquant comment déplacer des jetons d'Ethereum vers la couche Layer 2 à l'aide d'un pont (ou bridge)."
lang: fr
---

# Comment transférer des jetons aux réseaux de seconde couche {#how-to-bridge-tokens-to-layer-2}

Si le trafic sur Ethereum devient trop important, cela peut devenir coûteux. Une solution à cela est de créer de nouvelles "couches" : c'est-à-dire différents réseaux qui fonctionnent de manière similaire à Ethereum lui-même. Ces "Layer 2s" aident à réduire la congestion et les coûts sur Ethereum en traitant beaucoup plus de transactions à des frais réduits, et en ne stockant les résultats de ces transactions sur Ethereum que de temps en temps. Ainsi, ces couches secondaires nous permettent de réaliser des transactions plus rapidement et à moindre coût. Beaucoup de projets crypto adopte cette approche pour ces bénéfices. Le moyen le plus simple de déplacer des jetons d'Ethereum vers une "Layer 2" est d'utiliser un pont (bridge).

**Prérequis :**

- avoir un portefeuille de cryptomonnaies — si vous n'en avez pas, suivez ce guide pour [créer un compte Ethereum](/guides/how-to-create-an-ethereum-account/)
- ajouter des fonds à votre portefeuille

## 1. Déterminez le réseau de seconde couche que vous souhaitez utiliser {#1-determine-which-layer-2-network-you-want-to-use}

Vous pouvez en apprendre plus sur les différents projets et trouver des liens importants sur notre [page sur la couche 2](/layer-2/).

## 2. Accédez au pont sélectionné {#2-go-to-the-selected-bridge}

Quelques exemples de solutions de seconde couche populaires :

- [Pont Arbitrum](https://portal.arbitrum.io/bridge?l2ChainId=42161)
- [Pont Optimism](https://app.optimism.io/bridge/deposit)
- [Pont du réseau Boba](https://hub.boba.network/)

## 3. Connectez-vous au pont avec votre portefeuille {#3-connect-to-the-bridge-with-your-wallet}

Assurez-vous que votre portefeuille est connecté au réseau principal Ethereum. Si ce n'est pas le cas, le site vous demandera automatiquement de changer de réseau.

![Interface commune pour la mise en pont de jetons](./bridge1.png)

## 4. Indiquez le montant et transférez les fonds {#4-specify-the-amount-and-move-the-funds}

Vérifiez le montant que vous recevrez sur le réseau de seconde couche et les frais associés pour éviter les mauvaises surprises.

![Interface commune pour la mise en pont de jetons](./bridge2.png)

## 5. Confirmez cette transaction dans votre portefeuille {#5-confirm-the-transaction-in-your-wallet}

Vous devrez payer des frais (appelés [gaz](/glossary/#gas)) sous forme d'ETH pour le traitement de la transaction.

![Interface commune pour la mise en pont de jetons](./bridge3.png)

## 6. Attendez que vos fonds soient transférés {#6-wait-for-your-funds-to-be-moved}

Cette opération ne devrait pas prendre plus de 10 minutes.

## 7. Ajoutez le réseau de la seconde couche sélectionnée sur votre portefeuille (facultatif) {#7-add-the-selected-layer-2-network-to-your-wallet-optional}

Vous pouvez utiliser [chainlist.org](http://chainlist.org) pour trouver les détails RPC du réseau. Une fois le réseau ajouté et la transaction terminée, vous devriez voir les jetons dans votre portefeuille. <br />

<Alert variant="update">
<AlertEmoji text=":eyes:"/>
<AlertContent className="justify-between flex-row items-center">
  <div>Vous voulez en savoir plus ?</div>
  <ButtonLink href="/guides/">
    Consultez nos autres guides
  </ButtonLink>
</AlertContent>
</Alert>

## Questions fréquemment posées {#frequently-asked-questions}

### Et si j'ai des fonds sur une plateforme d'échange ? {#what-if-i-have-funds-on-an-exchange}

Il se pourrait que vous puissiez retirer vos fonds directement vers certains réseaux de seconde couche depuis une plateforme d'échange. Consultez la section « Passer à la couche 2 » de notre [page sur la couche 2](/layer-2/) pour plus d'informations.

### Puis-je revenir sur le réseau principal Ethereum après avoir transféré mes jetons vers une seconde couche 2 ? {#can-i-go-back-to-ethereum-mainnet-after-i-bridge-my-tokens-to-l2}

Oui, vous pouvez toujours rapatrier vos fonds vers le réseau principal en utilisant le même pont.
