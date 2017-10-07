---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Gestione risorse: Azure | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Creare e modificare i peering per un circuito ExpressRoute

In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello utilizzando hello portale di Azure. È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute. Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:


## <a name="configuration-prerequisites"></a>Prerequisiti di configurazione

* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere. Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per si toobe toorun in grado di hello cmdlet nelle sezioni successive di hello.
* Se si intende toouse un hash di chiave/MD5 condiviso, scegliere toouse che questo su entrambi i lati dell'hello tunnel e limite hello del numero massimo di caratteri tooa pari a 25.

Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito una VPN IP, come MPLS), il provider di connettività configura e gestisce il routing per conto dell'utente. 

> [!IMPORTANT]
> È attualmente non inviano annunci peering configurato dai provider di servizi tramite il portale di Gestione servizi hello. L'abilitazione di questa funzionalità sarà presto disponibile. Rivolgersi al provider di servizi prima di configurare peering BGP.
> 
> 

Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft). È possibile configurare i peering nell'ordine desiderato. Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.

## <a name="azure-private-peering"></a>Peering privato di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate peering privato di Azure

1. Configurare il circuito ExpressRoute hello. Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurare peering privato di Azure per il circuito hello. Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:

  * / 30 subnet per collegamento primario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * / 30 subnet per collegamento secondario hello. subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte. È possibile usare il numero AS privato per questo peering. Assicurarsi di non usare il numero 65515.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.
3. Selezionare il peering privato di Azure, riga di hello, come illustrato nell'esempio seguente hello:

  ![Privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Configurare il peering privato. Hello immagine seguente viene illustrato un esempio di configurazione:

  ![Configurare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Salvare la configurazione di hello dopo aver specificato tutti i parametri. Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello esempio seguente:

  ![Salvare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview dettagli di peering privato di Azure

È possibile visualizzare le proprietà di hello di peering privato di Azure selezionando hello peering.

![Visualizzare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>configurazione di peering privato Azure tooupdate

È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.

![Aggiornare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete peering privato di Azure

È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nella seguente immagine hello:

![Eliminare il peering privato](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Peering pubblico di Azure

In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate peering pubblico di Azure

1. Configurare il circuito ExpressRoute. Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare ulteriormente.

  ![Elencare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurare peering pubblico di Azure per il circuito hello. Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:

  * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido.
  * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.
3. Selezionare hello Azure riga peering pubblico, come mostrato nella seguente immagine hello:

  ![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Configurare il peering pubblico. Hello immagine seguente viene illustrato un esempio di configurazione:

  ![Configurare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Salvare la configurazione di hello dopo aver specificato tutti i parametri. Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello esempio seguente:

  ![Salvare la configurazione del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview dettagli di peering pubblico di Azure

È possibile visualizzare le proprietà di hello di peering pubblico di Azure selezionando hello peering.

![Visualizzare le proprietà del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>configurazione di peering pubblico Azure tooupdate

È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.

![Selezionare la riga del peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete peering pubblico di Azure

È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nell'esempio seguente hello:

![Eliminare il peering pubblico](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Peering Microsoft

In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.

> [!IMPORTANT]
> Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route. Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito. Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate peering Microsoft

1. Configurare il circuito ExpressRoute. Verificare che il circuito hello è stato effettuato il provisioning dal provider di connettività hello prima di continuare ulteriormente.

  ![Elencare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurare Microsoft peering per il circuito hello. Assicurarsi di aver hello le seguenti informazioni prima di procedere.

  * / 30 subnet per collegamento primario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
  * / 30 subnet per collegamento secondario hello. Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.
  * Un esempio di ID VLAN valido tooestablish il peer. Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.
  * Numero AS per il peering. È possibile usare numeri AS a 2 e a 4 byte.
  * I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello. Sono accettati solo prefissi di indirizzi IP pubblici. Se si prevede un set di prefissi toosend, è possibile inviare un elenco delimitato da virgole. I prefissi devono essere registrati tooyou in un RIR / IRR.
  * **Facoltativo:** cliente ASN: nel caso di annunci con prefissi non registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich sono registrati.
  * Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.
  * **Facoltativo:** un hash MD5 se si sceglie toouse uno.
3. È possibile selezionare hello peering desiderato tooconfigure, come illustrato nella seguente hello esempio. Selezionare una riga di peering Microsoft hello.

  ![Selezionare la riga del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Configurare il peering Microsoft. Hello immagine seguente viene illustrato un esempio di configurazione:

  ![Configurare il peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Salvare la configurazione di hello dopo aver specificato tutti i parametri.

  Se il circuito Ottiene tooa 'Convalida necessaria' stato (come illustrato nell'immagine hello), è necessario aprire una prova di proprietà del team di supporto di hello prefissi tooour tooshow di supporto ticket.

  ![Salvare la configurazione del peering Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  È possibile aprire un ticket di supporto direttamente dal portale di hello, come illustrato nell'esempio seguente hello:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Dopo la configurazione di hello è stata accettata correttamente, è visualizzato un codice simile toohello seguente immagine:

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>dettagli di peering Microsoft tooview

È possibile visualizzare le proprietà di hello di peering pubblico di Azure selezionando hello peering.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>configurazione di peering Microsoft tooupdate

È possibile selezionare la riga hello per il peering e modificare le proprietà di peering hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>toodelete peering Microsoft

È possibile rimuovere la configurazione di peering selezionando l'icona di eliminazione hello, come illustrato nella seguente immagine hello:

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Passaggi successivi

Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-portal-resource-manager.md)
* Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).
* Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)
* Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).
