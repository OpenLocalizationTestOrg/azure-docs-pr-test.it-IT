---
title: Argomenti avanzati sull'aggiornamento di un'applicazione | Documentazione Microsoft
description: Questo articolo illustra alcuni degli argomenti avanzati relativi all'aggiornamento di un'applicazione di Service Fabric.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: 8d3b922f3d50b645ac9db2cc879a319df1262e0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="1a9d1-103">Aggiornamento di un'applicazione di Service Fabric: argomenti avanzati</span><span class="sxs-lookup"><span data-stu-id="1a9d1-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="1a9d1-104">Aggiungere o rimuovere servizi durante l'aggiornamento di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="1a9d1-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="1a9d1-105">Se viene aggiunto un nuovo servizio a un'applicazione che è già distribuita e viene pubblicato come aggiornamento, il nuovo servizio viene aggiunto all'applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-105">If a new service is added to an application that is already deployed, and published as an upgrade, the new service is added to the deployed application.</span></span>  <span data-ttu-id="1a9d1-106">Un aggiornamento di questo tipo non influisce su nessuno dei servizi già inclusi nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-106">Such an upgrade does not affect any of the services that were already part of the application.</span></span> <span data-ttu-id="1a9d1-107">È tuttavia necessario che venga avviata un'istanza del servizio che è stato aggiunto, tramite il cmdlet `New-ServiceFabricService` , perché il nuovo servizio sia attivo.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-107">However, an instance of the service that was added must be started for the new service to be active (using the `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="1a9d1-108">Un aggiornamento può anche prevedere la rimozione di determinati servizi da un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="1a9d1-109">Tuttavia è necessario arrestare tutte le istanze correnti del servizio da eliminare prima di procedere con l'aggiornamento (usando il cmdlet `Remove-ServiceFabricService` ).</span><span class="sxs-lookup"><span data-stu-id="1a9d1-109">However, all current instances of the to-be-deleted service must be stopped before proceeding with the upgrade (using the `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="1a9d1-110">Modalità di aggiornamento manuale</span><span class="sxs-lookup"><span data-stu-id="1a9d1-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="1a9d1-111">La modalità di aggiornamento UnmonitoredManual deve essere presa in considerazione solo per un aggiornamento non riuscito o sospeso.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-111">The unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="1a9d1-112">La modalità di aggiornamento consigliata per le applicazioni di Service Fabric è la modalità monitorata.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-112">The monitored mode is the recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="1a9d1-113">Azure Service Fabric offre diverse modalità di aggiornamento per supportare i cluster di sviluppo e di produzione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-113">Azure Service Fabric provides multiple upgrade modes to support development and production clusters.</span></span> <span data-ttu-id="1a9d1-114">Le opzioni di distribuzione scelte possono essere diverse per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="1a9d1-115">L'aggiornamento in sequenza di applicazioni monitorato è il più comune da usare in un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-115">The monitored rolling application upgrade is the most typical upgrade to use in the production environment.</span></span> <span data-ttu-id="1a9d1-116">Se vengono specificati criteri di aggiornamento, Service Fabric verifica che l'applicazione sia integra prima di procedere con l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-116">When the upgrade policy is specified, Service Fabric ensures that the application is healthy before the upgrade proceeds.</span></span>

 <span data-ttu-id="1a9d1-117">L'amministratore dell'applicazione può usare la modalità di aggiornamento in sequenza manuale per avere il controllo totale sull'avanzamento dell'aggiornamento nei vari domini di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-117">The application administrator can use the manual rolling application upgrade mode to have total control over the upgrade progress through the various upgrade domains.</span></span> <span data-ttu-id="1a9d1-118">Questa modalità è utile quando sono necessari criteri di valutazione dell'integrità più personalizzati o complessi o è in corso un aggiornamento non convenzionale, ad esempio un'applicazione che presenta già una perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, the application is already in data loss).</span></span>

<span data-ttu-id="1a9d1-119">L'aggiornamento in sequenza automatizzato dell'applicazione è utile infine per ambienti di sviluppo o di test per garantire un ciclo di iterazione rapido durante lo sviluppo dei servizi.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-119">Finally, the automated rolling application upgrade is useful for development or testing environments to provide a fast iteration cycle during service development.</span></span>

## <a name="change-to-manual-upgrade-mode"></a><span data-ttu-id="1a9d1-120">Modificare la modalità di aggiornamento manuale</span><span class="sxs-lookup"><span data-stu-id="1a9d1-120">Change to manual upgrade mode</span></span>
<span data-ttu-id="1a9d1-121">**Manual**: arresta l'aggiornamento dell'applicazione in corrispondenza dell'UD corrente e cambia la modalità di aggiornamento in UnmonitoredManual.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-121">**Manual**--Stop the application upgrade at the current UD and change the upgrade mode to Unmonitored Manual.</span></span> <span data-ttu-id="1a9d1-122">L'amministratore deve chiamare manualmente il comando **MoveNextApplicationUpgradeDomainAsync** per procedere con l'aggiornamento o per attivare il ripristino allo stato precedente avviando un nuovo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-122">The administrator needs to manually call **MoveNextApplicationUpgradeDomainAsync** to proceed with the upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="1a9d1-123">Quando l'aggiornamento passa alla modalità Manual, resta in tale modalità finché non viene avviato un nuovo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-123">Once the upgrade enters into the Manual mode, it stays in the Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="1a9d1-124">Il comando **GetApplicationUpgradeProgressAsync** restituisce FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-124">The **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="1a9d1-125">Aggiornare con un pacchetto Diff</span><span class="sxs-lookup"><span data-stu-id="1a9d1-125">Upgrade with a diff package</span></span>
<span data-ttu-id="1a9d1-126">Un'applicazione di Service Fabric può essere aggiornata effettuando il provisioning con un pacchetto applicazione completo e autonomo.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="1a9d1-127">È possibile aggiornare un'applicazione anche usando un pacchetto Diff contenente solo i file dell'applicazione aggiornati, nonché i file manifesto dell'applicazione e del servizio aggiornati.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-127">An application can also be upgraded by using a diff package that contains only the updated application files, the updated application manifest, and the service manifest files.</span></span>

<span data-ttu-id="1a9d1-128">Un pacchetto applicazione completo contiene tutti i file necessari per avviare ed eseguire un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-128">A full application package contains all the files necessary to start and run a Service Fabric application.</span></span> <span data-ttu-id="1a9d1-129">Un pacchetto Diff contiene solo i file che sono cambiati tra l'ultimo provisioning e l'aggiornamento corrente, oltre ai file manifesto dell'applicazione e del servizio completi.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-129">A diff package contains only the files that changed between the last provision and the current upgrade, plus the full application manifest and the service manifest files.</span></span> <span data-ttu-id="1a9d1-130">Gli eventuali riferimenti nel manifesto dell'applicazione o del servizio che non vengono reperiti nel layout della build vengono cercati nell'archivio immagini.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-130">Any reference in the application manifest or service manifest that can't be found in the build layout is searched for in the image store.</span></span>

<span data-ttu-id="1a9d1-131">I pacchetti dell'applicazione completi sono necessari per la prima installazione di un'applicazione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-131">Full application packages are required for the first installation of an application to the cluster.</span></span> <span data-ttu-id="1a9d1-132">Gli aggiornamenti successivi possono essere eseguiti con un pacchetto applicazione completo o con un pacchetto Diff.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="1a9d1-133">L'uso di un pacchetto Diff è consigliato nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a9d1-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="1a9d1-134">Se è disponibile un pacchetto dell'applicazione di grandi dimensioni che fa riferimento a più file manifesto del servizio e/o a più pacchetti di codice, di configurazione o di dati.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="1a9d1-135">Se è disponibile un sistema di distribuzione che genera il layout della build direttamente dal processo di compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-135">A diff package is preferred when you have a deployment system that generates the build layout directly from your application build process.</span></span> <span data-ttu-id="1a9d1-136">In questo caso, anche se il codice è rimasto invariato, i nuovi assembly compilati avranno un checksum diverso.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-136">In this case, even though the code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="1a9d1-137">L'uso del pacchetto applicazione completo richiederebbe l'aggiornamento della versione in tutti i pacchetti di codice.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-137">Using a full application package would require you to update the version on all code packages.</span></span> <span data-ttu-id="1a9d1-138">Usando un pacchetto Diff invece è necessario fornire soltanto i file che sono stati modificati e i file manifesto in cui è cambiata la versione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-138">Using a diff package, you only provide the files that changed and the manifest files where the version has changed.</span></span>

<span data-ttu-id="1a9d1-139">Quando si aggiorna un'applicazione tramite Visual Studio, il pacchetto Diff viene pubblicato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-139">When an application is upgraded using Visual Studio, the diff package is published automatically.</span></span> <span data-ttu-id="1a9d1-140">Per creare manualmente un pacchetto Diff, è necessario aggiornare il manifesto dell'applicazione e i manifesti di servizio, ma solo i pacchetti modificati devono essere inclusi nel pacchetto finale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-140">To create a diff package manually, the application manifest, and the service manifests must be updated, but only the changed packages should be included in the final application package.</span></span>

<span data-ttu-id="1a9d1-141">Si supponga, ad esempio, di iniziare con la seguente applicazione (vengono specificati i numeri di versione per facilitare la comprensione):</span><span class="sxs-lookup"><span data-stu-id="1a9d1-141">For example, let's start with the following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="1a9d1-142">A questo punto, si supponga di voler aggiornare solo il pacchetto di codice di service1 usando un pacchetto Diff tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-142">Now, let's assume you wanted to update only the code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="1a9d1-143">A questo punto l'applicazione aggiornata presenta la struttura di cartelle seguente:</span><span class="sxs-lookup"><span data-stu-id="1a9d1-143">Now, your updated application has the following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="1a9d1-144">In questo caso, il manifesto dell'applicazione viene aggiornato alla versione 2.0.0, e il manifesto del servizio per service1 in modo da riflettere l'aggiornamento del pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-144">In this case, you update the application manifest to 2.0.0, and the service manifest for service1 to reflect the code package update.</span></span> <span data-ttu-id="1a9d1-145">La cartella per il pacchetto dell'applicazione sarebbe simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="1a9d1-145">The folder for your application package would have the following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="1a9d1-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1a9d1-146">Next steps</span></span>
<span data-ttu-id="1a9d1-147">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="1a9d1-148">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a9d1-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="1a9d1-149">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="1a9d1-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="1a9d1-150">Rendere compatibili gli aggiornamenti dell'applicazione imparando a usare [Serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="1a9d1-150">Make your application upgrades compatible by learning how to use [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="1a9d1-151">Per informazioni su come risolvere problemi comuni negli aggiornamenti dell'applicazione, vedere i passaggi indicati in [Risoluzione dei problemi relativi agli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1a9d1-151">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
