---
title: "aaaManage più ambienti in Service Fabric | Documenti Microsoft"
description: "È possibile eseguire le applicazioni di Service Fabric in cluster in un intervallo dimensioni da una macchina toothousands di macchine. In alcuni casi, si desidererà tooconfigure l'applicazione in modo diverso per i diversi ambienti. Questo articolo descrive come parametri di toodefine applicazioni diverso per ogni ambiente."
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
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a><span data-ttu-id="f3319-105">Gestire i parametri dell'applicazione per più ambienti</span><span class="sxs-lookup"><span data-stu-id="f3319-105">Manage application parameters for multiple environments</span></span>
<span data-ttu-id="f3319-106">È possibile creare cluster di Azure Service Fabric usando ovunque da uno toomany migliaia di computer.</span><span class="sxs-lookup"><span data-stu-id="f3319-106">You can create Azure Service Fabric clusters by using anywhere from one toomany thousands of machines.</span></span> <span data-ttu-id="f3319-107">Mentre i file binari dell'applicazione può essere eseguito senza alcuna modifica tra l'ampia gamma di ambienti, è spesso necessario applicazione hello tooconfigure in modo diverso, in base al numero hello macchine, che esegue la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f3319-107">While application binaries can run without modification across this wide spectrum of environments, you often want tooconfigure hello application differently, depending on hello number of machines you're deploying to.</span></span>

<span data-ttu-id="f3319-108">Ad esempio, considerare `InstanceCount` per un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="f3319-108">As a simple example, consider `InstanceCount` for a stateless service.</span></span> <span data-ttu-id="f3319-109">Quando si eseguono le applicazioni in Azure, è in genere opportuno tooset questo toohello speciale valore di parametro "-1".</span><span class="sxs-lookup"><span data-stu-id="f3319-109">When you are running applications in Azure, you generally want tooset this parameter toohello special value of "-1".</span></span> <span data-ttu-id="f3319-110">Questa configurazione assicura che il servizio sia in esecuzione in ogni nodo nel cluster hello (o tutti i nodi nel tipo di nodo hello se è stato impostato un vincolo di posizionamento).</span><span class="sxs-lookup"><span data-stu-id="f3319-110">This configuration ensures that your service is running on every node in hello cluster (or every node in hello node type if you have set a placement constraint).</span></span> <span data-ttu-id="f3319-111">Tuttavia, questa configurazione non è adatta per un cluster singolo computer perché non è possibile avere più processi in attesa su hello stesso endpoint in un singolo computer.</span><span class="sxs-lookup"><span data-stu-id="f3319-111">However, this configuration is not suitable for a single-machine cluster since you cannot have multiple processes listening on hello same endpoint on a single machine.</span></span> <span data-ttu-id="f3319-112">È invece in genere impostare `InstanceCount` troppo "1".</span><span class="sxs-lookup"><span data-stu-id="f3319-112">Instead, you typically set `InstanceCount` too"1".</span></span>

## <a name="specifying-environment-specific-parameters"></a><span data-ttu-id="f3319-113">Definizione dei parametri specifici dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="f3319-113">Specifying environment-specific parameters</span></span>
<span data-ttu-id="f3319-114">problema di configurazione toothis soluzione hello è un set di servizi con parametri predefiniti e i file dei parametri dell'applicazione che vengono compilati i valori dei parametri per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="f3319-114">hello solution toothis configuration issue is a set of parameterized default services and application parameter files that fill in those parameter values for a given environment.</span></span> <span data-ttu-id="f3319-115">Servizi predefiniti e i parametri dell'applicazione vengono configurati in un'applicazione hello e manifesti del servizio.</span><span class="sxs-lookup"><span data-stu-id="f3319-115">Default services and application parameters are configured in hello application and service manifests.</span></span> <span data-ttu-id="f3319-116">viene installato con hello Service Fabric SDK Hello definizione dello schema per file ServiceManifest.xml e ApplicationManifest.xml hello e strumenti troppo*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="f3319-116">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml files is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

