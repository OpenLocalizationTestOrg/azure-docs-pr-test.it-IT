---
title: "Gestire più ambienti in Service Fabric | Microsoft Docs"
description: "Le applicazioni di Service Fabric possono essere eseguite su cluster le cui dimensioni variano da un solo computer a molte migliaia. In alcuni casi è possibile che si voglia configurare l'applicazione in modo diverso per i diversi ambienti. Questo articolo illustra come definire diversi parametri dell'applicazione per ogni ambiente,"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 9317b3f0b7984e795c4205360ed58e2c4f3fbcb1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="67658-105">Gestire i parametri dell'applicazione per più ambienti</span><span class="sxs-lookup"><span data-stu-id="67658-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="67658-106">I cluster di Azure Service Fabric possono essere creati usando un solo computer fino a molte migliaia.</span><span class="sxs-lookup"><span data-stu-id="67658-106">You can create Azure Service Fabric clusters by using anywhere from one to many thousands of machines.</span></span> <span data-ttu-id="67658-107">Anche se i file binari dell'applicazione possono essere eseguiti senza modifiche in questa ampia gamma di ambienti, spesso è consigliabile configurare l'applicazione in modo diverso, in base al numero di computer in cui si esegue la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="67658-107">While application binaries can run without modification across this wide spectrum of environments, you often want to configure the application differently, depending on the number of machines you're deploying to.</span></span>

<span data-ttu-id="67658-108">Ad esempio, considerare `InstanceCount` per un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="67658-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="67658-109">Quando si eseguono applicazioni in Azure, in genere è consigliabile impostare questo parametro sul valore speciale "-1".</span><span class="sxs-lookup"><span data-stu-id="67658-109">When you are running applications in Azure, you generally want to set this parameter to the special value of "-1".</span></span> <span data-ttu-id="67658-110">Questa configurazione garantisce che il servizio sia in esecuzione in ogni nodo del cluster (o in ogni nodo nel tipo di nodo se è stato impostato un vincolo di posizionamento).</span><span class="sxs-lookup"><span data-stu-id="67658-110">This configuration ensures that your service is running on every node in the cluster (or every node in the node type if you have set a placement constraint).</span></span> <span data-ttu-id="67658-111">Non è tuttavia appropriata per un cluster con un singolo computer, perché non è possibile avere più processi in ascolto sullo stesso endpoint in un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="67658-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on the same endpoint on a single machine.</span></span> <span data-ttu-id="67658-112">Al contrario, `InstanceCount` viene in genere impostato su "1".</span><span class="sxs-lookup"><span data-stu-id="67658-112">Instead, you typically set `InstanceCount` to "1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="67658-113">Definizione dei parametri specifici dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="67658-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="67658-114">La soluzione per questo problema di configurazione è costituita da un set di servizi predefiniti con parametri e file di parametri dell'applicazione che compilano i valori dei parametri per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="67658-114">The solution to this configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="67658-115">I parametri predefiniti per servizi e applicazioni vengono configurati all'interno dei manifesti dei servizi e delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="67658-115">Default services and application parameters are configured in the application and service manifests.</span></span> <span data-ttu-id="67658-116">La definizione dello schema per i file ServiceManifest.xml e ApplicationManifest.xml viene installata con gli strumenti e l'SDK di Service Fabric in *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="67658-116">The schema definition for the ServiceManifest.xml and ApplicationManifest.xml files is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="67658-117">Servizi predefiniti</span><span class="sxs-lookup"><span data-stu-id="67658-117">Default services</span></span>
<span data-ttu-id="67658-118">Le applicazioni di infrastruttura di servizi sono costituite da una raccolta di istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="67658-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="67658-119">Anche se è possibile creare un'applicazione vuota e quindi tutte le istanze del servizio dinamicamente, la maggior parte delle applicazioni include un set di servizi di base che devono essere sempre creati quando si creano istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-119">While it is possible for you to create an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when the application is instantiated.</span></span> <span data-ttu-id="67658-120">Questi servizi sono detti "servizi predefiniti" e</span><span class="sxs-lookup"><span data-stu-id="67658-120">These are referred to as "default services".</span></span> <span data-ttu-id="67658-121">vengono specificati nel manifesto dell'applicazione, con i segnaposto per la configurazione specifica dei singoli ambienti racchiusi tra parentesi quadre:</span><span class="sxs-lookup"><span data-stu-id="67658-121">They are specified in the application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

