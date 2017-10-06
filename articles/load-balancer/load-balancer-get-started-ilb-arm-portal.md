---
title: aaaCreate un bilanciamento del carico interno - portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico di gestione risorse utilizzando hello portale di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Creare un servizio di bilanciamento del carico interno in hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Introduzione alla creazione di un servizio di bilanciamento del carico interno tramite il portale di Azure

Utilizzare hello seguendo i passaggi toocreate un bilanciamento del carico interno dalla hello portale di Azure.

1. Aprire un browser, passare toohello [portale di Azure](http://portal.azure.com)e accedere con l'account di Azure.
2. Nel lato superiore sinistro di hello della schermata ciao, fare clic su **New** > **rete** > **bilanciamento del carico**.
3. In hello **Crea servizio di bilanciamento del carico** pannello, immettere un **nome** per il bilanciamento del carico.
4. In **Schema** fare clic su **Interno**.
5. Fare clic su **rete virtuale**, e quindi selezionare hello rete virtuale in cui si desidera toocreate bilanciamento del carico di hello.

   > [!NOTE]
   > Se non si desidera toouse la rete virtuale hello, verificare hello **percorso** utilizza servizio di bilanciamento del carico hello e modificarla di conseguenza.

6. Fare clic su **Subnet**, quindi selezionare subnet hello in cui si desidera toocreate bilanciamento del carico di hello.
7. In **assegnazione di indirizzi IP**, fare clic su **dinamica** o **statico**, a seconda se si desidera l'indirizzo IP hello per hello carico bilanciamento toobe fisso (statico) o meno.

   > [!NOTE]
   > Se si seleziona un indirizzo IP statico toouse, sarà necessario tooprovide un indirizzo di bilanciamento del carico hello.

8. In **gruppo di risorse** specificare hello nome di un nuovo gruppo di risorse di bilanciamento del carico hello, oppure fare clic su **selezionare esistente** e selezionare un gruppo di risorse esistente.
9. Fare clic su **Crea**.

## <a name="configure-load-balancing-rules"></a>Configurare le regole del servizio di bilanciamento del carico

Creazione del servizio di bilanciamento di carico dopo hello, passare tooconfigure risorsa del servizio di bilanciamento carico di toohello è.
È necessario tooconfigure prima un pool di indirizzi back-end e un probe prima di configurare una regola di bilanciamento del carico.

### <a name="step-1-configure-a-back-end-pool"></a>Passaggio 1: Configurare un pool back-end

1. Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.
2. In hello **impostazioni** pannello, fare clic su **pool back-end**.
3. In hello **pool di indirizzi back-end** pannello, fare clic su **Aggiungi**.
4. In hello **aggiungere pool back-end** pannello, immettere un **nome** per pool back-end hello e quindi fare clic su **OK**.

### <a name="step-2-configure-a-probe"></a>Passaggio 2: Configurare un probe

1. Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.
2. In hello **impostazioni** pannello, fare clic su **probe**.
3. In hello **probe** pannello, fare clic su **Aggiungi**.
4. In hello **Aggiungi probe** pannello, immettere un **nome** per il probe hello.
5. In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.
6. In **porta**, specificare hello porta toouse quando si accede a probe hello.
7. In **percorso** (per HTTP ricerche solo), specificare hello percorso toouse come un probe.
8. In **intervallo** specificare la frequenza con cui tooprobe hello dell'applicazione.
9. In **soglia non integra**, specificare il numero di tentativi devono avere esito negativo prima macchina virtuale back-end di hello è contrassegnato come danneggiato.
10. Fare clic su **OK** toocreate probe.

### <a name="step-3-configure-load-balancing-rules"></a>Passaggio 3: Configurare le regole del servizio di bilanciamento del carico

1. Nel portale di Azure hello, fare clic su **Sfoglia** > **bilanciamenti del carico**, quindi fare clic su bilanciamento del carico hello creato in precedenza.
2. In hello **impostazioni** pannello, fare clic su **regole di bilanciamento del carico**.
3. In hello **regole di bilanciamento del carico** pannello, fare clic su **Aggiungi**.
4. In hello **regola di bilanciamento del carico di Aggiungi** pannello, immettere un **nome** per regola hello.
5. In **Protocollo** selezionare **HTTP** per i siti Web o **TCP** per le altre applicazioni basate su TCP.
6. In **porta**, specificare hello porta client si connettono tooin bilanciamento del carico di hello.
7. In **porta back-end**, specificare hello porta toobe utilizzati nel pool back-end hello (in genere, la porta del servizio di bilanciamento carico di hello e la porta back-end hello sono hello stesso).
8. In **pool back-end**, selezionare il pool back-end hello creato in precedenza.
9. In **persistenza della sessione**, selezionare il metodo toopersist sessioni.
10. In **il timeout di inattività (minuti)**, specificare il timeout di inattività hello.
11. In **IP mobile (Direct Server Return)** fare clic su **Disabilitato** o **Abilitato**.
12. Fare clic su **OK**.

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