### <a name="default-services"></a><span data-ttu-id="f3319-117">Servizi predefiniti</span><span class="sxs-lookup"><span data-stu-id="f3319-117">Default services</span></span>
<span data-ttu-id="f3319-118">Le applicazioni di infrastruttura di servizi sono costituite da una raccolta di istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="f3319-118">Service Fabric applications are made up of a collection of service instances.</span></span> <span data-ttu-id="f3319-119">Mentre è possibile che si toocreate un'applicazione vuota e quindi creare tutte le istanze di servizio in modo dinamico, la maggior parte delle applicazioni dispongono di un set di servizi di base che deve sempre essere creata quando viene creata un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-119">While it is possible for you toocreate an empty application and then create all service instances dynamically, most applications have a set of core services that should always be created when hello application is instantiated.</span></span> <span data-ttu-id="f3319-120">Si tratta di cui viene fatto riferimento tooas "servizi predefiniti".</span><span class="sxs-lookup"><span data-stu-id="f3319-120">These are referred tooas "default services".</span></span> <span data-ttu-id="f3319-121">Vengono specificati nel manifesto dell'applicazione hello, con segnaposto per la configurazione per ogni ambiente inclusi tra parentesi quadre:</span><span class="sxs-lookup"><span data-stu-id="f3319-121">They are specified in hello application manifest, with placeholders for per-environment configuration included in square brackets:</span></span>

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

<span data-ttu-id="f3319-122">Ognuno dei parametri denominato hello deve essere definito nell'elemento Parameters hello del manifesto dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="f3319-122">Each of hello named parameters must be defined within hello Parameters element of hello application manifest:</span></span>

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

<span data-ttu-id="f3319-123">l'attributo DefaultValue Hello specifica hello valore toobe utilizzata in assenza di hello di parametro più specifici per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="f3319-123">hello DefaultValue attribute specifies hello value toobe used in hello absence of a more-specific parameter for a given environment.</span></span>

> [!NOTE]
> <span data-ttu-id="f3319-124">Non tutti i parametri di istanza del servizio sono idonei alla configurazione specifica per il singolo ambiente.</span><span class="sxs-lookup"><span data-stu-id="f3319-124">Not all service instance parameters are suitable for per-environment configuration.</span></span> <span data-ttu-id="f3319-125">Nell'esempio hello sopra, hello LowKey e i valori di HighKey per lo schema di partizionamento del servizio hello definiti in modo esplicito per tutte le istanze del servizio hello dall'intervallo di partizione hello è una funzione hello di domini di dati, non l'ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-125">In hello example above, hello LowKey and HighKey values for hello service's partitioning scheme are explicitly defined for all instances of hello service since hello partition range is a function of hello data domain, not hello environment.</span></span>
> 
> 

### <a name="per-environment-service-configuration-settings"></a><span data-ttu-id="f3319-126">Impostazioni della configurazione del servizio specifica per il singolo ambiente</span><span class="sxs-lookup"><span data-stu-id="f3319-126">Per-environment service configuration settings</span></span>
<span data-ttu-id="f3319-127">Hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md) Abilita servizi tooinclude i pacchetti di configurazione che contengono coppie chiave-valore personalizzate che sono leggibili in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f3319-127">hello [Service Fabric application model](service-fabric-application-model.md) enables services tooinclude configuration packages that contain custom key-value pairs that are readable at run time.</span></span> <span data-ttu-id="f3319-128">i valori Hello di queste impostazioni possono essere distinti anche dall'ambiente specificando un `ConfigOverride` nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-128">hello values of these settings can also be differentiated by environment by specifying a `ConfigOverride` in hello application manifest.</span></span>

<span data-ttu-id="f3319-129">Si supponga di avere hello seguente impostazione nel file hello Config\Settings.xml hello `Stateful1` servizio:</span><span class="sxs-lookup"><span data-stu-id="f3319-129">Suppose that you have hello following setting in hello Config\Settings.xml file for hello `Stateful1` service:</span></span>

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
<span data-ttu-id="f3319-130">toooverride questo valore per una coppia di applicazione/ambiente specifico, creare un `ConfigOverride` quando si importa hello manifesto del servizio nel manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-130">toooverride this value for a specific application/environment pair, create a `ConfigOverride` when you import hello service manifest in hello application manifest.</span></span>

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
<span data-ttu-id="f3319-131">Questo parametro può quindi essere configurato dall'ambiente, come illustrato in precedenza,</span><span class="sxs-lookup"><span data-stu-id="f3319-131">This parameter can then be configured by environment as shown above.</span></span> <span data-ttu-id="f3319-132">È possibile farlo dichiararla nella sezione parametri hello del manifesto dell'applicazione hello e specificando i valori specifici dell'ambiente nei file di parametro dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-132">You can do this by declaring it in hello parameters section of hello application manifest and specifying environment-specific values in hello application parameter files.</span></span>

