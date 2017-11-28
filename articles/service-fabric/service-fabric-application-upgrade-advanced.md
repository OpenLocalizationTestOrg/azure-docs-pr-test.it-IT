---
title: Argomenti di eseguire l'aggiornamento dell'applicazione aaaAdvanced | Documenti Microsoft
description: Questo articolo descrive alcuni argomenti avanzati relativi tooupgrading un'applicazione di Service Fabric.
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
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a><span data-ttu-id="b082b-103">Aggiornamento di un'applicazione di Service Fabric: argomenti avanzati</span><span class="sxs-lookup"><span data-stu-id="b082b-103">Service Fabric application upgrade: advanced topics</span></span>
## <a name="adding-or-removing-services-during-an-application-upgrade"></a><span data-ttu-id="b082b-104">Aggiungere o rimuovere servizi durante l'aggiornamento di un'applicazione</span><span class="sxs-lookup"><span data-stu-id="b082b-104">Adding or removing services during an application upgrade</span></span>
<span data-ttu-id="b082b-105">Se un nuovo servizio viene aggiunto tooan applicazione già distribuita, viene pubblicato come un aggiornamento, nuovo servizio hello è applicazione aggiunta toohello distribuito.</span><span class="sxs-lookup"><span data-stu-id="b082b-105">If a new service is added tooan application that is already deployed, and published as an upgrade, hello new service is added toohello deployed application.</span></span>  <span data-ttu-id="b082b-106">Di un aggiornamento non influisce sugli servizi hello che erano già parte di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-106">Such an upgrade does not affect any of hello services that were already part of hello application.</span></span> <span data-ttu-id="b082b-107">Tuttavia, è necessario avviare un'istanza del servizio hello che è stato aggiunto per hello nuovo servizio toobe active (utilizzando hello `New-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="b082b-107">However, an instance of hello service that was added must be started for hello new service toobe active (using hello `New-ServiceFabricService` cmdlet).</span></span>

<span data-ttu-id="b082b-108">Un aggiornamento può anche prevedere la rimozione di determinati servizi da un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b082b-108">Services can also be removed from an application as part of an upgrade.</span></span> <span data-ttu-id="b082b-109">Tuttavia, è necessario arrestare tutte le istanze correnti del servizio di hello-eliminato prima di procedere con l'aggiornamento di hello (utilizzando hello `Remove-ServiceFabricService` cmdlet).</span><span class="sxs-lookup"><span data-stu-id="b082b-109">However, all current instances of hello to-be-deleted service must be stopped before proceeding with hello upgrade (using hello `Remove-ServiceFabricService` cmdlet).</span></span>

## <a name="manual-upgrade-mode"></a><span data-ttu-id="b082b-110">Modalità di aggiornamento manuale</span><span class="sxs-lookup"><span data-stu-id="b082b-110">Manual upgrade mode</span></span>
> [!NOTE]
> <span data-ttu-id="b082b-111">modalità manuale di Hello non monitorato deve essere considerata solo per un aggiornamento non riuscito o sospeso.</span><span class="sxs-lookup"><span data-stu-id="b082b-111">hello unmonitored manual mode should be considered only for a failed or suspended upgrade.</span></span> <span data-ttu-id="b082b-112">modalità monitorato Hello è hello consigliata la modalità di aggiornamento per le applicazioni di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b082b-112">hello monitored mode is hello recommended upgrade mode for Service Fabric applications.</span></span>
>
>

<span data-ttu-id="b082b-113">Azure Service Fabric fornisce più modalità di aggiornamento dei cluster di sviluppo e produzione toosupport.</span><span class="sxs-lookup"><span data-stu-id="b082b-113">Azure Service Fabric provides multiple upgrade modes toosupport development and production clusters.</span></span> <span data-ttu-id="b082b-114">Le opzioni di distribuzione scelte possono essere diverse per ambienti diversi.</span><span class="sxs-lookup"><span data-stu-id="b082b-114">Deployment options chosen may be different for different environments.</span></span>

<span data-ttu-id="b082b-115">aggiornamento dell'applicazione Hello monitorato è hello toouse più comuni di aggiornamento nell'ambiente di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-115">hello monitored rolling application upgrade is hello most typical upgrade toouse in hello production environment.</span></span> <span data-ttu-id="b082b-116">Quando hello esegue l'aggiornamento dei criteri sono specificato, Service Fabric assicura che un'applicazione hello sia integra prima di avviare l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-116">When hello upgrade policy is specified, Service Fabric ensures that hello application is healthy before hello upgrade proceeds.</span></span>

 <span data-ttu-id="b082b-117">amministratore dell'applicazione Hello è possibile utilizzare vari domini di aggiornamento in sequenza applicazione la modalità di aggiornamento toohave il controllo totale hello aggiornamento lo stato di avanzamento tramite hello manuale di hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-117">hello application administrator can use hello manual rolling application upgrade mode toohave total control over hello upgrade progress through hello various upgrade domains.</span></span> <span data-ttu-id="b082b-118">Questa modalità è utile quando è necessario un criterio di valutazione salute personalizzato o complesso, o si verifica un aggiornamento non convenzionali (ad esempio, un'applicazione hello è già la perdita di dati).</span><span class="sxs-lookup"><span data-stu-id="b082b-118">This mode is useful when a customized or complex health evaluation policy is required, or a non-conventional upgrade is happening (for example, hello application is already in data loss).</span></span>

