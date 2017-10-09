---
title: modello di applicazione di Service Fabric aaaAzure | Documenti Microsoft
description: Come toomodel e descrivere applicazioni e servizi di Service Fabric.
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
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="1bbec-103">Modellare un'applicazione in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1bbec-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="1bbec-104">In questo articolo viene fornita una panoramica del modello di applicazione di Azure Service Fabric hello e come toodefine un'applicazione e servizio tramite file manifesto.</span><span class="sxs-lookup"><span data-stu-id="1bbec-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="1bbec-105">Comprendere il modello di applicazione hello</span><span class="sxs-lookup"><span data-stu-id="1bbec-105">Understand hello application model</span></span>
<span data-ttu-id="1bbec-106">Un'applicazione è una raccolta di servizi costituenti che eseguono determinate funzioni.</span><span class="sxs-lookup"><span data-stu-id="1bbec-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="1bbec-107">Un servizio esegue una funzione completa e autonoma e può essere avviato ed eseguito in modo indipendente da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="1bbec-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="1bbec-108">Un servizio è costituito da codice, configurazione e dati.</span><span class="sxs-lookup"><span data-stu-id="1bbec-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="1bbec-109">Per ogni servizio, codice è costituito da file binari eseguibili hello e dati è costituito da dati statici arbitrario toobe utilizzato dal servizio hello configurazione è costituita da impostazioni del servizio che possono essere caricate in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="1bbec-110">Per ogni componente di questo modello applicativo gerarchico è possibile eseguire il controllo delle versioni e l'aggiornamento in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1bbec-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![modello dell'applicazione Hello Service Fabric][appmodel-diagram]

<span data-ttu-id="1bbec-112">Un tipo di applicazione è una categorizzazione di un'applicazione e consiste in un'aggregazione di tipi di servizi.</span><span class="sxs-lookup"><span data-stu-id="1bbec-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="1bbec-113">Un tipo di servizio è una categorizzazione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="1bbec-114">categorizzazione di Hello può avere diverse impostazioni e configurazioni, ma rimane la funzionalità di base hello hello stesso.</span><span class="sxs-lookup"><span data-stu-id="1bbec-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="1bbec-115">le istanze di un servizio Hello sono variazioni di configurazione di servizio diverso hello di hello stesso tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="1bbec-116">Le classi (o "tipi") di applicazioni e servizi vengono descritte nei file XML (manifesti dell'applicazione e manifesti del servizio).</span><span class="sxs-lookup"><span data-stu-id="1bbec-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="1bbec-117">i manifesti di Hello sono modelli hello rispetto al quale è possono creare applicazioni dall'archivio di immagini del cluster hello istanze.</span><span class="sxs-lookup"><span data-stu-id="1bbec-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="1bbec-118">viene installato con hello Service Fabric SDK Hello definizione dello schema per il file ServiceManifest.xml e ApplicationManifest.xml di hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="1bbec-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="1bbec-119">codice Hello per le istanze dell'applicazione diverso eseguiti come processi distinti, anche quando sono ospitati da hello stesso nodo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1bbec-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="1bbec-120">Inoltre, hello ciclo di vita di ogni istanza dell'applicazione può essere gestito (ad esempio, l'aggiornamento) in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1bbec-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="1bbec-121">Hello diagramma seguente mostra come tipi di applicazioni sono costituiti da tipi di servizio, che a sua volta sono costituiti da codice, configurazione e i pacchetti di dati.</span><span class="sxs-lookup"><span data-stu-id="1bbec-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="1bbec-122">diagramma di hello toosimplify, solo i pacchetti dati/config/codice hello per `ServiceType4` vengono visualizzati, anche se ogni tipo di servizio include alcuni o tutti i tipi di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="1bbec-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Tipi di applicazioni di Service Fabric e tipi di servizio][cluster-imagestore-apptypes]

<span data-ttu-id="1bbec-124">Due diversi file manifesti vengono usate toodescribe applicazioni e servizi: hello manifesto del servizio e manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="1bbec-125">I manifesti sono illustrati in dettaglio nelle sezioni che seguono hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="1bbec-126">Può essere attivo nel cluster hello uno o più istanze di un tipo di servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="1bbec-127">Ad esempio, le istanze del servizio con stato, o repliche, ottenere affidabilità replica dello stato tra le repliche che si trova in nodi diversi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="1bbec-128">Essenzialmente fornisce la ridondanza per hello servizio toobe disponibile anche se un nodo in un cluster non riesce.</span><span class="sxs-lookup"><span data-stu-id="1bbec-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="1bbec-129">Oggetto [partizionata servizio](service-fabric-concepts-partitioning.md) ulteriormente divide il relativo stato (e stato toothat modelli di accesso) tra i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="1bbec-130">Hello diagramma seguente mostra la relazione hello tra applicazioni e le istanze del servizio, partizioni e repliche.</span><span class="sxs-lookup"><span data-stu-id="1bbec-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Partizioni e repliche in un servizio][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="1bbec-132">È possibile visualizzare il layout di hello delle applicazioni in un cluster con lo strumento Service Fabric Explorer hello disponibile in http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="1bbec-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="1bbec-133">Per altre informazioni, vedere [Visualizzare il cluster con Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1bbec-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="1bbec-134">Descrivere un servizio</span><span class="sxs-lookup"><span data-stu-id="1bbec-134">Describe a service</span></span>
<span data-ttu-id="1bbec-135">manifesto del servizio Hello definisce in modo dichiarativo il tipo di servizio di hello e versione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="1bbec-136">Specifica i metadati del servizio, ad esempio il tipo di servizio, le proprietà di integrità, le metriche del bilanciamento del carico, i file binari del servizio e i file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="1bbec-137">In altre parole, pacchetti di codice, configurazione e dati hello che compongono un toosupport pacchetto servizio descrive uno o più tipi di servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="1bbec-138">Questo è un semplice esempio di manifesto del servizio:</span><span class="sxs-lookup"><span data-stu-id="1bbec-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="1bbec-139">**Versione** gli attributi sono stringhe non strutturate e non analizzato dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="1bbec-140">Attributi della versione sono utilizzati tooversion ogni componente per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="1bbec-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="1bbec-141">**ServiceTypes** dichiara i tipi di servizi supportati da **CodePackages** nel manifesto.</span><span class="sxs-lookup"><span data-stu-id="1bbec-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="1bbec-142">Quando viene creata un'istanza di un servizio sulla base di uno di questi tipi di servizi, tutti i pacchetti di codice dichiarati nel manifesto vengono attivati eseguendo i relativi punti di ingresso.</span><span class="sxs-lookup"><span data-stu-id="1bbec-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="1bbec-143">processi risultanti Hello sono tipi di servizio previsto tooregister hello è supportato in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="1bbec-144">Tipi di servizio vengono dichiarati a livello di manifesto hello e non livello di pacchetto codice hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="1bbec-145">Pertanto, quando sono presenti più pacchetti di codice, sono tutte attivate ogni volta che il sistema hello cerca uno qualsiasi dei tipi di servizio dichiarati hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="1bbec-146">**SetupEntryPoint** è un punto di ingresso con privilegi che viene eseguito con hello stesso credenziali come Service Fabric (in genere hello *LocalSystem* account) prima di qualsiasi altro punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="1bbec-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="1bbec-147">eseguibile Hello specificato da **EntryPoint** è in genere l'host del servizio hello con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1bbec-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="1bbec-148">presenza di Hello di un punto di ingresso del programma di installazione separato evita l'host del servizio hello toorun con privilegi elevati per lunghi periodi di tempo.</span><span class="sxs-lookup"><span data-stu-id="1bbec-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="1bbec-149">eseguibile Hello specificato da **EntryPoint** viene eseguito dopo **SetupEntryPoint** termina correttamente.</span><span class="sxs-lookup"><span data-stu-id="1bbec-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="1bbec-150">Se il processo di hello mai termina o si blocca, processo risultante hello viene monitorato e riavviato (a partire da nuovamente con **SetupEntryPoint**).</span><span class="sxs-lookup"><span data-stu-id="1bbec-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="1bbec-151">Scenari tipici per l'utilizzo di **SetupEntryPoint** sono quando si esegue un file eseguibile prima dell'avvio del servizio hello o si esegue un'operazione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="1bbec-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="1bbec-152">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1bbec-152">For example:</span></span>

* <span data-ttu-id="1bbec-153">Impostazione e l'inizializzazione di variabili di ambiente hello esigenze eseguibile del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="1bbec-154">Non si tratta di file eseguibili tooonly limitato scritti tramite modelli di programmazione di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="1bbec-155">Ad esempio, npm.exe richiede alcune variabili di ambiente configurate per la distribuzione di un'applicazione node.js.</span><span class="sxs-lookup"><span data-stu-id="1bbec-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="1bbec-156">Impostazione del controllo di accesso mediante l'installazione di certificati di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1bbec-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="1bbec-157">Per ulteriori informazioni su come hello tooconfigure **SetupEntryPoint** vedere [configurare criteri di hello per un punto di ingresso del programma di installazione del servizio](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="1bbec-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="1bbec-158">**EnvironmentVariables** offre un elenco di variabili di ambiente impostate per questo pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="1bbec-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="1bbec-159">Le variabili Environmentment possono essere sottoposto a override in hello `ApplicationManifest.xml` tooprovide valori diversi per diverse istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="1bbec-160">**DataPackage** dichiara una cartella, denominata da hello **nome** attributo, che contiene i dati statici arbitrario toobe utilizzata dal processo hello in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="1bbec-161">**ConfigPackage** dichiara una cartella, denominata da hello **nome** attributo, che contiene un *Settings* file.</span><span class="sxs-lookup"><span data-stu-id="1bbec-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="1bbec-162">file di impostazioni Hello contiene sezioni di impostazioni di coppia chiave-valore specifico definito dall'utente che il processo di hello legge nuovamente in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="1bbec-163">Durante un aggiornamento, se solo hello **ConfigPackage** **versione** è stata modificata, quindi hello esecuzione processo non viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="1bbec-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="1bbec-164">Al contrario, un callback di notifica processo hello che le impostazioni di configurazione sono state modificate in modo che possa essere ricaricati in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="1bbec-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="1bbec-165">Questo è un esempio di file *Settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="1bbec-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="1bbec-166">Un manifesto del servizio può contenere più pacchetti di codice, configurazione e dati.</span><span class="sxs-lookup"><span data-stu-id="1bbec-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="1bbec-167">Ognuna di queste può essere creata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1bbec-167">Each of those can be versioned independently.</span></span>
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a><span data-ttu-id="1bbec-168">Descrivere un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1bbec-168">Describe an application</span></span>
<span data-ttu-id="1bbec-169">manifesto dell'applicazione Hello descrive in modo dichiarativo il tipo di applicazione hello e la versione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="1bbec-170">Specifica i metadati di composizione dei servizi, ad esempio i nomi stabili, lo schema di partizionamento, il numero di istanze/fattore di replica, i criteri di sicurezza/isolamento, i vincoli di posizionamento, gli override di configurazione e i tipi di servizi costituenti.</span><span class="sxs-lookup"><span data-stu-id="1bbec-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="1bbec-171">sono descritti anche i domini di bilanciamento del carico Hello in cui viene inserita l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="1bbec-172">Di conseguenza, un manifesto dell'applicazione vengono descritti gli elementi a livello di applicazione hello e fa riferimento a uno o più servizio manifesti toocompose un tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="1bbec-173">Questo è un semplice esempio di manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="1bbec-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="1bbec-174">Ad esempio i manifesti del servizio, **versione** gli attributi sono stringhe non strutturate e non vengono analizzati dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="1bbec-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="1bbec-175">Attributi della versione sono anche utilizzati tooversion ogni componente per gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="1bbec-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="1bbec-176">**Oggetto ServiceManifestImport** contiene manifesti tooservice riferimenti che compongono questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="1bbec-177">I manifesti di servizi importati determinano i tipi di servizi validi per questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="1bbec-178">All'interno di hello oggetto ServiceManifestImport, eseguire l'override dei valori di configurazione nelle variabili di ambiente e Settings nel file ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="1bbec-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="1bbec-179">**DefaultServices** dichiara le istanze dei servizi create automaticamente ogni volta che viene creata un'istanza di un'applicazione sulla base di questo tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="1bbec-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="1bbec-180">I servizi predefiniti vengono forniti per comodità e dopo la creazione si comportano come normali servizi sotto ogni aspetto.</span><span class="sxs-lookup"><span data-stu-id="1bbec-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="1bbec-181">Essi vengono aggiornati con tutti gli altri servizi nell'istanza di applicazione hello e possono essere rimossi anche.</span><span class="sxs-lookup"><span data-stu-id="1bbec-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="1bbec-182">Un manifesto dell'applicazione può contenere più importazioni di manifesti di servizi e servizi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="1bbec-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="1bbec-183">È possibile controllare le versioni di ogni manifesto del servizio in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="1bbec-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="1bbec-184">toolearn toomaintain altra applicazione e i parametri di servizio per i singoli ambienti, vedere [la gestione dei parametri dell'applicazione per più ambienti](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="1bbec-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="1bbec-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bbec-185">Next steps</span></span>
<span data-ttu-id="1bbec-186">[Pacchetto di un'applicazione](service-fabric-package-apps.md) e renderlo pronto toodeploy.</span><span class="sxs-lookup"><span data-stu-id="1bbec-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="1bbec-187">[Distribuire e rimuovere le applicazioni] [ 10] viene descritto come le istanze dell'applicazione toomanage toouse PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bbec-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="1bbec-188">[Gestione dei parametri dell'applicazione per più ambienti] [ 11] viene descritto come tooconfigure parametri e variabili di ambiente per le istanze dell'applicazione diverso.</span><span class="sxs-lookup"><span data-stu-id="1bbec-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="1bbec-189">[Configurare i criteri di sicurezza per l'applicazione] [ 12] viene descritto come toorun servizi con accesso toorestrict criteri di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="1bbec-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="1bbec-190">[Modelli di hosting dell'applicazione][13] descrive la relazione tra le repliche (o istanze) di un servizio distribuito e il processo host del servizio.</span><span class="sxs-lookup"><span data-stu-id="1bbec-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
