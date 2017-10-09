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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="b198c-103">Servizio DNS in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b198c-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="b198c-104">Hello servizio DNS è un servizio di sistema facoltativo che è possibile abilitare il toodiscover cluster altri servizi che utilizzano il protocollo DNS hello.</span><span class="sxs-lookup"><span data-stu-id="b198c-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="b198c-105">Molti servizi, in particolare nei contenitori, possono avere un nome URL esistente e che sia in grado di tooresolve li utilizzando il protocollo DNS standard di hello (anziché il protocollo di Naming Service hello) è utile, in particolare in scenari "sollevare e spostare".</span><span class="sxs-lookup"><span data-stu-id="b198c-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="b198c-106">Hello servizio DNS consente si toomap nomi tooa servizio nome DNS e quindi risolvere indirizzi IP degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="b198c-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="b198c-107">Hello servizio DNS esegue il mapping di nomi tooservice i nomi DNS, che a sua volta vengono risolti dall'endpoint del servizio hello tooreturn hello Naming Service.</span><span class="sxs-lookup"><span data-stu-id="b198c-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="b198c-108">nome DNS Hello hello servizio viene fornito al momento di hello della creazione.</span><span class="sxs-lookup"><span data-stu-id="b198c-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Endpoint del servizio][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="b198c-110">Abilitazione del servizio DNS hello</span><span class="sxs-lookup"><span data-stu-id="b198c-110">Enabling hello DNS service</span></span>
<span data-ttu-id="b198c-111">È necessario innanzitutto il servizio DNS tooenable hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="b198c-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="b198c-112">Ottiene il modello di hello per cluster hello che si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b198c-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="b198c-113">È possibile l'uso hello [modelli di esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) oppure creare un modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="b198c-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="b198c-114">È possibile abilitare il servizio DNS hello con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b198c-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="b198c-115">Verificare che hello `apiversion` è troppo`2017-07-01-preview` per hello `Microsoft.ServiceFabric/clusters` risorsa e in caso contrario, lo aggiorna come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="b198c-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="b198c-116">Ora abilitare il servizio DNS hello aggiungendo segue hello `addonFeatures` sezione dopo hello `fabricSettings` sezione come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="b198c-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="b198c-117">Dopo aver aggiornato il modello di cluster con hello precedente le modifiche, applicarli e consentire l'aggiornamento completo hello.</span><span class="sxs-lookup"><span data-stu-id="b198c-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="b198c-118">Al termine dell'operazione, il servizio di sistema DNS hello viene avviata l'esecuzione del cluster che viene chiamato `fabric:/System/DnsService` nella sezione di servizio di sistema in Esplora Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="b198c-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="b198c-119">In alternativa, è possibile abilitare il servizio DNS tramite il portale di hello hello in fase di creazione del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="b198c-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="b198c-120">Hello servizio DNS può essere abilitata selezionando la casella hello per `Include DNS service` in hello `Cluster configuration` menu come illustrato nella seguente schermata hello:</span><span class="sxs-lookup"><span data-stu-id="b198c-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Abilitazione del servizio DNS tramite il portale di hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="b198c-122">Impostazione hello del nome DNS per il servizio</span><span class="sxs-lookup"><span data-stu-id="b198c-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="b198c-123">Una volta hello servizio DNS è in esecuzione nel cluster, è possibile impostare un nome DNS per i servizi in modo dichiarativo per servizi predefiniti in hello `ApplicationManifest.xml` o tramite i comandi di Powershell.</span><span class="sxs-lookup"><span data-stu-id="b198c-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="b198c-124">Impostazione del nome DNS hello per un servizio predefinito in ApplicationManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="b198c-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="b198c-125">Aprire il progetto in Visual Studio o l'editor preferito e hello `ApplicationManifest.xml` file.</span><span class="sxs-lookup"><span data-stu-id="b198c-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="b198c-126">Passare sezione servizi toohello predefinito e per ogni hello Aggiungi servizio `ServiceDnsName` attributo.</span><span class="sxs-lookup"><span data-stu-id="b198c-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="b198c-127">Hello di esempio seguente viene illustrato come tooset hello nome DNS del servizio hello troppo`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="b198c-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="b198c-128">Una volta distribuita un'applicazione hello, istanza servizio hello in hello Service Fabric explorer Mostra il nome DNS hello per questa istanza, come illustrato nella seguente illustrazione hello:</span><span class="sxs-lookup"><span data-stu-id="b198c-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![Endpoint del servizio][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="b198c-130">Impostazione del nome DNS hello per un servizio tramite Powershell</span><span class="sxs-lookup"><span data-stu-id="b198c-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="b198c-131">È possibile impostare il nome DNS hello per un servizio quando viene creata utilizzando hello `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="b198c-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="b198c-132">Hello seguente viene creato un nuovo servizio senza stato con nome DNS hello`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="b198c-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="b198c-133">Uso del protocollo DNS nei servizi</span><span class="sxs-lookup"><span data-stu-id="b198c-133">Using DNS in your services</span></span>
<span data-ttu-id="b198c-134">Se si distribuisce più di un servizio, è possibile trovare l'endpoint di hello di toocommunicate altri servizi con utilizzando un nome DNS.</span><span class="sxs-lookup"><span data-stu-id="b198c-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="b198c-135">Hello servizio DNS è solo servizi toostateless applicabile, poiché hello protocollo DNS non è possibile comunicare con i servizi con stati.</span><span class="sxs-lookup"><span data-stu-id="b198c-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="b198c-136">Per i servizi con stati, è possibile utilizzare i proxy inverso incorporato hello per toocall chiamate http una partizione specifica del servizio.</span><span class="sxs-lookup"><span data-stu-id="b198c-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="b198c-137">Hello codice seguente viene illustrato come toocall un altro servizio, è semplicemente un regolare http chiama in cui fornire porta hello e qualsiasi percorso facoltativi come parte dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="b198c-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b198c-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b198c-138">Next steps</span></span>
<span data-ttu-id="b198c-139">Ulteriori informazioni sulla comunicazione tra servizi all'interno di cluster hello con [connettersi e comunicare con i servizi](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="b198c-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
