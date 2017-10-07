---
title: aaaAzure Service Fabric Docker comporre Preview
description: "Azure Service Fabric accetta Docker Compose toomake formato è più facile tooorchestrate i contenitori esistenti usando Service Fabric. Questo supporto è attualmente disponibile in versione di anteprima."
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
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="82ec3-104">Supporto dell'applicazione Docker Compose in Azure Service Fabric (anteprima)</span><span class="sxs-lookup"><span data-stu-id="82ec3-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="82ec3-105">Docker utilizza hello [docker compose.yml](https://docs.docker.com/compose) file per la definizione di un contenitore a più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="82ec3-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="82ec3-106">toomake è facile per i clienti familiari con Docker tooorchestrate applicazioni contenitore esistenti in Azure Service Fabric è stato incluso il supporto di anteprima per Docker Compose in modo nativo nella piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="82ec3-107">Service Fabric può accettare la versione 3 (o successiva) dei file `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="82ec3-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="82ec3-108">Poiché questo supporto è disponibile in anteprima, è supportato solo un subset delle direttive Compose.</span><span class="sxs-lookup"><span data-stu-id="82ec3-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="82ec3-109">Non sono supportati, ad esempio, gli aggiornamenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="82ec3-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="82ec3-110">Tuttavia, è sempre possibile rimuovere e distribuire le applicazioni invece di aggiornarle.</span><span class="sxs-lookup"><span data-stu-id="82ec3-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="82ec3-111">toouse questa anteprima, creare il cluster con la versione 5.7 o versione successiva del runtime di Service Fabric hello tramite hello Azure portal insieme hello corrispondente SDK.</span><span class="sxs-lookup"><span data-stu-id="82ec3-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="82ec3-112">Questa funzionalità è in versione di anteprima e non è supportata in produzione.</span><span class="sxs-lookup"><span data-stu-id="82ec3-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="82ec3-113">Distribuire un file Docker Compose in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="82ec3-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="82ec3-114">i comandi seguenti Hello creano un'applicazione di Service Fabric (denominato `fabric:/TestContainerApp` nel precedente esempio hello), che è possibile monitorare e gestire come qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="82ec3-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="82ec3-115">È possibile utilizzare il nome di applicazione specificato hello per le query di integrità.</span><span class="sxs-lookup"><span data-stu-id="82ec3-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="82ec3-116">Usare PowerShell</span><span class="sxs-lookup"><span data-stu-id="82ec3-116">Use PowerShell</span></span>

<span data-ttu-id="82ec3-117">Creare un'applicazione di servizio Fabric comporre da un file docker compose.yml eseguendo hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="82ec3-118">`RegistryUserName`e `RegistryPassword` riferimento toohello contenitore del Registro di sistema username e password.</span><span class="sxs-lookup"><span data-stu-id="82ec3-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="82ec3-119">Dopo aver completato un'applicazione hello, è possibile controllare lo stato tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="82ec3-120">toodelete hello applicazione comporre tramite PowerShell, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="82ec3-121">Usare l'interfaccia della riga di comando di Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="82ec3-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="82ec3-122">In alternativa, è possibile utilizzare hello comando CLI di infrastruttura del servizio seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="82ec3-123">Dopo aver creato un'applicazione hello, è possibile controllare lo stato tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="82ec3-124">hello toodelete comporre applicazione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82ec3-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="82ec3-125">Direttive Compose supportate</span><span class="sxs-lookup"><span data-stu-id="82ec3-125">Supported Compose directives</span></span>

<span data-ttu-id="82ec3-126">Questa versione di anteprima supporta un subset di opzioni di configurazione hello dal formato di versione 3 comporre hello, inclusi hello primitive seguenti:</span><span class="sxs-lookup"><span data-stu-id="82ec3-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="82ec3-127">Services > Deploy > Replicas</span><span class="sxs-lookup"><span data-stu-id="82ec3-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="82ec3-128">Services > Deploy > Placement > Constraints</span><span class="sxs-lookup"><span data-stu-id="82ec3-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="82ec3-129">Services > Deploy > Resources > Limits</span><span class="sxs-lookup"><span data-stu-id="82ec3-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="82ec3-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="82ec3-130">-cpu-shares</span></span>
    * <span data-ttu-id="82ec3-131">-memory</span><span class="sxs-lookup"><span data-stu-id="82ec3-131">-memory</span></span>
    * <span data-ttu-id="82ec3-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="82ec3-132">-memory-swap</span></span>
