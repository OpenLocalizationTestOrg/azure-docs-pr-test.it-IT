---
title: bilanciamento del carico con una connessione Internet aaaCreate - portale di Azure classico | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico in modello di distribuzione classica utilizzando hello portale di Azure classico
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Introduzione alla creazione di un bilanciamento del carico (classico) nel portale di Azure classico hello per Internet

> [!div class="op_single_selector"]
> * [portale di Azure classico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servizi cloud di Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica. È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure. È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo. Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Configurazione del servizio di bilanciamento del carico Internet per le macchine virtuali

In ordine tooload bilanciare il traffico di rete da hello Internet tra macchine virtuali hello di un servizio cloud, è necessario creare un set con carico bilanciato. Questa procedura si presuppone che sia stato già creato le macchine virtuali hello e che siano tutti all'interno di hello stesso servizio cloud.

**tooconfigure un set con carico bilanciato per le macchine virtuali**

1. Nel portale di Azure classico hello, fare clic su **macchine virtuali**, quindi fare clic su nome hello di una macchina virtuale nel set di bilanciamento del carico hello.
2. Far clic su **Endpoint** e selezionare **Aggiungi**.
3. In hello **aggiungere una macchina virtuale di endpoint tooa** pagina, fare clic sulla freccia a destra di hello.
4. In hello **specificare hello i dettagli dell'endpoint hello** pagina:

   * In **nome**, digitare un nome per l'endpoint di hello o selezionare il nome di hello hello elenco degli endpoint predefiniti per i protocolli comuni.
   * In **protocollo**, selezionare il protocollo di hello richiesto dal tipo di hello dell'endpoint, TCP o UDP, in base alle esigenze.
   * In **porta pubblica e privata**, digitare i numeri di porta hello che si desidera hello toouse macchina virtuale, in base alle esigenze. È possibile utilizzare la porta privata hello e regole del firewall al traffico tooredirect hello macchina virtuale in modo appropriato per l'applicazione. porta privata Hello può essere hello come porta pubblica hello. Per un endpoint per il traffico web (HTTP), ad esempio, è Impossibile assegnare la porta 80 tooboth hello porta pubblica e privata.

5. Selezionare **creare un set con carico bilanciato**e quindi fare clic sulla freccia a destra di hello.
6. In hello **configurare il set di bilanciamento del carico hello** pagina, digitare un nome per il set di bilanciamento del carico hello e quindi assegnare valori hello per il comportamento di probe di bilanciamento del carico di Azure hello. Hello bilanciamento del carico utilizza probe toodetermine se hello di macchine virtuali nel set di bilanciamento del carico hello sono disponibili tooreceive il traffico in entrata.
7. Fare clic su endpoint con bilanciamento del carico toocreate hello di hello segno di spunta. Si noterà **Sì** in hello **nome set con carico bilanciato** colonna di hello **endpoint** pagina per la macchina virtuale hello.
8. Nel portale di hello, fare clic su **macchine virtuali**, fare clic sul nome di una macchina virtuale aggiuntiva nel set di bilanciamento del carico hello hello, fare clic su **endpoint**, quindi fare clic su **Aggiungi**.
9. In hello **aggiungere una macchina virtuale di endpoint tooa** pagina, fare clic su **aggiungere set di bilanciamento del carico esistente di endpoint tooan**, selezionare il nome del set di bilanciamento del carico hello hello e quindi fare clic sulla freccia a destra di hello.
10. In hello **specificare hello i dettagli dell'endpoint hello** pagina, digitare un nome per l'endpoint di hello e quindi fare clic su hello segno di spunta.

Per hello altre macchine virtuali nel set di bilanciamento del carico hello, ripetere i passaggi da 8 a 10.

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
