---
title: "bilanciamento del carico su più configurazioni IP in Azure aaaLoad | Documenti Microsoft"
description: Bilanciamento del carico tra configurazioni IP primarie e secondarie.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Il bilanciamento del carico su più configurazioni IP utilizzando hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

In questo articolo viene descritto come indirizzi di bilanciamento del carico di Azure con più IP toouse su un'interfaccia di rete secondaria (NIC). Per questo scenario, si dispone di due macchine virtuali che eseguono Windows, ognuna con un database primario e una scheda di rete secondaria. Ognuno di hello secondario schede di rete dispone di due configurazioni IP. Ogni macchina virtuale ospita entrambi i siti Web: contoso.com e fabrikam.com. Ogni sito Web è associato tooone delle configurazioni IP hello sulla hello di rete secondaria. Utilizziamo bilanciamento del carico di Azure tooexpose due front-end indirizzi IP, una per ogni sito Web, toodistribute traffico toohello rispettiva configurazione IP per il sito Web di hello. Questo scenario utilizza hello stesso numero di porta tra i server front-end, così come entrambi indirizzi IP del pool back-end.

![Immagine dello scenario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Prerequisiti
In questo esempio presuppone che si disponga di un gruppo di risorse denominato *contosofabrikam* con hello seguente configurazione:
 -  include una rete virtuale denominata *myVNet*, due macchine virtuali chiamate *VM1* e *VM2* rispettivamente interno hello stesso disponibilità set denominata *myAvailset*. 
 - ogni macchina virtuale dispone di una scheda di interfaccia di rete primaria e una scheda di interfaccia di rete secondaria. Hello primario schede di rete sono denominati *VM1NIC1* e *VM2NIC1* e hello secondario schede di rete sono denominati *VM1NIC2* e *VM2NIC2*. Per altre informazioni sulla creazione di macchine virtuali con più schede di interfacce di rete, vedere [Creare una macchina virtuale con più schede di interfaccia di rete usando PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Saldo tooload passaggi su più configurazioni IP

Eseguire la procedura seguente scenario hello tooachieve descritta in questo articolo:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>PASSAGGIO 1: Configurare hello NIC secondaria per ogni macchina virtuale

Per ogni macchina virtuale nella rete virtuale, aggiungere set di configurazione IP hello NIC secondario come indicato di seguito:  

1. Da un browser passare toohello portale di Azure: http://portal.azure.com e accedere con l'account di Azure.
2. A hello superiore sinistra della schermata di hello, fare clic sull'icona di gruppo di risorse hello e quindi fare clic su hello gruppo di risorse hello macchine virtuali si trovano in (ad esempio, *contosofabrikam*). Hello **gruppi di risorse** blade che elenca tutte le risorse di hello insieme a interfacce di rete hello per le macchine virtuali hello viene ora visualizzata.
3. database secondario toohello NIC di ogni macchina virtuale, aggiungere una configurazione IP come indicato di seguito:
    1. Interfaccia di rete selezionare hello che si desidera tooadd hello IP configurazione.
    2. Nel pannello hello che viene visualizzata per hello NIC selezionato, fare clic su **le configurazioni IP**. Quindi fare clic su **Aggiungi** parte superiore di hello del pannello hello che viene visualizzato.
    3. In hello **le configurazioni IP aggiungere** pannello, aggiungere un secondo toohello di configurazione IP scheda di rete nel modo seguente: 
        1. Digitare un nome per la configurazione IP secondaria (ad esempio, per VM1 e VM2 nome hello configurazioni IP come *VM1NIC2 ipconfig2* e *VM2NIC2 ipconfig2* rispettivamente).
        2. Per **Indirizzo IP privato** in **Allocazione**selezionare **Statico**.
        3. Fare clic su **OK**.
        4. Hello secondo la configurazione IP per hello NIC secondaria è stata completata, viene visualizzato in hello **le configurazioni IP** pannello impostazioni hello data scheda di rete.

### <a name="step-2-create-a-load-balancer"></a>PASSAGGIO 2: Creare un servizio di bilanciamento del carico

Creare un servizio di bilanciamento del carico nel modo seguente:

1. Da un browser passare toohello portale di Azure: http://portal.azure.com e accedere con l'account di Azure.
2. Scegliere hello superiore sinistra della schermata Ciao fare **New** > **rete** > **bilanciamento del carico**. Quindi fare clic su **Crea**.
3. In hello **Crea servizio di bilanciamento del carico** pannello, digitare un nome per il bilanciamento del carico. Qui viene chiamato *mylb*.
4. In Indirizzo IP pubblico creare un nuovo indirizzo IP pubblico denominato **PublicIP1**.
5. Nel gruppo di risorse, selezionare hello gruppo di risorse esistente delle macchine virtuali (ad esempio, *contosofabrikam*). Selezionare quindi un percorso appropriato e fare clic su **OK**. servizio di bilanciamento del carico Hello inizierà quindi toodeploy e richiederà alcuni minuti la distribuzione completa di toosuccessfully.
6. Una volta distribuito, bilanciamento del carico hello viene visualizzato come una risorsa nel gruppo di risorse.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>PASSAGGIO 3: Configurare i pool IP front-end di hello

Configurare il pool di indirizzi IP front-end per ogni sito Web (Contoso e Fabrikam) nel modo seguente:

1. Nel portale di hello, fare clic su **più servizi** > tipo **indirizzo IP pubblico** in hello casella filtro e quindi fare clic su **gli indirizzi IP pubblici**. Fare clic su **Aggiungi** parte superiore di hello del pannello hello che viene visualizzato.
2. Configurare due indirizzi IP pubblici (*PublicIP1* e *PublicIP2*) per entrambi i siti Web (contoso e fabrikam) nel modo seguente:
    1. Digitare un nome per l'indirizzo IP front-end.
    2. Per **gruppo di risorse**, selezionare il gruppo di risorse esistente di hello macchine virtuali di hello (ad esempio, *contosofabrikam*).
    3. Per **percorso**, selezionare hello nello stesso percorso come hello macchine virtuali.
    4. Fare clic su **OK**.
    5. Una volta creati gli indirizzi IP pubblici hello due, essi vengono visualizzati nella hello **indirizzo IP pubblico** pannello indirizzi.
3. Nel portale di hello, fare clic su **più servizi** > tipo **bilanciamento del carico** in hello casella filtro e quindi fare clic su **bilanciamento del carico**.  
4. Selezionare servizio di bilanciamento del carico hello (*mylb*) che si desidera tooadd hello front-end IP pool.
5. In **Impostazioni** selezionare **Pool front-end**. Quindi fare clic su **Aggiungi** parte superiore di hello del pannello hello che viene visualizzato.
6. Digitare un nome per l'indirizzo IP front-end (*farbikamfe* o **contosofe*).
7. Fare clic su **indirizzo IP** e hello **indirizzo IP pubblico scegliere** blade, gli indirizzi IP hello selezionare per il server front-end (*PublicIP1* o *PublicIP2*).
8. Ripetere i passaggi da 3 too7 all'interno di questa sezione toocreate hello secondo front-end indirizzo IP.
9. Una volta completato, configurazione del pool IP front-end di hello entrambi gli indirizzi IP front-end vengono visualizzati in hello **Pool IP front-end** pannello del servizio di bilanciamento del carico. 
    
### <a name="step-4-configure-hello-backend-pool"></a>PASSAGGIO 4: Configurare i pool di back-end hello   
Configurare i pool di indirizzi back-end hello nel servizio di bilanciamento del carico per ogni sito Web (Contoso e Fabrikam) come segue:
        
1. Nel portale di hello, fare clic su **più servizi** > digitare bilanciamento del carico nella casella Filtro hello e quindi fare clic su **bilanciamento del carico**.  
2. Selezionare servizio di bilanciamento del carico hello (*mylb*) che si desidera pool back-end di hello tooadd da.
3. In **Impostazioni** selezionare **Pool di back-end**. Digitare un nome per il pool di back-end, ad esempio *contosopool* o *fabrikampool*. Quindi fare clic su hello **Aggiungi** pulsante verso l'alto hello del pannello hello che viene visualizzato. 
4. Per **Associate a** selezionare **Set di disponibilità**.
5. Nella casella **Set di disponibilità** selezionare **myAvailset**.
6. Aggiungere le configurazioni IP della rete di destinazione per entrambe le macchine virtuali nel modo seguente (vedere la figura 2):  
    1. Per **macchina virtuale di destinazione**, selezionare hello macchina virtuale che si desidera che il pool back-end toohello tooadd (ad esempio, VM1 o VM2).
    2. Per **configurazione IP di rete**selezionare configurazione IP delle schede di rete secondaria di hello per la macchina virtuale (ad esempio, VM1NIC2 ipconfig2 o VM2NIC2 ipconfig2).
    ![Immagine dello scenario di bilanciamento del carico](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Figura 2**: configurazione di bilanciamento del carico hello con pool back-end  
7. Fare clic su **OK**.
8. Quando configurazione del pool back-end hello è stata completata, entrambi i pool di indirizzi back-end vengono visualizzati nella hello **pannello pool back-end** del servizio di bilanciamento del carico.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>PASSAGGIO 5: Configurare un probe di integrità per il bilanciamento del carico
Configurare un probe di integrità per il bilanciamento del carico nel modo seguente:
    1. Fare clic su più servizi nel portale di hello > digitare bilanciamento del carico nella casella Filtro hello e quindi fare clic su **bilanciamento del carico**.  
    2. Selezionare bilanciamento del carico hello che si desidera pool back-end di hello tooadd da.
    3. In **Impostazioni** selezionare **Probe di integrità**. Quindi fare clic su **Aggiungi** parte superiore di hello del pannello hello che viene visualizzato.
    4. Digitare un nome per il probe di integrità hello (ad esempio, HTTP) e fare clic su **OK**.

### <a name="step-6-configure-load-balancing-rules"></a>PASSAGGIO 6: Configurare le regole del servizio di bilanciamento del carico
Configurare le regole di bilanciamento del carico (*HTTPc* e *HTTPf*) per ogni sito Web nel modo seguente:
    
1. In **Impostazioni** selezionare **Probe di integrità**. Quindi fare clic su **Aggiungi** parte superiore di hello del pannello hello che viene visualizzato.
2. Per **nome**, digitare un nome per la regola di bilanciamento del carico di hello (ad esempio, *HTTPc* per Contoso, o *HTTPf* per Fabrikam)
3. Per indirizzo IP Frontend, selezionare l'indirizzo IP di front-end hello hello (ad esempio *Contosofe* o *Fabrikamfe*)
4. Per **porta** e **porta back-end**, valore predefinito di hello **80**.
5. Per **IP mobile (Direct Server Return)** fare clic su **Abilitato**.
6. Fare clic su **OK**.
7. Ripetere i passaggi da 1 too6 all'interno di questa regola di bilanciamento del carico seconda sezione toocreate hello.
8. Quando il bilanciamento del carico hello regole di configurazione è stata completata, entrambe le regole ((*HTTPc* e *HTTPf*) vengono visualizzati in hello **regole di bilanciamento del carico** pannello del servizio di bilanciamento del carico.

### <a name="step-7-configure-dns-records"></a>PASSAGGIO 7: Configurare i record DNS
Infine, è necessario configurare DNS risorse record toopoint toohello front-end rispettivi indirizzo IP di bilanciamento del carico hello. È possibile ospitare i domini nel servizio DNS di Azure. Per altre informazioni sull'uso del servizio DNS di Azure con Azure Load Balancer, vedere [Uso del servizio DNS di Azure con altri servizi di Azure](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su come il bilanciamento del carico toocombine servizi in Azure in [utilizzando servizi di bilanciamento del carico in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Informazioni su come è possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi di bilanciamento del carico in [Log analitica per il bilanciamento del carico di Azure](../load-balancer/load-balancer-monitor-log.md).
