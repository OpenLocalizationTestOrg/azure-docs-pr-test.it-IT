---
title: toodo aaaWhat nell'evento hello di un'interruzione del servizio Azure conseguenze per le reti virtuali di Azure | Documenti Microsoft
description: Informazioni su quali toodo nell'evento hello di un'interruzione del servizio Azure conseguenze per le reti virtuali di Azure.
services: virtual-network
documentationcenter: 
author: NarayanAnnamalai
manager: jefco
editor: 
ms.assetid: ad260ab9-d873-43b3-8896-f9a1db9858a5
ms.service: virtual-network
ms.workload: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: narayan;aglick
ms.openlocfilehash: db022d2a042d255cf8ec6afb68cd8436aeecfe08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network--business-continuity"></a>Rete virtuale - Continuità aziendale
## <a name="overview"></a>Panoramica
Una rete virtuale (VNet) è una rappresentazione logica della rete nel cloud hello. Consente di toodefine proprio hello privata di spazio e segmento dello indirizzo IP di rete in subnet. Le reti virtuali viene utilizzato come un toohost limiti di trust le risorse di calcolo come macchine virtuali di Azure e servizi Cloud (ruoli web/di lavoro). Una rete virtuale consente la comunicazione di IP privata diretta tra le risorse di hello ospitato in essa contenuti. Una rete virtuale può anche essere collegato tooan rete locale tramite una delle opzioni di hello ibrido, ad esempio un Gateway VPN o ExpressRoute.

Una rete virtuale viene creata nell'ambito di hello di un'area. È possibile creare reti virtuali allo stesso spazio di indirizzi in due aree diverse (ad esempio Stati Uniti orientali e Stati Uniti occidentali, ma non è possibile connettere tali elementi tooone direttamente un'altra). 

## <a name="business-continuity"></a>Continuità aziendale
Le applicazioni potrebbero essere soggette a interruzioni di varia natura. Una determinata regione potrebbe essere completamente troncata a causa di calamità naturali tooa o di un'emergenza parziale a causa di un errore tooa di più dispositivi e servizi. impatto di Hello sulle hello servizio di rete virtuale è diverso in ognuna di queste situazioni.

**D: in che modo nell'evento hello di un'intera regione tooan di interruzione? ad esempio se un'area è completamente cambio data a causa di calamità naturale tooa? Cosa accade toohello reti virtuali ospitate nell'area di hello?**

R: hello virtuale hello risorse di rete e in hello interessate area rimane accessibile durante la fase di hello di interruzioni del servizio hello.

![Diagramma della rete virtuale semplice](./media/virtual-network-disaster-recovery-guidance/vnet.png)

**D: che cosa è possibile toodo ricreare hello stessa rete virtuale in un'area diversa?**

R: La rete virtuale è una risorsa piuttosto semplice. È possibile richiamare l'API di Azure toocreate una rete virtuale con hello stesso spazio indirizzi in un'area diversa. toore-creare hello stesso ambiente che era presente nel hello interessate area, è necessario toomake API chiamate toore-distribuire i servizi Cloud (ruoli web/di lavoro) e le macchine virtuali era. Toospin sarà inoltre necessario configurare un Gateway VPN e la connessione di rete locale tooyour se si dispone di connettività locale (ad esempio una distribuzione ibrida).

Hello le istruzioni per la creazione di una rete virtuale sono disponibili [qui](virtual-networks-create-vnet-arm-pportal.md). 

**D: È possibile ricreare in anticipo una replica di una rete virtuale di una determinata area in un'altra area?**

R: Sì, è possibile creare due reti virtuali utilizzando hello spazio di indirizzi IP privati stesso e le risorse in due aree diverse nell'ora. Se un cliente ospitava servizi in hello rete virtuale è connessa a internet, potrebbe sono impostate area di gestione traffico toogeo route traffico toohello attivo. Tuttavia, un cliente non è possibile connettere due reti virtuali con hello stesso indirizzo rete locale tootheir di spazio in quanto causerebbe problemi di routing. In fase di hello un'emergenza e la perdita di una rete virtuale in un'unica area, è possibile connettersi un cliente hello altre reti virtuali nell'area di disponibili hello con rete locale di tootheir spazio di indirizzi corrispondente.

Hello le istruzioni per la creazione di una rete virtuale sono disponibili [qui](virtual-networks-create-vnet-arm-pportal.md).

