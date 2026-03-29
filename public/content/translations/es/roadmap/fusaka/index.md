---
title: Fulu-Osaka (Fusaka)
description: "Conozca mejor la actualización del protocolo Fusaka"
lang: es
---

# Fusaka <Emoji text="🦓" /> {#fusaka}

**La tan esperada actualización Fusaka de Ethereum se puso en marcha el 3 de diciembre de 2025**

La actualización de la red Fusaka llega después de [Pectra](/roadmap/pectra/) e incorpora nuevas funciones y mejora la experiencia de todos los usuarios y desarrolladores de Ethereum. El nombre combina la actualización de la capa de ejecución Osaka y la versión de la capa de consenso, que lleva el nombre de la estrella Fulu. Ambas partes de Ethereum reciben una actualización que impulsa la escalabilidad, la seguridad y la experiencia de usuario hacia el futuro de Ethereum.

<Alert variant="update">
<AlertContent>
<AlertDescription>
La actualización de Fusaka es solo un paso en los objetivos de desarrollo a largo plazo de Ethereum. Más información sobre [la hoja de ruta del protocolo](/roadmap/) y [las actualizaciones anteriores](/ethereum-forks/).
</AlertDescription>
</AlertContent>
</Alert>

## Mejoras de Fusaka {#improvements-in-fusaka}

### Escalar blobs {#scale-blobs}

#### PeerDAS {#peerdas}

Este es el _principal atractivo_ de la bifurcación Fusaka, la característica principal añadida en esta actualización. La capa 2 publica actualmente sus datos en Ehtereum usando blobs, un tipo de dato efímero creado específicamente para la capa 2. Antes de Fusaka, cada nodo completo tenía que almacenar todos los blobs para asegurase que los datos existían. A medida que aumenta el rendimiento de los blobs, tener que descargar todos estos datos se vuelve insostenible en cuanto a recursos.