<span data-ttu-id="b082b-119">Infine, hello automatizzati applicazione aggiornamento in sequenza è utile per lo sviluppo o test ambienti tooprovide una rapida iterazione del ciclo durante lo sviluppo del servizio.</span><span class="sxs-lookup"><span data-stu-id="b082b-119">Finally, hello automated rolling application upgrade is useful for development or testing environments tooprovide a fast iteration cycle during service development.</span></span>

## <a name="change-toomanual-upgrade-mode"></a><span data-ttu-id="b082b-120">Modifica della modalità di aggiornamento toomanual</span><span class="sxs-lookup"><span data-stu-id="b082b-120">Change toomanual upgrade mode</span></span>
<span data-ttu-id="b082b-121">**Manuale**: aggiornamento dell'applicazione hello Stop nel hello UD e modifica corrente hello aggiornare tooUnmonitored modalità manuale.</span><span class="sxs-lookup"><span data-stu-id="b082b-121">**Manual**--Stop hello application upgrade at hello current UD and change hello upgrade mode tooUnmonitored Manual.</span></span> <span data-ttu-id="b082b-122">amministratore Hello deve chiamata toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed con hello aggiornare o attivare un'operazione di rollback avviando un nuovo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b082b-122">hello administrator needs toomanually call **MoveNextApplicationUpgradeDomainAsync** tooproceed with hello upgrade or trigger a rollback by initiating a new upgrade.</span></span> <span data-ttu-id="b082b-123">Dopo l'aggiornamento di hello entra in modalità manuale hello, rimane in modalità manuale hello fino a quando non viene avviato un nuovo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="b082b-123">Once hello upgrade enters into hello Manual mode, it stays in hello Manual mode until a new upgrade is initiated.</span></span> <span data-ttu-id="b082b-124">Hello **GetApplicationUpgradeProgressAsync** comando restituisce infrastruttura\_applicazione\_aggiornamento\_stato\_materiale\_Avanti\_in sospeso.</span><span class="sxs-lookup"><span data-stu-id="b082b-124">hello **GetApplicationUpgradeProgressAsync** command returns FABRIC\_APPLICATION\_UPGRADE\_STATE\_ROLLING\_FORWARD\_PENDING.</span></span>

## <a name="upgrade-with-a-diff-package"></a><span data-ttu-id="b082b-125">Aggiornare con un pacchetto Diff</span><span class="sxs-lookup"><span data-stu-id="b082b-125">Upgrade with a diff package</span></span>
<span data-ttu-id="b082b-126">Un'applicazione di Service Fabric può essere aggiornata effettuando il provisioning con un pacchetto applicazione completo e autonomo.</span><span class="sxs-lookup"><span data-stu-id="b082b-126">A Service Fabric application can be upgraded by provisioning with a full, self-contained application package.</span></span> <span data-ttu-id="b082b-127">Un'applicazione può inoltre essere aggiornata tramite un pacchetto delle differenze che contiene solo i file di applicazione hello aggiornato, hello aggiornata manifesto dell'applicazione e file manifesto del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-127">An application can also be upgraded by using a diff package that contains only hello updated application files, hello updated application manifest, and hello service manifest files.</span></span>

<span data-ttu-id="b082b-128">Un pacchetto dell'applicazione completo contiene tutti i toostart necessarie di hello file ed esegue un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b082b-128">A full application package contains all hello files necessary toostart and run a Service Fabric application.</span></span> <span data-ttu-id="b082b-129">Un pacchetto diff contiene solo i file hello modificato tra il provisioning di ultima hello e l'aggiornamento corrente di hello più hello completo manifesto applicazione e servizio hello file manifesto.</span><span class="sxs-lookup"><span data-stu-id="b082b-129">A diff package contains only hello files that changed between hello last provision and hello current upgrade, plus hello full application manifest and hello service manifest files.</span></span> <span data-ttu-id="b082b-130">Qualsiasi riferimento nel manifesto dell'applicazione hello o manifesto del servizio che non possa essere trovata nel layout di compilazione hello viene cercata nell'archivio immagini hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-130">Any reference in hello application manifest or service manifest that can't be found in hello build layout is searched for in hello image store.</span></span>