> [!NOTE]
> <span data-ttu-id="f3319-133">Nel caso di hello di impostazioni di configurazione del servizio, ci sono tre posizioni in cui è possibile impostare il valore di hello di una chiave: pacchetto di configurazione del servizio hello manifesto dell'applicazione hello e file di parametro dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-133">In hello case of service configuration settings, there are three places where hello value of a key can be set: hello service configuration package, hello application manifest, and hello application parameter file.</span></span> <span data-ttu-id="f3319-134">Service Fabric verrà sempre scegliere da file di parametro dell'applicazione hello prima (se specificato), quindi hello manifesto dell'applicazione e infine hello pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3319-134">Service Fabric will always choose from hello application parameter file first (if specified), then hello application manifest, and finally hello configuration package.</span></span>
> 
> 

### <a name="setting-and-using-environment-variables"></a><span data-ttu-id="f3319-135">Impostazione e uso delle variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="f3319-135">Setting and using environment variables</span></span> 
<span data-ttu-id="f3319-136">È possibile specificare e impostare le variabili di ambiente nel file ServiceManifest.xml hello e quindi eseguire l'override di questi elementi nel file ApplicationManifest XML hello in ogni istanza.</span><span class="sxs-lookup"><span data-stu-id="f3319-136">You can specify and set environment variables in hello ServiceManifest.xml file and then override these in hello ApplicationManifest.xml file on a per instance basis.</span></span>
<span data-ttu-id="f3319-137">Hello di esempio seguente mostra che due variabili di ambiente, uno con un valore impostato e viene eseguito l'override di altri hello.</span><span class="sxs-lookup"><span data-stu-id="f3319-137">hello example below shows two environment variables, one with a value set and hello other is overridden.</span></span> <span data-ttu-id="f3319-138">È possibile utilizzare i parametri dell'applicazione, le variabili di ambiente tooset valori hello stesso modo che questi sono stati utilizzati per le sostituzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f3319-138">You can use application parameters tooset environment variables values in hello same way that these were used for config overrides.</span></span>

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
<span data-ttu-id="f3319-139">variabili di ambiente toooverride hello in ApplicationManifest.xml, pacchetto di codice hello riferimento nel manifesto del servizio di hello con hello hello `EnvironmentOverrides` elemento.</span><span class="sxs-lookup"><span data-stu-id="f3319-139">toooverride hello environment variables in hello ApplicationManifest.xml, reference hello code package in hello ServiceManifest with hello `EnvironmentOverrides` element.</span></span>

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 <span data-ttu-id="f3319-140">Una volta creato l'istanza di servizio denominata hello è possibile accedere a variabili di ambiente hello dal codice.</span><span class="sxs-lookup"><span data-stu-id="f3319-140">Once hello named service instance is created you can access hello environment variables from code.</span></span> <span data-ttu-id="f3319-141">ad esempio In c# è possibile eseguire il seguente hello</span><span class="sxs-lookup"><span data-stu-id="f3319-141">e.g. In C# you can do hello following</span></span>

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a><span data-ttu-id="f3319-142">Variabili di ambiente di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3319-142">Service Fabric environment variables</span></span>
<span data-ttu-id="f3319-143">Service Fabric dispone di variabili di ambiente predefinite, impostate per ciascuna istanza di servizio.</span><span class="sxs-lookup"><span data-stu-id="f3319-143">Service Fabric has built in environment variables set for each service instance.</span></span> <span data-ttu-id="f3319-144">Hello elenco completo delle variabili di ambiente viene di seguito, dove hello quelle in grassetto sono hello quelle che si utilizzerà nel servizio, hello altro che utilizzate dal runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f3319-144">hello full list of environment variables is below, where hello ones in bold are hello ones that you will use in your service, hello other being used by Service Fabric runtime.</span></span> 

