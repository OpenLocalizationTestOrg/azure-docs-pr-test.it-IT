---
title: Servizio DNS di Azure Service Fabric | Microsoft Docs
description: Usare il servizio DNS di Service Fabric per individuare microservizi dall'interno del cluster.
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
ms.openlocfilehash: 9871bc5aa4e74ab0faef401d67c4e9558eb5e14b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="48ff0-103">Servizio DNS in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="48ff0-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="48ff0-104">Il servizio DNS è un servizio di sistema facoltativo che è possibile abilitare nel cluster per individuare altri servizi usando il protocollo DNS.</span><span class="sxs-lookup"><span data-stu-id="48ff0-104">The DNS Service is an optional system service that you can enable in your cluster to discover other services using the DNS protocol.</span></span>

<span data-ttu-id="48ff0-105">Molti servizi, in particolare quelli in contenitori, possono avere un nome di URL esistente. La possibilità di risolverli usando il protocollo DNS standard, invece del protocollo di servizio Naming, è preferibile, in particolare negli scenari di applicazioni "lift-and-shift".</span><span class="sxs-lookup"><span data-stu-id="48ff0-105">Many services, especially containerized services, can have an existing URL name, and being able to resolve them using the standard DNS protocol (rather than the Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="48ff0-106">Il servizio DNS consente di eseguire il mapping di nomi DNS a nomi di servizi e di conseguenza di risolvere gli indirizzi IP degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="48ff0-106">The DNS service enables you to map DNS names to a service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="48ff0-107">Il servizio DNS esegue il mapping dei nomi DNS ai nomi di servizi, che vengono quindi risolti dal servizio Naming per restituire l'endpoint di servizio.</span><span class="sxs-lookup"><span data-stu-id="48ff0-107">The DNS service maps DNS names to service names, which in turn are resolved by the Naming Service to return the service endpoint.</span></span> <span data-ttu-id="48ff0-108">Il nome DNS per il servizio viene fornito al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="48ff0-108">The DNS name for the service is provided at the time of creation.</span></span> 

![Endpoint del servizio][0]

## <a name="enabling-the-dns-service"></a><span data-ttu-id="48ff0-110">Abilitazione del servizio DNS</span><span class="sxs-lookup"><span data-stu-id="48ff0-110">Enabling the DNS service</span></span>
<span data-ttu-id="48ff0-111">È innanzitutto necessario abilitare il servizio DNS nel cluster.</span><span class="sxs-lookup"><span data-stu-id="48ff0-111">First you need to enable the DNS service in your cluster.</span></span> <span data-ttu-id="48ff0-112">Ottenere il modello per il cluster che si vuole distribuire.</span><span class="sxs-lookup"><span data-stu-id="48ff0-112">Get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="48ff0-113">È possibile usare i [modelli di esempio](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) o creare un modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48ff0-113">You can either use the [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="48ff0-114">Per abilitare il servizio DNS, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="48ff0-114">You can enable the DNS service with the following steps:</span></span>

1. <span data-ttu-id="48ff0-115">Verificare che `apiversion` sia impostato su `2017-07-01-preview` per la risorsa `Microsoft.ServiceFabric/clusters` e, se non lo è, aggiornarlo come illustrato nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="48ff0-115">Check that the `apiversion` is set to `2017-07-01-preview` for the `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in the following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="48ff0-116">A questo punto abilitare il servizio DNS aggiungendo la sezione `addonFeatures` seguente dopo la sezione `fabricSettings`, come illustrato nel frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="48ff0-116">Now enable the DNS service by adding the following `addonFeatures` section after the `fabricSettings` section as shown in the following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="48ff0-117">Dopo avere aggiornato il modello di cluster con le modifiche precedenti, applicarle e consentire il completamento dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="48ff0-117">Once you have updated your cluster template with the preceding changes, apply them and let the upgrade complete.</span></span> <span data-ttu-id="48ff0-118">Dopo aver completato l'aggiornamento, viene avviata l'esecuzione nel cluster del servizio di sistema DNS, denominato `fabric:/System/DnsService`, sotto la sezione dei servizi di sistema in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="48ff0-118">Once complete, the DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in the Service Fabric explorer.</span></span> 

<span data-ttu-id="48ff0-119">In alternativa, è possibile abilitare il servizio DNS tramite il portale durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="48ff0-119">Alternatively, you can enable the DNS service through the portal at the time of cluster creation.</span></span> <span data-ttu-id="48ff0-120">Il servizio DNS può essere abilitato selezionando la casella per `Include DNS service` nel menu `Cluster configuration`, come illustrato nello screenshot seguente:</span><span class="sxs-lookup"><span data-stu-id="48ff0-120">The DNS service can be enabled by checking the box for `Include DNS service` in the `Cluster configuration` menu as shown in the following screenshot:</span></span>

![Abilitazione del servizio DNS tramite il portale][2]


## <a name="setting-the-dns-name-for-your-service"></a><span data-ttu-id="48ff0-122">Impostazione del nome DNS del servizio</span><span class="sxs-lookup"><span data-stu-id="48ff0-122">Setting the DNS name for your service</span></span>
<span data-ttu-id="48ff0-123">Quando il servizio DNS è in esecuzione nel cluster, è possibile impostare un nome DNS per i servizi in modo dichiarativo per i servizi predefiniti in `ApplicationManifest.xml` oppure tramite i comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48ff0-123">Once the DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in the `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-the-dns-name-for-a-default-service-in-the-applicationmanifestxml"></a><span data-ttu-id="48ff0-124">Impostazione del nome DNS per un servizio predefinito nel file ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="48ff0-124">Setting the DNS name for a default service in the ApplicationManifest.xml</span></span>
<span data-ttu-id="48ff0-125">Aprire il progetto in Visual Studio, o nell'editor preferito, quindi aprire il file `ApplicationManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="48ff0-125">Open your project in Visual Studio, or your favorite editor, and open the `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="48ff0-126">Passare alla sezione relativa ai servizi predefiniti e per ciascuno di esso aggiungere l'attributo `ServiceDnsName`.</span><span class="sxs-lookup"><span data-stu-id="48ff0-126">Go to the default services section, and for each service add the `ServiceDnsName` attribute.</span></span> <span data-ttu-id="48ff0-127">Nell'esempio seguente viene mostrato come impostare il nome DNS del servizio su `service1.application1`</span><span class="sxs-lookup"><span data-stu-id="48ff0-127">The following example shows how to set the DNS name of the service to `service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="48ff0-128">Dopo aver distribuito l'applicazione, l'istanza del servizio in Service Fabric Explorer visualizza il nome DNS di tale istanza, come mostrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="48ff0-128">Once the application is deployed, the service instance in the Service Fabric explorer shows the DNS name for this instance, as shown in the following figure:</span></span> 

![Endpoint del servizio][1]

### <a name="setting-the-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="48ff0-130">Impostazione del nome DNS per un servizio mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="48ff0-130">Setting the DNS name for a service using Powershell</span></span>
<span data-ttu-id="48ff0-131">È possibile impostare il nome DNS di un servizio al momento della creazione usando `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="48ff0-131">You can set the DNS name for a service when creating it using the `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="48ff0-132">Nell'esempio seguente viene creato un nuovo servizio senza stato con il nome DNS `service1.application1`</span><span class="sxs-lookup"><span data-stu-id="48ff0-132">The following example creates a new stateless service with the DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="48ff0-133">Uso del protocollo DNS nei servizi</span><span class="sxs-lookup"><span data-stu-id="48ff0-133">Using DNS in your services</span></span>
<span data-ttu-id="48ff0-134">Se si distribuisce più di un servizio, è possibile trovare gli endpoint di altri servizi con cui comunicare usando un nome DNS.</span><span class="sxs-lookup"><span data-stu-id="48ff0-134">If you deploy more than one service, you can find the endpoints of other services to communicate with  by using a DNS name.</span></span> <span data-ttu-id="48ff0-135">Il servizio DNS è valido solo per i servizi senza stato perché il protocollo DNS non può comunicare con i servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="48ff0-135">The DNS service is only applicable to stateless services, since the DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="48ff0-136">Per i servizi con stato, è possibile usare il proxy inverso predefinito in modo che le chiamate HTTP siano dirette a una particolare partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="48ff0-136">For stateful services, you can use the built-in reverse proxy for http calls to call a particular service partition.</span></span>

<span data-ttu-id="48ff0-137">Il codice seguente illustra come chiamare un altro servizio. Si tratta semplicemente di una normale chiamata HTTP in cui si specificano la porta ed eventuali percorsi facoltativi come parte dell'URL.</span><span class="sxs-lookup"><span data-stu-id="48ff0-137">The following code shows how to call another service, which is simply a regular http call where you provide the port and any optional path as part of the URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="48ff0-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48ff0-138">Next steps</span></span>
<span data-ttu-id="48ff0-139">Per altre informazioni sulla comunicazione tra i servizi all'interno del cluster, vedere [Connettersi e comunicare con i servizi in Service Fabric](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="48ff0-139">Learn more about service communication within the cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