* <span data-ttu-id="82ec3-133">Services > Commands</span><span class="sxs-lookup"><span data-stu-id="82ec3-133">Services > Commands</span></span>
* <span data-ttu-id="82ec3-134">Services > Environment</span><span class="sxs-lookup"><span data-stu-id="82ec3-134">Services > Environment</span></span>
* <span data-ttu-id="82ec3-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="82ec3-135">Services > Ports</span></span>
* <span data-ttu-id="82ec3-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="82ec3-136">Services > Image</span></span>
* <span data-ttu-id="82ec3-137">Services > Isolation (solo per Windows)</span><span class="sxs-lookup"><span data-stu-id="82ec3-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="82ec3-138">Services > Logging > Driver</span><span class="sxs-lookup"><span data-stu-id="82ec3-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="82ec3-139">Services > Logging > Driver > Options</span><span class="sxs-lookup"><span data-stu-id="82ec3-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="82ec3-140">Volume & Deploy > Volume</span><span class="sxs-lookup"><span data-stu-id="82ec3-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="82ec3-141">Configurazione di cluster di hello per applicare i limiti delle risorse, come descritto in [governance delle risorse di Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="82ec3-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="82ec3-142">Tutte le altre direttive Docker Compose non sono supportate per questa versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="82ec3-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="82ec3-143">Calcolo di ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="82ec3-143">ServiceDnsName computation</span></span>

<span data-ttu-id="82ec3-144">Se il nome del servizio hello specificato in un file di contenuto è un nome di dominio completo (ovvero, contiene un punto [.]), il nome DNS hello registrato da Service Fabric è `<ServiceName>` (incluso il punto di hello).</span><span class="sxs-lookup"><span data-stu-id="82ec3-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="82ec3-145">In caso contrario, ogni segmento di percorso nel nome dell'applicazione hello diventa un'etichetta di dominio nel nome DNS del servizio hello, con hello primo segmento del percorso diventando etichetta di dominio di primo livello hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="82ec3-146">Ad esempio, se hello specificato nome di applicazione è `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` sarebbe hello nome DNS registrato.</span><span class="sxs-lookup"><span data-stu-id="82ec3-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="82ec3-147">Differenze tra Compose (definizione di istanza) e il modello di applicazione di Service Fabric (definizione di tipo)</span><span class="sxs-lookup"><span data-stu-id="82ec3-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="82ec3-148">Un file docker-compose.yml descrive un set distribuibile di contenitori, incluse le relative proprietà e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="82ec3-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="82ec3-149">Ad esempio, file hello può contenere variabili di ambiente e porte.</span><span class="sxs-lookup"><span data-stu-id="82ec3-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="82ec3-150">È anche possibile specificare parametri di distribuzione, ad esempio i vincoli di posizione, i limiti delle risorse e i nomi DNS nel file docker compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="82ec3-151">Hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md) Usa i tipi di servizio e tipi di applicazione, in cui si possono avere molte istanze di applicazione di hello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="82ec3-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="82ec3-152">È possibile, ad esempio, che sia presente un'istanza dell'applicazione per ogni cliente.</span><span class="sxs-lookup"><span data-stu-id="82ec3-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="82ec3-153">Questo modello basato sul tipo supporta più versioni di hello stesso tipo di applicazione è registrata con il runtime di hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="82ec3-154">Ad esempio, il cliente può disporre di un'applicazione creata un'istanza con tipo, 1.0 di AppTypeA e cliente B può disporre di un'altra applicazione creata con hello lo stesso tipo e versione.</span><span class="sxs-lookup"><span data-stu-id="82ec3-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="82ec3-155">Definire i tipi di applicazione hello nei manifesti di applicazione hello e specificare i parametri di nome e la distribuzione di applicazione hello quando si crea un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="82ec3-156">Anche se questo modello offre flessibilità, è inoltre pianificare toosupport un modello di distribuzione più semplice, basato su istanza in cui tipi sono impliciti dal file manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="82ec3-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="82ec3-157">In questo modello, ogni applicazione ottiene il proprio manifesto indipendente.</span><span class="sxs-lookup"><span data-stu-id="82ec3-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="82ec3-158">Questa funzionalità viene offerta in anteprima aggiungendo il supporto per docker-compose.yml, che è un formato di distribuzione basato su istanze.</span><span class="sxs-lookup"><span data-stu-id="82ec3-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82ec3-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82ec3-159">Next steps</span></span>

* <span data-ttu-id="82ec3-160">Informazioni sull'hello [il modello di applicazione di Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="82ec3-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* [<span data-ttu-id="82ec3-161">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="82ec3-161">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)