* <span data-ttu-id="f3319-145">Fabric_ApplicationHostId</span><span class="sxs-lookup"><span data-stu-id="f3319-145">Fabric_ApplicationHostId</span></span>
* <span data-ttu-id="f3319-146">Fabric_ApplicationHostType</span><span class="sxs-lookup"><span data-stu-id="f3319-146">Fabric_ApplicationHostType</span></span>
* <span data-ttu-id="f3319-147">Fabric_ApplicationId</span><span class="sxs-lookup"><span data-stu-id="f3319-147">Fabric_ApplicationId</span></span>
* <span data-ttu-id="f3319-148">**Fabric_ApplicationName**</span><span class="sxs-lookup"><span data-stu-id="f3319-148">**Fabric_ApplicationName**</span></span>
* <span data-ttu-id="f3319-149">Fabric_CodePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="f3319-149">Fabric_CodePackageInstanceId</span></span>
* <span data-ttu-id="f3319-150">**Fabric_CodePackageName**</span><span class="sxs-lookup"><span data-stu-id="f3319-150">**Fabric_CodePackageName**</span></span>
* <span data-ttu-id="f3319-151">**Fabric_Endpoint_[NomeDelServizio]TypeEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f3319-151">**Fabric_Endpoint_[YourServiceName]TypeEndpoint**</span></span>
* <span data-ttu-id="f3319-152">**Fabric_Folder_App_Log**</span><span class="sxs-lookup"><span data-stu-id="f3319-152">**Fabric_Folder_App_Log**</span></span>
* <span data-ttu-id="f3319-153">**Fabric_Folder_App_Temp**</span><span class="sxs-lookup"><span data-stu-id="f3319-153">**Fabric_Folder_App_Temp**</span></span>
* <span data-ttu-id="f3319-154">**Fabric_Folder_App_Work**</span><span class="sxs-lookup"><span data-stu-id="f3319-154">**Fabric_Folder_App_Work**</span></span>
* <span data-ttu-id="f3319-155">**Fabric_Folder_Application**</span><span class="sxs-lookup"><span data-stu-id="f3319-155">**Fabric_Folder_Application**</span></span>
* <span data-ttu-id="f3319-156">Fabric_NodeId</span><span class="sxs-lookup"><span data-stu-id="f3319-156">Fabric_NodeId</span></span>
* <span data-ttu-id="f3319-157">**Fabric_NodeIPOrFQDN**</span><span class="sxs-lookup"><span data-stu-id="f3319-157">**Fabric_NodeIPOrFQDN**</span></span>
* <span data-ttu-id="f3319-158">**Fabric_NodeName**</span><span class="sxs-lookup"><span data-stu-id="f3319-158">**Fabric_NodeName**</span></span>
* <span data-ttu-id="f3319-159">Fabric_RuntimeConnectionAddress</span><span class="sxs-lookup"><span data-stu-id="f3319-159">Fabric_RuntimeConnectionAddress</span></span>
* <span data-ttu-id="f3319-160">Fabric_ServicePackageInstanceId</span><span class="sxs-lookup"><span data-stu-id="f3319-160">Fabric_ServicePackageInstanceId</span></span>
* <span data-ttu-id="f3319-161">Fabric_ServicePackageName</span><span class="sxs-lookup"><span data-stu-id="f3319-161">Fabric_ServicePackageName</span></span>
* <span data-ttu-id="f3319-162">Fabric_ServicePackageVersionInstance</span><span class="sxs-lookup"><span data-stu-id="f3319-162">Fabric_ServicePackageVersionInstance</span></span>
* <span data-ttu-id="f3319-163">FabricPackageFileName</span><span class="sxs-lookup"><span data-stu-id="f3319-163">FabricPackageFileName</span></span>

<span data-ttu-id="f3319-164">Hello belows di codice viene illustrato come toolist hello le variabili di ambiente di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f3319-164">hello code belows shows how toolist hello Service Fabric environment variables</span></span>
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
<span data-ttu-id="f3319-165">Hello esempi seguenti vengono illustrate le variabili di ambiente per un tipo di applicazione denominato `GuestExe.Application` con un tipo di servizio denominato `FrontEndService` quando viene eseguito sul computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="f3319-165">hello following are examples of environment variables for an application type called `GuestExe.Application` with a service type called `FrontEndService` when run on your local dev machine.</span></span>

* <span data-ttu-id="f3319-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span><span class="sxs-lookup"><span data-stu-id="f3319-166">**Fabric_ApplicationName = fabric:/GuestExe.Application**</span></span>
* <span data-ttu-id="f3319-167">**Fabric_CodePackageName = Code**</span><span class="sxs-lookup"><span data-stu-id="f3319-167">**Fabric_CodePackageName = Code**</span></span>
* <span data-ttu-id="f3319-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span><span class="sxs-lookup"><span data-stu-id="f3319-168">**Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**</span></span>
* <span data-ttu-id="f3319-169">**Fabric_NodeIPOrFQDN = localhost**</span><span class="sxs-lookup"><span data-stu-id="f3319-169">**Fabric_NodeIPOrFQDN = localhost**</span></span>
* <span data-ttu-id="f3319-170">**Fabric_NodeName = _Node_2**</span><span class="sxs-lookup"><span data-stu-id="f3319-170">**Fabric_NodeName = _Node_2**</span></span>

