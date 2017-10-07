---
title: aaaAzure Service Fabric con avvio rapido di gestione API | Documenti Microsoft
description: "Questa guida viene spiegato come tooquickly può iniziare con l'API di gestione e Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Avvio rapido di Service Fabric con Gestione API

Questa guida viene spiegato come tooset gestione API di Azure con Service Fabric e configurare i primi API operazione toosend traffico tooback-end servizi nell'infrastruttura del servizio. toolearn più sugli scenari di gestione API di Azure con Service Fabric, vedere hello [Panoramica](service-fabric-api-management-overview.md) articolo. 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>Distribuire l'API di gestione e infrastruttura a servizio tooAzure

primo passaggio Hello è toodeploy gestione API e un tooAzure di cluster di Service Fabric in una rete virtuale condivisa. In questo modo toocommunicate gestione API direttamente con Service Fabric modo da poter eseguire l'individuazione del servizio, la risoluzione della partizione del servizio e inoltrare il traffico direttamente il servizio back-end tooany Service Fabric.

### <a name="topology"></a>Topologia

Questa Guida consente di distribuire seguente hello tooAzure topologia in cui gestione API e infrastruttura a servizio presenti in subnet di hello stessa rete virtuale:

 ![Sottotitolo immagine][sf-apim-topology-overview]

tooget iniziare rapidamente, sono disponibili modelli di gestione risorse per ogni passaggio di distribuzione:

 - Topologia di rete:
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Cluster di Service Fabric:
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - Gestione API:
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>Accedi tooAzure e selezionare la sottoscrizione

Questa guida usa [Azure PowerShell][azure-powershell]. Quando si avvia una nuova sessione PowerShell, accedi tooyour account Azure e selezionare la sottoscrizione prima di eseguire i comandi di Azure.
 
Accedi tooyour account di Azure:

```powershell
PS > Login-AzureRmAccount
```

Selezionare la propria sottoscrizione:

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un nuovo gruppo di risorse per la propria distribuzione. Assegnargli un nome e una posizione.

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>Distribuire la topologia di rete hello

primo passaggio Hello è tooset backup toowhich topologia di rete hello gestione API e verrà distribuito il cluster di Service Fabric hello. Hello [network.json] [ network-arm] modello di gestione risorse è toocreate configurata una rete virtuale (VNET) con due subnet e due di sicurezza gruppi (rete). 

Hello [network.parameters.json] [ network-parameters-arm] file dei parametri contiene nomi di hello di subnet hello e NSGs che API di gestione e infrastruttura a servizio verrà distribuito. In questa Guida, i valori dei parametri hello non è necessario toobe modificato. modelli di gestione API e Gestione risorse di infrastruttura servizio Hello utilizzano questi valori, in modo che vengano modificati in questo caso, è necessario modificare in conseguenza hello altri modelli di gestione risorse. 

 1. Scaricare i seguenti file di modello e i parametri di gestione risorse hello:

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. Utilizzare i seguenti PowerShell comando toodeploy hello Gestione risorse modello e parametro file per l'installazione di rete hello hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>Distribuire i cluster di Service Fabric hello

Una volta terminata la distribuzione di risorse di rete hello, hello è toodeploy un toohello di cluster di Service Fabric tra reti VIRTUALI nella subnet hello e NSG designato per il cluster di Service Fabric hello. Per questa esercitazione, il modello di gestione risorse di infrastruttura servizio hello è preconfigurato toouse hello nomi di hello rete virtuale, subnet e gruppo che è impostato nel passaggio precedente hello. 

modello di gestione risorse del cluster di Service Fabric Hello è toocreate configurato un cluster protetto con protezione certificati. certificato di Hello è comunicazione da nodo a nodo toosecure utilizzato per il cluster e il cluster di Service Fabric tooyour toomanage utente l'accesso. Gestione API utilizza questo hello tooaccess certificato servizio Service Fabric di denominazione per l'individuazione del servizio.

Per questo passaggio è necessario disporre di un certificato nel Key Vault per la sicurezza del cluster. Per ulteriori informazioni sull'impostazione di un cluster protetto con Key Vault, vedere [questa guida per la creazione di un cluster di Service Fabric mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).

