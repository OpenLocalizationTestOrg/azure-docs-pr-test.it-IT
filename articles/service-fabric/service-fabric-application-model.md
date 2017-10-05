---
title: Modello di applicazione di Azure Service Fabric | Documentazione Microsoft
description: Come modellare e descrivere le applicazioni e servizi in infrastruttura di servizi.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: e30482427b88eb3e58d39075c7f0734664b79aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="5f9e0-103">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5f9e0-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="5f9e0-104">Questo articolo fornisce una panoramica del modello applicativo di Azure Service Fabric e come definire un'applicazione e un servizio attraverso file manifesto.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-104">This article provides an overview of the Azure Service Fabric application model and how to define an application and service via manifest files.</span></span>

## <a name="understand-the-application-model"></a><span data-ttu-id="5f9e0-105">Informazioni sul modello applicativo</span><span class="sxs-lookup"><span data-stu-id="5f9e0-105">Understand the application model</span></span>
<span data-ttu-id="5f9e0-106">Un'applicazione è una raccolta di servizi costituenti che eseguono determinate funzioni.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="5f9e0-107">Un servizio esegue una funzione completa e autonoma e può essere avviato ed eseguito in modo indipendente da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="5f9e0-108">Un servizio è costituito da codice, configurazione e dati.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="5f9e0-109">Per ogni servizio, il codice è costituito dai file binari eseguibili, la configurazione è costituita dalle impostazioni del servizio che possono essere caricate in fase di esecuzione e i dati sono costituiti da dati statici arbitrari che devono essere usati dal servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-109">For each service, code consists of the executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data to be consumed by the service.</span></span> <span data-ttu-id="5f9e0-110">Per ogni componente di questo modello applicativo gerarchico è possibile eseguire il controllo delle versioni e l'aggiornamento in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Modello di applicazione di Service Fabric][appmodel-diagram]

<span data-ttu-id="5f9e0-112">Un tipo di applicazione è una categorizzazione di un'applicazione e consiste in un'aggregazione di tipi di servizi.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="5f9e0-113">Un tipo di servizio è una categorizzazione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="5f9e0-114">La categorizzazione di un servizio può disporre di impostazioni e configurazioni diverse, ma la funzionalità di base resta la stessa.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-114">The categorization can have different settings and configurations, but the core functionality remains the same.</span></span> <span data-ttu-id="5f9e0-115">Le istanze di un servizio sono le diverse varianti di configurazione dello stesso tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-115">The instances of a service are the different service configuration variations of the same service type.</span></span>  

<span data-ttu-id="5f9e0-116">Le classi (o "tipi") di applicazioni e servizi vengono descritte nei file XML (manifesti dell'applicazione e manifesti del servizio).</span><span class="sxs-lookup"><span data-stu-id="5f9e0-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="5f9e0-117">I manifesti sono i modelli in base ai quali è possibile creare istanze delle applicazioni dall'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-117">The manifests are the templates against which applications can be instantiated from the cluster's image store.</span></span> <span data-ttu-id="5f9e0-118">La definizione dello schema per i file ServiceManifest.xml e ApplicationManifest.xml viene installata con l'SDK e gli strumenti di Service Fabric in *C:\Programmi\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-118">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="5f9e0-119">Il codice di istanze di applicazioni diverse viene eseguito come processo separato anche se ospitato dallo stesso nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-119">The code for different application instances run as separate processes even when hosted by the same Service Fabric node.</span></span> <span data-ttu-id="5f9e0-120">Il ciclo di vita di ogni istanza dell'applicazione può inoltre essere gestito, ad esempio aggiornato, in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-120">Furthermore, the lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="5f9e0-121">Il diagramma seguente illustra come i tipi di applicazioni siano costituiti da tipi di servizi, che a loro volta sono costituiti da codice, configurazione e pacchetti di dati.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-121">The following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="5f9e0-122">Per semplificare il diagramma, vengono visualizzati solo i pacchetti codice/configurazione/dati relativi a `ServiceType4`, anche se ogni tipo di servizio può includere tutti questi tipi di pacchetti o solo alcuni.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-122">To simplify the diagram, only the code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Tipi di applicazioni di Service Fabric e tipi di servizio][cluster-imagestore-apptypes]