<span data-ttu-id="b082b-131">I pacchetti dell'intera applicazione sono necessari per l'installazione prima di un cluster di toohello applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-131">Full application packages are required for hello first installation of an application toohello cluster.</span></span> <span data-ttu-id="b082b-132">Gli aggiornamenti successivi possono essere eseguiti con un pacchetto applicazione completo o con un pacchetto Diff.</span><span class="sxs-lookup"><span data-stu-id="b082b-132">Subsequent updates can be either a full application package or a diff package.</span></span>

<span data-ttu-id="b082b-133">L'uso di un pacchetto Diff è consigliato nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b082b-133">Occasions when using a diff package would be a good choice:</span></span>

* <span data-ttu-id="b082b-134">Se è disponibile un pacchetto dell'applicazione di grandi dimensioni che fa riferimento a più file manifesto del servizio e/o a più pacchetti di codice, di configurazione o di dati.</span><span class="sxs-lookup"><span data-stu-id="b082b-134">A diff package is preferred when you have a large application package that references several service manifest files and/or several code packages, config packages, or data packages.</span></span>
* <span data-ttu-id="b082b-135">Un pacchetto delle differenze è preferito quando si dispone di un sistema di distribuzione che genera il layout di compilazione hello direttamente dal processo di compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b082b-135">A diff package is preferred when you have a deployment system that generates hello build layout directly from your application build process.</span></span> <span data-ttu-id="b082b-136">In questo caso, anche se non è stato modificato il codice hello, assembly appena compilato ottenere un checksum diverso.</span><span class="sxs-lookup"><span data-stu-id="b082b-136">In this case, even though hello code hasn't changed, newly built assemblies get a different checksum.</span></span> <span data-ttu-id="b082b-137">Utilizzo di un pacchetto di applicazione completa richiederebbe si tooupdate hello versione per tutti i pacchetti di codice.</span><span class="sxs-lookup"><span data-stu-id="b082b-137">Using a full application package would require you tooupdate hello version on all code packages.</span></span> <span data-ttu-id="b082b-138">Utilizzo di un pacchetto di differenze, è solo fornire file hello modificata e i file di manifesto hello in versione di hello è stata modificata.</span><span class="sxs-lookup"><span data-stu-id="b082b-138">Using a diff package, you only provide hello files that changed and hello manifest files where hello version has changed.</span></span>

<span data-ttu-id="b082b-139">Quando si aggiorna un'applicazione con Visual Studio, è possibile che il pacchetto di diff hello viene pubblicato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b082b-139">When an application is upgraded using Visual Studio, hello diff package is published automatically.</span></span> <span data-ttu-id="b082b-140">un pacchetto diff toocreate hello manualmente, il manifesto dell'applicazione e hello manifesti di servizio devono essere aggiornati, ma solo i pacchetti hello modificato devono essere inclusi nel pacchetto finale dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-140">toocreate a diff package manually, hello application manifest, and hello service manifests must be updated, but only hello changed packages should be included in hello final application package.</span></span>

<span data-ttu-id="b082b-141">Ad esempio, iniziamo con hello seguito domanda (forniti per facilitare la comprensione i numeri di versione):</span><span class="sxs-lookup"><span data-stu-id="b082b-141">For example, let's start with hello following application (version numbers provided for ease of understanding):</span></span>

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="b082b-142">A questo punto, si supponga che si desiderava tooupdate solo hello codice pacchetto Service1 utilizzando un pacchetto diff tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b082b-142">Now, let's assume you wanted tooupdate only hello code package of service1 using a diff package using PowerShell.</span></span> <span data-ttu-id="b082b-143">A questo punto, l'applicazione aggiornata è hello seguente struttura di cartelle:</span><span class="sxs-lookup"><span data-stu-id="b082b-143">Now, your updated application has hello following folder structure:</span></span>

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

<span data-ttu-id="b082b-144">In questo caso, aggiornare too2.0.0 manifesto di applicazione hello e manifesto del servizio per l'aggiornamento del pacchetto di service1 tooreflect hello codice hello.</span><span class="sxs-lookup"><span data-stu-id="b082b-144">In this case, you update hello application manifest too2.0.0, and hello service manifest for service1 tooreflect hello code package update.</span></span> <span data-ttu-id="b082b-145">cartella Hello per il pacchetto di applicazione avrebbe hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="b082b-145">hello folder for your application package would have hello following structure:</span></span>

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a><span data-ttu-id="b082b-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b082b-146">Next steps</span></span>
<span data-ttu-id="b082b-147">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b082b-147">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>

<span data-ttu-id="b082b-148">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b082b-148">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>

<span data-ttu-id="b082b-149">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="b082b-149">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>

<span data-ttu-id="b082b-150">Apportare aggiornamenti applicazione compatibile da learning come toouse [la serializzazione dei dati](service-fabric-application-upgrade-data-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="b082b-150">Make your application upgrades compatible by learning how toouse [Data Serialization](service-fabric-application-upgrade-data-serialization.md).</span></span>

<span data-ttu-id="b082b-151">Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="b082b-151">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
