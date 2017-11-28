---
title: Gateway di gestione per Data Factory aaaData | Documenti Microsoft
description: Impostare un data gateway toomove di dati tra sedi locali e hello cloud. Usare Gateway di gestione dati in Azure Data Factory toomove i dati.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="2ca7a-104">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="2ca7a-104">Data Management Gateway</span></span>
<span data-ttu-id="2ca7a-105">gateway di gestione dati Hello è un agente client che è necessario installare nei dati on-premise ambiente toocopy tra archivi dati locali e cloud.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="2ca7a-106">Hello dati locali supportati da Data Factory di archivi sono disponibili in hello [origini dati supportate](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sezione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="2ca7a-107">In questo articolo si integra con questa procedura dettagliata hello in hello [spostare i dati tra sedi locali e cloud archivi dati](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2ca7a-108">In questa procedura dettagliata hello, creare una pipeline che utilizza hello gateway toomove dati da un tooan di database di SQL Server on-premise blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="2ca7a-109">Questo articolo fornisce informazioni dettagliate sul gateway di gestione dati hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="2ca7a-110">È possibile scalare orizzontalmente un gateway di gestione di dati mediante l'associazione di più computer locali con gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="2ca7a-111">È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="2ca7a-112">Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="2ca7a-113">Per informazioni dettagliate, vedere l'articolo [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) (Gateway di gestione dati - Disponibilità elevata e scalabilità (anteprima).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="2ca7a-114">Gateway supporta attualmente solo attività di copia hello e attività di stored procedure in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="2ca7a-115">Non è il gateway hello toouse possibili origini dati locali di tooaccess un'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="2ca7a-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2ca7a-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="2ca7a-117">Funzionalità del gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="2ca7a-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="2ca7a-118">Gateway di gestione dati fornisce hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="2ca7a-119">Modello le origini dati e origini dati cloud interno hello stessa data factory e spostano i dati.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="2ca7a-120">Disporre di un unico riquadro per il monitoraggio e gestione con visibilità lo stato del gateway dalla pagina di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="2ca7a-121">Gestire origini dati di accesso tooon locali in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="2ca7a-122">Firewall toocorporate è necessaria alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="2ca7a-123">Gateway consente solo le connessioni basate su HTTP in uscita tooopen internet.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="2ca7a-124">È possibile crittografare le informazioni sulle credenziali per gli archivi dati locali usando il proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="2ca7a-125">Spostare i dati in modo efficiente, i dati vengono trasferiti in parallelo, resilienti toointermittent problemi di rete con la logica di ripetizione automatica.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="2ca7a-126">Flusso dei comandi e flusso di dati</span><span class="sxs-lookup"><span data-stu-id="2ca7a-126">Command flow and data flow</span></span>
<span data-ttu-id="2ca7a-127">Quando si usa un copia attività toocopy di dati tra sedi locali e cloud, attività hello Usa un gateway tootransfer di dati da toocloud di origine dati locale e viceversa.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="2ca7a-128">Ecco il flusso di dati di alto livello hello per e un riepilogo dei passaggi per la copia con gateway dati: ![flusso di dati utilizzando gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2ca7a-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="2ca7a-129">Sviluppatori di dati crea un gateway per una Data Factory di Azure utilizzando entrambi hello [portale di Azure](https://portal.azure.com) o [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="2ca7a-130">Sviluppatori di dati consente di creare un servizio collegato per un archivio dati locale specificando gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="2ca7a-131">Come servizio collegato da parte dell'impostazione hello, sviluppatori di dati utilizzano le credenziali e i tipi di autenticazione toospecify applicazione hello impostazione delle credenziali.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="2ca7a-132">finestra di dialogo applicazione comunica con i dati di hello Hello impostare credenziali archiviate tootest credenziali toosave gateway hello e di connessione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="2ca7a-133">Gateway crittografa le credenziali di hello con hello certificato associata gateway hello (fornito dallo sviluppatore di dati), prima di salvare le credenziali di hello in cloud hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="2ca7a-134">Servizio Data Factory comunica con il gateway hello per la pianificazione e gestione dei processi tramite un canale di controllo che utilizza una coda del bus di servizio condiviso di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="2ca7a-135">Quando un processo di attività di copia deve toobe avviata, in Data Factory coda richiesta hello insieme a informazioni sulle credenziali.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="2ca7a-136">Gateway verrà avviato il processo di hello dopo il polling della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="2ca7a-137">gateway Hello decrittografa le credenziali di hello con hello stesso certificato e quindi si connette toohello archivio di dati locale con le credenziali e il tipo di autenticazione appropriato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="2ca7a-138">gateway Hello copia dati da un archivio di cloud tooa archivio locale o, viceversa, a seconda della configurazione in pipeline di dati hello hello attività di copia.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="2ca7a-139">Per questo passaggio, gateway hello comunica direttamente con i servizi di archiviazione basata su cloud, ad esempio l'archiviazione Blob di Azure tramite un canale di sicuro (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="2ca7a-140">Considerazioni sull'uso del gateway</span><span class="sxs-lookup"><span data-stu-id="2ca7a-140">Considerations for using gateway</span></span>
* <span data-ttu-id="2ca7a-141">Una singola istanza del gateway di gestione dati può essere usata per più origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="2ca7a-142">Tuttavia, **una singola istanza del gateway è abbinato tooonly una data factory di Azure** e non può essere condivisa con data factory di un altro.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="2ca7a-143">In un computer può essere installata **una sola istanza del gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="2ca7a-144">Si supponga che si dispone di due data factory necessarie tooaccess origini di dati locali, è necessario gateway tooinstall sul computer due locale.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="2ca7a-145">In altre parole, un gateway è abbinato tooa data factory specificata</span><span class="sxs-lookup"><span data-stu-id="2ca7a-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="2ca7a-146">Hello **gateway non è necessario toobe su hello stesso computer come origine dati hello**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="2ca7a-147">Tuttavia, con l'origine dati toohello più vicino di gateway riduce il tempo di hello per origine dati di hello gateway tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="2ca7a-148">Si consiglia di installare gateway hello in un computer diverso da hello uno quell'origine dati host locale.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="2ca7a-149">Quando hello gateway e l'origine dati si trovano in computer diversi, gateway hello non si contendono le risorse con l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="2ca7a-150">È possibile avere **più gateway in computer diversi, la connessione toohello stessa origine dati locale**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="2ca7a-151">Ad esempio, si dispone di due gateway gestisce due data factory ma hello stessa origine dati locale è registrato con entrambe le data factory hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="2ca7a-152">Se un gateway è già installato nel computer per uno scenario **Power BI**, installare un **gateway separato per Azure Data Factory** in un altro computer.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="2ca7a-153">È necessario usare il gateway anche quando si usa **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="2ca7a-154">Considerare l'origine dati come origine dati locale, ovvero protetta da firewall, anche quando si usa **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="2ca7a-155">Usare la connettività di tooestablish hello gateway tra il servizio di hello e origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="2ca7a-156">È necessario **usare gateway hello** anche se l'archivio dati hello è nel cloud hello in un **VM IaaS di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="2ca7a-157">Installazione</span><span class="sxs-lookup"><span data-stu-id="2ca7a-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="2ca7a-158">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ca7a-158">Prerequisites</span></span>
* <span data-ttu-id="2ca7a-159">Hello supportato **del sistema operativo** versioni sono Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="2ca7a-160">Installazione di gateway di gestione dati hello in un controller di dominio non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="2ca7a-161">È necessario .NET Framework 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="2ca7a-162">Se si installa il gateway in un computer Windows 7, installare .NET Framework 4.5 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="2ca7a-163">Per informazioni dettagliate, vedere [Requisiti di sistema di .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2ca7a-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="2ca7a-164">Hello consigliato **configurazione** per il computer gateway hello è di almeno 2 GHz, 4 core, 8 GB di RAM e disco 80 GB.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="2ca7a-165">Se il computer host hello entra in sospensione, gateway hello non risponde toodata richieste.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="2ca7a-166">Pertanto, configurare un'apposita **risparmio di energia** computer hello prima di installare gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="2ca7a-167">Se configurato toohibernate macchina hello, installazione del gateway hello richiede un messaggio.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="2ca7a-168">È necessario essere un amministratore tooinstall macchina hello e configurare il gateway di gestione dati hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="2ca7a-169">È possibile aggiungere altri utenti toohello **gateway di gestione dati utenti** gruppo locale di Windows.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="2ca7a-170">i membri di Hello di questo gruppo sono in grado di toouse hello **Gestione configurazione di Gateway di gestione di dati** gateway hello tooconfigure di strumento.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="2ca7a-171">Come copiare verificarsi esecuzioni di attività in una frequenza specifica, hello utilizzo delle risorse (CPU, memoria) nel computer di hello anche segue hello stesso modello con ore di punta e periodi di inattività.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="2ca7a-172">Utilizzo delle risorse anche dipende molto quantità hello di spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="2ca7a-173">Quando sono in corso più processi di copia, l'utilizzo delle risorse aumenta durante i periodi di picco.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="2ca7a-174">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="2ca7a-174">Installation options</span></span>
<span data-ttu-id="2ca7a-175">È possibile installare il gateway di gestione di dati in hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="2ca7a-176">Mediante il download di un pacchetto di installazione MSI dal hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="2ca7a-177">Hello MSI può anche essere utilizzati tooupgrade esistente dati Gestione gateway toohello versione più recente, con tutte le impostazioni mantenute.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="2ca7a-178">Facendo clic sul collegamento **Scaricare e installare il gateway dati** in INSTALLAZIONE MANUALE o **Installa direttamente in questo computer** in INSTALLAZIONE RAPIDA.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="2ca7a-179">Vedere l'articolo [Spostare dati tra origini locali e il cloud mediante il Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per le istruzioni dettagliate sull'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="2ca7a-180">passaggio manuale Hello consente toohello download center.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="2ca7a-181">istruzioni di Hello per scaricare e installare il gateway hello dall'area download sono riportate nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="2ca7a-182">Procedure consigliate per l'installazione:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-182">Installation best practices:</span></span>
1. <span data-ttu-id="2ca7a-183">Configurare risparmio di energia sul computer host hello per gateway hello in modo che hello macchina non lo stato di ibernazione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="2ca7a-184">Se il computer host hello entra in sospensione, gateway hello non risponde toodata richieste.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="2ca7a-185">Eseguire il backup hello certificato associata hello gateway.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="2ca7a-186">Installare il gateway hello dall'area download</span><span class="sxs-lookup"><span data-stu-id="2ca7a-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="2ca7a-187">Passare troppo[pagina di download di Gateway di gestione dati Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="2ca7a-188">Fare clic su **scaricare**, selezionare la versione appropriata di hello (**32-bit** Visual Studio. **a 64 bit**) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="2ca7a-189">Eseguire hello **MSI** direttamente o salvarlo tooyour disco ed eseguire.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="2ca7a-190">In hello **iniziale** pagina, selezionare un **language** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="2ca7a-191">**Accettare** hello contratto di licenza e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="2ca7a-192">Selezionare **cartella** tooinstall hello gateway e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="2ca7a-193">In hello **tooinstall pronto** pagina, fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="2ca7a-194">Fare clic su **fine** toocomplete installazione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="2ca7a-195">Ottenere la chiave di hello dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="2ca7a-196">Sezione successiva di hello per le istruzioni dettagliate, vedere.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="2ca7a-197">In hello **registro gateway** pagina di **Gestione configurazione di Gateway di gestione di dati** in esecuzione nel computer, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="2ca7a-198">Incollare la chiave hello testo hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="2ca7a-199">Facoltativamente, fare clic su **chiave del gateway Mostra** toosee testo del tasto hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="2ca7a-200">Fare clic su **Register**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="2ca7a-201">Registrare il gateway con la chiave</span><span class="sxs-lookup"><span data-stu-id="2ca7a-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="2ca7a-202">Se è ancora stato creato un gateway logico nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="2ca7a-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="2ca7a-203">un gateway nella chiave di hello hello portal e ottenere da hello toocreate **configura** pagina, eseguire i passaggi della procedura dettagliata in hello [spostare i dati tra sedi locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="2ca7a-204">Se il gateway logico hello è già stato creato nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="2ca7a-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="2ca7a-205">Nel portale di Azure passare toohello **Data Factory** pagina e fare clic su **servizi collegati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Pagina Data factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="2ca7a-207">In hello **servizi collegati** pagina, seleziona hello logico **gateway** creato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![gateway logico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="2ca7a-209">In hello **Gateway dati** pagina, fare clic su **scaricare e installare il gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Collegamento nel portale di hello per il download](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="2ca7a-211">In hello **configura** pagina, fare clic su **chiave ricreare**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="2ca7a-212">Fare clic su Sì nella finestra di messaggio hello dopo la lettura con attenzione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Ricrea chiave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="2ca7a-214">Fare clic sulla chiave di toohello copia pulsante Avanti.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="2ca7a-215">chiave di Hello è Appunti toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-215">hello key is copied toohello clipboard.</span></span>

    ![Copiare la chiave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="2ca7a-217">Notifiche/icone nell'area di notifica</span><span class="sxs-lookup"><span data-stu-id="2ca7a-217">System tray icons/ notifications</span></span>
<span data-ttu-id="2ca7a-218">Hello immagine seguente vengono illustrate alcune hello cassetto icone presenti.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-218">hello following image shows some of hello tray icons that you see.</span></span>

![icone dell'area di notifica](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="2ca7a-220">Se il cursore si sposta sul messaggio di icona/notifica hello sistema barra delle applicazioni, vedrai i dettagli sullo stato di hello dell'operazione di aggiornamento del gateway/hello in una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="2ca7a-221">Porte e firewall</span><span class="sxs-lookup"><span data-stu-id="2ca7a-221">Ports and firewall</span></span>
<span data-ttu-id="2ca7a-222">Sono disponibili due firewall, è necessario tooconsider: **firewall aziendale** in esecuzione sul router centrale di hello dell'organizzazione di hello, e **Windows firewall** configurato come un daemon sul computer locale hello dove hello gateway è installato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![firewall](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="2ca7a-224">A livello di firewall aziendale, è necessario configurare seguente hello domini e le porte in uscita:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="2ca7a-225">Nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="2ca7a-225">Domain names</span></span> | <span data-ttu-id="2ca7a-226">Porte</span><span class="sxs-lookup"><span data-stu-id="2ca7a-226">Ports</span></span> | <span data-ttu-id="2ca7a-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2ca7a-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ca7a-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2ca7a-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="2ca7a-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="2ca7a-229">443, 80</span></span> |<span data-ttu-id="2ca7a-230">Utilizzato per la comunicazione con il backend Data Movement Service</span><span class="sxs-lookup"><span data-stu-id="2ca7a-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="2ca7a-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2ca7a-231">*.core.windows.net</span></span> |<span data-ttu-id="2ca7a-232">443</span><span class="sxs-lookup"><span data-stu-id="2ca7a-232">443</span></span> |<span data-ttu-id="2ca7a-233">Utilizzato per la copia di staging mediante il BLOB di Azure (se configurata)</span><span class="sxs-lookup"><span data-stu-id="2ca7a-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="2ca7a-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="2ca7a-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="2ca7a-235">443</span><span class="sxs-lookup"><span data-stu-id="2ca7a-235">443</span></span> |<span data-ttu-id="2ca7a-236">Utilizzato per la comunicazione con il backend Data Movement Service</span><span class="sxs-lookup"><span data-stu-id="2ca7a-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="2ca7a-237">A livello di Windows Firewall queste porte in uscita sono generalmente abilitate.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="2ca7a-238">Se non è possibile configurare le porte e domini hello conseguenza nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="2ca7a-239">In base all'origine / sink, è possibile toowhitelist altri domini e le porte in uscita in aziendali/Windows firewall.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="2ca7a-240">Per alcuni database Cloud (ad esempio: [Database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)e così via), potrebbe essere necessario toowhitelist di indirizzo IP del Gateway per la configurazione di firewall.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="2ca7a-241">Copiare i dati da un archivio dati di origine dati archivio tooa sink</span><span class="sxs-lookup"><span data-stu-id="2ca7a-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="2ca7a-242">Verificare che le regole del firewall hello sono attivate correttamente sul firewall aziendale hello, Windows firewall nel computer gateway hello, e dati hello archiviano stesso.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="2ca7a-243">L'abilitazione di queste regole consente hello origine tooboth tooconnect di gateway e sink correttamente.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="2ca7a-244">Abilitare le regole per ogni archivio dati coinvolto nell'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="2ca7a-245">Ad esempio, toocopy da **un sink di Database SQL di Azure locale dati archivio tooan o un sink di Azure SQL Data Warehouse**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="2ca7a-246">Consentire comunicazioni **TCP** in uscita sulla porta **1433** per Windows Firewall e il firewall aziendale.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="2ca7a-247">Configurare le impostazioni di firewall hello di SQL Azure tooadd hello indirizzo IP del server dell'elenco di hello gateway macchina toohello di indirizzi IP consentiti.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="2ca7a-248">Se il firewall non consente la porta in uscita 1433, il gateway non riesce ad accedere direttamente ad Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="2ca7a-249">In questo caso, è possibile utilizzare [staging copia](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Database Azure / Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="2ca7a-250">In questo scenario, richiederebbe solo HTTPS (porta 443) per lo spostamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="2ca7a-251">Considerazioni sui server proxy</span><span class="sxs-lookup"><span data-stu-id="2ca7a-251">Proxy server considerations</span></span>
<span data-ttu-id="2ca7a-252">Se nell'ambiente di rete aziendale utilizza un proxy server tooaccess hello internet, configurare le impostazioni proxy appropriati toouse di dati Gestione gateway.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="2ca7a-253">È possibile impostare il proxy di hello durante la fase di registrazione iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-253">You can set hello proxy during hello initial registration phase.</span></span>

![Impostare il proxy durante la registrazione](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="2ca7a-255">Gateway utilizza il servizio cloud toohello tooconnect di hello proxy server.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="2ca7a-256">Fare clic sul collegamento **Modifica** durante la configurazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="2ca7a-257">Vedrai hello **impostazione proxy** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-257">You see hello **proxy setting** dialog.</span></span>

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="2ca7a-259">Sono disponibili tre opzioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-259">There are three configuration options:</span></span>

* <span data-ttu-id="2ca7a-260">**Non usare il proxy**: Gateway non utilizza i servizi di toocloud tooconnect proxy in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="2ca7a-261">**Utilizzare il proxy di sistema**: il Gateway utilizza proxy hello impostazione configurata in diahost.exe.config e diawp.exe.config.  Se è configurato alcun proxy diahost.exe.config e diawp.exe.config, gateway si connette toocloud servizio direttamente senza dover passare attraverso proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="2ca7a-262">**Utilizzare il proxy personalizzato**: configurare hello HTTP proxy impostazione toouse per il gateway, invece di usare le configurazioni in diahost.exe.config e diawp.exe.config.  L'indirizzo e la porta sono valori obbligatori.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="2ca7a-263">Nome utente e password sono facoltativi a seconda dell'impostazione di autenticazione del proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="2ca7a-264">Tutte le impostazioni vengono crittografate con il certificato delle credenziali hello del gateway hello e archiviate in locale nel computer host di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="2ca7a-265">Servizio Host di gateway di gestione dati Hello viene riavviata automaticamente dopo aver salvato le impostazioni del proxy hello aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="2ca7a-266">Dopo che gateway è stato registrato correttamente, se si desidera tooview o aggiornare le impostazioni proxy, utilizzare Gestione configurazione di Gateway di gestione di dati.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="2ca7a-267">Avviare **Gestione configurazione di Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="2ca7a-268">Passare toohello **impostazioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="2ca7a-269">Fare clic su **modifica** collegamento **HTTP Proxy** hello toolaunch sezione **Set Proxy HTTP** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="2ca7a-270">Dopo aver fatto clic hello **Avanti** pulsante, viene visualizzato un messaggio di avviso che chiede di per l'impostazione proxy di autorizzazione toosave hello e riavviare il servizio Host di Gateway di hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="2ca7a-271">È possibile visualizzare e aggiornare il proxy HTTP tramite lo strumento Gestione configurazione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="2ca7a-273">Se si configura un server proxy con l'autenticazione NTLM, account di dominio hello viene eseguito il servizio Host di Gateway.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="2ca7a-274">Se si modifica la password di hello per l'account di dominio hello in un secondo momento, ricordare tooupdate le impostazioni di configurazione per il servizio hello e riavviarlo di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="2ca7a-275">A causa di toothis requisito, si consiglia di che utilizzare un dominio dedicato account tooaccess hello server proxy che non richiede la password di hello tooupdate frequentemente.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="2ca7a-276">Configurare le impostazioni del server proxy</span><span class="sxs-lookup"><span data-stu-id="2ca7a-276">Configure proxy server settings</span></span>
<span data-ttu-id="2ca7a-277">Se si seleziona **Usa il proxy di sistema** impostazione per il proxy HTTP di hello, gateway Usa impostazione diahost.exe.config e diawp.exe.config proxy hello.  Se viene specificato alcun proxy in diahost.exe.config e diawp.exe.config, gateway si connette toocloud servizio direttamente senza dover passare attraverso proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="2ca7a-278">Hello procedura riportata di seguito vengono fornite istruzioni per l'aggiornamento dei file diahost.exe.config hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="2ca7a-279">In Esplora File, file originale hello costituiscono una copia di C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback-safe.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="2ca7a-280">Avviare Notepad.exe come amministratore e aprire il file di testo "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config". Trovare un tag predefinito hello per system.net come illustrato nel seguente codice hello:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="2ca7a-281">È quindi possibile aggiungere i dettagli del server proxy come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="2ca7a-282">Proprietà aggiuntive sono consentite all'interno di hello proxy tag toospecify hello necessarie impostazioni come scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="2ca7a-283">Fare riferimento troppo[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) sulla sintassi.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="2ca7a-284">Salvare il file di configurazione di hello nel percorso originale di hello, quindi riavviare il servizio Host di Gateway di gestione dati, che preleva modifiche hello hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="2ca7a-285">servizio hello toorestart: utilizzare l'applet Servizi dal Pannello di controllo hello o da hello **Gestione configurazione di Gateway di gestione di dati** > fare clic su hello **Arresta servizio** , quindi fare clic su hello **Avviare servizio**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="2ca7a-286">Se non viene avviato il servizio di hello, è probabile che sia stato aggiunto una sintassi non corretta di tag XML nel file di configurazione dell'applicazione hello che è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ca7a-287">Non dimenticare tooupdate **entrambi** diahost.exe.config e diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="2ca7a-288">Inoltre punti toothese, è inoltre necessario che Microsoft Azure sia nell'elenco elementi consentiti dell'azienda toomake.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="2ca7a-289">elenco di Hello di indirizzi IP di Microsoft Azure può essere scaricato da hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="2ca7a-290">Possibili sintomi di problemi correlati al firewall e al server proxy</span><span class="sxs-lookup"><span data-stu-id="2ca7a-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="2ca7a-291">Se si verifica errori toohello simile dopo quelli, è probabile causa configurazione tooimproper di hello server proxy o firewall, che blocca i gateway di connessione tooauthenticate di Factory tooData stesso.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="2ca7a-292">Fare riferimento tooprevious sezione tooensure il server proxy e firewall siano configurate correttamente.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="2ca7a-293">Quando si tenta di gateway hello tooregister, viene visualizzato il seguente errore hello: "chiave del gateway hello tooregister non riuscito.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="2ca7a-294">Prima di tentare nuovamente la chiave del gateway hello tooregister, verificare che sia stato avviato hello gateway di gestione dati è in uno stato di connessione e hello servizio Host di Gateway di gestione di dati."</span><span class="sxs-lookup"><span data-stu-id="2ca7a-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="2ca7a-295">Quando si apre Gestione configurazione, lo stato del gateway visualizzato può essere "Disconnesso" o "Connessione".</span><span class="sxs-lookup"><span data-stu-id="2ca7a-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="2ca7a-296">Quando si visualizzano i registri eventi di Windows, in "Visualizzatore eventi" > "Registri applicazioni e servizi" > "Gateway di gestione dati" vedere i messaggi di errore, ad esempio hello errore seguente:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="2ca7a-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="2ca7a-297">Aprire la porta 8050 per la crittografia delle credenziali</span><span class="sxs-lookup"><span data-stu-id="2ca7a-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="2ca7a-298">Hello **impostazione delle credenziali** utilizzi dell'applicazione hello porta in ingresso **8050** toorelay gateway toohello di credenziali quando si configura una locale il servizio nel portale di Azure hello collegato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="2ca7a-299">Durante l'installazione di gateway, per impostazione predefinita, installazione del gateway hello verrà aperto nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="2ca7a-300">Se si utilizza un firewall di terze parti, è possibile aprire manualmente la porta hello 8050.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="2ca7a-301">In caso di problema di firewall durante l'installazione di gateway, è possibile provare a usare hello seguenti gateway hello tooinstall di comando senza configurare il firewall hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="2ca7a-302">Se si sceglie di non tooopen porta hello 8050 nel computer gateway hello, utilizzare meccanismi diversi dalla hello **impostazione delle credenziali** dati dell'applicazione tooconfigure archiviano le credenziali.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="2ca7a-303">È ad esempio possibile usare il cmdlet di PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2ca7a-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="2ca7a-304">Per informazioni su come impostare le credenziali dell'archivio dati, vedere la sezione [Impostare le credenziali e la sicurezza](#set-credentials-and-securityy) .</span><span class="sxs-lookup"><span data-stu-id="2ca7a-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="2ca7a-305">Aggiornare</span><span class="sxs-lookup"><span data-stu-id="2ca7a-305">Update</span></span>
<span data-ttu-id="2ca7a-306">Per impostazione predefinita, il gateway di gestione di dati viene automaticamente aggiornato quando è disponibile una versione più recente del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="2ca7a-307">gateway Hello non viene aggiornata fino a quando non vengono eseguite tutte le attività pianificata hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="2ca7a-308">Nessuna ulteriore attività viene elaborata dal gateway hello fino a quando non viene completata l'operazione di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="2ca7a-309">Se hello aggiornamento non riesce, gateway viene eseguito il rollback toohello vecchia versione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="2ca7a-310">Viene visualizzato l'ora dell'aggiornamento pianificato hello in hello seguenti posizioni:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="2ca7a-311">pagina delle proprietà di gateway Hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="2ca7a-312">Home page di hello Gestione configurazione di Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="2ca7a-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="2ca7a-313">Messaggi di notifica dell'aria di notifica</span><span class="sxs-lookup"><span data-stu-id="2ca7a-313">System tray notification message.</span></span>

<span data-ttu-id="2ca7a-314">scheda Home di Hello di hello Gestione configurazione di Gateway di gestione di dati consente di visualizzare la pianificazione di aggiornamento hello e hello ultimo tempo hello gateway non ha installato o aggiornato.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Pianificare gli aggiornamenti](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="2ca7a-316">È possibile installare update hello immediatamente o attendere hello gateway toobe aggiornati automaticamente in fase di hello pianificata.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="2ca7a-317">Ad esempio, hello seguente immagine Mostra hello messaggio di notifica nell'hello Gateway Configuration Manager con il pulsante di aggiornamento hello che è possibile fare clic su tooinstall viene immediatamente.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Aggiorna in Gestione configurazione di Gateway di gestione dati](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="2ca7a-319">messaggio di notifica Hello nella barra delle applicazioni hello sarebbe come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Messaggio nell'area di notifica](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="2ca7a-321">Viene visualizzato lo stato di hello dell'operazione di aggiornamento (manuale o automatica) nella barra delle applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="2ca7a-322">Quando si avvia Gestione configurazione di Gateway successivo, viene visualizzato un messaggio per la notifica di hello barra gateway hello è stato aggiornato insieme a un collegamento troppo[novità nuovo argomento](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="2ca7a-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="2ca7a-323">funzionalità di aggiornamento automatico toodisable/attiva</span><span class="sxs-lookup"><span data-stu-id="2ca7a-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="2ca7a-324">È possibile Abilita/disabilita la funzionalità di aggiornamento automatico hello effettuando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="2ca7a-325">[Per gateway a nodo singolo]</span><span class="sxs-lookup"><span data-stu-id="2ca7a-325">[For single node gateway]</span></span>
1. <span data-ttu-id="2ca7a-326">Avviare Windows PowerShell nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="2ca7a-327">Passa a cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="2ca7a-328">Esecuzione hello successivo comando tooturn hello l'aggiornamento automatico delle funzionalità di disattivare.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="2ca7a-329">tooturn nuovamente in:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="2ca7a-330">[[Per gateway a più nodi a disponibilità e scalabilità elevate (anteprima)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="2ca7a-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="2ca7a-331">Avviare Windows PowerShell nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="2ca7a-332">Passa a cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="2ca7a-333">Esecuzione hello successivo comando tooturn hello l'aggiornamento automatico delle funzionalità di disattivare.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="2ca7a-334">Per il gateway con funzionalità di disponibilità elevata (anteprima), è necessario un parametro di AuthKey aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="2ca7a-335">tooturn nuovamente in:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="2ca7a-336">Se si accede portale hello da un computer diverso dal computer del gateway hello, è necessario assicurarsi che un'applicazione hello Gestione credenziali può connettersi toohello computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="2ca7a-337">Se un'applicazione hello non può raggiungere i computer del gateway hello, quindi non consente tooset le credenziali per l'origine dati hello e tootest connessione toohello dati.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="2ca7a-338">Quando si utilizza hello **impostazione delle credenziali** applicazione portale hello consente di crittografare credenziali hello con certificato hello specificato in hello **certificato** scheda di hello **Gateway Configuration Manager** nel computer gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="2ca7a-339">Se si sta cercando un approccio basato su API per la crittografia delle credenziali hello, è possibile utilizzare hello [New AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) credenziali tooencrypt cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="2ca7a-340">cmdlet di Hello Usa certificato hello che tale gateway è configurato toouse tooencrypt hello credenziali.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="2ca7a-341">Aggiungere le credenziali crittografate toohello **EncryptedCredential** elemento di hello **connectionString** in hello JSON.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="2ca7a-342">Per utilizzare JSON hello hello [New AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet o nell'Editor delle Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="2ca7a-343">Esiste un altro approccio per impostare le credenziali usando l'editor delle data factory.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="2ca7a-344">Se si crea un SQL Server collegato usando hello editor e immettere le credenziali in testo normale, le credenziali di hello vengono crittografate utilizzando un certificato a cui appartiene il servizio di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="2ca7a-345">Non utilizza il certificato di hello che tale gateway è configurato toouse.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="2ca7a-346">Anche se questo approccio può apparire leggermente più veloce, in alcuni casi risulta meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="2ca7a-347">È pertanto consigliabile seguire questo approccio solo per scopi di sviluppo o di test.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="2ca7a-348">Cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca7a-348">PowerShell cmdlets</span></span>
<span data-ttu-id="2ca7a-349">Questa sezione viene descritto come toocreate e registrare un gateway con i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="2ca7a-350">Avviare **Azure PowerShell** in modalità di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="2ca7a-351">Accedi tooyour account Azure eseguendo hello comando seguente e immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="2ca7a-352">Hello utilizzare **New AzureRmDataFactoryGateway** toocreate cmdlet un gateway logico come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="2ca7a-353">**Comando di esempio e output**:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="2ca7a-354">In Azure PowerShell, passare cartella toohello: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="2ca7a-355">Eseguire **RegisterGateway.ps1** associata alla variabile locale hello **$Key** come illustrato nel comando seguente hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="2ca7a-356">Questo script registra l'agente client hello installato nel computer con gateway di hello logico creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="2ca7a-357">È possibile registrare il gateway hello in un computer remoto utilizzando il parametro IsRegisterOnRemoteMachine hello.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="2ca7a-358">Esempio:</span><span class="sxs-lookup"><span data-stu-id="2ca7a-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="2ca7a-359">È possibile utilizzare hello **Get AzureRmDataFactoryGateway** elenco hello tooget di cmdlet di gateway nella data factory.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="2ca7a-360">Quando hello **stato** Mostra **online**, significa che il gateway è toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="2ca7a-361">È possibile rimuovere un gateway tramite hello **Remove AzureRmDataFactoryGateway** descrizione cmdlet e aggiornamento per un gateway tramite hello **Set AzureRmDataFactoryGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="2ca7a-362">Per la sintassi e altri dettagli relativi a questi cmdlet, vedere Riferimento ai cmdlet di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="2ca7a-363">Elencare i gateway usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca7a-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="2ca7a-364">Rimuovere il gateway usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ca7a-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="2ca7a-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ca7a-365">Next steps</span></span>
* <span data-ttu-id="2ca7a-366">Vedere l'articolo [Spostare dati tra archivi dati locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2ca7a-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2ca7a-367">In questa procedura dettagliata hello, creare una pipeline che utilizza hello gateway toomove dati da un tooan di database di SQL Server on-premise blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca7a-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