<span data-ttu-id="5f9e0-124">Vengono usati due diversi file manifesto per descrivere le applicazioni e i servizi: il manifesto del servizio e il manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-124">Two different manifest files are used to describe applications and services: the service manifest and application manifest.</span></span> <span data-ttu-id="5f9e0-125">I manifesti sono descritti dettagliatamente nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-125">Manifests are covered in detail in the following sections.</span></span>

<span data-ttu-id="5f9e0-126">Nel cluster possono essere attive una o più istanze di un tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-126">There can be one or more instances of a service type active in the cluster.</span></span> <span data-ttu-id="5f9e0-127">Le istanze o le repliche del servizio con stato ad esempio raggiungono un'elevata affidabilità replicando lo stato tra le repliche contenute in nodi diversi del cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in the cluster.</span></span> <span data-ttu-id="5f9e0-128">Essenzialmente, la replica fornisce ridondanza in modo che il servizio sia disponibile anche se un nodo in un cluster ha un malfunzionamento.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-128">Replication essentially provides redundancy for the service to be available even if one node in a cluster fails.</span></span> <span data-ttu-id="5f9e0-129">Un [servizio partizionato](service-fabric-concepts-partitioning.md) suddivide ulteriormente il proprio stato e i modelli di accesso a tale stato tra i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns to that state) across nodes in the cluster.</span></span>

<span data-ttu-id="5f9e0-130">Il diagramma seguente illustra la relazione tra applicazioni e istanze di servizi, partizioni e repliche.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-130">The following diagram shows the relationship between applications and service instances, partitions, and replicas.</span></span>

