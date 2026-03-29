---
title: "Kripto fonlarınızın akıllı sözleşme erişimini nasıl iptal edebilirsiniz?"
description: "İstismarcı akıllı sözleşmenin token erişimini kaldırma üzerine bir rehber"
lang: tr
---

# Kripto fonlarınızın akıllı sözleşme erişimini nasıl iptal edebilirsiniz? {#how-to-revoke-smart-contract-access-to-your-crypto-funds}

Bu rehber, fonlarınıza erişim izni verdiğiniz [akıllı sözleşmeler](/glossary/#smart-contract) listesini nasıl görebileceğinize ve izinlerinizi nasıl iptal edebileceğinize dair size bilgi verir.

Bazen kötü amaçlı geliştiriciler akıllı sözleşmelere bu sözleşmelerle etkileşime geçen habersiz kullanıcıların fonlarına erişim sağlayacak arka kapılar eklerler. Genellikle bu tür platformlar, gelecekte küçük miktarlarda [gaz](/glossary/#gas) tasarrufu sağlamak amacıyla kullanıcıdan **sınırsız sayıda jeton** harcama izni ister ancak bu, artan riskleri de beraberinde getirir.

Bir platform [cüzdanınızdaki](/glossary/#wallet) bir jetona sınırsız erişim hakkına sahip olduğunda, platformdan fonlarınızı çekmiş olsanız bile o jetonların hepsini harcayabilir. Kötü amaçlı aktörler hâlâ fonlarınıza erişim sağlayabilir ve size kurtarma şansı vermeden kendi cüzdanlarına çekebilirler.

Buna karşı biricik korunma yolları test edilmemiş yeni projeleri kullanmaktan kaçınmak, sadece ihtiyacınız kadarına izin vermek veya düzenli olarak erişimi kaldırmaktır. Peki, bunu nasıl yaparsınız?

## 1. Adım: Erişim kaldırma araçları kullanın {#step-1-use-revoke-access-tools}

Bazı web siteleri adresinize bağlı akıllı sözleşmeleri görmenize ve kaldırmanıza olanak sağlar. Web sitesini ziyaret edin ve cüzdanınızı bağlayın:

- [Etherscan](https://etherscan.io/tokenapprovalchecker) (Ethereum)
- [Blockscout](https://eth.blockscout.com/essential-dapps/revoke) (Ethereum)
- [Revoke](https://revoke.cash/) (birden çok ağ)
- [Unrekt](https://app.unrekt.net/) (birden çok ağ)
- [EverRevoke](https://everrise.com/everrevoke/) (birden çok ağ)

## 2. Adım: Cüzdanınızı bağlayın {#step-2-connect-your-wallet}

Siteye girdiğiniz anda, "Connect wallet"(Cüzdanı bağla) üzerine tıklayın. Web sitesi sizi cüzdanı bağlamaya yönlendirmelidir.

Cüzdanınızda ve web sitesinde aynı ağı kullandığınızdan emin olun. Sadece seçili ağla ilişkili akıllı sözleşmeleri göreceksiniz. Örnek olarak, Ethereum Ana Ağı'na bağlanırsanız sadece Ethereum sözleşmeleri göreceksiniz, Polygon gibi diğer ağlardaki sözleşmeleri değil.

## 3. Adım: Kaldırmak istediğiniz bir akıllı sözleşme seçin {#step-3-select-a-smart-contract-you-wish-to-revoke}

Token'larınıza erişim izni olan tüm sözleşmeleri ve bunların harcama limitlerini görmelisiniz. Sonlandırmak istediğinizi bulun.

Hangi sözleşmeyi seçmek istediğinizi bilmiyorsanız, hepsini kaldırabilirsiniz. Sizin için herhangi bir sıkıntı yaratmaz, ancak bu sözleşmelerle etkileşime geçtiğiniz bir dahaki seferde yeni izinler vermeniz gerekecektir.

## 4. Adım: Fonlarınıza erişimi kaldırın {#step-4-revoke-access-to-your-funds}

Kaldırdığınızda, cüzdanınızda yeni bir işlem önerisi görmelisiniz. Bu beklenen bir durumdur. Kaldırmanın başarılı olması için ücreti ödemeniz gerekecektir. Ağa bağlı olarak bu işlem bir veya birkaç dakika arasında sürebilir.

Kaldırılmış sözleşmenin listeden gidip gitmediğini kontrol etmek için birkaç dakika sonra kaldırma aracını yenilemenizi öneririz.

<mark>Asla projelere jetonlarınıza sınırsız erişim vermemenizi ve tüm jeton izinlerini düzenli olarak kaldırmanızı öneririz. Jeton erişimini kaldırmak asla bir fon kaybına sebep olmamalı, özellikle de yukarıda listelenmiş araçları kullanırsanız.</mark>

<br />

<Alert variant="update">
<AlertEmoji text=":eyes:"/>
<AlertContent className="justify-between flex-row items-center">
  <div>Daha fazlasını mı öğrenmek istiyorsunuz?</div>
  <ButtonLink href="/guides/">
    Diğer rehberlerimizi inceleyin
  </ButtonLink>
</AlertContent>
</Alert>

## Sıkça sorulan sorular {#frequently-asked-questions}

### Token erişimini kaldırma ayrıca hisseleme, havuz oluşturma, borç verme işlemlerini de kaldırır mı? {#does-revoking-token-access-also-terminate-staking-pooling-lending-etc}

Hayır, hiçbir [DeFi](/glossary/#defi) stratejinizi etkilemez. Pozisyonlarınızda kalırsınız ve ödüller vb. elde etmeye devam edersiniz.

### Bir projeden cüzdanın bağlantısını kesmek fonlarımın kullanım izinlerini kaldırmakla aynı mıdır? {#is-disconnecting-a-wallet-from-a-project-the-same-as-removing-permission-to-use-my-funds}

Hayır, cüzdanınızın bağlantısını projeden kestiyseniz, ancak token izinleri verdiyseniz bunlar, bu token'ları kullanmata devam edebilir. Söz konusu erişimi kaldırmanız gerekir.

### Sözleşme izinleri ne zaman sona erer? {#when-will-the-contract-permission-expire}

Sözleşme izinleri için sona erme tarihi bulunmaz. Sözleşme izinleri verirseniz, verildiğinden yıllar sonrasında bile kullanılabilirler.

### Neden projeler sınırsız token izni ayarlarlar? {#why-do-projects-set-unlimited-token-allowance}

Projeler bunu genellikle gereken istek sayısını azaltmak için yaparlar, yani kullanıcı sadece bir defa izin verir ve işlem ücretini bir defa öder. Uygun olmasına rağmen, bu kullanıcıların zamanla yerleşmemiş veya denetlenmemiş sitelerde dikkatsizce izin vermesinden dolayı zararlı olabilir. Bazı cüzdanlar riskinizi sınırlamanız için izin verilen token miktarını sınırlamanıza imkân verir. Daha fazla bilgi için cüzdan sağlayıcınıza başvurun.
