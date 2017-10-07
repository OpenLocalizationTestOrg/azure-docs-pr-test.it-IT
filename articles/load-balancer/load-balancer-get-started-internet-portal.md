---
title: bilanciamento del carico con una connessione Internet aaaCreate - portale di Azure | Documenti Microsoft
description: Informazioni su come bilanciamento del carico toocreate con una connessione Internet con Gestione risorse hello portale di Azure
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Creazione di un bilanciamento del carico con connessione Internet tramite hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modello](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione di gestione risorse di hello. È anche possibile [informazioni su come toocreate con una connessione Internet bilanciamento del carico utilizzando la distribuzione classica](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Questo articolo descrive la sequenza hello delle singole attività che hanno fatto toobe toocreate un bilanciamento del carico e illustrano in dettaglio cosa è stato fatto obiettivo hello tooaccomplish.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Che cos'è obbligatorio toocreate un bilanciamento del carico con connessione Internet?

È necessario toocreate e configurare hello seguenti oggetti toodeploy un bilanciamento del carico.

* Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.
* Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.
* Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.
* Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.
* Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.

È possibile ottenere altre informazioni sui componenti del servizio di bilanciamento del carico con Azure Resource Manager in [Supporto di Azure Resource Manager per il bilanciamento del carico](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Configurare un servizio di bilanciamento del carico nel portale di Azure

> [!IMPORTANT]
> L'esempio presuppone che ci sia una rete virtuale denominata **myVNet**. Fare riferimento troppo[crea rete virtuale](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo questo. Presuppone anche se è presente una subnet all'interno di **myVNet** chiamato **LB Subnet essere** e due macchine virtuali chiamate **web1** e **web2** rispettivamente interno Hello stesso set denominata di disponibilità **myAvailSet** in **myVNet**. Fare riferimento troppo[questo collegamento](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate macchine virtuali.

1. Da un browser passare toohello portale di Azure: [http://portal.azure.com](http://portal.azure.com) e accedere con l'account di Azure.
2. Scegliere hello superiore sinistra della schermata di hello **New** > **rete** > **bilanciamento del carico.**
3. In hello **Crea servizio di bilanciamento del carico** pannello, digitare un nome per il bilanciamento del carico. Qui viene chiamato **myLoadBalancer**.
4. In **Tipo** selezionare **Pubblica**.
5. In **Indirizzo IP pubblico** creare un nuovo indirizzo IP pubblico denominato **myPublicIP**.
6. In Gruppo di risorse, selezionare **myRG**. Selezionare quindi un **Percorso** appropriato e fare clic su **OK**. servizio di bilanciamento del carico Hello inizierà quindi toodeploy e richiederà alcuni minuti la distribuzione completa di toosuccessfully.

    ![Aggiornamento del gruppo di risorse di bilanciamento del carico](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Creare un pool di indirizzi back-end

1. Dopo aver distribuito correttamente il bilanciamento del carico, selezionarlo dalle risorse. In impostazioni, selezionare i pool di back-end. Immettere un nome per il pool di back-end. Fare clic su hello **Aggiungi** pulsante verso l'alto hello del pannello hello che viene visualizzato.
2. Fare clic su **aggiungere una macchina virtuale** in hello **aggiungere pool back-end** blade.  Selezionare **Scegliere un set di disponibilità** in **Set di disponibilità**, quindi selezionare **myAvailSet**. Selezionare quindi **scegliere macchine virtuali hello** in hello sezione macchine virtuali nel pannello hello e fare clic su **web1** e **web2**, hello due macchine virtuali create per il bilanciamento del carico. Assicurarsi che entrambi dispongano di segni di spunta blu toohello come illustrato nell'immagine di hello in basso a sinistra. Quindi, fare clic su **selezionare** in tale pannello seguito da OK in hello **macchine virtuali scegliere** blade e quindi **OK** in hello **aggiungere pool back-end** pannello.

    ![Aggiunta di pool di indirizzi back-end toohello- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Verificare che le notifiche nell'elenco a discesa toomake dispone di un aggiornamento per quanto riguarda il salvataggio di pool back-end di bilanciamento del carico hello nell'interfaccia di rete aggiunta tooupdating hello per entrambe le macchine virtuali di hello **web1** e **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Creare un probe, una regola LB e le regole NAT

1. Creare un probe di integrità.

    In impostazioni di bilanciamento del carico, selezionare Probe, Quindi fare clic su **Aggiungi** nella parte superiore di hello del pannello hello.

    Esistono due modi tooconfigure un probe: HTTP o TCP. In questo esempio viene utilizzato HTTP, ma TCP può essere configurato in modo anaolo.
    Aggiornare le informazioni necessarie hello. Come accennato, **myLoadBalancer** caricherà il traffico bilanciato sulla porta 80. percorso di Hello selezionato è HealthProbe.aspx, l'intervallo è 15 secondi e soglia non integra è 2. Al termine, fare clic su **OK** probe hello toocreate.

    Posizionare il puntatore del mouse su toolearn icona hello 'i' informazioni su queste configurazioni singole e come possono essere modificate toocater tooyour requisiti.

    ![Aggiunta di un probe](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Creare una regola del servizio di bilanciamento del carico.

    Fare clic su regole di hello di bilanciamento del carico sezione Impostazioni del servizio di bilanciamento del carico. Nel pannello nuova hello, fare clic su **Aggiungi**. Rinominare la regola. In questo caso, è HTTP. Scegliere hello porte di front-end e back-end. In questo caso, la porta 80 viene usata per entrambi. Scegliere **LB-back-end** come il pool back-end e hello creato in precedenza **HealthProbe** come hello Probe. Altre configurazioni possono essere impostate in base a requisiti tooyour. Fare clic su OK toosave regola di bilanciamento carico di hello.

    ![Aggiunta di una regola di bilanciamento del carico](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Creare le regole NAT in ingresso

    Fare clic su regole NAT in ingresso nella sezione Impostazioni hello del servizio di bilanciamento del carico. In hello nuovo pannello, fare clic su **Aggiungi**. Poi rinominare la regola NAT in ingresso. In questo caso, **inboundNATrule1**. destinazione Hello deve essere hello che IP pubblico creato in precedenza. Selezionare personalizzata nel servizio e selezionare il protocollo di hello toouse desiderato. Qui è stato selezionato il protocollo TCP. Immettere la porta hello, 3441 e hello porta di destinazione, in questo caso, 3389. quindi fare clic su OK toosave questa regola.

    Dopo aver creato prima regola hello, ripetere questo passaggio per hello seconda regola NAT in ingresso chiamato inboundNATrule2 da 3442 tooTarget porta 3389.

    ![Aggiunta di una regola NAT in ingresso](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Rimuovere un bilanciamento del carico

toodelete un bilanciamento del carico, Bilanciamento carico di hello selezionare da tooremove. In hello *bilanciamento del carico* pannello, fare clic su **eliminare** nella parte superiore di hello del pannello hello. Fare clic su **Sì** quando richiesto.

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
