---
title: aaaCreate un Gateway applicazione - portale di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Gateway applicazione utilizzando hello portale
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Creare un gateway applicazione con il portale di hello

Il [gateway applicazione](application-gateway-introduction.md) è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller) e varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione. In questo articolo illustra hello passaggi toocreate un Gateway applicazione uso hello portale di Azure e l'aggiunta di un server esistente come membro back-end.

## <a name="log-in-tooazure"></a>Accedi tooAzure

Accedere al portale di Azure toohello [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Creare il gateway applicazione

toocreate un gateway di applicazione, hello completato i passaggi che seguono. Il gateway applicazione richiede una propria subnet. Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet. Dopo aver distribuito tooa subnet gateway applicazione hello, è possibile aggiungere solo altri gateway applicazione tooit.

1. Nel riquadro di Preferiti hello del portale di hello, fare clic su **New**
1. In hello **New** pannello, fare clic su **rete**. In hello **rete** pannello, fare clic su **Gateway applicazione**, come illustrato nella seguente immagine hello:

    ![Creazione di un gateway applicazione][1]

1. In hello **nozioni di base** blade che viene visualizzata, immettere i seguenti valori hello, quindi fare clic su **OK**:

   | **Impostazione** | **Valore** | **Dettagli**|
   |---|---|---|
   |**Nome**|AdatumAppGateway|nome Hello del gateway applicazione hello|
   |**Livello**|Standard|I valori disponibili sono Standard e WAF. Visitare [firewall applicazione web](application-gateway-web-application-firewall-overview.md) toolearn ulteriori informazioni sulla WAF.|
   |**Dimensioni SKU**|Media|Opzioni disponibili quando si sceglie il livello Standard: Small, Medium e Large. Quando si sceglie il livello WAF, le opzioni sono solo Medium e Large.|
   |**Numero di istanze**|2|Numero di istanze del gateway applicazione hello per la disponibilità elevata. I numeri di istanze di 1 devono essere usati solo a scopo di test.|
   |**Sottoscrizione**|[Sottoscrizione]|Selezionare un gateway applicazione di sottoscrizione toocreate hello in.|
   |**Gruppo di risorse**|**Crea nuovo:** AdatumAppGatewayRG|Creare un gruppo di risorse. nome del gruppo di risorse Hello deve essere univoco all'interno di sottoscrizione hello selezionata. ulteriori informazioni sui gruppi di risorse, leggere hello toolearn [Gestione risorse](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) articolo introduttivo.|
   |**Posizione**|Stati Uniti occidentali||

1. In hello **impostazioni** pannello visualizzato sotto **rete virtuale**, fare clic su **scegliere una rete virtuale**. Hello **rete virtuale scegliere** apre blade.  Fare clic su **Crea nuovo** tooopen hello **crea rete virtuale** blade.

   ![scegliere una rete virtuale][2]

1. In hello **blade di rete virtuale crea** immettere i seguenti valori hello, quindi fare clic su **OK**. Hello **crea rete virtuale** e **rete virtuale scegliere** chiudere pannelli. Questo passaggio popola hello **Subnet** campo hello **impostazioni** pannello con subnet hello scelto.

   | **Impostazione** | **Valore** | **Dettagli**|
   |---|---|---|
   |**Nome**|AdatumAppGatewayVNET|Nome del gateway applicazione hello|
   |**Spazio di indirizzi:**|10.0.0.0/16|Hello uno spazio di indirizzi per la rete virtuale hello|
   |**Nome della subnet**|AppGatewaySubnet|Nome della subnet di hello per il gateway applicazione hello|
   |**Intervallo di indirizzi subnet**|10.0.0.0/28|Questa subnet consente ulteriori altre subnet nella rete virtuale hello per i membri del pool back-end|

1. In hello **impostazioni** pannello **configurazione IP Frontend**, scegliere **pubblica** come hello **tipo di indirizzo IP**

1. In hello **impostazioni** pannello **indirizzo IP pubblico** fare clic su **scegliere un indirizzo IP pubblico**, hello **scegliere l'indirizzo IP pubblico** apre Pannello , fare clic su **Crea nuovo**.

   ![scegliere un indirizzo IP pubblico][3]

1. In hello **creare l'indirizzo IP pubblico** pannello, accettare il valore di predefinito hello e fare clic su **OK**. Pannello Hello chiude e popola hello **indirizzo IP pubblico** con indirizzo IP pubblico hello scelto.

1. In hello **impostazioni** pannello **configurazione Listener**, fare clic su **HTTP** in **protocollo**. Immettere toouse porta hello in hello **porta** campo.

2. Fare clic su **OK** su hello **impostazioni** toocontinue blade.

1. Rivedere le impostazioni di hello in hello **riepilogo** pannello e fare clic su **OK** toostart creazione del gateway applicazione hello. Creazione di un gateway applicazione è un'attività a esecuzione prolungata e accetta ora toocomplete.

## <a name="add-servers-toobackend-pools"></a>Aggiungere server toobackend pool

Dopo aver creato il gateway di applicazione hello, sistemi hello host con bilanciamento del carico toobe dell'applicazione hello devono comunque gateway di applicazione toobe toohello aggiunto. gli indirizzi IP di Hello, FQDN o schede di interfaccia di questi server vengono aggiunti toohello pool di indirizzi back-end.

### <a name="ip-address-or-fqdn"></a>Indirizzo IP o nome di dominio completo

1. Con gateway applicazione hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **AdatumAppGateway** gateway applicazione hello tutti pannello risorse. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **AdatumAppGateway** in hello **filtrare in base al nome...** gateway applicazione hello di accesso tooeasily di casella.

1. gateway applicazione Hello creato viene visualizzato. Fare clic su **pool back-end**e selezionare il pool back-end corrente di hello **appGatewayBackendPool**, hello **appGatewayBackendPool** apre blade.

   ![Pool back-end del gateway applicazione][4]

1. Fare clic su **Aggiungi destinazione** tooadd di indirizzi IP dei valori di nome di dominio completo. Scegliere **IP FQDN o indirizzo** come hello **tipo** e immettere l'indirizzo IP o FQDN nel campo hello. Ripetere questo passaggio per gli altri membri del pool di back-end. Al termine, fare clic su **Salva**.

### <a name="virtual-machine-and-nic"></a>Macchina virtuale e scheda di interfaccia di rete

È anche possibile aggiungere le schede di interfaccia di rete delle macchine virtuali come membri del pool back-end. Solo le macchine virtuali all'interno di hello stessa rete virtuale hello Gateway applicazione sono disponibili tramite hello elenco a discesa.

1. Con gateway applicazione hello creato, nel portale di Azure hello **Preferiti** riquadro, fare clic su **tutte le risorse**. Fare clic su hello **AdatumAppGateway** gateway applicazione hello tutti pannello risorse. Sottoscrizione hello selezionati sono già dispone di numerose risorse in essa contenuti, è possibile immettere **AdatumAppGateway** in hello **filtrare in base al nome...** gateway applicazione hello di accesso tooeasily di casella.

1. gateway applicazione Hello creato viene visualizzato. Fare clic su **pool back-end**e selezionare il pool back-end corrente di hello **appGatewayBackendPool**, hello **appGatewayBackendPool** apre blade.

   ![Pool back-end del gateway applicazione][5]

1. Fare clic su **Aggiungi destinazione** tooadd di indirizzi IP dei valori di nome di dominio completo. Scegliere **macchina virtuale** come hello **tipo** e selezionare macchina virtuale hello e toouse NIC. Al termine, fare clic su **Salva**.

   > [!NOTE]
   > Solo le macchine virtuali in hello stessa rete virtuale come gateway applicazione hello sono disponibili nella casella a discesa hello.

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, eliminare il gruppo di risorse hello, gateway applicazione e tutte le risorse correlate. toodo in tal caso, selezionare il gruppo di risorse di hello blade di gateway applicazione hello e fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questo scenario, un gateway applicazione distribuita e aggiunto a un back-end toohello server. passaggi successivi Hello sono gateway di applicazione hello tooconfigure la modifica delle impostazioni e le regole di rettifica nel gateway hello. Questi passaggi sono reperibili visitando hello seguenti articoli:

Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)

Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-portal.md)

Informazioni su come tooprotect le applicazioni con [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) una funzionalità di gateway applicazione.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
