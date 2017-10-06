---
title: aaaHost siti multipli con Gateway applicazione Azure | Documenti Microsoft
description: "Questa pagina fornisce istruzioni tooconfigure un gateway applicazione Azure esistente per ospitare più applicazioni web su hello stesso gateway con hello portale di Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Configurare un gateway applicazione esistente per l'hosting di più applicazioni Web

> [!div class="op_single_selector"]
> * [portale di Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Hosting di più siti consente toodeploy più di una sola applicazione web su hello stesso gateway applicazione. Si basa su presenza dell'intestazione host nella richiesta HTTP in ingresso hello, toodetermine quali listener riceve traffico. listener di Hello indirizza quindi il pool back-end tooappropriate traffico come configurato nella definizione delle regole hello del gateway hello. Nelle applicazioni web SSL abilitato, i gateway applicazione si basa su hello indicazione nome Server (SNI) estensione toochoose hello corretto del listener per il traffico web hello. Viene in genere utilizzata per l'hosting del sito più tooload bilanciamento delle richieste per i pool di server back-end web diversi domini toodifferent. Analogamente, più sottodomini del dominio radice della stessa può essere ospitato su hello hello stesso gateway applicazione.

## <a name="scenario"></a>Scenario

Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: contoso pool di server e il pool di server di fabrikam. Il programma di installazione simile potrebbe essere sottodomini toohost usato come app.contoso.com e blog.contoso.com.

![scenario multisito][multisite]

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario aggiunge supporto multisito tooan gateway di applicazioni esistente. toocomplete tooconfigure disponibile toobe è necessario questo scenario, un gateway applicazione esistente. Visitare [creare un gateway applicazione tramite il portale di hello](application-gateway-create-gateway-portal.md) toolearn come toocreate un gateway applicazione basic nel portale di hello.

di seguito Hello sono passaggi hello necessari gateway di applicazione hello tooupdate:

1. Creare toouse pool back-end per ogni sito.
2. Creare un listener per ogni sito che viene supportato dal gateway applicazione.
3. Creare regole toomap ogni listener con hello appropriato back-end.

## <a name="requirements"></a>Requisiti

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico. È possibile usare anche FQDN.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload). Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.
* **Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Le regole vengono elaborate in ordine di hello che sono elencati e il traffico verrà indirizzato tramite hello prima regola che corrisponde indipendentemente dal fatto di specificità. Ad esempio, se si dispone di una regola di utilizzo di un listener di base e una regola di utilizzo di un listener multisito entrambi nella stessa regola di porta, hello con hello listener multisito hello deve essere elencato prima regola hello con listener di base hello affinché hello multisito regola toofunction come previsto. 
* **Certificati**: ogni listener richiede un certificato univoco. In questo esempio vengono creati due listener per più siti. Due certificati PFX e password hello relativa necessario toobe creato.

## <a name="create-back-end-pools-for-each-site"></a>Creare i pool di back-end per ogni sito

È necessario un pool di back-end per ogni sito che supporta il gateway applicazione. In questo caso ne vengono creati due, uno per contoso11.com e uno per fabrikam11.com.

### <a name="step-1"></a>Passaggio 1

Passare tooan gateway di applicazione esistente nel portale di Azure (https://portal.azure.com) hello. Selezionare **Pool back-end** e fare clic su **Aggiungi**.

![aggiunta di pool di back-end][7]

### <a name="step-2"></a>Passaggio 2

Immettere le informazioni di hello per il pool back-end hello **pool1**, l'aggiunta di indirizzi ip hello o FQDN per i server back-end hello e fare clic su **OK**

![impostazioni del pool di back-end pool1][8]

### <a name="step-3"></a>Passaggio 3

Nel Pannello di pool back-end hello clic **Aggiungi** tooadd un pool back-end aggiuntivo **pool2**, l'aggiunta di indirizzi ip hello o FQDN per i server back-end hello e fare clic su **OK**

![impostazioni del pool di back-end pool2][9]

## <a name="create-listeners-for-each-back-end"></a>Creare listener per ogni back-end

Gateway applicazione si basa su HTTP 1.1 toohost intestazioni host più di un sito Web in hello stesso indirizzo IP pubblico e la porta. listener di base Hello creato nel portale di hello non contiene questa proprietà.

### <a name="step-1"></a>Passaggio 1

Fare clic su **listener** hello gateway applicazione esistente e fare clic su **multisito** listener prima di tooadd hello.

![pannello della panoramica dei listener][1]

### <a name="step-2"></a>Passaggio 2

Immettere le informazioni di hello per listener hello. In questo esempio la terminazione SSL è configurata, creare una nuova porta front-end. Caricare toobe di certificato PFX hello utilizzato per la terminazione SSL. Hello l'unica differenza in questo pannello listener base standard di blade confrontati toohello è hostname hello.

![pannello delle proprietà del listener][2]

### <a name="step-3"></a>Passaggio 3

Fare clic su **multisito** e creare un altro listener come descritto nel passaggio precedente di hello per secondo sito hello. Verificare che toouse un certificato diverso per il listener secondo hello. Hello l'unica differenza in questo pannello listener base standard di blade confrontati toohello è hostname hello. Immettere le informazioni di hello per listener hello e fare clic su **OK**.

![pannello delle proprietà del listener][3]

> [!NOTE]
> La creazione di listener nel portale di Azure per il gateway applicazione hello è un'attività a esecuzione prolungata, potrebbe richiedere alcuni hello toocreate ora due listener in questo scenario. Quando il listener di completamento hello Visualizza nel portale di hello, come illustrato nella seguente immagine hello:

![panoramica dei listener][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Creare regole di pool di toobackend toomap listener

### <a name="step-1"></a>Passaggio 1

Passare tooan gateway di applicazione esistente nel portale di Azure (https://portal.azure.com) hello. Selezionare **regole** e scegliere regole predefinito esistente hello **rule1** e fare clic su **modifica**.

### <a name="step-2"></a>Passaggio 2

Compilare pannello regole hello, come illustrato nella seguente immagine hello. Listener del primo hello e primo pool e fare clic su **salvare** al completamento.

![modifica della regola esistente][6]

### <a name="step-3"></a>Passaggio 3

Fare clic su **regola base** seconda regola di toocreate hello. Compilare il modulo di hello con pool back-end del listener e secondo secondo hello e fare clic su **OK** toosave.

![pannello Aggiungi regola di base][10]

Questo scenario consente di completare la configurazione di un gateway applicazione esistente con il supporto di più siti tramite hello portale di Azure.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooprotect i siti Web con [Gateway applicazione - Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