![Partizioni e repliche in un servizio][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="5f9e0-132">È possibile visualizzare il layout delle applicazioni in un cluster usando lo strumento Service Fabric Explorer disponibile all'indirizzo http://&lt;yourclusteraddress&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-132">You can view the layout of applications in a cluster using the Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="5f9e0-133">Per altre informazioni, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5f9e0-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="5f9e0-134">Descrivere un servizio</span><span class="sxs-lookup"><span data-stu-id="5f9e0-134">Describe a service</span></span>
<span data-ttu-id="5f9e0-135">Il manifesto del servizio definisce in modo dichiarativo il tipo di servizio e la versione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-135">The service manifest declaratively defines the service type and version.</span></span> <span data-ttu-id="5f9e0-136">Specifica i metadati del servizio, ad esempio il tipo di servizio, le proprietà di integrità, le metriche del bilanciamento del carico, i file binari del servizio e i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="5f9e0-137">In altri termini, descrive i pacchetti di codice, configurazione e dati che costituiscono un pacchetto servizio per supportare uno o più tipi di servizi.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-137">Put another way, it describes the code, configuration, and data packages that compose a service package to support one or more service types.</span></span> <span data-ttu-id="5f9e0-138">Questo è un semplice esempio di manifesto del servizio:</span><span class="sxs-lookup"><span data-stu-id="5f9e0-138">Here is a simple example service manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

<span data-ttu-id="5f9e0-139">**Version** sono stringhe non strutturate e non analizzate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-139">**Version** attributes are unstructured strings and not parsed by the system.</span></span> <span data-ttu-id="5f9e0-140">Gli attributi Version vengono usati per il controllo delle versioni di ogni componente per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-140">Version attributes are used to version each component for upgrades.</span></span>

<span data-ttu-id="5f9e0-141">**ServiceTypes** dichiara i tipi di servizi supportati da **CodePackages** nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="5f9e0-142">Quando viene creata un'istanza di un servizio sulla base di uno di questi tipi di servizi, tutti i pacchetti di codice dichiarati nel manifesto vengono attivati eseguendo i relativi punti di ingresso.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="5f9e0-143">I processi risultanti devono registrare i tipi di servizi supportati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-143">The resulting processes are expected to register the supported service types at run time.</span></span> <span data-ttu-id="5f9e0-144">I tipi di servizi sono dichiarati a livello di manifesto e non a livello di pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-144">Service types are declared at the manifest level and not the code package level.</span></span> <span data-ttu-id="5f9e0-145">Se pertanto sono presenti più pacchetti di codice, questi verranno tutti attivati ogni volta che il sistema ricerca uno dei tipi di servizi dichiarati.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-145">So when there are multiple code packages, they are all activated whenever the system looks for any one of the declared service types.</span></span>

<span data-ttu-id="5f9e0-146">**SetupEntryPoint** è un punto di ingresso con privilegi che viene eseguito con le stesse credenziali di Service Fabric (in genere l'account *LocalSystem* ) prima di qualsiasi altro punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-146">**SetupEntryPoint** is a privileged entry point that runs with the same credentials as Service Fabric (typically the *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="5f9e0-147">L'eseguibile specificato da **EntryPoint** è in genere l'host del servizio a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-147">The executable specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="5f9e0-148">La presenza di un punto di ingresso di configurazione separato consente di evitare di dover eseguire l'host del servizio con privilegi elevati per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-148">The presence of a separate setup entry point avoids having to run the service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="5f9e0-149">L'eseguibile specificato da **EntryPoint** viene eseguito dopo che **SetupEntryPoint** termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-149">The executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="5f9e0-150">Se il processo termina o si arresta in modo anomalo, il processo risultante viene monitorato e riavviato (iniziando di nuovo con **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="5f9e0-150">If the process ever terminates or crashes, the resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="5f9e0-151">Gli scenari tipici per l'uso di **SetupEntryPoint** sono l'esecuzione di un file eseguibile prima dell'avvio del servizio o l'esecuzione di un'operazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before the service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="5f9e0-152">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5f9e0-152">For example:</span></span>

* <span data-ttu-id="5f9e0-153">Impostazione e inizializzazione di variabili di ambiente necessari per il file eseguibile del servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-153">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="5f9e0-154">Questo non è limitato solo agli eseguibili scritti tramite i modelli di programmazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-154">This is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="5f9e0-155">Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="5f9e0-156">Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="5f9e0-157">Per altre informazioni su come configurare **SetupEntryPoint**, vedere [Configurare i criteri per il punto di ingresso dell'installazione del servizio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="5f9e0-157">For more details on how to configure the **SetupEntryPoint** see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="5f9e0-158">**EnvironmentVariables** offre un elenco di variabili di ambiente impostate per questo pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="5f9e0-159">Le variabili di ambiente possono essere sostituite in `ApplicationManifest.xml` per specificare valori diversi per diverse istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-159">Environmentment variables can be overridden in the `ApplicationManifest.xml` to provide different values for different service instances.</span></span> 

<span data-ttu-id="5f9e0-160">**DataPackage** dichiara una cartella, denominata dall'attributo **Name**, che contiene i dati statici arbitrari che devono essere usati dal processo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-160">**DataPackage** declares a folder, named by the **Name** attribute, that contains arbitrary static data to be consumed by the process at run time.</span></span>

<span data-ttu-id="5f9e0-161">**ConfigPackage** dichiara una cartella, denominata dall'attributo **Name**, che contiene un file *Settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-161">**ConfigPackage** declares a folder, named by the **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="5f9e0-162">Questo file di impostazioni contiene sezioni di impostazioni di coppie chiave-valore definite dall'utente che vengono lette dal processo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-162">The settings file contains sections of user-defined, key-value pair settings that the process reads back at run time.</span></span> <span data-ttu-id="5f9e0-163">Se durante un aggiornamento è cambiato solo l'attributo **version** **ConfigPackage**, il processo in esecuzione non viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-163">During an upgrade, if only the **ConfigPackage** **version** has changed, then the running process is not restarted.</span></span> <span data-ttu-id="5f9e0-164">Un callback piuttosto notifica al processo che le impostazioni di configurazione sono cambiate affinché vengano ricaricate in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-164">Instead, a callback notifies the process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="5f9e0-165">Questo è un esempio di file *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="5f9e0-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="5f9e0-166">Un manifesto del servizio può contenere più pacchetti di codice, configurazione e dati.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="5f9e0-167">Ognuna di queste può essere creata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="5f9e0-168">Descrivere un'applicazione</span><span class="sxs-lookup"><span data-stu-id="5f9e0-168">Describe an application</span></span>
<span data-ttu-id="5f9e0-169">Il manifesto dell'applicazione descrive in modo dichiarativo il tipo di applicazione e la versione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-169">The application manifest declaratively describes the application type and version.</span></span> <span data-ttu-id="5f9e0-170">Specifica i metadati di composizione dei servizi, ad esempio i nomi stabili, lo schema di partizionamento, il numero di istanze/fattore di replica, i criteri di sicurezza/isolamento, i vincoli di posizionamento, gli override di configurazione e i tipi di servizi costituenti.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="5f9e0-171">Vengono descritti anche i domini di bilanciamento del carico in cui viene posizionata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-171">The load-balancing domains into which the application is placed are also described.</span></span>

<span data-ttu-id="5f9e0-172">Un manifesto dell'applicazione quindi descrive elementi a livello di applicazione e fa riferimento a uno o più manifesti dei servizi per comporre un tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-172">Thus, an application manifest describes elements at the application level and references one or more service manifests to compose an application type.</span></span> <span data-ttu-id="5f9e0-173">Questo è un semplice esempio di manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="5f9e0-173">Here is a simple example application manifest:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

<span data-ttu-id="5f9e0-174">Analogamente ai manifesti dei servizi, gli attributi **Version** sono stringhe non strutturate e non analizzate dal sistema.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by the system.</span></span> <span data-ttu-id="5f9e0-175">Gli attributi Version vengono anche usati per il controllo delle versioni di ogni componente per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-175">Version attributes are also used to version each component for upgrades.</span></span>

<span data-ttu-id="5f9e0-176">**ServiceManifestImport** contiene riferimenti a manifesti di servizi che costituiscono questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-176">**ServiceManifestImport** contains references to service manifests that compose this application type.</span></span> <span data-ttu-id="5f9e0-177">I manifesti di servizi importati determinano i tipi di servizi validi per questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="5f9e0-178">In ServiceManifestImport si esegue l'override dei valori di configurazione nel file Settings.xml e delle variabili di ambiente nel file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-178">Within the ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="5f9e0-179">**DefaultServices** dichiara le istanze dei servizi create automaticamente ogni volta che viene creata un'istanza di un'applicazione sulla base di questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="5f9e0-180">I servizi predefiniti vengono forniti per comodità e dopo la creazione si comportano come normali servizi sotto ogni aspetto.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="5f9e0-181">Vengono aggiornati insieme agli altri servizi nell'istanza dell'applicazione e possono anche essere rimossi.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-181">They are upgraded along with any other services in the application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="5f9e0-182">Un manifesto dell'applicazione può contenere più importazioni di manifesti di servizi e servizi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="5f9e0-183">È possibile controllare le versioni di ogni manifesto del servizio in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="5f9e0-184">Per informazioni su come mantenere applicazioni diverse e parametri di servizio per ambienti singoli, vedere [Gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="5f9e0-184">To learn how to maintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="5f9e0-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f9e0-185">Next steps</span></span>
<span data-ttu-id="5f9e0-186">[Creare il pacchetto di un'applicazione](service-fabric-package-apps.md) e prepararlo per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-186">[Package an application](service-fabric-package-apps.md) and make it ready to deploy.</span></span>

<span data-ttu-id="5f9e0-187">[Distribuire e rimuovere applicazioni con PowerShell][10]: descrive come usare PowerShell per gestire le istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-187">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances.</span></span>

<span data-ttu-id="5f9e0-188">[Gestire i parametri dell'applicazione per più ambienti][11]: descrive come configurare parametri e variabili di ambiente per istanze di applicazione diverse.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-188">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="5f9e0-189">[Configurare i criteri di sicurezza per l'applicazione][12]: descrive come eseguire i servizi nell'ambito dei criteri di sicurezza per limitare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-189">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<span data-ttu-id="5f9e0-190">[Modelli di hosting dell'applicazione][13] descrive la relazione tra le repliche (o istanze) di un servizio distribuito e il processo host del servizio.</span><span class="sxs-lookup"><span data-stu-id="5f9e0-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
