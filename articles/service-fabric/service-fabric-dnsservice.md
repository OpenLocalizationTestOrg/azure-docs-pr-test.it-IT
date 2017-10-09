---
title: servizio Service Fabric DNS aaaAzure | Documenti Microsoft
description: Il servizio dns dell'infrastruttura servizio per l'individuazione di microservizi da utilizzare all'interno di cluster hello.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Servizio DNS in Azure Service Fabric
Hello servizio DNS è un servizio di sistema facoltativo che è possibile abilitare il toodiscover cluster altri servizi che utilizzano il protocollo DNS hello.

Molti servizi, in particolare nei contenitori, possono avere un nome URL esistente e che sia in grado di tooresolve li utilizzando il protocollo DNS standard di hello (anziché il protocollo di Naming Service hello) è utile, in particolare in scenari "sollevare e spostare". Hello servizio DNS consente si toomap nomi tooa servizio nome DNS e quindi risolvere indirizzi IP degli endpoint. 

Hello servizio DNS esegue il mapping di nomi tooservice i nomi DNS, che a sua volta vengono risolti dall'endpoint del servizio hello tooreturn hello Naming Service. nome DNS Hello hello servizio viene fornito al momento di hello della creazione. 

![Endpoint del servizio][0]

## <a name="enabling-hello-dns-service"></a>Abilitazione del servizio DNS hello
È necessario innanzitutto il servizio DNS tooenable hello del cluster. Ottiene il modello di hello per cluster hello che si desidera toodeploy. È possibile l'uso hello [modelli di esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) oppure creare un modello di gestione risorse. È possibile abilitare il servizio DNS hello con hello alla procedura seguente:

1. Verificare che hello `apiversion` è troppo`2017-07-01-preview` per hello `Microsoft.ServiceFabric/clusters` risorsa e in caso contrario, lo aggiorna come illustrato nel seguente frammento di codice hello:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Ora abilitare il servizio DNS hello aggiungendo segue hello `addonFeatures` sezione dopo hello `fabricSettings` sezione come illustrato nel seguente frammento di codice hello: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. Dopo aver aggiornato il modello di cluster con hello precedente le modifiche, applicarli e consentire l'aggiornamento completo hello. Al termine dell'operazione, il servizio di sistema DNS hello viene avviata l'esecuzione del cluster che viene chiamato `fabric:/System/DnsService` nella sezione di servizio di sistema in Esplora Service Fabric hello. 

In alternativa, è possibile abilitare il servizio DNS tramite il portale di hello hello in fase di creazione del cluster di hello. Hello servizio DNS può essere abilitata selezionando la casella hello per `Include DNS service` in hello `Cluster configuration` menu come illustrato nella seguente schermata hello:

![Abilitazione del servizio DNS tramite il portale di hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Impostazione hello del nome DNS per il servizio
Una volta hello servizio DNS è in esecuzione nel cluster, è possibile impostare un nome DNS per i servizi in modo dichiarativo per servizi predefiniti in hello `ApplicationManifest.xml` o tramite i comandi di Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Impostazione del nome DNS hello per un servizio predefinito in ApplicationManifest.xml hello
Aprire il progetto in Visual Studio o l'editor preferito e hello `ApplicationManifest.xml` file. Passare sezione servizi toohello predefinito e per ogni hello Aggiungi servizio `ServiceDnsName` attributo. Hello di esempio seguente viene illustrato come tooset hello nome DNS del servizio hello troppo`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
Una volta distribuita un'applicazione hello, istanza servizio hello in hello Service Fabric explorer Mostra il nome DNS hello per questa istanza, come illustrato nella seguente illustrazione hello: 

![Endpoint del servizio][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Impostazione del nome DNS hello per un servizio tramite Powershell
È possibile impostare il nome DNS hello per un servizio quando viene creata utilizzando hello `New-ServiceFabricService` Powershell. Hello seguente viene creato un nuovo servizio senza stato con nome DNS hello`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>Uso del protocollo DNS nei servizi
Se si distribuisce più di un servizio, è possibile trovare l'endpoint di hello di toocommunicate altri servizi con utilizzando un nome DNS. Hello servizio DNS è solo servizi toostateless applicabile, poiché hello protocollo DNS non è possibile comunicare con i servizi con stati. Per i servizi con stati, è possibile utilizzare i proxy inverso incorporato hello per toocall chiamate http una partizione specifica del servizio.

Hello codice seguente viene illustrato come toocall un altro servizio, è semplicemente un regolare http chiama in cui fornire porta hello e qualsiasi percorso facoltativi come parte dell'URL hello.

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sulla comunicazione tra servizi all'interno di cluster hello con [connettersi e comunicare con i servizi](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
