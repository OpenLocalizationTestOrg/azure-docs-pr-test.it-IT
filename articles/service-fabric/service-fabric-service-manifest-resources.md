---
title: Specifica degli endpoint di servizio di Service Fabric | Documentazione Microsoft
description: Come descrivere le risorse di endpoint in un manifesto del servizio, inclusa l'impostazione di endpoint HTTPS
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="b7950-103">Specificare le risorse in un manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="b7950-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="b7950-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b7950-104">Overview</span></span>
<span data-ttu-id="b7950-105">Il manifesto del servizio consente alle risorse di essere usate dal servizio per essere dichiarate/modificate senza modificare il codice compilato.</span><span class="sxs-lookup"><span data-stu-id="b7950-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="b7950-106">Azure Service Fabric supporta la configurazione delle risorse dell'endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="b7950-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="b7950-107">È possibile controllare l'accesso alle risorse specificate nel manifesto del servizio tramite SecurityGroup nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7950-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="b7950-108">La dichiarazione delle risorse consente a queste ultime di essere modificate in fase di distribuzione, in questo modo il servizio non deve introdurre un nuovo meccanismo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b7950-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="b7950-109">La definizione dello schema per il file ServiceManifest.xml viene installata con l'SDK e gli strumenti di Service Fabric in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="b7950-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="b7950-110">Endpoint</span><span class="sxs-lookup"><span data-stu-id="b7950-110">Endpoints</span></span>
<span data-ttu-id="b7950-111">Quando una risorsa dell'endpoint viene definita nel manifesto del servizio, Service Fabric assegna le porte dall'intervallo di porte riservate dell'applicazione se la porta non è esplicitamente specificata.</span><span class="sxs-lookup"><span data-stu-id="b7950-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="b7950-112">Ad esempio, esaminare l'endpoint *ServiceEndpoint1* specificato nel frammento di manifesto fornito dopo questo paragrafo.</span><span class="sxs-lookup"><span data-stu-id="b7950-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="b7950-113">Inoltre, i servizi possono richiedere anche una porta specifica in una risorsa.</span><span class="sxs-lookup"><span data-stu-id="b7950-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="b7950-114">Alle repliche del servizio in esecuzione sui diversi nodi del cluster possono essere assegnati diversi numeri di porta, mentre le repliche di un servizio in esecuzione nello stesso nodo condividono la porta.</span><span class="sxs-lookup"><span data-stu-id="b7950-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="b7950-115">Le repliche del servizio possono quindi usare queste porte in base alle esigenze per la replica e l'ascolto delle richieste client.</span><span class="sxs-lookup"><span data-stu-id="b7950-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="b7950-116">Per altre informazioni sugli endpoint di riferimento del file delle impostazioni del pacchetto di configurazione (settings.xml), vedere [Configurazione di Reliable Services con stato](service-fabric-reliable-services-configuration.md) .</span><span class="sxs-lookup"><span data-stu-id="b7950-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="b7950-117">Esempio: specificare un endpoint HTTP per il servizio</span><span class="sxs-lookup"><span data-stu-id="b7950-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="b7950-118">Il manifesto del servizio seguente definisce una risorsa di endpoint TCP e due risorse di endpoint HTTP nell'elemento &lt;Risorse&gt;.</span><span class="sxs-lookup"><span data-stu-id="b7950-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="b7950-119">Gli endpoint HTTP vengono automaticamente inseriti nell'elenco di controllo di accesso da Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7950-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="b7950-120">Esempio: specificare un endpoint HTTPS per il servizio</span><span class="sxs-lookup"><span data-stu-id="b7950-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="b7950-121">Il protocollo HTTPS fornisce l’autenticazione del server e viene anche usato per crittografare la comunicazione del client-server.</span><span class="sxs-lookup"><span data-stu-id="b7950-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="b7950-122">Per abilitare il protocollo HTTPS nel servizio di Service Fabric, specificare il protocollo nella sezione *Risorse -> Endpoint -> Endpoint* del manifesto del servizio, come illustrato in precedenza per l'endpoint *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="b7950-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="b7950-123">Un protocollo del servizio non può essere modificato durante l'aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b7950-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="b7950-124">Se viene modificato durante l'aggiornamento, si tratta di una modifica importante.</span><span class="sxs-lookup"><span data-stu-id="b7950-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="b7950-125">Di seguito è riportato un esempio ApplicationManifest che è necessario impostare per il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b7950-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="b7950-126">È necessario fornire l'identificazione personale per il certificato.</span><span class="sxs-lookup"><span data-stu-id="b7950-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="b7950-127">EndpointRef è un riferimento a EndpointResource in ServiceManifest per cui si imposta il protocollo HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b7950-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="b7950-128">È possibile aggiungere più Endpointcertificate.</span><span class="sxs-lookup"><span data-stu-id="b7950-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="b7950-129">Override degli endpoint in ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b7950-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="b7950-130">In ApplicationManifest aggiungere una sezione ResourceOverride che sarà un elemento di pari livello della sezione ConfigOverrides.</span><span class="sxs-lookup"><span data-stu-id="b7950-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="b7950-131">In questa sezione è possibile specificare l'override per la sezione Endpoint nella sezione delle risorse specificata in ServiceManifest.</span><span class="sxs-lookup"><span data-stu-id="b7950-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="b7950-132">Per eseguire l'override di EndPoint in ServiceManifest usando ApplicationParameters, modificare ApplicationManifest come riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7950-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="b7950-133">Nella sezione ServiceManifestImport aggiungere una nuova sezione "ResourceOverrides"</span><span class="sxs-lookup"><span data-stu-id="b7950-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="b7950-134">In Parameters aggiungere quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b7950-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="b7950-135">Durante la distribuzione dell'applicazione ora è possibile trasmettere questi valori come ApplicationParameters, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b7950-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="b7950-136">Nota: se i valori forniti per ApplicationParameters sono vuoti, si torna al il valore predefinito fornito in ServiceManifest per l'EndPointName corrispondente.</span><span class="sxs-lookup"><span data-stu-id="b7950-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="b7950-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b7950-137">For example:</span></span>

<span data-ttu-id="b7950-138">Se in ServiceManifest è stato specificato</span><span class="sxs-lookup"><span data-stu-id="b7950-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="b7950-139">e i valori Port1 e Protocol1 per i parametri di Aplication sono null o vuoti.</span><span class="sxs-lookup"><span data-stu-id="b7950-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="b7950-140">La porta è comunque stabilita da ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="b7950-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="b7950-141">E il protocollo sarà tcp.</span><span class="sxs-lookup"><span data-stu-id="b7950-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="b7950-142">Si supponga di specificare un valore errato.</span><span class="sxs-lookup"><span data-stu-id="b7950-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="b7950-143">Ad esempio per la porta è stato specificato un valore stringa "Foo" anziché di tipo int.  Il comando New-ServiceFabricApplication avrà esito negativo con l'errore seguente: The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid (Il parametro di override con nome "ServiceEndpoint1" attributo "Port1" nella sezione "ResourceOverrides" non è valido).</span><span class="sxs-lookup"><span data-stu-id="b7950-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="b7950-144">Il valore specificato è "Foo", mentre era richiesto "int".</span><span class="sxs-lookup"><span data-stu-id="b7950-144">The value specified is 'Foo' and required is 'int'.</span></span>