<span data-ttu-id="67658-122">Ogni parametro denominato deve essere definito nell'elemento Parameters del manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="67658-122">Each of the named parameters must be defined within the Parameters element of the application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="67658-123">L'attributo DefaultValue specifica il valore da usare in assenza di un parametro più specifico per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="67658-123">The DefaultValue attribute specifies the value to be used in the absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="67658-124">Non tutti i parametri di istanza del servizio sono idonei alla configurazione specifica per il singolo ambiente.</span><span class="sxs-lookup"><span data-stu-id="67658-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="67658-125">Nell'esempio precedente i valori LowKey e HighKey per lo schema di partizionamento del servizio sono definiti in modo esplicito per tutte le istanze del servizio, perché l'intervallo di partizione è una funzione del dominio di dati, non dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="67658-125">In the example above, the LowKey and HighKey values for the service's partitioning scheme are explicitly defined for all instances of the service since the partition range is a function of the data domain, not the environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="67658-126">Impostazioni della configurazione del servizio specifica per il singolo ambiente</span><span class="sxs-lookup"><span data-stu-id="67658-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="67658-127">Il [modello applicativo di Service Fabric](service-fabric-application-model.md) consente ai servizi di includere pacchetti di configurazione che contengono coppie chiave-valore personalizzate leggibili in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="67658-127">The [Service Fabric application model](service-fabric-application-model.md) enables services to include configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="67658-128">È anche possibile differenziare i valori di queste impostazioni in base all'ambiente, specificando un valore `ConfigOverride` nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-128">The values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in the application manifest.</span></span>

<span data-ttu-id="67658-129">Si supponga di avere la seguente impostazione nel file Config\Settings.xml per il servizio `Stateful1`:</span><span class="sxs-lookup"><span data-stu-id="67658-129">Suppose that you have the following setting in the Config\Settings.xml file for the `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="67658-130">Per eseguire l'override di questo valore per una coppia applicazione/ambiente specifica, creare un valore `ConfigOverride` durante l'importazione del manifesto del servizio nel manifesto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-130">To override this value for a specific application/environment pair, create a `ConfigOverride` when you import the service manifest in the application manifest.</span></span>

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
<span data-ttu-id="67658-131">Questo parametro può quindi essere configurato dall'ambiente, come illustrato in precedenza,</span><span class="sxs-lookup"><span data-stu-id="67658-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="67658-132">dichiarandolo nella sezione Parameters del manifesto dell'applicazione e definendo i valori specifici per il singolo ambiente nel file di parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-132">You can do this by declaring it in the parameters section of the application manifest and specifying environment-specific values in the application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="67658-133">Nel caso delle impostazioni di configurazione del servizio, è possibile impostare il valore di una chiave in tre posizioni, ovvero nel pacchetto di configurazione del servizio, nel manifesto dell'applicazione e nel file di parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-133">In the case of service configuration settings, there are three places where the value of a key can be set: the service configuration package, the application manifest, and the application parameter file.</span></span> <span data-ttu-id="67658-134">Service Fabric sceglierà sempre prima di tutto dal file di parametri dell'applicazione, se specificato, quindi dal manifesto dell'applicazione e infine dal pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="67658-134">Service Fabric will always choose from the application parameter file first (if specified), then the application manifest, and finally the configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="67658-135">Impostazione e uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="67658-135">Setting and using environment variables</span></span> 
<span data-ttu-id="67658-136">È possibile specificare e impostare le variabili di ambiente nel file ServiceManifest.xml e quindi sostituire tali impostazioni nel file ApplicationManifest.xml per ogni istanza.</span><span class="sxs-lookup"><span data-stu-id="67658-136">You can specify and set environment variables in the ServiceManifest.xml file and then override these in the ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="67658-137">L'esempio seguente illustra due variabili di ambiente, una con un valore impostato e l'altra sostituita.</span><span class="sxs-lookup"><span data-stu-id="67658-137">The example below shows two environment variables, one with a value set and the other is overridden.</span></span> <span data-ttu-id="67658-138">È possibile usare i parametri dell'applicazione per impostare i valori delle variabili di ambiente in modo analogo a come verrebbero usati per le sostituzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="67658-138">You can use application parameters to set environment variables values in the same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="67658-139">Per sostituire le variabili di ambiente nel file ApplicationManifest.xml, fare riferimento al pacchetto di codice in ServiceManifest con l'elemento `EnvironmentOverrides`.</span><span class="sxs-lookup"><span data-stu-id="67658-139">To override the environment variables in the ApplicationManifest.xml, reference the code package in the ServiceManifest with the `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="67658-140">Dopo aver creato l'istanza del servizio denominato, è possibile accedere alle variabili di ambiente dal codice.</span><span class="sxs-lookup"><span data-stu-id="67658-140">Once the named service instance is created you can access the environment variables from code.</span></span> <span data-ttu-id="67658-141">In C# è possibile ad esempio eseguire queste operazioni</span><span class="sxs-lookup"><span data-stu-id="67658-141">e.g. In C# you can do the following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="67658-142">Variabili di ambiente di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="67658-142">Service Fabric environment variables</span></span>
<span data-ttu-id="67658-143">Service Fabric dispone di variabili di ambiente predefinite, impostate per ciascuna istanza di servizio.</span><span class="sxs-lookup"><span data-stu-id="67658-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="67658-144">Di seguito viene riportato l'elenco completo delle variabili di ambiente. Quelle in grassetto verranno usate nel servizio, le altre sono usate dal runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="67658-144">The full list of environment variables is below, where the ones in bold are the ones that you will use in your service, the other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="67658-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="67658-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="67658-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="67658-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="67658-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="67658-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="67658-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="67658-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="67658-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="67658-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="67658-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="67658-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="67658-151">**Fabric_Endpoint_[NomeDelServizio]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="67658-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="67658-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="67658-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="67658-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="67658-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="67658-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="67658-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="67658-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="67658-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="67658-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="67658-156">Fabric_NodeId</span></span>
* <span data-ttu-id="67658-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="67658-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="67658-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="67658-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="67658-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="67658-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="67658-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="67658-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="67658-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="67658-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="67658-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="67658-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="67658-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="67658-163">FabricPackageFileName</span></span>

