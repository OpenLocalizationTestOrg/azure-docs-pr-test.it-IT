---
title: gli endpoint del servizio Service Fabric aaaSpecifying | Documenti Microsoft
description: "Il manifesto toodescribe risorse di endpoint in un servizio, compresa la modalità tooset degli endpoint HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="447bd-103">Specificare le risorse in un manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="447bd-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="447bd-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="447bd-104">Overview</span></span>
<span data-ttu-id="447bd-105">manifesto del servizio Hello consente le risorse usate da hello servizio toobe dichiarato modificato senza modificare il codice compilato hello.</span><span class="sxs-lookup"><span data-stu-id="447bd-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="447bd-106">Azure Service Fabric supporta la configurazione delle risorse di endpoint per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="447bd-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="447bd-107">è possibile controllare le risorse di toohello accesso Hello specificate nel manifesto del servizio hello tramite hello SecurityGroup nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="447bd-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="447bd-108">dichiarazione di Hello delle risorse consente toobe queste risorse modificato in fase di distribuzione, vale a dire servizio hello non deve necessariamente toointroduce un nuovo meccanismo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="447bd-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="447bd-109">viene installato con hello Service Fabric SDK Hello definizione dello schema per il file ServiceManifest.xml hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="447bd-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="447bd-110">Endpoint</span><span class="sxs-lookup"><span data-stu-id="447bd-110">Endpoints</span></span>
<span data-ttu-id="447bd-111">Quando una risorsa endpoint viene definita nel manifesto del servizio hello, Service Fabric assegna le porte dall'intervallo di porte riservata hello applicazione quando non è specificata una porta in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="447bd-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="447bd-112">Ad esempio, esaminare endpoint hello *ServiceEndpoint1* specificato nel frammento di manifesto hello fornito dopo il paragrafo.</span><span class="sxs-lookup"><span data-stu-id="447bd-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="447bd-113">Inoltre, i servizi possono richiedere anche una porta specifica in una risorsa.</span><span class="sxs-lookup"><span data-stu-id="447bd-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="447bd-114">Le repliche del servizio in esecuzione in nodi di cluster diversi possono essere assegnate diversi numeri di porta, mentre le repliche di un servizio in esecuzione su hello stessa porta hello condivisione di nodo.</span><span class="sxs-lookup"><span data-stu-id="447bd-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="447bd-115">repliche servizio Hello è quindi possono utilizzare queste porte come necessario per la replica e per le richieste client in ascolto.</span><span class="sxs-lookup"><span data-stu-id="447bd-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="447bd-116">Fare riferimento troppo[configurazione servizi affidabili con stato](service-fabric-reliable-services-configuration.md) tooread ulteriori informazioni sull'endpoint di riferimento dal file di impostazioni pacchetto config hello (Settings).</span><span class="sxs-lookup"><span data-stu-id="447bd-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="447bd-117">Esempio: specificare un endpoint HTTP per il servizio</span><span class="sxs-lookup"><span data-stu-id="447bd-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="447bd-118">Hello manifesto del servizio seguente definisce una risorsa di endpoint TCP e due risorse di endpoint HTTP in hello &lt;risorse&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="447bd-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="447bd-119">Gli endpoint HTTP vengono automaticamente inseriti nell'elenco di controllo di accesso da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="447bd-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="447bd-120">Esempio: specificare un endpoint HTTPS per il servizio</span><span class="sxs-lookup"><span data-stu-id="447bd-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="447bd-121">Hello il protocollo HTTPS fornisce l'autenticazione server e viene usato anche per crittografare le comunicazioni client-server.</span><span class="sxs-lookup"><span data-stu-id="447bd-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="447bd-122">tooenable HTTPS nel servizio Service Fabric, specificare il protocollo di hello in hello *risorse -> endpoint -> Endpoint* sezione hello del manifesto del servizio, come illustrato in precedenza per l'endpoint di hello *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="447bd-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="447bd-123">Un protocollo del servizio non può essere modificato durante l'aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="447bd-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="447bd-124">Se viene modificato durante l'aggiornamento, si tratta di una modifica importante.</span><span class="sxs-lookup"><span data-stu-id="447bd-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="447bd-125">Di seguito è riportato un esempio ApplicationManifest che è necessario tooset per HTTPS.</span><span class="sxs-lookup"><span data-stu-id="447bd-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="447bd-126">è necessario specificare l'identificazione personale Hello per il certificato.</span><span class="sxs-lookup"><span data-stu-id="447bd-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="447bd-127">Hello EndpointRef è tooEndpointResource un riferimento nel manifesto del servizio, per cui impostare il protocollo HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="447bd-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="447bd-128">È possibile aggiungere più Endpointcertificate.</span><span class="sxs-lookup"><span data-stu-id="447bd-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="447bd-129">Override degli endpoint in ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="447bd-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="447bd-130">In hello ApplicationManifest aggiungere una sezione ResourceOverrides che sarà una sezione tooConfigOverrides di pari livello.</span><span class="sxs-lookup"><span data-stu-id="447bd-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="447bd-131">In questa sezione è possibile specificare hello override per la sezione di endpoint hello nella sezione risorse hello specificato nel manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="447bd-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="447bd-132">In ordine toooverride EndPoint nel manifesto del servizio utilizzando Modifica ApplicationParameters hello ApplicationManifest come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="447bd-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="447bd-133">Nella sezione oggetto ServiceManifestImport hello aggiungere una nuova sezione "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="447bd-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="447bd-134">In hello che aggiungono parametri di seguito:</span><span class="sxs-lookup"><span data-stu-id="447bd-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="447bd-135">Durante la distribuzione di un'applicazione hello ora è possibile passare questi valori come ApplicationParameters ad esempio:</span><span class="sxs-lookup"><span data-stu-id="447bd-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="447bd-136">Nota: Se i valori hello forniscono per hello ApplicationParameters è vuota tornando predefinito toohello valore fornito in hello manifesto del servizio per hello EndPointName corrispondente.</span><span class="sxs-lookup"><span data-stu-id="447bd-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="447bd-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="447bd-137">For example:</span></span>

<span data-ttu-id="447bd-138">Se nel manifesto del servizio specificato hello</span><span class="sxs-lookup"><span data-stu-id="447bd-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="447bd-139">Hello Port1 e il valore di Protocol1 per i parametri dell'applicazione è null o vuoto.</span><span class="sxs-lookup"><span data-stu-id="447bd-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="447bd-140">porta Hello è ancora stabilita dalla ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="447bd-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="447bd-141">E hello protocollo tcp.</span><span class="sxs-lookup"><span data-stu-id="447bd-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="447bd-142">Si supponga di specificare un valore errato.</span><span class="sxs-lookup"><span data-stu-id="447bd-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="447bd-143">Ad esempio per la porta è stato specificato un valore stringa "Foo" anziché di tipo int.  Nuovo ServiceFabricApplication comando avrà esito negativo con errore: parametro di sostituzione hello dell'attributo name 'ServiceEndpoint1' "Port1" nella sezione 'ResourceOverrides' non è valido.</span><span class="sxs-lookup"><span data-stu-id="447bd-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="447bd-144">il valore di Hello specificato è "Foo" e necessario 'int'.</span><span class="sxs-lookup"><span data-stu-id="447bd-144">hello value specified is 'Foo' and required is 'int'.</span></span>
