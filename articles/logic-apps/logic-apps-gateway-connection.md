---
title: origini dei dati in locale per le app di Azure logica aaaAccess | Documenti Microsoft
description: Configurare gateway dati locale di hello per accedere a origini dati in locale da App per la logica
keywords: accesso ai dati, locale, trasferimento dei dati, crittografia, origini dei dati
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Accedere alle origini dati in locale da app logica con gateway dati locale di hello

origini dati tooaccess in locale da App per la logica, impostare da un gateway dati locale che App per la logica è possibile utilizzare con i connettori supportati. gateway Hello funge da ponte che fornisce il trasferimento dei dati rapido e la crittografia tra origini dati in locale e App per la logica. gateway Hello inoltra i dati da origini locali sui canali crittografati tramite hello Azure Service Bus. Tutto il traffico viene generato come proteggere il traffico in uscita dall'agente gateway hello. Altre informazioni, vedere [funzionamento gateway dati hello](logic-apps-gateway-install.md#gateway-cloud-service). 

gateway Hello supporta le connessioni delle origini dati toothese in locale:

*   BizTalk Server 2016
*   DB2  
*   File system
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   Server applicazioni SAP 
*   Server messaggi SAP
*   SharePoint
*   SQL Server
*   Teradata

Questi passaggi mostrano come tooset backup hello locale toowork gateway dati con le applicazioni di logica. Per altre informazioni sui connettori supportati, vedere [Connettori per le app per la logica di Azure](../connectors/apis-list.md). 

Per informazioni su come toouse hello gateway con altri servizi, vedere i seguenti articoli:

*   [Gateway dati locale di Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Gateway dati locale di Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Gateway dati locale di Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Gateway dati locale di Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Requisiti

* È necessario disporre già [installato gateway dati hello in un computer locale](logic-apps-gateway-install.md).

* Quando si accede toohello portale di Azure, si dispone di toouse hello stesso lavoro o scuola account che è stata usata troppo[installare il gateway dati locale di hello](logic-apps-gateway-install.md#requirements). L'account di accesso deve inoltre avere toouse una sottoscrizione di Azure quando si crea una risorsa per il gateway in hello portale di Azure per l'installazione del gateway.

* L'installazione del gateway non può essere già richiesta da una risorsa del gateway di Azure. È possibile associare la risorsa di Azure gateway un gateway installazione tooonly. Attestazione si verifica quando si crea risorsa gateway hello in modo che l'installazione di hello non è disponibile per le altre risorse.

## <a name="set-up-hello-data-gateway-connection"></a>Impostare la connessione del gateway dati hello

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Installare il gateway dati locale di hello

Se hai già fatto, seguire hello [il gateway dati locale di passaggi tooinstall hello](logic-apps-gateway-install.md). Prima di continuare con hello altri passaggi, assicurarsi che il gateway dati di hello è stato installato in un computer locale.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Creare una risorsa di Azure per il gateway dati locale di hello

Dopo aver installato il gateway hello in un computer locale, è necessario creare il gateway dati come risorsa in Azure. Questo passaggio associa anche la risorsa di gateway con la sottoscrizione di Azure.

1. Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure"). Assicurarsi che toouse hello stesso lavoro di Azure o l'indirizzo e-mail dell'istituto di istruzione usato gateway hello tooinstall.

2. Nel menu a sinistra di hello in Azure, scegliere **New** > **Enterprise Integration** > **gateway dati locale** come illustrato di seguito:

   ![Trovare "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. In hello **crea gateway di connessione** pannello fornire toocreate questi dettagli della risorsa del gateway dati:

    * **Nome**: inserire un nome per la risorsa del gateway. 

    * **Sottoscrizione**: selezionare hello tooassociate sottoscrizione di Azure alla risorsa del gateway. 
    La sottoscrizione deve essere hello app logica stessa sottoscrizione.
   
      sottoscrizione predefinita Hello è basata su account di Azure utilizzato toosign in hello.

    * **Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente per distribuire la risorsa del gateway. 
    I gruppi di risorse consentono di gestire gli asset di Azure correlati come una raccolta.

    * **Percorso**: Azure limita questo toohello percorso stessa area che è stato selezionato per il servizio cloud gateway di hello durante [dell'installazione del gateway](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Verificare che il percorso di risorsa gateway hello corrisponda posizione del servizio cloud gateway hello. In caso contrario, l'installazione del gateway potrebbe non essere nell'elenco a gateway installato hello è tooselect nel passaggio successivo hello.
      > 
      > È possibile usare aree diverse per la risorsa del gateway e per le app per la logica.

    * **Nome di installazione**: se l'installazione del gateway non è già selezionata, selezionare il gateway hello installata in precedenza. 

    tooadd hello gateway risorsa tooyour dashboard di Azure, scegliere **toodashboard Pin**. 
    Al termine dell'operazione, scegliere **Crea**.

    ad esempio:

    ![Fornire dettagli toocreate gateway dati locale](./media/logic-apps-gateway-connection/createblade.png)

    toofind o vista il gateway dati in qualsiasi momento, hello Azure sinistro menu principale, andare troppo **più servizi** > **Enterprise Integration** > **dati locali Gateway**.

    ![Andare troppo "Più servizi", "Integrazione di Enterprise", "Gateway dati locale"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Connettere il gateway dati locale di logica app toohello

Dopo aver creato la risorsa del gateway dati e associati alla sottoscrizione di Azure alla risorsa, creare una connessione tra il gateway dati logica app e hello.

> [!NOTE]
> Il percorso di connessione del gateway deve essere presente in hello stessa area dell'app logica, ma è possibile utilizzare un gateway dati esistente in un'area diversa.

1. In hello portale di Azure, creare o aprire l'app logica nella finestra di progettazione logica App.

2. Aggiungere un connettore che supporta la connettività locale, ad esempio SQL Server.

3. Selezionare lo stesso ordine hello illustrato, **Connetti tramite il gateway dati locale**, fornire un nome univoco della connessione hello le informazioni necessarie e selezionare una risorsa per il gateway dati hello che si desidera toouse. Al termine dell'operazione, scegliere **Crea**.

   > [!TIP]
   > Un nome di connessione univoco consente di identificare facilmente la connessione in un secondo momento, soprattutto quando si creano più connessioni. Se applicabile, è necessario includere anche dominio hello per il proprio nome utente. 

   ![Creare una connessione tra l'app per la logica e il gateway dati](./media/logic-apps-gateway-connection/blankconnection.png)

Complimenti, la connessione del gateway è pronta per il toouse app logica.

## <a name="edit-your-gateway-connection-settings"></a>Modificare le impostazioni di connessione del gateway

Dopo aver creato una connessione gateway per l'app logica, è le impostazioni di hello aggiornamento toolater per tale connessione specifico.

1. connessione al gateway toofind hello:

   * Nel pannello app logica hello in **gli strumenti di sviluppo**selezionare **connessioni API**. 
   
     Hello **connessioni API** riquadro vengono visualizzate tutte le connessioni delle API associate all'app di logica, incluse le connessioni di gateway.

     ![Passare tooyour logica app, selezionare "Connessioni API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * O, hello Azure sinistro menu principale, andare troppo **più servizi** > **Web e servizi mobili** > **connessioni API** per tutte le connessioni di API, tra cui le connessioni gateway, che sono associate alla sottoscrizione di Azure. 

   * In alternativa, hello Azure sinistro menu principale, accedere troppo**tutte le risorse** per tutte le connessioni di API, comprese le connessioni di gateway, che sono associate alla sottoscrizione di Azure.

2. Selezionare una connessione al gateway hello che desidera tooview o modificare e scegliere **connessione modificare API**.

   > [!TIP]
   > Se gli aggiornamenti non avrà effetto, provare a [arrestare e riavviare il servizio di Windows gateway hello](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Cambiare o eliminare una risorsa gateway dati locale

associare il gateway a una risorsa diversa toocreate una risorsa, gateway diverso o rimuovere risorse gateway hello, è possibile eliminare una risorsa per il gateway hello senza influire sull'installazione del gateway hello. 

1. Hello Azure sinistro menu principale, andare troppo**tutte le risorse**. 
2. Individuare e selezionare la risorsa del gateway dati.
3. Scegliere **Gateway dati locale**, sulla barra degli strumenti risorse hello, scegliere **eliminare**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Domande frequenti

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Passaggi successivi

* [Proteggere le app per la logica](./logic-apps-securing-a-logic-app.md)
* [Esempi e scenari comuni per le app per la logica](./logic-apps-examples-and-scenarios.md)