<span data-ttu-id="67658-164">Il codice seguente mostra come elencare le variabili di ambiente di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="67658-164">The code belows shows how to list the Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="67658-165">Di seguito sono riportati esempi di variabili di ambiente per un tipo di applicazione chiamato `GuestExe.Application` con un tipo di servizio denominato `FrontEndService`, in esecuzione sul computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="67658-165">The following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="67658-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="67658-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="67658-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="67658-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="67658-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="67658-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="67658-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="67658-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="67658-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="67658-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="67658-171">File di parametri dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="67658-171">Application parameter files</span></span>
<span data-ttu-id="67658-172">Il progetto di applicazione di Service Fabric può includere uno o più file di parametri dell'applicazione,</span><span class="sxs-lookup"><span data-stu-id="67658-172">The Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="67658-173">ognuno dei quali definisce i valori specifici per i parametri definiti nel manifesto dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="67658-173">Each of them defines the specific values for the parameters that are defined in the application manifest:</span></span>

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
<span data-ttu-id="67658-174">Per impostazione predefinita, una nuova applicazione include tre file di parametro dell'applicazione, denominati Local.1Node.xml, Local.5Node.xml e Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="67658-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![File di parametri dell'applicazione in Esplora soluzioni][app-parameters-solution-explorer]

<span data-ttu-id="67658-176">Per creare un file di parametri, è sufficiente copiarne e incollarne uno esistente e specificare un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="67658-176">To create a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="67658-177">Identificazione di parametri specifici per il singolo ambiente durante la distribuzione</span><span class="sxs-lookup"><span data-stu-id="67658-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="67658-178">In fase di distribuzione è necessario scegliere il file di parametri appropriato da usare con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-178">At deployment time, you need to choose the appropriate parameter file to apply with your application.</span></span> <span data-ttu-id="67658-179">È possibile eseguire questa operazione nella finestra di dialogo Pubblica in Visual Studio o in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67658-179">You can do this through the Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="67658-180">Eseguire una distribuzione da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67658-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="67658-181">Si può scegliere dall'elenco dei file di parametri disponibili quando si pubblica l'applicazione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67658-181">You can choose from the list of available parameter files when you publish your application in Visual Studio.</span></span>

![Scelta di un file di parametri nella finestra di dialogo Pubblica][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="67658-183">Distribuire da PowerShell</span><span class="sxs-lookup"><span data-stu-id="67658-183">Deploy from PowerShell</span></span>
<span data-ttu-id="67658-184">Lo script `Deploy-FabricApplication.ps1` di PowerShell incluso nel modello del progetto dell'applicazione accetta un profilo di pubblicazione come parametro e PublishProfile contiene un riferimento al file dei parametri dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67658-184">The `Deploy-FabricApplication.ps1` PowerShell script included in the application project template accepts a publish profile as a parameter and the PublishProfile contains a reference to the application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="67658-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67658-185">Next steps</span></span>
<span data-ttu-id="67658-186">Per altre informazioni su alcuni concetti di base illustrati in questo argomento, vedere [Panoramica della terminologia di Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67658-186">To learn more about some of the core concepts that are discussed in this topic, see the [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="67658-187">Per informazioni su altre funzionalità di gestione delle app disponibili in Visual Studio, vedere [Usare Visual Studio per semplificare la scrittura e la gestione delle applicazioni di Service Fabric](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="67658-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