### <a name="application-parameter-files"></a><span data-ttu-id="f3319-171">File di parametri dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f3319-171">Application parameter files</span></span>
<span data-ttu-id="f3319-172">progetto di applicazione di Service Fabric Hello può includere uno o più file di parametro dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3319-172">hello Service Fabric application project can include one or more application parameter files.</span></span> <span data-ttu-id="f3319-173">Ognuno di essi definisce hello specifici valori hello parametri definiti nel manifesto dell'applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="f3319-173">Each of them defines hello specific values for hello parameters that are defined in hello application manifest:</span></span>

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
<span data-ttu-id="f3319-174">Per impostazione predefinita, una nuova applicazione include tre file di parametro dell'applicazione, denominati Local.1Node.xml, Local.5Node.xml e Cloud.xml:</span><span class="sxs-lookup"><span data-stu-id="f3319-174">By default, a new application includes three application parameter files, named Local.1Node.xml, Local.5Node.xml, and Cloud.xml:</span></span>

![File di parametri dell'applicazione in Esplora soluzioni][app-parameters-solution-explorer]

<span data-ttu-id="f3319-176">un file di parametro, toocreate semplicemente copiare e incollare uno esistente quindi assegnarle un nuovo nome.</span><span class="sxs-lookup"><span data-stu-id="f3319-176">toocreate a parameter file, simply copy and paste an existing one and give it a new name.</span></span>

## <a name="identifying-environment-specific-parameters-during-deployment"></a><span data-ttu-id="f3319-177">Identificazione di parametri specifici per il singolo ambiente durante la distribuzione</span><span class="sxs-lookup"><span data-stu-id="f3319-177">Identifying environment-specific parameters during deployment</span></span>
<span data-ttu-id="f3319-178">In fase di distribuzione, è necessario toochoose hello parametro appropriato file tooapply con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3319-178">At deployment time, you need toochoose hello appropriate parameter file tooapply with your application.</span></span> <span data-ttu-id="f3319-179">È possibile farlo tramite una finestra di dialogo pubblicazione hello in Visual Studio o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3319-179">You can do this through hello Publish dialog in Visual Studio or through PowerShell.</span></span>

### <a name="deploy-from-visual-studio"></a><span data-ttu-id="f3319-180">Eseguire una distribuzione da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3319-180">Deploy from Visual Studio</span></span>
<span data-ttu-id="f3319-181">È possibile scegliere dall'elenco di hello del file dei parametri disponibili quando si pubblica l'applicazione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f3319-181">You can choose from hello list of available parameter files when you publish your application in Visual Studio.</span></span>

![Scegliere un file di parametri nella finestra di dialogo pubblicazione hello][publishdialog]

### <a name="deploy-from-powershell"></a><span data-ttu-id="f3319-183">Distribuire da PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3319-183">Deploy from PowerShell</span></span>
<span data-ttu-id="f3319-184">Hello `Deploy-FabricApplication.ps1` script di PowerShell incluso nel modello di progetto applicazione hello accetta come parametro di un profilo di pubblicazione e hello PublishProfile contiene un file di parametri di riferimento toohello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f3319-184">hello `Deploy-FabricApplication.ps1` PowerShell script included in hello application project template accepts a publish profile as a parameter and hello PublishProfile contains a reference toohello application parameters file.</span></span>

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a><span data-ttu-id="f3319-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3319-185">Next steps</span></span>
<span data-ttu-id="f3319-186">toolearn informazioni su alcuni dei concetti di base hello discussi sono trattati in questo argomento, vedere hello [Panoramica tecnica di Service Fabric](service-fabric-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3319-186">toolearn more about some of hello core concepts that are discussed in this topic, see hello [Service Fabric technical overview](service-fabric-technical-overview.md).</span></span> <span data-ttu-id="f3319-187">Per informazioni su altre funzionalità di gestione delle app disponibili in Visual Studio, vedere [Usare Visual Studio per semplificare la scrittura e la gestione delle applicazioni di Service Fabric](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f3319-187">For information about other app management capabilities that are available in Visual Studio, see [Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