Con el [muestreo de disponibilidad de datos](https://notes.ethereum.org/@fradamt/das-fork-choice), en lugar de tener que almacenar todos los datos de los blobs, cada nodo será responsable de una parte del total. Los blobs se distribuyen de forma uniforme y aleatoria entre los nodos de la red, y cada nodo completo solo almacena una octava parte de los datos, lo que permite, en teoría, escalar hasta 8 veces más. Para garantizar la disponibilidad de los datos, cualquier porción de los datos puede reconstruirse a partir de cualquier 50 % existente del total con métodos que reducen la probabilidad de que los datos sean incorrectos o falten a un nivel criptográficamente insignificante (~uno de cada 10<sup>20</sup> a uno de cada 10<sup>24</sup>).

Esto mantiene unos requisitos de hardware y ancho de banda asumibles para los nodos, mientras permite escalar los blobs, lo que se traduce en más capacidad y comisiones bajas para la capa 2.

[Más información sobre PeerDAS](/roadmap/fusaka/peerdas/)

**Recursos**:

- [Especificación técnica del EIP-7594](https://eips.ethereum.org/EIPS/eip-7594)
- [DappLion sobre PeerDAS: Escalando Ethereum hoy | ETHSofia 2024](https://youtu.be/bONWd1x2TjQ?t=328)
- [Académico: una documentación del PeerDAS de Ethereum (PDF)](https://eprint.iacr.org/2024/1362.pdf)

#### Bifurcaciones solo de parámetros de blob {#blob-parameter-only-forks}

Las capas 2 escalan Ethereum: a medida que sus redes crecen, necesitan publicar más datos en Ethereum. Esto significa que Ethereum tendrá que aumentar el número de blobs disponibles para ellas con el tiempo. Aunque PeerDAS permite escalar los datos de blobs, es algo que debe hacerse de forma gradual y segura.

Debido a que Ethereum es un código que se ejecuta en miles de nodos independientes que requieren un acuerdo sobre las mismas reglas, no podemos simplemente introducir cambios como aumentar el recuento de blobs de la misma manera que se implementa una actualización de un sitio web. Cualquier cambio en las reglas debe hacerse mediante una actualización coordinada, en la que todos los nodos, clientes y actualizaciones del software del validador antes de un mismo bloque predeterminado.

Estas actualizaciones coordinadas generalmente suelen incluir muchos cambios, requieren muchas pruebas y eso lleva tiempo. Para poder adaptarse más rápido a las necesidades cambiantes de los blobs en las capas 2, las bifurcaciones que solo modifican parámetros de blobs permiten aumentar su cantidad sin esperar a una actualización mayor.

Los clientes pueden configurar las bifurcaciones que solo modifican parámetros de blobs, de forma similar a otros ajustes como el límite de gas. Entre actualizaciones extensas de Ethereum, los clientes pueden acordar aumentar los valores «target» y «max» de blobs, por ejemplo, a 9 y 12, y luego los operadores de nodos actualizan su software para participar en esa pequeña bifurcación. Las bifurcaciones que solo modifican parámetros de blobs se pueden configurar en cualquier momento.

Cuando se añadieron los blobs a la red por primera vez en la actualización Dencun, el objetivo era de 3. Ese número aumentó a 6 en Pectra y, después de Fusaka, ahora puede aumentarse a un ritmo sostenible independientemente de estas importantes actualizaciones de la red.

![Gráfico que muestra el recuento promedio de blobs por bloque y los objetivos crecientes con las actualizaciones](./average-blob-count-per-block.webp)

Fuente del gráfico: [Ethereum Blobs - @hildobby, Dune Analytics](https://dune.com/hildobby/blobs)

**Recursos**: [Especificación técnica del EIP-7892](https://eips.ethereum.org/EIPS/eip-7892)

#### Blobs basados en comisiones limitados por los costes de ejecución {#blob-base-fee-bounded-by-execution-costs}

Las capas 2 pagan dos facturas al publicar datos: la comisión por blob y el gas de ejecución necesario para verificar esos blobs. Si el gas de ejecución domina, la subasta de la comisión por blob puede caer hasta 1 wei y dejar de ser una señal de precio.

EIP-7918 fija un precio mínimo proporcional para cada blob. Cuando la reserva es superior a la comisión base nominal de los blobs, el algoritmo de ajuste de comisiones trata el bloque como si superara el objetivo, deja de bajar la comisión y permite que aumente con normalidad. Como resultado:

- el mercado de comisiones por blobs siempre reacciona al embotellamiento
- Las capas 2 pagan como mínimo una parte significativa del cómputo que imponen a los nodos
- los picos en la comisión base de la capa de ejecución ya no pueden dejar la comisión por blob atrapada en 1 wei

**Recursos**:

- [Especificación técnica del EIP-7918](https://eips.ethereum.org/EIPS/eip-7918)
- [Explicación de Storybook](https://notes.ethereum.org/@anderselowsson/AIG)

### Escalar la L1 {#scale-l1}

#### Caducidad del historial y recibos más sencillos {#history-expiry}

En julio de 2025, los clientes de ejecución de Ethereum [comenzaron a admitir la caducidad parcial del historial](https://blog.ethereum.org/2025/07/08/partial-history-exp). Esto eliminó el historial anterior a [la Fusión](https://ethereum.org/roadmap/merge/) para reducir el espacio en disco que necesitan los operadores de nodos a medida que Ethereum sigue creciendo.

Este EIP se encuentra en una sección aparte de los "EIP del núcleo" porque la bifurcación no implementa ningún cambio en realidad; es un aviso de que los equipos de clientes deben admitir la caducidad del historial para la actualización de Fusaka. En la práctica, los clientes pueden implementarlo en cualquier momento, pero añadirlo a la actualización lo incluyó de forma concreta en su lista de tareas pendientes y les permitió probar los cambios de Fusaka junto con esta característica.

**Recursos**: [Especificación técnica del EIP-7642](https://eips.ethereum.org/EIPS/eip-7642)

#### Establecer límites superiores para MODEXP {#set-upper-bounds-for-modexp}

Hasta ahora, la MODEXP precompilada aceptaba números de prácticamente cualquier tamaño. Eso hacía que fuera difícil de comprobar, fácil de abusar y un riesgo para la estabilidad de los clientes. EIP-7823 establece un límite claro: cada número de entrada puede tener como máximo 8192 bits (1024 bytes) de longitud. Cualquier valor que supere ese límite será rechazado, se consumirá el gas de la transacción y no se producirá ningún cambio de estado. Cubre de sobra las necesidades del mundo real, eliminando los casos extremos que complicaban la planificación de límite de gas y las revisiones de seguridad. Este cambio proporciona mayor seguridad y protección contra ataques DoS sin interferir en la experiencia de usuarios ni desarrolladores.

**Recursos**: [Especificación técnica del EIP-7823](https://eips.ethereum.org/EIPS/eip-7823)

#### Límite de gas por transacción {#transaction-gas-limit-cap}

EIP-[7825](https://eips.ethereum.org/EIPS/eip-7825) introduce un límite máximo de 16.777.216 (2^24) de gas por transacción. Es una medida proactiva de refuerzo contra ataques DoS, que pone un límite al peor caso posible de coste por transacción individual a medida que se aumenta el límite de gas por bloque. Facilita la validación y la propagación, lo que permite modelarlas mejor para abordar la escalabilidad aumentando el límite de gas.

¿Por qué exactamente 2^24 en gas? Es una cifra cómodamente inferior que el límite de gas actual, lo bastante grande para desplegar contratos reales y ejecutar precompilaciones de envergadura, y al tener una potencia de 2, es fácil de implementar en todos los clientes. Este nuevo tamaño máximo de transacción es similar al tamaño medio de bloque anterior a Pectra, lo que lo convierte en un límite razonable para cualquier operación en Ethereum.

**Recursos**: [Especificación técnica del EIP-7825](https://eips.ethereum.org/EIPS/eip-7825)

#### Aumento del coste de gas de `MODEXP` {#modexp-gas-cost-increase}

MODEXP es una función precompilada integrada que realiza potenciación modular, un tipo de cálculo de grandes cifras utilizado en la verificación de firmas RSA y en sistemas de pruebas. Permite que los contratos ejecuten estos cálculos directamente, sin tener que implementarlos por su cuenta.

Los equipos de desarrollo y de cliente identificaron MODEXP como un gran obstáculo para aumentar el límite de gas por bloque, ya que el precio de gas actual suele subestimar la cantidad de potencia de cómputo que requieren ciertas entradas. Esto significa que una sola transacción que use MODEXP podría consumir la mayor parte del tiempo necesario para procesar un bloque entero, ralentizando la red.

Este EIP cambia el precio para que coincida con los costes computacionales reales de la siguiente manera:

- el aumento del cargo mínimo de 200 a 500 unidades de gas y la eliminación del descuento de un tercio introducido por EIP-2565 en el cálculo general del coste
- incrementar el coste de forma más pronunciada cuando la entrada del exponente es muy larga. si el exponente (la "potencia" del número que se pasa como segundo argumento) supera los 32 bytes / 256 bits, el coste de gas aumenta mucho más rápido por cada byte adicional
- el cobro de un coste adicional también cuando la base o el módulo sean grandes. Las otras dos cifras (la base y el módulo) tienen al menos 32 bytes; si alguna de ellas es más grande, el coste aumenta en proporcion a su tamaño

Al ajustar mejor los costes al tiempo de procesamiento real, MODEXP ya no puede hacer que un bloque tarde demasiado en validarse. Este cambio es uno de varios pensados para hacer seguro un posible aumento del límite de gas por bloque en Ethereum en el futuro.

**Recursos**: [Especificación técnica del EIP-7883](https://eips.ethereum.org/EIPS/eip-7883)

#### Límite de tamaño de bloque de ejecución en RLP {#rlp-execution-block-size-limit}

Esto crea un límite máximo sobre el tamaño que puede tener un bloque: este es un límite sobre lo que se _envía_ por la red y es independiente del límite de gas, que limita el _trabajo_ dentro de un bloque. El límite de tamaño del bloque es de 10 MiB, con un pequeño margen (2 MiB) reservado para los datos de consenso para que todo encaje y se propague limpiamente. Si un bloque es más grande que eso, los clientes lo rechazan.
Esto es necesario porque los bloques muy grandes tardan más en propagarse y verificarse en toda la red, y pueden crear problemas de consenso o ser utilizados como un vector de DoS. Además, el protocolo de cotilleo (gossip) de la capa de consenso ya no reenvía bloques de más de ~10 MiB, por lo que alinear la capa de ejecución con ese límite evita situaciones extrañas de «visto por algunos, descartado por otros».

En detalle: se trata de un límite para el tamaño del bloque de ejecución codificado con [RLP](/developers/docs/data-structures-and-encoding/rlp/). 10 MiB en total, con un margen de seguridad de 2 MiB reservado para el entramado del bloque de baliza. En la práctica, los clientes definen

`MAX_BLOCK_SIZE = 10,485,760` bytes y

`SAFETY_MARGIN = 2,097,152` bytes,

y rechazan cualquier bloque de ejecución cuya carga útil RLP exceda

`MAX_RLP_BLOCK_SIZE = MAX_BLOCK_SIZE − SAFETY_MARGIN`

El objetivo es limitar el tiempo de propagación/validación en el peor de los casos y alinearse con el comportamiento del protocolo de cotilleo (gossip) de la capa de consenso, reduciendo el riesgo de reorganización/DoS sin cambiar la contabilidad del gas.

**Recursos**: [Especificación técnica del EIP-7934](https://eips.ethereum.org/EIPS/eip-7934)

#### Establecer el límite de gas predeterminado en 60 millones {#set-default-gas-limit-to-60-million}

Antes de aumentar el límite de gas de 30M a 36M en febrero de 2025 (y posteriormente a 45M), este valor no había cambiado desde la Fusión (septiembre de 2022). Esta EIP tiene como objetivo dar prioirdad a una escalabilidad constante.

EIP-7935 coordina a los equipos de clientes de la capa de ejecución para aumentar el límite de gas por defecto por encima de los 45M actuales como parte de Fusaka. Es una EIP informativa, pero pide explícitamente a los clientes que prueben límtes más altos en redes de desarrollo, que lleguen a un valor seguro en común y lo incluyan en sus versiones de Fusaka.

La planificación en Devnet apunta a un estrés de ~60M (bloques completos con carga sintética) y aumentos iterativos; según la investigación, las patologías de tamaño de bloque en el peor caso no deberían imponer límites por debajo de ~150M. El despliegue debería ir acompañado del límite de gas por transacción (EIP-7825), para que ninguna transacción individual pueda dominar a medida que aumentan los límites.

**Recursos**: [Especificación técnica del EIP-7935](https://eips.ethereum.org/EIPS/eip-7935)

### Mejorar la experiencia de usuario {#improve-ux}

#### Anticipación determinista del proponente {#deterministic-proposer-lookahead}

Con EIP-7917, la cadena de baliza tendrá conocimiento anticipado de los proponentes de bloques para la próxima época. Tener una visión determinista de qué validadores propondrán los próximos bloques permite habilitar [preconfirmaciones](https://ethresear.ch/t/based-preconfirmations/17353): un compromiso con el proponente entrante que garantiza que la transacción del usuario se incluya en su bloque sin necesidad de esperar al bloque real.

Esta funcionalidad beneficia tanto a las implementaciones de clientes como a la seguridad de la red, ya que evita casos extremos en los que los validadores prodrían manipular el calendario de proponentes. La anticipación también permite una implementación menos compleja.

**Recursos**: [Especificación técnica del EIP-7917](https://eips.ethereum.org/EIPS/eip-7917)

#### Código operativo CLZ (que cuenta los ceros iniciales) {#count-leading-zeros-opcode}

Esta característica añade una pequeña instrucción de la EVM, **contar ceros a la izquierda (CLZ)**. Casi todo en la EVM se representa como un valor de 256 bits; este nuevo código de operación devuelve cuántos bits cero hay al principio. Es una funcionalidad común en muchas arquitecturas de conjuntos de instrucciones, ya que permite realizar operaciones aritméticas de forma más eficiente. En la práctica, esto reemplaza los escaneos de bits hechos a mano que se usan hoy en día por una sola instrucción, lo que simplifica y abarata tareas como encontrar el primer bit, escanear bytes o analizar campos de bits. El código de operación tiene un coste bajo y fijo, y se ha comprobado que su rendimiento es comparable al de una suma básica, lo que reduce el código de bytes y ahorra gas para realizar el mismo trabajo.

**Recursos**: [Especificación técnica del EIP-7939](https://eips.ethereum.org/EIPS/eip-7939)

#### Precompilado para admitir la curva secp256r1 {#secp256r1-precompile}

Introduce un verificador de firmas secp256r1 (P-256) integrado, de tipo passkey, en la dirección fija `0x100`, utilizando el mismo formato de llamada ya adoptado por muchas L2 y corrigiendo casos excepcionales, de modo que los contratos escritos para esos entornos funcionen en la L1 sin cambios.

¡Mejora de la experiencia de usuario! Para los usuarios, esto habilita la firma nativa del dispositivo y las passkeys. Las carteras pueden acceder directamente a Apple Secure Enclave, Android Keystore, los módulos de seguridad de hardware (HSM) y FIDO2/WebAuthn, sin frase semilla, con una incorporación más fluida y flujos multifactor que se sienten como aplicaciones modernas. Esto da como resultado una mejor experiencia de usuario, una recuperación más fácil y patrones de abstracción de cuentas que coinciden con lo que ya hacen miles de millones de dispositivos.

Para los desarrolladores, toma una entrada de 160 bytes y devuelve una salida de 32 bytes, lo que facilita la portabilidad de las bibliotecas existentes y los contratos de L2. Internamente, incluye comprobaciones de punto en el infinito y de comparación modular para eliminar casos excepcionales complicados sin romper los llamadores válidos.

**Recursos**:

- [Especificación técnica del EIP-7951](https://eips.ethereum.org/EIPS/eip-7951)
- [Más sobre RIP-7212](https://www.alchemy.com/blog/what-is-rip-7212) _(Tenga en cuenta que el EIP-7951 sustituyó al RIP-7212)_

### Meta {#meta}

#### Método JSON-RPC `eth_config` {#eth-config}

Esta es una llamada JSON-RPC que le permite preguntar a su nodo qué configuración de bifurcación está ejecutando. Devuelve tres instantáneas: `current`, `next` y `last`, para que los validadores y las herramientas de supervisión puedan verificar que los clientes están preparados para una próxima bifurcación.

En la práctica, esto es para abordar una deficiencia descubierta cuando la bifurcación Pectra se puso en marcha en la red de pruebas Holesky a principios de 2025 con errores de configuración menores que resultaron en un estado de no finalización. Esto ayuda a los equipos de pruebas y a los desarrolladores a garantizar que las bifurcaciones principales se comportarán como se espera al pasar de las redes de desarrollo a las redes de prueba, y de las redes de prueba a la red principal.

Las instantáneas incluyen: `chainId`, `forkId`, la hora de activación de la bifurcación planificada, qué precompilados están activos, las direcciones de los precompilados, las dependencias de los contratos del sistema y el programa de blobs de la bifurcación.

Este EIP se encuentra en una sección aparte de los "EIP del núcleo" porque la bifurcación no implementa ningún cambio en realidad; es un aviso de que los equipos de clientes deben implementar este método JSON-RPC para la actualización de Fusaka.

**Recursos**: [Especificación técnica del EIP-7910](https://eips.ethereum.org/EIPS/eip-7910)

## Preguntas frecuentes {#faq}

### ¿Afecta esta actualización a todos los nodos y validadores de Ethereum? {#does-this-upgrade-affect-all-ethereum-nodes-and-validators}

Sí, la actualización Fusaka requiere actualizar [los clientes de ejecución y los clientes de consenso](/developers/docs/nodes-and-clients/). Todos los principales clientes de Ethereum lanzarán versiones compatibles con la bifurcación dura marcada como alta prioridad. Puede estar al tanto de cuándo estarán disponibles estas versiones en los repositorios de GitHub de los clientes, en sus [canales de Discord](https://ethstaker.org/support), en el [Discord EthStaker](https://dsc.gg/ethstaker), o suscribiéndose al blog de Ethereum para recibir actualizaciones del protocolo. Para mantener la sincronización con la red de Ethereum posactualización, los operadores de nodos deben asegurarse de que están ejecutando una versión de cliente compatible. Tenga en cuenta que la información sobre las versiones de los clientes es sensible al tiempo, y los usuarios deben consultar las últimas actualizaciones para obtener los últimos detalles.

### ¿Cómo se puede convertir ETH después de la bifurcación dura? {#how-can-eth-be-converted-after-the-hardfork}

- **No se requiere ninguna acción para sus ETH**: después de la actualización Fusaka de Ethereum, no hay necesidad de convertir o actualizar sus ETH. Los saldos de su cuenta seguirán siendo los mismos, y el ETH que tiene actualmente seguirá siendo accesible en su forma existente después de la bifurcación dura.
- **¡Cuídese de fraudes!** <Emoji text="⚠️" /> **Cualquiera que le indique que "actualice" su ETH está tratando de estafarlo.** No hay nada que tenga que hacer en relación con esta actualización. Sus activos no se verán afectados en absoluto. Recuerde, mantenerse informado es la mejor defensa contra las estafas.

[Más sobre el reconocimiento y la prevención de estafas](/security/)

### ¿A qué vienen las cebras? <Emoji text="🦓" /> {#whats-with-the-zebras}

Una cebra es la «mascota» elegida por los desarrolladores de Fusaka porque sus rayas reflejan el muestreo de disponibilidad de datos basado en columnas de PeerDAS, donde los nodos custodian ciertas subredes de columnas y muestrean algunas otras columnas de cada ranura de pares para comprobar que los datos de los blobs están disponibles.

La Fusión en 2022 [utilizó un panda](https://x.com/hwwonx/status/1431970802040127498) como mascota para señalar la unión de las capas de ejecución y de consenso. Desde entonces, se han elegido mascotas de manera informal para cada bifurcación y aparecen como arte ASCII en los registros del cliente en el momento de la actualización. Es solo una forma divertida de celebrarlo.

### ¿Qué mejoras se incluyen para el escalado de la L2? {#what-improvements-are-included-for-l2-scaling}

[PeerDAS](/roadmap/fusaka/peerdas) es la característica principal de la bifurcación. Implementa el muestreo de disponibilidad de datos (DAS) que desbloquea más escalabilidad para los rollups, escalando teóricamente el espacio de blobs hasta 8 veces el tamaño actual. El mercado de comisiones de blobs también se mejorará para reaccionar eficientemente a la congestión y garantizar que las L2 paguen una comisión significativa por el cómputo y el espacio que los blobs imponen a los nodos.

### ¿En qué se diferencian las bifurcaciones BPO? {#how-are-bpo-forks-different}

Las bifurcaciones solo de parámetros de blob proporcionan un mecanismo para aumentar continuamente el recuento de blobs (tanto el objetivo como el máximo) después de que se active PeerDAS, sin tener que esperar a una actualización coordinada completa. Cada aumento está codificado para ser preconfigurado en las versiones de cliente que admiten Fusaka.

Como usuario o validador, no necesita actualizar sus clientes para cada BPO y solo debe asegurarse de seguir las bifurcaciones duras principales como Fusaka. Esta es la misma práctica que antes, no se necesitan acciones especiales. Se sigue recomendando supervisar sus clientes en torno a las actualizaciones y BPO y mantenerlos actualizados incluso entre las versiones principales, ya que las correcciones u optimizaciones pueden seguir a la bifurcación dura.

### ¿Cuál es el calendario de las BPO? {#what-is-the-bpo-schedule}

El calendario exacto de las actualizaciones de las BPO se determinará con las versiones de Fusaka. Siga los [Anuncios del protocolo](https://blog.ethereum.org/category/protocol) y las notas de la versión de sus clientes.

Ejemplo de cómo podría ser:

- Antes de Fusaka: objetivo 6, máx. 9
- En la activación de Fusaka: objetivo 6, máx. 9
- BPO1, unas semanas después de la activación de Fusaka: objetivo 10, máx. 15, aumentando en dos tercios
- BPO2, unas semanas después de BPO1: objetivo 14, máx. 21

### ¿Reducirá esto las comisiones en Ethereum (capa 1)? {#will-this-lower-gas}

Esta actualización no reduce las comisiones de gas en la L1, al menos no directamente. El objetivo principal es tener más espacio de blobs para los datos de los rollups y, por lo tanto, reducir las comisiones en la capa 2. Esto podría tener algunos efectos secundarios en el mercado de comisiones de la L1, pero no se espera ningún cambio significativo.

### Como staker, ¿qué tengo que hacer para la actualización? {#as-a-staker-what-do-i-need-to-do-for-the-upgrade}

Al igual que con cada actualización de la red, asegúrese de actualizar sus clientes a las últimas versiones marcadas con soporte para Fusaka. Siga las actualizaciones en la lista de correo y los [Anuncios del protocolo en el blog de la EF](https://blog.ethereum.org/category/protocol) para informarse sobre las versiones.
Para validar su configuración antes de que Fusaka se active en la red principal, puede ejecutar un validador en las redes de prueba. Fusaka [se activa antes en las redes de prueba](https://blog.ethereum.org/2025/09/26/fusaka-testnet-announcement), lo que le da más margen para asegurarse de que todo funciona y para informar de errores. Las bifurcaciones de la red de prueba también se anuncian en la lista de correo y en el blog.

### ¿Afecta a los validadores la «visión anticipada determinista del proponente» (EIP-7917)? {#does-7917-affect-validators}

Este cambio no modifica el funcionamiento de su cliente validador; sin embargo, proporcionará más información sobre el futuro de sus deberes como validador. Asegúrese de actualizar sus herramientas de supervisión para mantenerse al día con las nuevas características.

### ¿Cómo afecta Fusaka a los requisitos de ancho de banda para los nodos y validadores? {#how-does-fusaka-affect-bandwidth-requirements-for-nodes-and-validators}

PeerDAS supone un cambio significativo en la forma en que los nodos transmiten los datos de los blobs. Todos los datos se dividen en fragmentos llamados columnas a través de 128 subredes, y los nodos se suscriben solo a algunas de ellas. La cantidad de columnas de subred que los nodos tienen que custodiar depende de su configuración y del número de validadores conectados. Los requisitos reales de ancho de banda dependerán de la cantidad de blobs permitidos en la red y del tipo de nodo. En el momento de la activación de Fusaka, el objetivo de blobs se mantiene igual que antes, pero con PeerDAS, los operadores de nodos pueden ver una disminución en el uso de disco de los blobs y en el tráfico de red. A medida que las BPO configuren un mayor número de blobs en la red, el ancho de banda necesario aumentará con cada BPO.

Los requisitos de los nodos siguen estando dentro de los [márgenes recomendados](https://eips.ethereum.org/EIPS/eip-7870) incluso después de las BPO de Fusaka.

#### Nodos completos {#full-nodes}

Los nodos regulares sin validadores se suscribirán a solo 4 subredes, proporcionando custodia para 1/8 de los datos originales. Esto significa que, con la misma cantidad de datos de blob, el ancho de banda del nodo para descargarlos sería ocho (8) veces menor. El uso de disco y el ancho de banda de descarga de los blobs para un nodo completo normal podría disminuir alrededor del 80 %, a solo unos pocos Mb.

#### Stakers individuales {#solo-stakers}

Si el nodo se utiliza para un cliente validador, tiene que custodiar más columnas y, por lo tanto, procesar más datos. Con un validador añadido, el nodo se suscribe al menos a 8 subredes de columnas y, por lo tanto, procesa el doble de datos que un nodo regular, pero aun así menos que antes de Fusaka. Si el saldo del validador supera los 287 ETH, se suscribirá a cada vez más subredes.

Para un staker en solitario, esto significa que su uso de disco y ancho de banda de descarga disminuirán alrededor del 50 %. Sin embargo, para construir bloques localmente y subir todos los blobs a la red, se necesita más ancho de banda de subida. Los constructores locales necesitarán un ancho de banda de subida entre 2 y 3 veces mayor que antes en el momento de Fusaka y, con el objetivo de BPO2 de 15/21 blobs, el ancho de banda de subida final necesario tendrá que ser unas 5 veces mayor, a 100 Mbps.

#### Grandes validadores {#large-validators}

El número de subredes suscritas crece a medida que se añaden más saldo y validadores al nodo. Por ejemplo, con un saldo de alrededor de 800 ETH, el nodo custodia 25 columnas y necesitará alrededor de un 30 % más de ancho de banda de descarga que antes. La subida necesaria aumenta de forma similar a la de los nodos regulares y se necesitan al menos 100 Mbps.

Con 4096 ETH y 2 validadores de saldo máximo, el nodo se convierte en un «supernodo» que custodia todas las columnas, por lo que descarga y almacena todo. Estos nodos reparan activamente la red contribuyendo con los datos que faltan, pero también requieren mucho más ancho de banda y almacenamiento. Con el objetivo final de blobs siendo 6 veces mayor que antes, los supernodos tendrán que almacenar alrededor de 600 GB de datos de blobs adicionales y tener un ancho de banda de descarga sostenido más rápido de alrededor de 20 Mbps.

[Lea más detalles sobre los requisitos esperados.](https://ethpandaops.io/posts/fusaka-bandwidth-estimation/#theoretical-requirements)

### ¿Qué cambios se implementan en la EVM? {#what-evm-changes-are-implemented}

Fusaka consolida la EVM con nuevos cambios y características menores.

- Por seguridad durante el escalado, el tamaño máximo de una única transacción se [limitará a 16,7 millones](https://eips.ethereum.org/EIPS/eip-7825) de unidades de gas.
- Se añade a la EVM el [nuevo código de operación para contar ceros a la izquierda (CLZ)](https://eips.ethereum.org/EIPS/eip-7939) y permitirá que los lenguajes de contratos inteligentes realicen ciertas operaciones de manera más eficiente.
- [Aumentará el coste del precompilado `ModExp`](https://eips.ethereum.org/EIPS/eip-7883): los contratos que lo utilicen cobrarán más gas por la ejecución.

### ¿Cómo afecta el nuevo límite de gas de 16 M a los desarrolladores de contratos? {#how-does-new-16m-gas-limit-affects-contract-developers}

Fusaka introduce un límite al [tamaño máximo de una única transacción a 16,7 millones](https://eips.ethereum.org/EIPS/eip-7825) (2^24) de unidades de gas. Esto es aproximadamente el tamaño anterior de un bloque promedio, lo que lo hace lo suficientemente grande como para dar cabida a transacciones complejas que consumirían un bloque entero. Este límite crea una protección para los clientes, previniendo posibles ataques de DoS en el futuro con un límite de gas de bloque más alto. El objetivo del escalado es permitir que más transacciones entren en la cadena de bloques sin que una sola consuma todo el bloque.

Las transacciones de los usuarios habituales están lejos de alcanzar este límite. Ciertos casos extremos, como operaciones DeFi grandes y complejas, grandes implementaciones de contratos inteligentes o transacciones por lotes dirigidas a múltiples contratos, podrían verse afectados por este cambio. Estas transacciones tendrán que dividirse en otras más pequeñas u optimizarse de otra manera. Utilice la simulación antes de enviar transacciones que potencialmente alcancen el límite.

El método RPC `eth_call` no está limitado y permitirá la simulación de transacciones más grandes que el límite real de la cadena de bloques. El límite real para los métodos RPC puede ser configurado por el operador del cliente para prevenir abusos.

### ¿Qué significa CLZ para los desarrolladores? {#what-clz-means-for-developers}

Los compiladores de la EVM, como Solidity, implementarán y utilizarán internamente la nueva función para contar ceros. Los nuevos contratos podrían beneficiarse del ahorro de gas si dependen de este tipo de operación. Siga las versiones y los anuncios de características del lenguaje de contratos inteligentes para obtener documentación sobre los posibles ahorros.

### ¿Hay algún cambio para mis contratos inteligentes existentes? {#what-clz-means-for-developers-2}

Fusaka no tiene ningún efecto directo que rompa los contratos existentes o cambie su comportamiento. Los cambios introducidos en la capa de ejecución se realizan con retrocompatibilidad; sin embargo, siempre esté atento a los casos extremos y al posible impacto.

[Con el aumento del coste del precompilado `ModExp`](https://eips.ethereum.org/EIPS/eip-7883), los contratos que dependen de él consumirán más gas para la ejecución. Si su contrato depende en gran medida de esto y se vuelve más caro para los usuarios, reconsidere cómo se utiliza.

Considere el [nuevo límite de 16,7 millones](https://eips.ethereum.org/EIPS/eip-7825) si las transacciones que ejecutan sus contratos podrían alcanzar un tamaño similar.

## Lecturas adicionales {#further-reading}

- [Hoja de ruta de Ethereum](/roadmap/)
- [Forkcast: Fusaka](https://forkcast.org/upgrade/fusaka)
- [Fusaka Meta EIP](https://eips.ethereum.org/EIPS/eip-7607)
- [Anuncio en el blog de la red de pruebas de Fusaka](https://blog.ethereum.org/2025/09/26/fusaka-testnet-announcement)
- [Bankless: qué le aportarán a Ethereum Fusaka y Pectra](https://www.bankless.com/read/what-fusaka-pectra-will-bring-ethereum)
- [Bankless: las próximas actualizaciones de Ethereum: Fusaka, Glamsterdam y más, con Preston Van Loon](https://x.com/BanklessHQ/status/1956017743289020633?t=502)
- [Los archivos de Fusaka](https://www.youtube.com/playlist?list=PL4cwHXAawZxpz-erUbKKUnnGoQNdF8s7Z)
- [PEEPanEIPs Explicados](https://www.youtube.com/playlist?list=PL4cwHXAawZxoIenfk7OJry4rxcqX-eqBt)
