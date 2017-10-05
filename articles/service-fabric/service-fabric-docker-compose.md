---
title: Anteprima di Docker Compose di Azure Service Fabric
description: "Azure Service Fabric accetta il formato Docker Compose per orchestrare più facilmente i contenitori esistenti. Questo supporto è attualmente disponibile in versione di anteprima."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="77bd8-104">Supporto dell'applicazione Docker Compose in Azure Service Fabric (anteprima)</span><span class="sxs-lookup"><span data-stu-id="77bd8-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="77bd8-105">Docker usa il file [docker-compose.yml](https://docs.docker.com/compose) per la definizione di applicazioni multi-contenitore.</span><span class="sxs-lookup"><span data-stu-id="77bd8-105">Docker uses the [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="77bd8-106">Per consentire ai clienti che hanno familiarità con Docker di coordinare più facilmente le applicazioni contenitore presenti in Azure Service Fabric, è stato incluso nella piattaforma il supporto nativo per Docker Compose, in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="77bd8-106">To make it easy for customers familiar with Docker to orchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in the platform.</span></span> <span data-ttu-id="77bd8-107">Service Fabric può accettare la versione 3 (o successiva) dei file `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="77bd8-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="77bd8-108">Poiché questo supporto è disponibile in anteprima, è supportato solo un subset delle direttive Compose.</span><span class="sxs-lookup"><span data-stu-id="77bd8-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="77bd8-109">Non sono supportati, ad esempio, gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="77bd8-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="77bd8-110">Tuttavia, è sempre possibile rimuovere e distribuire le applicazioni invece di aggiornarle.</span><span class="sxs-lookup"><span data-stu-id="77bd8-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="77bd8-111">Per usare questa versione di anteprima, creare il cluster con la versione 5.7 o versione successiva del runtime di Service Fabric tramite il portale di Azure con l'SDK corrispondente.</span><span class="sxs-lookup"><span data-stu-id="77bd8-111">To use this preview, create your cluster with version 5.7 or greater of the Service Fabric runtime through the Azure portal along with the corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="77bd8-112">Questa funzionalità è in versione di anteprima e non è supportata in produzione.</span><span class="sxs-lookup"><span data-stu-id="77bd8-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="77bd8-113">Distribuire un file Docker Compose in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="77bd8-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="77bd8-114">I comandi seguenti creano un'applicazione di Service Fabric (denominata `fabric:/TestContainerApp` nell'esempio precedente) che è possibile monitorare e gestire analogamente a qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="77bd8-114">The following commands create a Service Fabric application (named `fabric:/TestContainerApp` in the preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="77bd8-115">Per eseguire query sull'integrità, è possibile usare il nome dell'applicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="77bd8-115">You can use the specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="77bd8-116">Usare PowerShell</span><span class="sxs-lookup"><span data-stu-id="77bd8-116">Use PowerShell</span></span>

<span data-ttu-id="77bd8-117">Creare un'applicazione Compose di Service Fabric da un file docker-compose.yml eseguendo il comando seguente in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="77bd8-117">Create a Service Fabric Compose application from a docker-compose.yml file by running the following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="77bd8-118">`RegistryUserName` e `RegistryPassword` fanno riferimento al nome utente e alla password del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="77bd8-118">`RegistryUserName` and `RegistryPassword` refer to the container registry username and password.</span></span> <span data-ttu-id="77bd8-119">Dopo aver completato l'applicazione, è possibile controllarne lo stato usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77bd8-119">After you've completed the application, you can check its status by using the following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="77bd8-120">Per eliminare l'applicazione Compose tramite PowerShell, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77bd8-120">To delete the Compose application through PowerShell, use the following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="77bd8-121">Usare l'interfaccia della riga di comando di Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="77bd8-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="77bd8-122">In alternativa, è possibile usare il comando dell'interfaccia della riga di comando di Service Fabric seguente:</span><span class="sxs-lookup"><span data-stu-id="77bd8-122">Alternatively, you can use the following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="77bd8-123">Dopo aver creato l'applicazione, è possibile controllarne lo stato usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77bd8-123">After you've created the application, you can check its status by using the following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="77bd8-124">Per eliminare l'applicazione Compose, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="77bd8-124">To delete the Compose application, use the following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="77bd8-125">Direttive Compose supportate</span><span class="sxs-lookup"><span data-stu-id="77bd8-125">Supported Compose directives</span></span>

<span data-ttu-id="77bd8-126">Questa versione di anteprima supporta un subset delle opzioni di configurazione a partire dal formato Compose versione 3, incluse le primitive seguenti:</span><span class="sxs-lookup"><span data-stu-id="77bd8-126">This preview supports a subset of the configuration options from the Compose version 3 format, including the following primitives:</span></span>

* <span data-ttu-id="77bd8-127">Services > Deploy > Replicas</span><span class="sxs-lookup"><span data-stu-id="77bd8-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="77bd8-128">Services > Deploy > Placement > Constraints</span><span class="sxs-lookup"><span data-stu-id="77bd8-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="77bd8-129">Services > Deploy > Resources > Limits</span><span class="sxs-lookup"><span data-stu-id="77bd8-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="77bd8-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="77bd8-130">-cpu-shares</span></span>
    * <span data-ttu-id="77bd8-131">-memory</span><span class="sxs-lookup"><span data-stu-id="77bd8-131">-memory</span></span>
    * <span data-ttu-id="77bd8-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="77bd8-132">-memory-swap</span></span>
* <span data-ttu-id="77bd8-133">Services > Commands</span><span class="sxs-lookup"><span data-stu-id="77bd8-133">Services > Commands</span></span>
* <span data-ttu-id="77bd8-134">Services > Environment</span><span class="sxs-lookup"><span data-stu-id="77bd8-134">Services > Environment</span></span>
* <span data-ttu-id="77bd8-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="77bd8-135">Services > Ports</span></span>
* <span data-ttu-id="77bd8-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="77bd8-136">Services > Image</span></span>
* <span data-ttu-id="77bd8-137">Services > Isolation (solo per Windows)</span><span class="sxs-lookup"><span data-stu-id="77bd8-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="77bd8-138">Services > Logging > Driver</span><span class="sxs-lookup"><span data-stu-id="77bd8-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="77bd8-139">Services > Logging > Driver > Options</span><span class="sxs-lookup"><span data-stu-id="77bd8-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="77bd8-140">Volume & Deploy > Volume</span><span class="sxs-lookup"><span data-stu-id="77bd8-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="77bd8-141">Configurare il cluster in modo da applicare i limiti delle risorse, come descritto in [Governance delle risorse di Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="77bd8-141">Set up the cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="77bd8-142">Tutte le altre direttive Docker Compose non sono supportate per questa versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="77bd8-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="77bd8-143">Calcolo di ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="77bd8-143">ServiceDnsName computation</span></span>

<span data-ttu-id="77bd8-144">Se il nome del servizio specificato nel file Compose è un nome di dominio completo (ovvero contiene un punto [.]), il nome DNS registrato da Service Fabric è `<ServiceName>`, incluso il punto.</span><span class="sxs-lookup"><span data-stu-id="77bd8-144">If the service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), the DNS name registered by Service Fabric is `<ServiceName>` (including the dot).</span></span> <span data-ttu-id="77bd8-145">In caso contrario, ogni segmento di percorso nel nome dell'applicazione diventa un'etichetta di dominio nel nome DNS del servizio, con il primo segmento di percorso che diventa l'etichetta di dominio di primo livello.</span><span class="sxs-lookup"><span data-stu-id="77bd8-145">If not, each path segment in the application name becomes a domain label in the service DNS name, with the first path segment becoming the top-level domain label.</span></span>

<span data-ttu-id="77bd8-146">Se, ad esempio, il nome specificato per l'applicazione è `fabric:/SampleApp/MyComposeApp`, il nome DNS registrato sarà `<ServiceName>.MyComposeApp.SampleApp`.</span><span class="sxs-lookup"><span data-stu-id="77bd8-146">For example, if the specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be the registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="77bd8-147">Differenze tra Compose (definizione di istanza) e il modello di applicazione di Service Fabric (definizione di tipo)</span><span class="sxs-lookup"><span data-stu-id="77bd8-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="77bd8-148">Un file docker-compose.yml descrive un set distribuibile di contenitori, incluse le relative proprietà e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="77bd8-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="77bd8-149">Il file può contenere, ad esempio, variabili di ambiente e porte.</span><span class="sxs-lookup"><span data-stu-id="77bd8-149">For example, the file can contain environment variables and ports.</span></span> <span data-ttu-id="77bd8-150">Nel file docker-compose.yml è possibile specificare anche i parametri di distribuzione, ad esempio i vincoli di posizionamento, i limiti delle risorse e i nomi DNS.</span><span class="sxs-lookup"><span data-stu-id="77bd8-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in the docker-compose.yml file.</span></span>

<span data-ttu-id="77bd8-151">Il [modello di applicazione di Service Fabric](service-fabric-application-model.md) usa tipi di servizio e tipi di applicazione, in cui possono coesistere numerose istanze dell'applicazione dello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="77bd8-151">The [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of the same type.</span></span> <span data-ttu-id="77bd8-152">È possibile, ad esempio, che sia presente un'istanza dell'applicazione per ogni cliente.</span><span class="sxs-lookup"><span data-stu-id="77bd8-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="77bd8-153">Questo modello basato sul tipo supporta più versioni dello stesso tipo di applicazione registrato con il runtime.</span><span class="sxs-lookup"><span data-stu-id="77bd8-153">This type-based model supports multiple versions of the same application type that's registered with the runtime.</span></span>

<span data-ttu-id="77bd8-154">Il cliente A, ad esempio, può avere un'applicazione di cui è stata creata un'istanza con il tipo 1.0 di AppTypeA e il cliente B può avere un'altra applicazione di cui è stata creata un'istanza con lo stesso tipo e la stessa versione.</span><span class="sxs-lookup"><span data-stu-id="77bd8-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with the same type and version.</span></span> <span data-ttu-id="77bd8-155">I tipi di applicazione vengono definiti nei manifesti dell'applicazione e il nome dell'applicazione e i parametri di distribuzione vengono specificati al momento della creazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="77bd8-155">You define the application types in the application manifests, and you specify the application name and deployment parameters when you create the application.</span></span>

<span data-ttu-id="77bd8-156">Questo modello offre flessibilità, ma è previsto anche il supporto di un modello di distribuzione basato su istanze più semplice, in cui i tipi sono impliciti nel file manifesto.</span><span class="sxs-lookup"><span data-stu-id="77bd8-156">Although this model offers flexibility, we are also planning to support a simpler, instance-based deployment model where types are implicit from the manifest file.</span></span> <span data-ttu-id="77bd8-157">In questo modello, ogni applicazione ottiene il proprio manifesto indipendente.</span><span class="sxs-lookup"><span data-stu-id="77bd8-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="77bd8-158">Questa funzionalità viene offerta in anteprima aggiungendo il supporto per docker-compose.yml, che è un formato di distribuzione basato su istanze.</span><span class="sxs-lookup"><span data-stu-id="77bd8-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77bd8-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77bd8-159">Next steps</span></span>

* <span data-ttu-id="77bd8-160">Leggere le informazioni sul [modello di applicazione di Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="77bd8-160">Read up on the [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="77bd8-161">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="77bd8-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