> [!NOTE]
> In aggiunta toohello certificato utilizzato per l'accesso del cluster, è possibile aggiungere l'autenticazione di Azure Active Directory. Azure Active Directory è hello consigliato del cluster di Service Fabric tooyour modo toomanage utente l'accesso, ma è toocomplete non necessari in questa esercitazione. In entrambi i casi, è richiesto un certificato per la sicurezza del cluster da nodo a nodo e per l'autenticazione di Gestione API di Azure, che attualmente non supporta l'autenticazione con Azure Active Directory per un back-end di Service Fabric.

 1. Scaricare i seguenti file di modello e i parametri di gestione risorse hello:
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. Specificare parametri vuoto di hello in hello `cluster.parameters.json` file per la distribuzione, tra cui hello [informazioni chiave dell'insieme di credenziali](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) per il certificato del cluster.

 3. Utilizzare hello PowerShell comando toodeploy hello Gestione risorse modello e parametro file toocreate hello cluster di Service Fabric seguenti:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>Distribuire Gestione API

Infine, distribuire toohello API Gestione reti VIRTUALI nella subnet hello e NSG designato per la gestione API. Non è necessario toowait per hello Service Fabric cluster distribuzione toofinish prima della distribuzione di gestione API. 

Per questa esercitazione, il modello di gestione risorse di gestione API hello è preconfigurato toouse hello nomi di hello rete virtuale, subnet e gruppo che è impostato nel passaggio precedente hello. 

 1. Scaricare i seguenti file di modello e i parametri di gestione risorse hello:
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. Specificare parametri vuoto di hello in hello `apim.parameters.json` per la distribuzione.

 3. Utilizzare hello seguenti PowerShell comando toodeploy hello Gestione risorse modello e parametro file per la gestione API:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>Configurare Gestione API

Dopo aver distribuito Gestione API e il cluster di Service Fabric, è possibile configurare un back-end di Service Fabric in Gestione API. In questo modo toocreate un criterio del servizio back-end che invia i cluster di Service Fabric tooyour traffico.

### <a name="api-management-security"></a>Sicurezza di Gestione API

Service Fabric hello tooconfigure back-end, è necessario innanzitutto le impostazioni di sicurezza di gestione API tooconfigure. le impostazioni di sicurezza tooconfigure, andare tooyour API servizio di gestione nel portale di Azure hello.

#### <a name="enable-hello-api-management-rest-api"></a>Abilitare hello API REST gestione API

API REST gestione API Hello è attualmente hello solo modo tooconfigure un servizio back-end. primo passaggio Hello è hello tooenable API REST gestione API e proteggerla.

 1. Nel servizio Gestione API hello, selezionare **API di gestione - anteprima** in **sicurezza**.
 2. Controllare hello **Abilita API REST gestione API** casella di controllo.
 3. Nota hello URL delle API di gestione - URL hello utilizzeremo tooset successive di back-end di Service Fabric hello
 4. Genera un **Token di accesso** selezionando una data di scadenza e una chiave, quindi fare clic su hello **genera** pulsante verso il basso hello hello pagina.
 5. Hello copia **token di accesso** e salvarlo, che verrà usata in hello alla procedura seguente. Tenere presente che questo comportamento è diverso da hello di chiave primaria e secondaria.

#### <a name="upload-a-service-fabric-client-certificate"></a>Caricare un certificato client di Service Fabric

Gestione API deve eseguire l'autenticazione con il cluster di Service Fabric per l'individuazione del servizio mediante un certificato client con i cluster tooyour di accesso. Per semplicità, questa esercitazione viene utilizzato hello stesso certificato specificato durante la creazione di cluster di Service Fabric hello, che per impostazione predefinita può essere utilizzato tooaccess del cluster.

 1. Nel servizio Gestione API hello, selezionare **certificati Client - anteprima** in **sicurezza**.
 2. Fare clic su hello **+ Aggiungi** pulsante
 2. Selezionare hello file di chiave privata (con estensione pfx) del certificato cluster hello specificata durante la creazione del cluster di Service Fabric, assegnargli un nome e fornire una password della chiave privata hello.

> [!NOTE]
> Questa esercitazione Usa hello stesso certificato per la sicurezza del nodo a nodo cluster e di autenticazione client. Se si dispone di un tooaccess configurato il cluster di Service Fabric, è possibile utilizzare un certificato client separato.

### <a name="configure-hello-backend"></a>Configurare back-end hello

Ora che viene configurata la sicurezza di gestione API, è possibile configurare back-end di Service Fabric hello. Per back-end dell'infrastruttura di servizio, il cluster di Service Fabric hello è back-end hello, anziché uno specifico servizio di Service Fabric. In questo modo un toomore tooroute singolo criterio rispetto a un servizio cluster hello.

Questo passaggio richiede il token di accesso hello generati in precedenza e identificazione personale per il certificato del cluster che è stata caricata tooAPI Management nel passaggio precedente hello hello.

> [!NOTE]
> Se si utilizza un certificato client separato nel passaggio precedente hello di gestione API, è necessario identificazione personale hello per il certificato client hello in identificazione personale del certificato del cluster toohello aggiunta in questo passaggio.

Inviare hello seguente toohello di richiesta HTTP PUT URL API di gestione API annotati in precedenza durante l'abilitazione del servizio back-end di hello API REST gestione API tooconfigure hello Service Fabric. Verrà visualizzato un `HTTP 201 Created` risposta quando il comando hello ha esito positivo. Per ulteriori informazioni su ogni campo, vedere Gestione API hello [la documentazione di riferimento API back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).

Comando e URL HTTP:
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

Intestazioni della richiesta:
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

Corpo della richiesta:
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

Hello **url** parametro qui è un nome di servizio completo di un servizio del cluster che tutte le richieste vengono indirizzate tooby predefinito se è specificato alcun nome di servizio in un criterio di back-end. È possibile utilizzare un nome di servizio fittizio, ad esempio "fabric: / false/servizio" Se non si intende toohave un servizio di fallback.

Fare riferimento a gestione API toohello [la documentazione di riferimento API back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) per ulteriori informazioni su ogni campo.

#### <a name="example"></a>Esempio

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>Distribuire un servizio back-end di Service Fabric

Dopo aver creato hello che Service Fabric è configurato come un tooAPI back-end, gestione, è possibile creare criteri di back-end per le API che inviano traffico tooyour servizi di Service Fabric. Ma prima è necessario un servizio in esecuzione nelle richieste tooaccept Service Fabric.

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>Creare un servizio Service Fabric con un endpoint HTTP

Per questa esercitazione si creerà una base ASP.NET Core servizio Reliable senza stato con modello di progetto API Web hello predefinito. Questo permetterà di generare un endpoint HTTP per il servizio, che verrà esposto tramite Gestione API di Azure:

```
/api/values
```

Partire dall'[impostazione dell'ambiente per lo sviluppo di ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).

