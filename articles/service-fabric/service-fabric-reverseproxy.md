---
title: proxy inverso aaaAzure Service Fabric | Documenti Microsoft
description: Utilizza un proxy inverso dell'infrastruttura servizio per la comunicazione toomicroservices dall'interno e all'esterno del cluster di hello.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Proxy inverso in Azure Service Fabric
proxy inverso Hello compilato in Azure Service Fabric indirizzi microservizi nel cluster di Service Fabric hello che espone gli endpoint HTTP.

## <a name="microservices-communication-model"></a>Modello di comunicazione di microservizi
Microservizi nell'infrastruttura del servizio in genere eseguiti su un sottoinsieme di macchine virtuali nel cluster hello e spostarsi da una macchina virtuale tooanother per vari motivi. In tal caso, gli endpoint di hello per microservizi può essere modificato dinamicamente. Hello tipico modello toocommunicate toohello microservizio è seguente hello risolvere ciclo:

1. Risolvere il percorso del servizio hello inizialmente tramite servizio di denominazione hello.
2. Connettere il servizio toohello.
3. Determinare hello causa degli errori di connessione e risolvere nuovo percorso del servizio di hello quando necessario.

Questo processo è in genere implica il wrapping delle librerie di comunicazione client-side in un ciclo di tentativi che implementa criteri di risoluzione e ripetere servizi hello.
Per altre informazioni, vedere [Connettersi e comunicare con i servizi](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>La comunicazione tramite proxy inverso hello
proxy inverso di Hello nell'infrastruttura del servizio viene eseguito su tutti i nodi nel cluster hello hello. Consente di processo di risoluzione hello intero servizio per conto del client e inoltra la richiesta di hello del client. In tal caso, i client in esecuzione nel cluster hello possono usare qualsiasi servizio di destinazione di sul lato client HTTP comunicazione librerie tootalk toohello mediante un proxy inverso di hello che viene eseguito localmente su hello stesso nodo.

![Comunicazione interna][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Raggiungere microservizi dal cluster hello esterno
modello di comunicazione esterna Hello predefinito per microservizi è un modello di consenso esplicito in ogni servizio può accedervi direttamente da client esterni. [Il bilanciamento del carico Azure](../load-balancer/load-balancer-overview.md), che è un limite di rete tra microservizi e i client esterni, esegue la conversione degli indirizzi di rete e che esegue l'inoltro esterno richiede toointernal creato endpoint. toomake client di tooexternal direttamente accessibile del microservizio un endpoint, è innanzitutto necessario configurare il bilanciamento del carico tooforward traffico tooeach porta che hello servizio utilizza cluster hello. Inoltre, la maggior parte delle microservizi, soprattutto con stato microservizi, non in tempo reale su tutti i nodi del cluster di hello. Hello microservizi possono spostare tra i nodi di failover. In questi casi, bilanciamento del carico non è possibile determinare in modo efficace percorso hello del nodo di destinazione hello di hello repliche toowhich inoltra il traffico.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Raggiungere microservizi attraverso il proxy inverso hello dal cluster hello esterno
Anziché configurare una porta hello di un singolo servizio di bilanciamento del carico, è possibile configurare solo hello porta proxy inverso hello nel servizio di bilanciamento del carico. Questa configurazione consente ai client esterni a cluster hello raggiungere servizi all'interno di cluster hello tramite proxy inverso di hello senza alcuna configurazione aggiuntiva.

![Comunicazione esterna][0]

> [!WARNING]
> Quando si configura la porta del proxy inverso hello in servizio di bilanciamento del carico, sono indirizzabili da all'esterno del cluster hello microservizi tutti i cluster hello che espongono un endpoint HTTP.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Formato dell'URI per l'indirizzamento di servizi mediante un proxy inverso hello
Usa proxy inverso di Hello che deve essere inoltrata un'URI specifico identifier (URI) formato tooidentify hello partizione toowhich hello in arrivo richiesta di servizio:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http (s):** proxy inverso hello può essere configurato tooaccept HTTP o il traffico HTTPS. Per l'inoltro di HTTPS, fare riferimento troppo[connessione servizio protetto tooa con proxy inverso hello](service-fabric-reverseproxy-configure-secure-communication.md) dopo aver toolisten il programma di installazione di proxy inverso su HTTPS.
* **Nome del cluster nome di dominio completo (FQDN) | indirizzo IP interno:** per i client esterni, è possibile configurare proxy inverso hello in modo che sia raggiungibile tramite dominio cluster hello, ad esempio mycluster.eastus.cloudapp.azure.com. Per impostazione predefinita, i proxy inverso hello viene eseguito in ogni nodo. Per il traffico interno, proxy inverso hello può essere raggiunto in localhost o in qualsiasi indirizzo IP nodo interno, ad esempio 10.0.0.1.
* **Porta:** porta hello, ad esempio 19081, che è stato specificato per il proxy inverso hello.
* **ServiceInstanceName:** hello di nome completo dell'istanza di servizio hello distribuito che si sta tentando di tooreach senza hello "fabric: /" dello schema. Ad esempio, tooreach hello *fabric: / myapp/myservice/* servizio, si utilizzerebbe *myapp/myservice*.

    nome dell'istanza del servizio Hello è tra maiuscole e minuscole. Utilizzando una maiuscole/minuscole del nome di istanza servizio hello nell'URL hello determina hello richieste toofail con 404 (non trovato).
* **Percorso di suffisso:** si tratta di percorso URL effettivo hello, ad esempio *myapi/valori/Aggiungi/3*, per il servizio di hello che si desidera tooconnect per.
* **PartitionKey:** per un servizio partizionato, si tratta di chiave di partizione calcolata hello della partizione hello che si desidera tooreach. Si noti che questo *non* hello GUID dell'ID di partizione. Questo parametro non è obbligatorio per i servizi che utilizzano lo schema di partizione singleton hello.
* **PartitionKind:** schema di partizione del servizio hello. Può essere "Int64Range" o "Named". Questo parametro non è obbligatorio per i servizi che utilizzano lo schema di partizione singleton hello.
* **ListenerName** endpoint hello dal servizio hello sono hello formato {"Endpoint": {"Listener1": "Endpoint1", "Listener2": "Endpoint2"...}}. Quando il servizio di hello espone più endpoint, endpoint hello identifica tale richiesta hello del client deve essere inoltrato a. Può essere omesso se hello servizio dispone di un solo listener.
* **TargetReplicaSelector** specifica come replica di destinazione hello o istanza deve essere selezionata.
  * Quando il servizio di destinazione hello è con stato, può essere uno dei seguenti hello hello TargetReplicaSelector: 'PrimaryReplica', 'RandomSecondaryReplica' o 'RandomReplica'. Quando questo parametro viene omesso, il valore predefinito di hello è 'PrimaryReplica'.
  * Quando il servizio di destinazione hello è senza stato, proxy inverso prende un'istanza di hello partizione tooforward hello richiesta al servizio per casuale.
* **Timeout:** specifica hello timeout per la richiesta HTTP hello creato dal servizio di toohello hello proxy inverso per conto di richiesta di hello del client. valore predefinito di Hello è 60 secondi. Questo è un parametro facoltativo.

### <a name="example-usage"></a>Esempio di utilizzo
Ad esempio, è opportuno hello *fabric: / MyApp/MyService* servizio che consente di aprire un listener HTTP sull'hello URL seguente:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Di seguito sono risorse hello per il servizio di hello:

* `/index.html`
* `/api/users/<userId>`

Se il servizio di hello utilizza singleton hello schema di partizionamento, hello *PartitionKey* e *PartitionKind* parametri di stringa di query non sono necessari e servizio hello può essere raggiunto tramite gateway hello come:

* Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Internamente: `http://localhost:19081/MyApp/MyService`

Se il servizio di hello utilizza hello Int64 uniformi schema di partizionamento, hello *PartitionKey* e *PartitionKind* i parametri di stringa di query devono essere utilizzato tooreach una partizione del servizio hello:

* Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

risorse hello tooreach che espone il servizio di hello, posizionare semplicemente percorso della risorsa hello dopo il nome del servizio hello hello URL:

* Esternamente: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Internamente: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

gateway Hello inoltrerà quindi URL del servizio toohello queste richieste:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Gestione speciale per servizi di condivisione porta
Gateway applicazione Azure tenta tooresolve un servizio risolvere nuovamente e ripetere la richiesta di hello quando un servizio non è raggiungibile. Si tratta dei principali vantaggi di Gateway applicazione perché il codice client non necessario tooimplement risoluzione per il proprio servizio e risolvere il ciclo.

In genere, quando un servizio non è raggiungibile, l'istanza del servizio hello o la replica è stato spostato tooa nodo diverso come parte del ciclo di vita normale. In questo caso, Gateway applicazione potrebbe ricevere un rete connessione errore che indica che un endpoint non aperto più hello risolto originariamente indirizzo.

Tuttavia, le repliche o le istanze del servizio possono condividere un processo host e una porta quando ospitate da un server Web basato su http.sys, tra cui:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [WebListener ASP.NET Core](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

In questo caso, è probabile che il server web hello è disponibile nel processo host hello e risponde toorequests ma hello risolto l'istanza del servizio o di replica non è più disponibile nell'host di hello. In questo caso, i gateway hello riceverà una risposta HTTP 404 dal server web hello. Un errore HTTP 404 presenta quindi due significati distinti:

- Caso #1: indirizzo del servizio hello è corretto, ma la risorsa hello che hello l'utente ha richiesto non esiste.
- Caso &#2;: indirizzo del servizio hello è corretto e potrebbe esistere risorsa hello hello richiesto dall'utente in un nodo diverso.

Hello primo caso è un normale HTTP 404, che è considerata un errore dell'utente. Tuttavia, nel secondo caso hello utente hello ha richiesto una risorsa che esiste. Gateway applicazione è stato Impossibile toolocate che è stato spostato perché hello servizio stesso. Applicazione esigenze tooresolve hello indirizzo Gateway nuovamente e ripetere la richiesta hello.

Gateway applicazione deve pertanto un toodistinguish modo tra questi due casi. toomake che distinzione, un suggerimento dal server hello è necessario.

* Per impostazione predefinita, il Gateway applicazione presuppone caso &#2; e tenta nuovamente di richiesta hello tooresolve e il problema.
* tooindicate caso &#1; tooApplication Gateway, il servizio di hello deve restituire hello intestazione risposta HTTP seguenti:

  `X-ServiceFabric : ResourceNotFound`

L'intestazione della risposta HTTP indica una situazione di HTTP 404 normale in cui hello risorsa richiesta non esiste e il Gateway applicazione non tenterà nuovamente indirizzo del servizio tooresolve hello.

## <a name="setup-and-configuration"></a>Installazione e configurazione

### <a name="enable-reverse-proxy-via-azure-portal"></a>Abilitare il proxy inverso tramite il portale di Azure

Portale di Azure fornisce un proxy inverso di opzione tooenable durante la creazione di un nuovo cluster di Service Fabric.
In **cluster di Service Fabric crea**, passaggio 2: configurazione del Cluster, configurazione del tipo di nodo, selezionare la casella di controllo di hello troppo "Abilitazione proxy inverso".
Per la configurazione di proxy inverso sicura, è possibile specificare il certificato SSL nel passaggio 3: protezione, configurare le impostazioni di sicurezza cluster, la casella di controllo selezionare hello troppo "Include un certificato SSL per il proxy inverso" e immettere i dettagli del certificato hello.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Abilitare il proxy inverso tramite modelli di Azure Resource Manager

È possibile utilizzare hello [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) tooenable hello proxy inverso nell'infrastruttura del servizio per cluster hello.

Fare riferimento troppo[Proxy inverso HTTPS di configurare in un cluster protetto](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) per Gestione risorse di Azure tooconfigure proxy inverso protetta con un rollover dei certificati di certificato e la gestione degli esempi di modello.

In primo luogo, si ottiene il modello di hello per cluster hello che si desidera toodeploy. È possibile utilizzare i modelli di esempio hello o creare un modello di gestione risorse personalizzato. Quindi, è possibile abilitare i proxy inverso hello utilizzando hello alla procedura seguente:

1. Definire una porta per il proxy inverso hello in hello [sezione parametri](../azure-resource-manager/resource-group-authoring-templates.md) del modello di hello.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Specificare la porta hello per tutti gli oggetti di tipo di nodo hello in hello **Cluster** [sezione tipo di risorsa](../azure-resource-manager/resource-group-authoring-templates.md).

    porta Hello è identificata dal nome del parametro hello, reverseProxyEndpointPort.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. hello tooaddress proxy inverso da hello all'esterno del cluster di Azure, imposta le regole di bilanciamento del carico di Azure hello per la porta hello specificata nel passaggio 1.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. i certificati SSL tooconfigure sulla porta hello di proxy inverso hello, aggiungere hello certificato toohello ***reverseProxyCertificate*** proprietà hello **Cluster** [sezionetipodirisorsa](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Supporto di un certificato di proxy inverso che è diverso dal certificato cluster hello
 Se il certificato di proxy inverso hello è diverso dal certificato hello che protegge cluster hello, quindi hello specificato in precedenza certificato deve essere installato nella macchina virtuale hello e aggiunti toohello elenco di controllo di accesso (ACL) in modo che possano Service Fabric diritti di accesso. Questa operazione può essere eseguita in hello **virtualMachineScaleSets** [sezione tipo di risorsa](../resource-group-authoring-templates.md). Per l'installazione, aggiungere tale osProfile toohello certificato. sezione di estensione Hello del modello di hello è possibile aggiornare il certificato di hello in hello ACL.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Quando si usano i certificati che sono diversi da hello cluster certificato tooenable hello proxy inverso di un cluster esistente, installare il certificato di proxy inverso hello e aggiornare hello ACL nel cluster hello prima di abilitare proxy inverso hello. Hello completo [modello di Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) distribuzione usando le impostazioni di hello menzionate in precedenza prima di avviare un proxy inverso di distribuzione tooenable hello in passaggi 1-4.

## <a name="next-steps"></a>Passaggi successivi
* Vedere un esempio di comunicazione HTTP tra i servizi in un [progetto di esempio in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [Servizio HTTP toosecure di inoltro con proxy inverso hello](service-fabric-reverseproxy-configure-secure-communication.md)
* [Chiamate di procedura remota con i Reliable Services remoti](service-fabric-reliable-services-communication-remoting.md)
* [Web API che usa OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicazione di WCF tramite Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* Per altre opzioni di configurazione del proxy inverso, vedere la sezione ApplicationGateway/Http in [Personalizzare le impostazioni del cluster Service Fabric](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