Dopo aver impostato l'ambiente di sviluppo, avviare Visual Studio come Amministratore e creare un servizio ASP.NET Core:

 1. In Visual Studio selezionare File -> Nuovo progetto.
 2. Selezionare il modello di applicazione di Service Fabric hello nel Cloud e denominarlo **"ApiApplication"**.
 3. Selezionare il modello di servizio ASP.NET Core hello e progetto hello nome **"WebApiService"**.
 4. Selezionare il modello di progetto di Web API ASP.NET Core 1.1 hello.
 5. Una volta creato il progetto di hello, aprire `PackageRoot\ServiceManifest.xml` e rimuovere hello `Port` attributo dalla configurazione di risorsa endpoint hello:
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    In questo modo toospecify Service Fabric una porta in modo dinamico da intervallo di porte applicazione hello, che è stata aperta tramite hello il gruppo di sicurezza di rete nel modello di gestione risorse di cluster hello, che consente il traffico tooflow tooit da Gestione API.
 
 6. Premere F5 nell'API web hello tooverify di Visual Studio sono disponibili localmente. 

    Aprire Service Fabric Explorer e il drill-down tooa istanza specifica di hello ASP.NET Core toosee hello indirizzo di base hello del servizio è in ascolto. Aggiungere `/api/values` toohello indirizzo di base e aprirlo in un browser. Viene richiamato il metodo Get su hello ValuesController nel modello API Web hello hello. Restituisce una risposta predefinita hello fornito dal modello hello, una matrice JSON contenente due stringhe:

    ```json
    ["value1", "value2"]`
    ```

    Si tratta di endpoint hello Esponi tramite Gestione API in Azure.

 7. Infine, distribuire cluster di tooyour applicazione hello in Azure. [Utilizzo di Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)del progetto di applicazione hello di mouse e scegliere **pubblica**. Specificare l'endpoint del cluster (ad esempio, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello applicazione tooyour dell'infrastruttura del servizio cluster in Azure.

In tale cluster dovrebbe essere ora in esecuzione un servizio ASP.NET Core senza stato denominato `fabric:/ApiApplication/WebApiService`.

## <a name="create-an-api-operation"></a>Creare un'operazione per le API

Ora siamo toocreate pronto un'operazione in Gestione API toocommunicate di utilizzare tale client esterni con hello servizio senza stato di ASP.NET Core in esecuzione nel cluster di Service Fabric hello.

 1. Accedi al portale di Azure toohello e passare tooyour distribuzione del servizio Gestione API.
 2. Nel Pannello di servizio di gestione API hello, selezionare **API - anteprima**
 3. Aggiungere una nuova API facendo hello **API vuoto** casella e compilare la finestra di dialogo hello:

     - **URL del servizio Web**: per i back-end di Service Fabric, questo valore URL non viene usato. È possibile inserire un valore qualsiasi nel campo. Per questa esercitazione, usare `http://servicefabric`.
     - **Nome**: inserire il nome dell'API. Per questa esercitazione, usare `Service Fabric App`.
     - **Schema URL**: selezionare HTTP, HTTPS o entrambi i valori. Per questa esercitazione, usare `both`.
     - **Suffisso URL API**: inserire un suffisso per l'API. Per questa esercitazione, usare `myapp`.
 
 4. Una volta creato hello API, fare clic su **+ Aggiungi operazione** operazione tooadd un'API front-end. Compilare i valori hello:
    
     - **URL**: selezionare `GET` e fornire un percorso URL per hello API. Per questa esercitazione, usare `/api/values`.
     
       Per impostazione predefinita, il percorso di URL hello specificato qui è il percorso di URL hello inviato toohello servizio di Service Fabric back-end. Se si utilizza hello stesso percorso URL di seguito in questo caso il servizio utilizza `/api/values`, quindi operazione hello funziona senza ulteriori modifiche. È inoltre possibile specificare un percorso URL qui è diverso dal percorso dell'URL hello utilizzato dal back-end del servizio Service Fabric, nel qual caso sarà anche necessario toospecify un percorso di riscrittura nei criteri di operazione in un secondo momento.
     - **Nome visualizzato**: fornire un nome qualsiasi per hello API. Per questa esercitazione, usare `Values`.

## <a name="configure-a-backend-policy"></a>Configurare un criterio di back-end

criteri di back-end Hello collega tutti gli elementi. Questo è possibile configurare hello back-end dell'infrastruttura di servizio vengono indirizzate le richieste di servizio toowhich. È possibile applicare l'operazione API tooany di criteri. Hello [configurazione back-end per l'infrastruttura del servizio](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) seguente hello richiesta di routing controlli: 
 - Selezione dell'istanza del servizio specificando un nome di istanza di servizio di Service Fabric, entrambi hardcoded (ad esempio, `"fabric:/myapp/myservice"`) o generato dalla richiesta hello HTTP (ad esempio, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).
 - Risoluzione della partizione mediante la generazione di una chiave di partizione che usa uno schema di partizionamento di Service Fabric.
 - Selezione della replica per i servizi con stato.
 - Risoluzione ripetere le condizioni che consentono di condizioni di hello toospecify per risolvere di nuovo una posizione del servizio e inviare una richiesta.

Per questa esercitazione, creare un criterio di back-end che le route richieste direttamente toohello servizio senza stato di ASP.NET Core distribuito in precedenza:

 1. Selezionare e modificare hello **in ingresso criteri** per hello `Values` operazione facendo clic sull'icona di modifica hello e quindi selezionando **visualizzazione codice**.
 2. Nell'editor di codice hello criteri, aggiungere un `set-backend-service` criteri in ingresso criteri, come illustrato di seguito e fare clic su hello **salvare** pulsante:
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

Per un set completo di attributi di criteri di back-end di Service Fabric, fare riferimento toohello [documentazione back-end di gestione API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>Aggiungere hello API tooa prodotto. 

Prima di chiamare API hello, è necessario aggiungerlo tooa prodotto in cui è possibile concedere l'accesso toousers. 

 1. Nel servizio Gestione API hello, selezionare **prodotti - anteprima**.
 2. Per impostazione predefinita, Gestione API include due prodotti: Starter e Illimitato. Selezionare prodotto illimitato hello.
 3. Selezionare API.
 4. Fare clic su hello **+ Aggiungi** pulsante.
 5. Seleziona hello `Service Fabric App` API creata nei passaggi precedenti hello e fare clic su hello **selezionare** pulsante.

### <a name="test-it"></a>Eseguirne il test

È possibile ritentare l'invio di un servizio back-end di tooyour richiesta nell'infrastruttura del servizio tramite Gestione API direttamente dal portale di Azure hello.

 1. Nel servizio Gestione API hello, selezionare **API - anteprima**.
 2. In hello `Service Fabric App` API creato nei passaggi precedenti hello, selezionare hello **Test** scheda.
 3. Fare clic su hello **inviare** pulsante toosend un servizio back-end di test richiesta toohello.

## <a name="next-steps"></a>Passaggi successivi

A questo punto, dovrebbe essere disponibile un'installazione di base con i servizi Service Fabric e Gestione API.

In questa esercitazione Usa l'autenticazione utente basata su certificati di base per impostare rapidamente il tooget di cluster Service Fabric. È consigliabile eseguire un'autenticazione utente più avanzata per il cluster di Service Fabric basata su [Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication). 

Successivamente, [creare e configurare le impostazioni di prodotto avanzate in Gestione API di Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare l'applicazione per il traffico reale.

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
