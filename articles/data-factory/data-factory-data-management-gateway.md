---
title: Gateway di gestione dati per Data Factory | Microsoft Docs
description: Configurare un gateway dati per spostare dati tra origini locali e il cloud. Usare Gateway di gestione dati in Azure Data Factory per spostare dati.
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
ms.openlocfilehash: 9e40eba285aeb1cce6b77311d1b69a6b96967a0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="428f6-104">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="428f6-104">Data Management Gateway</span></span>
<span data-ttu-id="428f6-105">Il gateway di gestione dati è un agente client che deve essere installato nell'ambiente locale per copiare i dati tra archivi dati cloud e locali.</span><span class="sxs-lookup"><span data-stu-id="428f6-105">The Data management gateway is a client agent that you must install in your on-premises environment to copy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="428f6-106">Gli archivi dati locali supportati da Data Factory sono disponibili nella sezione [Archivi dati e formati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="428f6-106">The on-premises data stores supported by Data Factory are listed in the [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="428f6-107">Questo articolo completa la procedura dettagliata descritta in [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="428f6-107">This article complements the walkthrough in the [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="428f6-108">In questa procedura dettagliata viene creata una pipeline che usa il gateway per spostare i dati da un database di SQL Server locale a un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-108">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span> <span data-ttu-id="428f6-109">Questo articolo offre informazioni approfondite sul gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-109">This article provides detailed in-depth information about the data management gateway.</span></span> 

<span data-ttu-id="428f6-110">È possibile aumentare il numero di istanze di un gateway di gestione dati associando più computer locali al gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-110">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="428f6-111">È possibile aumentare le prestazioni aumentando il numero di processi di spostamento di dati eseguibili contemporaneamente in un nodo.</span><span class="sxs-lookup"><span data-stu-id="428f6-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="428f6-112">Questa funzionalità è disponibile anche per un gateway logico con un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="428f6-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="428f6-113">Per informazioni dettagliate, vedere l'articolo [Ridimensionamento del gateway di gestione dati in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="428f6-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="428f6-114">Attualmente il gateway supporta solo l'attività di copia e l'attività di stored procedure in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-114">Currently, gateway supports only the copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="428f6-115">Non è possibile usare il gateway da un'attività personalizzata per accedere alle origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="428f6-115">It is not possible to use the gateway from a custom activity to access on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="428f6-116">Panoramica</span><span class="sxs-lookup"><span data-stu-id="428f6-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="428f6-117">Funzionalità del gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="428f6-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="428f6-118">Il gateway di gestione dati offre le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="428f6-118">Data management gateway provides the following capabilities:</span></span>

* <span data-ttu-id="428f6-119">Consente di modellare le origini dati locali e le origini dati nel cloud all'interno di un'unica istanza di Data Factory e di spostare i dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="428f6-119">Model on-premises data sources and cloud data sources within the same data factory and move data.</span></span>
* <span data-ttu-id="428f6-120">Consente di monitorare e gestire lo stato del gateway in un'unica schermata dalla pagina di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-120">Have a single pane of glass for monitoring and management with visibility into gateway status from the Data Factory page.</span></span>
* <span data-ttu-id="428f6-121">Consente di gestire in modo sicuro l'accesso alle origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="428f6-121">Manage access to on-premises data sources securely.</span></span>
  * <span data-ttu-id="428f6-122">Non è richiesta alcuna modifica del firewall aziendale.</span><span class="sxs-lookup"><span data-stu-id="428f6-122">No changes required to corporate firewall.</span></span> <span data-ttu-id="428f6-123">Il gateway stabilisce soltanto connessioni basate su HTTP in uscita per accedere a Internet.</span><span class="sxs-lookup"><span data-stu-id="428f6-123">Gateway only makes outbound HTTP-based connections to open internet.</span></span>
  * <span data-ttu-id="428f6-124">È possibile crittografare le informazioni sulle credenziali per gli archivi dati locali usando il proprio certificato.</span><span class="sxs-lookup"><span data-stu-id="428f6-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="428f6-125">Consente di spostare i dati in modo efficace: i dati vengono trasferiti in parallelo e sono resilienti ai problemi di rete intermittente grazie alla logica di ripetizione dei tentativi automatica.</span><span class="sxs-lookup"><span data-stu-id="428f6-125">Move data efficiently – data is transferred in parallel, resilient to intermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="428f6-126">Flusso dei comandi e flusso di dati</span><span class="sxs-lookup"><span data-stu-id="428f6-126">Command flow and data flow</span></span>
<span data-ttu-id="428f6-127">Quando si usa un'attività di copia per copiare dati tra ambiente cloud e locale, l'attività sfrutta un gateway per trasferire i dati dall'origine dati locale al cloud e viceversa.</span><span class="sxs-lookup"><span data-stu-id="428f6-127">When you use a copy activity to copy data between on-premises and cloud, the activity uses a gateway to transfer data from on-premises data source to cloud and vice versa.</span></span>

<span data-ttu-id="428f6-128">Di seguito sono riportati un flusso di dati generale e un riepilogo dei passaggi per la copia con il gateway dati: ![Flusso di dati mediante gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="428f6-128">Here is the high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="428f6-129">Lo sviluppatore di dati crea un gateway per un'istanza di Azure Data Factory usando il [portale di Azure](https://portal.azure.com) oppure un [cmdlet di PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="428f6-129">Data developer creates a gateway for an Azure Data Factory using either the [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="428f6-130">Viene creato un servizio collegato per un archivio dati locale specificando il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-130">Data developer creates a linked service for an on-premises data store by specifying the gateway.</span></span> <span data-ttu-id="428f6-131">Una parte della configurazione del servizio collegato consiste nell'uso dell'applicazione Impostazione credenziali per specificare i tipi di autenticazione e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="428f6-131">As part of setting up the linked service, data developer uses the Setting Credentials application to specify authentication types and credentials.</span></span>  <span data-ttu-id="428f6-132">La finestra di dialogo dell'applicazione Impostazione credenziali comunica con l'archivio dati per eseguire il test della connessione e con il gateway per salvare le credenziali.</span><span class="sxs-lookup"><span data-stu-id="428f6-132">The Setting Credentials application dialog communicates with the data store to test connection and the gateway to save credentials.</span></span>
3. <span data-ttu-id="428f6-133">Il gateway crittografa le credenziali tramite il certificato associato al gateway (fornito dallo sviluppatore) prima di salvare le credenziali nel cloud.</span><span class="sxs-lookup"><span data-stu-id="428f6-133">Gateway encrypts the credentials with the certificate associated with the gateway (supplied by data developer), before saving the credentials in the cloud.</span></span>
4. <span data-ttu-id="428f6-134">Il servizio Data Factory comunica con il gateway per la pianificazione e la gestione dei processi tramite un canale di controllo che usa una coda condivisa del bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-134">Data Factory service communicates with the gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="428f6-135">Quando occorre avviare il processo di attività di copia, Data Factory accoda la richiesta insieme alle informazioni sulle credenziali.</span><span class="sxs-lookup"><span data-stu-id="428f6-135">When a copy activity job needs to be kicked off, Data Factory queues the request along with credential information.</span></span> <span data-ttu-id="428f6-136">Il gateway avvia il processo dopo avere eseguito il polling della coda.</span><span class="sxs-lookup"><span data-stu-id="428f6-136">Gateway kicks off the job after polling the queue.</span></span>
5. <span data-ttu-id="428f6-137">Il gateway decrittografa le credenziali tramite lo stesso certificato e quindi si connette all'archivio dati locale con il tipo di autenticazione appropriato e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="428f6-137">The gateway decrypts the credentials with the same certificate and then connects to the on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="428f6-138">Il gateway copia i dati dall'archivio locale in una risorsa di archiviazione cloud o viceversa in base alla configurazione dell'attività di copia nella pipeline di dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-138">The gateway copies data from an on-premises store to a cloud storage, or vice versa depending on how the Copy Activity is configured in the data pipeline.</span></span> <span data-ttu-id="428f6-139">Per questo passaggio il gateway comunica direttamente con i servizi di archiviazione basati sul cloud, ad esempio BLOB di Azure su un canale protetto (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="428f6-139">For this step, the gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="428f6-140">Considerazioni sull'uso del gateway</span><span class="sxs-lookup"><span data-stu-id="428f6-140">Considerations for using gateway</span></span>
* <span data-ttu-id="428f6-141">Una singola istanza del gateway di gestione dati può essere usata per più origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="428f6-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="428f6-142">Tuttavia, **una singola istanza del gateway viene associata a un solo Data Factory di Azure** e non può essere condivisa con un altro Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-142">However, **a single gateway instance is tied to only one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="428f6-143">In un computer può essere installata **una sola istanza del gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="428f6-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="428f6-144">Si supponga di avere due istanze di Data Factory che richiedono l'accesso alle origini dati locali: è necessario installare i gateway nei due computer locali.</span><span class="sxs-lookup"><span data-stu-id="428f6-144">Suppose, you have two data factories that need to access on-premises data sources, you need to install gateways on two on-premises computers.</span></span> <span data-ttu-id="428f6-145">In altre parole, ogni gateway viene associato a un'istanza specifica di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-145">In other words, a gateway is tied to a specific data factory</span></span>
* <span data-ttu-id="428f6-146">Il **gateway non deve trovarsi sullo stesso computer dell'origine dati**.</span><span class="sxs-lookup"><span data-stu-id="428f6-146">The **gateway does not need to be on the same machine as the data source**.</span></span> <span data-ttu-id="428f6-147">Tuttavia, se i gateway sono posizionati in prossimità dell'origine dati, il tempo di connessione del gateway all'origine dati si riduce.</span><span class="sxs-lookup"><span data-stu-id="428f6-147">However, having gateway closer to the data source reduces the time for the gateway to connect to the data source.</span></span> <span data-ttu-id="428f6-148">Si consiglia di installare il gateway in un computer diverso da quello che ospita l'origine dati locale.</span><span class="sxs-lookup"><span data-stu-id="428f6-148">We recommend that you install the gateway on a machine that is different from the one that hosts on-premises data source.</span></span> <span data-ttu-id="428f6-149">Quando il gateway e l'origine dati si trovano in computer diversi non si contendono le risorse.</span><span class="sxs-lookup"><span data-stu-id="428f6-149">When the gateway and data source are on different machines, the gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="428f6-150">È possibile disporre di **più gateway su diversi computer che si connettono alla stessa origine dati locale**.</span><span class="sxs-lookup"><span data-stu-id="428f6-150">You can have **multiple gateways on different machines connecting to the same on-premises data source**.</span></span> <span data-ttu-id="428f6-151">Ad esempio, potrebbero essere disponibili due gateway che servono due data factory, ma la stessa origine dati locale viene registrata con entrambe le data factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-151">For example, you may have two gateways serving two data factories but the same on-premises data source is registered with both the data factories.</span></span>
* <span data-ttu-id="428f6-152">Se un gateway è già installato nel computer per uno scenario **Power BI**, installare un **gateway separato per Azure Data Factory** in un altro computer.</span><span class="sxs-lookup"><span data-stu-id="428f6-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="428f6-153">È necessario usare il gateway anche quando si usa **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="428f6-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="428f6-154">Considerare l'origine dati come origine dati locale, ovvero protetta da firewall, anche quando si usa **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="428f6-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="428f6-155">Usare il gateway per stabilire la connettività tra il servizio e l'origine dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-155">Use the gateway to establish connectivity between the service and the data source.</span></span>
* <span data-ttu-id="428f6-156">È necessario **usare il gateway** anche se l'archivio dati è nel cloud in una **VM IaaS di Azure**.</span><span class="sxs-lookup"><span data-stu-id="428f6-156">You must **use the gateway** even if the data store is in the cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="428f6-157">Installazione</span><span class="sxs-lookup"><span data-stu-id="428f6-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="428f6-158">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="428f6-158">Prerequisites</span></span>
* <span data-ttu-id="428f6-159">Sono supportati i **sistemi operativi** Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="428f6-159">The supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="428f6-160">L'installazione del gateway di gestione dati nel controller di dominio al momento non è supportata.</span><span class="sxs-lookup"><span data-stu-id="428f6-160">Installation of the data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="428f6-161">È necessario .NET Framework 4.5.1 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="428f6-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="428f6-162">Se si installa il gateway in un computer Windows 7, installare .NET Framework 4.5 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="428f6-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="428f6-163">Per informazioni dettagliate, vedere [Requisiti di sistema di .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) .</span><span class="sxs-lookup"><span data-stu-id="428f6-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="428f6-164">La **configurazione** consigliata per il computer gateway è di almeno 2 GHz, 4 core, 8 GB di RAM e un disco da 80 GB.</span><span class="sxs-lookup"><span data-stu-id="428f6-164">The recommended **configuration** for the gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="428f6-165">Se il computer host entra in stato di ibernazione, il gateway non risponde alle richieste di dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-165">If the host machine hibernates, the gateway does not respond to data requests.</span></span> <span data-ttu-id="428f6-166">Pertanto, configurare una **combinazione per il risparmio di energia** appropriata nel computer prima di installare il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-166">Therefore, configure an appropriate **power plan** on the computer before installing the gateway.</span></span> <span data-ttu-id="428f6-167">Se il computer è configurato per l'ibernazione, l'installazione del gateway invia un messaggio.</span><span class="sxs-lookup"><span data-stu-id="428f6-167">If the machine is configured to hibernate, the gateway installation prompts a message.</span></span>
* <span data-ttu-id="428f6-168">È necessario essere un amministratore del computer per installare e configurare correttamente il gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-168">You must be an administrator on the machine to install and configure the data management gateway successfully.</span></span> <span data-ttu-id="428f6-169">È possibile aggiungere altri utenti al gruppo di Windows locale **Data Management Gateway Users**.</span><span class="sxs-lookup"><span data-stu-id="428f6-169">You can add additional users to the **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="428f6-170">I membri di questo gruppo possono usare lo strumento **Gestione configurazione di Gateway di gestione dati** per configurare il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-170">The members of this group are able to use the **Data Management Gateway Configuration Manager** tool to configure the gateway.</span></span>

<span data-ttu-id="428f6-171">Dato che le esecuzioni dell'attività di copia seguono una frequenza specifica, l'utilizzo delle risorse, ovvero CPU e memoria, nel computer segue lo stesso ciclo costituito da periodi di picco alternati a periodi di inattività.</span><span class="sxs-lookup"><span data-stu-id="428f6-171">As copy activity runs happen on a specific frequency, the resource usage (CPU, memory) on the machine also follows the same pattern with peak and idle times.</span></span> <span data-ttu-id="428f6-172">L'utilizzo delle risorse dipende molto anche dalla quantità di dati da spostare.</span><span class="sxs-lookup"><span data-stu-id="428f6-172">Resource utilization also depends heavily on the amount of data being moved.</span></span> <span data-ttu-id="428f6-173">Quando sono in corso più processi di copia, l'utilizzo delle risorse aumenta durante i periodi di picco.</span><span class="sxs-lookup"><span data-stu-id="428f6-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="428f6-174">Opzioni di installazione</span><span class="sxs-lookup"><span data-stu-id="428f6-174">Installation options</span></span>
<span data-ttu-id="428f6-175">Il gateway di gestione dati può essere installato nei seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="428f6-175">Data management gateway can be installed in the following ways:</span></span>

* <span data-ttu-id="428f6-176">Scaricando un pacchetto di installazione MSI dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="428f6-176">By downloading an MSI setup package from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="428f6-177">Il pacchetto MSI può anche essere usato per aggiornare il gateway di gestione dati esistente alla versione più recente mantenendo tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="428f6-177">The MSI can also be used to upgrade existing data management gateway to the latest version, with all settings preserved.</span></span>
* <span data-ttu-id="428f6-178">Facendo clic sul collegamento **Scaricare e installare il gateway dati** in INSTALLAZIONE MANUALE o **Installa direttamente in questo computer** in INSTALLAZIONE RAPIDA.</span><span class="sxs-lookup"><span data-stu-id="428f6-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="428f6-179">Vedere l'articolo [Spostare dati tra origini locali e il cloud mediante il Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md) per le istruzioni dettagliate sull'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="428f6-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="428f6-180">Il passaggio manuale consente di accedere all'area download.</span><span class="sxs-lookup"><span data-stu-id="428f6-180">The manual step takes you to the download center.</span></span>  <span data-ttu-id="428f6-181">Le istruzioni per scaricare e installare il gateway dall'area download sono disponibili nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="428f6-181">The instructions for downloading and installing the gateway from download center are in the next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="428f6-182">Procedure consigliate per l'installazione:</span><span class="sxs-lookup"><span data-stu-id="428f6-182">Installation best practices:</span></span>
1. <span data-ttu-id="428f6-183">Configurare la combinazione per il risparmio di energia nel computer host del gateway in modo che il computer non entri in stato di ibernazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-183">Configure power plan on the host machine for the gateway so that the machine does not hibernate.</span></span> <span data-ttu-id="428f6-184">Se il computer host entra in stato di ibernazione, il gateway non risponde alle richieste di dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-184">If the host machine hibernates, the gateway does not respond to data requests.</span></span>
2. <span data-ttu-id="428f6-185">Eseguire il backup del certificato associato al gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-185">Back up the certificate associated with the gateway.</span></span>

### <a name="install-the-gateway-from-download-center"></a><span data-ttu-id="428f6-186">Installare il gateway dall'Area download</span><span class="sxs-lookup"><span data-stu-id="428f6-186">Install the gateway from download center</span></span>
1. <span data-ttu-id="428f6-187">Andare alla [pagina di download del Gateway di gestione dati di Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="428f6-187">Navigate to [Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="428f6-188">Fare clic su **Scarica**, selezionare la versione appropriata (**a 32 bit** o **a 64 bit**) e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="428f6-188">Click **Download**, select the appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="428f6-189">Eseguire direttamente il file **MSI** oppure salvarlo sul disco rigido ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="428f6-189">Run the **MSI** directly or save it to your hard disk and run.</span></span>
4. <span data-ttu-id="428f6-190">Nella pagina di **benvenuto** selezionare una **lingua** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="428f6-190">On the **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="428f6-191">**Accettare** il contratto di licenza e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="428f6-191">**Accept** the End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="428f6-192">Selezionare la **cartella** per installare il gateway e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="428f6-192">Select **folder** to install the gateway and click **Next**.</span></span>
7. <span data-ttu-id="428f6-193">Nella pagina **Pronto per l'installazione** fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="428f6-193">On the **Ready to install** page, click **Install**.</span></span>
8. <span data-ttu-id="428f6-194">Fare clic su **Fine** per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-194">Click **Finish** to complete installation.</span></span>
9. <span data-ttu-id="428f6-195">Ottenere la chiave dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-195">Get the key from the Azure portal.</span></span> <span data-ttu-id="428f6-196">Vedere la sezione successiva per le istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="428f6-196">See the next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="428f6-197">Nella pagina **Registra gateway** di **Gestione configurazione di Gateway di gestione dati** in esecuzione sul computer in uso attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-197">On the **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do the following steps:</span></span>
    1. <span data-ttu-id="428f6-198">Incollare la chiave nel testo.</span><span class="sxs-lookup"><span data-stu-id="428f6-198">Paste the key in the text.</span></span>
    2. <span data-ttu-id="428f6-199">Facoltativamente, fare clic su **Mo_stra chiave del gateway** per visualizzare il testo della chiave.</span><span class="sxs-lookup"><span data-stu-id="428f6-199">Optionally, click **Show gateway key** to see the key text.</span></span>
    3. <span data-ttu-id="428f6-200">Fare clic su **Register**.</span><span class="sxs-lookup"><span data-stu-id="428f6-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="428f6-201">Registrare il gateway con la chiave</span><span class="sxs-lookup"><span data-stu-id="428f6-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-the-portal"></a><span data-ttu-id="428f6-202">Se non è ancora stato creato un gateway logico nel portale</span><span class="sxs-lookup"><span data-stu-id="428f6-202">If you haven't already created a logical gateway in the portal</span></span>
<span data-ttu-id="428f6-203">Per creare un gateway nel portale e ottenere la chiave dalla pagina **Configura**, seguire i passaggi della procedura dettagliata dell'articolo [Spostare dati tra origini locali e il cloud con Gateway di gestione dati](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="428f6-203">To create a gateway in the portal and get the key from the **Configure** page, Follow steps from walkthrough in the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-the-logical-gateway-in-the-portal"></a><span data-ttu-id="428f6-204">Se è già stato creato un gateway logico nel portale</span><span class="sxs-lookup"><span data-stu-id="428f6-204">If you have already created the logical gateway in the portal</span></span>
1. <span data-ttu-id="428f6-205">Nel portale di Azure passare alla pagina **Data factory** e fare clic sul riquadro **Servizi collegati**.</span><span class="sxs-lookup"><span data-stu-id="428f6-205">In Azure portal, navigate to the **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Pagina Data factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="428f6-207">Nella pagina **Servizi collegati** selezionare il **gateway** logico creato nel portale.</span><span class="sxs-lookup"><span data-stu-id="428f6-207">In the **Linked Services** page, select the logical **gateway** you created in the portal.</span></span>

    ![gateway logico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="428f6-209">Nella pagina **Gateway dati** fare clic su **Scaricare e installare il gateway dati**.</span><span class="sxs-lookup"><span data-stu-id="428f6-209">In the **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Link di download nel portale](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="428f6-211">Nella pagina **Configura** fare clic su **Ricrea chiave**.</span><span class="sxs-lookup"><span data-stu-id="428f6-211">In the **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="428f6-212">Fare clic su Sì nel messaggio di avviso dopo averlo letto con attenzione.</span><span class="sxs-lookup"><span data-stu-id="428f6-212">Click Yes on the warning message after reading it carefully.</span></span>

    ![Ricrea chiave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="428f6-214">Fare clic su pulsante Copia accanto alla chiave.</span><span class="sxs-lookup"><span data-stu-id="428f6-214">Click Copy button next to the key.</span></span> <span data-ttu-id="428f6-215">La chiave viene copiata negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="428f6-215">The key is copied to the clipboard.</span></span>

    ![Copiare la chiave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="428f6-217">Notifiche/icone nell'area di notifica</span><span class="sxs-lookup"><span data-stu-id="428f6-217">System tray icons/ notifications</span></span>
<span data-ttu-id="428f6-218">L'immagine seguente mostra alcune delle icone visualizzate nell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="428f6-218">The following image shows some of the tray icons that you see.</span></span>

![icone dell'area di notifica](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="428f6-220">Spostando il cursore sul messaggio di notifica o sull'icona nell'area di notifica, vengono visualizzati i dettagli relativi allo stato del gateway o dell'operazione di aggiornamento in una finestra popup.</span><span class="sxs-lookup"><span data-stu-id="428f6-220">If you move cursor over the system tray icon/notification message, you see details about the state of the gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="428f6-221">Porte e firewall</span><span class="sxs-lookup"><span data-stu-id="428f6-221">Ports and firewall</span></span>
<span data-ttu-id="428f6-222">È necessario considerare due firewall, ovvero il **firewall aziendale** in esecuzione nel router centrale dell'organizzazione e **Windows firewall**, configurato come servizio daemon nel computer locale in cui è installato il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-222">There are two firewalls you need to consider: **corporate firewall** running on the central router of the organization, and **Windows firewall** configured as a daemon on the local machine where the gateway is installed.</span></span>  

![firewall](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="428f6-224">A livello di firewall aziendale è necessario configurare le porte in uscita e i domini seguenti:</span><span class="sxs-lookup"><span data-stu-id="428f6-224">At corporate firewall level, you need configure the following domains and outbound ports:</span></span>

| <span data-ttu-id="428f6-225">Nomi di dominio</span><span class="sxs-lookup"><span data-stu-id="428f6-225">Domain names</span></span> | <span data-ttu-id="428f6-226">Porte</span><span class="sxs-lookup"><span data-stu-id="428f6-226">Ports</span></span> | <span data-ttu-id="428f6-227">Descrizione</span><span class="sxs-lookup"><span data-stu-id="428f6-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="428f6-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="428f6-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="428f6-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="428f6-229">443, 80</span></span> |<span data-ttu-id="428f6-230">Utilizzato per la comunicazione con il backend Data Movement Service</span><span class="sxs-lookup"><span data-stu-id="428f6-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="428f6-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="428f6-231">*.core.windows.net</span></span> |<span data-ttu-id="428f6-232">443</span><span class="sxs-lookup"><span data-stu-id="428f6-232">443</span></span> |<span data-ttu-id="428f6-233">Utilizzato per la copia di staging mediante il BLOB di Azure (se configurata)</span><span class="sxs-lookup"><span data-stu-id="428f6-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="428f6-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="428f6-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="428f6-235">443</span><span class="sxs-lookup"><span data-stu-id="428f6-235">443</span></span> |<span data-ttu-id="428f6-236">Utilizzato per la comunicazione con il backend Data Movement Service</span><span class="sxs-lookup"><span data-stu-id="428f6-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="428f6-237">A livello di Windows Firewall queste porte in uscita sono generalmente abilitate.</span><span class="sxs-lookup"><span data-stu-id="428f6-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="428f6-238">In caso contrario, è possibile configurare le porte e i domini nel modo appropriato nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-238">If not, you can configure the domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="428f6-239">In base all'origine o ai sink, potrebbe essere necessario consentire altri domini e porte in uscita nel firewall aziendale o in Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="428f6-239">Based on your source/ sinks, you may have to whitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="428f6-240">Per alcuni database cloud (ad esempio, [Database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access) e così via), potrebbe essere necessario consentire l'indirizzo IP del computer gateway nella configurazione del firewall.</span><span class="sxs-lookup"><span data-stu-id="428f6-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need to whitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-to-a-sink-data-store"></a><span data-ttu-id="428f6-241">Copiare dati da un archivio dati di origine a un archivio dati sink</span><span class="sxs-lookup"><span data-stu-id="428f6-241">Copy data from a source data store to a sink data store</span></span>
<span data-ttu-id="428f6-242">Verificare che le regole del firewall siano abilitate correttamente sul firewall aziendale, su Windows Firewall nel computer del gateway e sull'archivio dati stesso,</span><span class="sxs-lookup"><span data-stu-id="428f6-242">Ensure that the firewall rules are enabled properly on the corporate firewall, Windows firewall on the gateway machine, and the data store itself.</span></span> <span data-ttu-id="428f6-243">in modo da consentire al gateway di connettersi all'origine e al sink.</span><span class="sxs-lookup"><span data-stu-id="428f6-243">Enabling these rules allows the gateway to connect to both source and sink successfully.</span></span> <span data-ttu-id="428f6-244">Abilitare le regole per ogni archivio dati interessato dall'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="428f6-244">Enable rules for each data store that is involved in the copy operation.</span></span>

<span data-ttu-id="428f6-245">Ad esempio, per eseguire la copia da **un archivio dati locale a un sink di Database SQL di Azure o a un sink di SQL Data Warehouse di Azure**, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-245">For example, to copy from **an on-premises data store to an Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do the following steps:</span></span>

* <span data-ttu-id="428f6-246">Consentire comunicazioni **TCP** in uscita sulla porta **1433** per Windows Firewall e il firewall aziendale.</span><span class="sxs-lookup"><span data-stu-id="428f6-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="428f6-247">Configurare le impostazioni del firewall del server SQL di Azure aggiungendo l'indirizzo IP relativo al computer del gateway all'elenco degli indirizzi IP consentiti.</span><span class="sxs-lookup"><span data-stu-id="428f6-247">Configure the firewall settings of Azure SQL server to add the IP address of the gateway machine to the list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="428f6-248">Se il firewall non consente la porta in uscita 1433, il gateway non riesce ad accedere direttamente ad Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="428f6-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="428f6-249">In questo caso, è possibile usare la [copia di staging](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) sul database SQL di Azure o SQL Azure DW.</span><span class="sxs-lookup"><span data-stu-id="428f6-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) to SQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="428f6-250">In questo scenario è necessario solo HTTPS (porta 443) per lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-250">In this scenario, you would only require HTTPS (port 443) for the data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="428f6-251">Considerazioni sui server proxy</span><span class="sxs-lookup"><span data-stu-id="428f6-251">Proxy server considerations</span></span>
<span data-ttu-id="428f6-252">Se l'ambiente di rete aziendale usa un server proxy per accedere a Internet, configurare il gateway di gestione dati per l'uso delle impostazioni proxy appropriate.</span><span class="sxs-lookup"><span data-stu-id="428f6-252">If your corporate network environment uses a proxy server to access the internet, configure data management gateway to use appropriate proxy settings.</span></span> <span data-ttu-id="428f6-253">È possibile impostare il proxy durante la fase di registrazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="428f6-253">You can set the proxy during the initial registration phase.</span></span>

![Impostare il proxy durante la registrazione](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="428f6-255">Il gateway usa il server proxy per connettersi al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="428f6-255">Gateway uses the proxy server to connect to the cloud service.</span></span> <span data-ttu-id="428f6-256">Fare clic sul collegamento **Modifica** durante la configurazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="428f6-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="428f6-257">Viene visualizzata la finestra di dialogo **impostazione proxy** .</span><span class="sxs-lookup"><span data-stu-id="428f6-257">You see the **proxy setting** dialog.</span></span>

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="428f6-259">Sono disponibili tre opzioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="428f6-259">There are three configuration options:</span></span>

* <span data-ttu-id="428f6-260">**Non utilizzare proxy**: il gateway non usa in modo esplicito i proxy per connettersi ai servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="428f6-260">**Do not use proxy**: Gateway does not explicitly use any proxy to connect to cloud services.</span></span>
* <span data-ttu-id="428f6-261">**Usa il proxy di sistema**: il gateway usa l'impostazione del proxy configurata in diahost.exe.config e diawp.exe.config.  Se non è stato configurato alcun proxy in diahost.exe.config e diawp.exe.config, il gateway si connette al servizio cloud direttamente senza passare attraverso il proxy.</span><span class="sxs-lookup"><span data-stu-id="428f6-261">**Use system proxy**: Gateway uses the proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span>
* <span data-ttu-id="428f6-262">**Usa proxy personalizzato**: configurare le impostazioni del proxy HTTP che il gateway deve usare al posto delle configurazioni in diahost.exe.config e diawp.exe.config.  L'indirizzo e la porta sono valori obbligatori.</span><span class="sxs-lookup"><span data-stu-id="428f6-262">**Use custom proxy**: Configure the HTTP proxy setting to use for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="428f6-263">Nome utente e password sono facoltativi a seconda dell'impostazione di autenticazione del proxy.</span><span class="sxs-lookup"><span data-stu-id="428f6-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="428f6-264">Tutte le impostazioni vengono crittografate con il certificato delle credenziali del gateway e archiviate localmente nel computer che ospita il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-264">All settings are encrypted with the credential certificate of the gateway and stored locally on the gateway host machine.</span></span>

<span data-ttu-id="428f6-265">Il servizio host del gateway di gestione dati viene riavviato automaticamente dopo avere salvato le impostazioni proxy aggiornate.</span><span class="sxs-lookup"><span data-stu-id="428f6-265">The data management gateway Host Service restarts automatically after you save the updated proxy settings.</span></span>

<span data-ttu-id="428f6-266">Dopo aver registrato correttamente il gateway, se si desidera visualizzare o aggiornare le impostazioni proxy, usare Gestione configurazione di Gateway di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-266">After gateway has been successfully registered, if you want to view or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="428f6-267">Avviare **Gestione configurazione di Gateway di gestione dati**.</span><span class="sxs-lookup"><span data-stu-id="428f6-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="428f6-268">Passare alla scheda **Impostazioni** .</span><span class="sxs-lookup"><span data-stu-id="428f6-268">Switch to the **Settings** tab.</span></span>
3. <span data-ttu-id="428f6-269">Fare clic sul collegamento **Cambia** nella sezione **Proxy HTTP** per avviare la finestra di dialogo **Imposta proxy HTTP**.</span><span class="sxs-lookup"><span data-stu-id="428f6-269">Click **Change** link in **HTTP Proxy** section to launch the **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="428f6-270">Dopo aver selezionato il pulsante **Avanti** , una finestra di dialogo di avviso richiede l'autorizzazione per salvare le impostazioni del proxy e riavviare il servizio che ospita il gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-270">After you click the **Next** button, you see a warning dialog asking for your permission to save the proxy setting and restart the Gateway Host Service.</span></span>

<span data-ttu-id="428f6-271">È possibile visualizzare e aggiornare il proxy HTTP tramite lo strumento Gestione configurazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Impostare il proxy tramite Gestione configurazione](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="428f6-273">Se si configura un server proxy con autenticazione NTLM, il servizio che ospita il gateway viene eseguito nell'account di dominio.</span><span class="sxs-lookup"><span data-stu-id="428f6-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under the domain account.</span></span> <span data-ttu-id="428f6-274">Se in un secondo momento si modifica la password per l'account di dominio, ricordarsi di aggiornare le impostazioni di configurazione per il servizio e riavviarlo.</span><span class="sxs-lookup"><span data-stu-id="428f6-274">If you change the password for the domain account later, remember to update configuration settings for the service and restart it accordingly.</span></span> <span data-ttu-id="428f6-275">Per questo requisito, si consiglia di usare un account di dominio dedicato per accedere al server proxy che non richieda l'aggiornamento frequente della password.</span><span class="sxs-lookup"><span data-stu-id="428f6-275">Due to this requirement, we suggest you use a dedicated domain account to access the proxy server that does not require you to update the password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="428f6-276">Configurare le impostazioni del server proxy</span><span class="sxs-lookup"><span data-stu-id="428f6-276">Configure proxy server settings</span></span>
<span data-ttu-id="428f6-277">Se si seleziona l'impostazione **Usa il proxy di sistema** per il proxy HTTP, il gateway usa l'impostazione proxy contenuta in diahost.exe.config e diawp.exe.config.  Se non è stato specificato alcun proxy in diahost.exe.config e diawp.exe.config, il gateway si connette al servizio cloud direttamente senza passare attraverso il proxy.</span><span class="sxs-lookup"><span data-stu-id="428f6-277">If you select **Use system proxy** setting for the HTTP proxy, gateway uses the proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects to cloud service directly without going through proxy.</span></span> <span data-ttu-id="428f6-278">La procedura seguente fornisce istruzioni per l'aggiornamento del file diahost.exe.config.</span><span class="sxs-lookup"><span data-stu-id="428f6-278">The following procedure provides instructions for updating the diahost.exe.config file.</span></span>  

1. <span data-ttu-id="428f6-279">In Esplora file creare una copia sicura di C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config per eseguire il backup del file originale.</span><span class="sxs-lookup"><span data-stu-id="428f6-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config to back up the original file.</span></span>
2. <span data-ttu-id="428f6-280">Avviare Notepad.exe come amministratore e aprire il file di testo "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config". Il tag predefinito per system.net viene trovato come indicato nel codice seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find the default tag for system.net as shown in the following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="428f6-281">È quindi possibile aggiungere i dettagli del server proxy, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-281">You can then add proxy server details as shown in the following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="428f6-282">È possibile aggiungere altre proprietà all'interno del tag del proxy per specificare le impostazioni obbligatorie, ad esempio scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="428f6-282">Additional properties are allowed inside the proxy tag to specify the required settings like scriptLocation.</span></span> <span data-ttu-id="428f6-283">Per informazioni sulla sintassi, vedere [Elemento proxy (Impostazioni di rete)](https://msdn.microsoft.com/library/sa91de1e.aspx) .</span><span class="sxs-lookup"><span data-stu-id="428f6-283">Refer to [proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="428f6-284">Salvare il file di configurazione nel percorso originale, quindi riavviare il servizio che ospita il gateway di gestione dati per rilevare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="428f6-284">Save the configuration file into the original location, then restart the Data Management Gateway Host service, which picks up the changes.</span></span> <span data-ttu-id="428f6-285">Per riavviare il servizio: con l'applet dei servizi dal Pannello di controllo o da **Gestione configurazione di Gateway di gestione dati** > fare clic sul pulsante **Arresta servizio** quindi su **Avvia servizio**.</span><span class="sxs-lookup"><span data-stu-id="428f6-285">To restart the service: use services applet from the control panel, or from the **Data Management Gateway Configuration Manager** > click the **Stop Service** button, then click the **Start Service**.</span></span> <span data-ttu-id="428f6-286">Se il servizio non viene avviato, è probabile che una sintassi non corretta del tag XML sia stata aggiunta al file di configurazione dell'applicazione modificato.</span><span class="sxs-lookup"><span data-stu-id="428f6-286">If the service does not start, it is likely that an incorrect XML tag syntax has been added into the application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="428f6-287">Non dimenticare di aggiornare **entrambi i file**: diahost.exe.config e diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="428f6-287">Do not forget to update **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="428f6-288">Oltre ai punti precedenti, è necessario assicurarsi anche Microsoft Azure sia stato aggiunto all'elenco aziendale degli elementi consentiti.</span><span class="sxs-lookup"><span data-stu-id="428f6-288">In addition to these points, you also need to make sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="428f6-289">È possibile scaricare l'elenco di indirizzi IP validi per Microsoft Azure dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="428f6-289">The list of valid Microsoft Azure IP addresses can be downloaded from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="428f6-290">Possibili sintomi di problemi correlati al firewall e al server proxy</span><span class="sxs-lookup"><span data-stu-id="428f6-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="428f6-291">Se si verificano errori simili ai seguenti, è possibile che siano dovuti a una configurazione non corretta del firewall o del server proxy, che impedisce al gateway di connettersi a Data Factory per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-291">If you encounter errors similar to the following ones, it is likely due to improper configuration of the firewall or proxy server, which blocks gateway from connecting to Data Factory to authenticate itself.</span></span> <span data-ttu-id="428f6-292">Per assicurarsi che la configurazione del firewall e del server proxy sia corretta, vedere la sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="428f6-292">Refer to previous section to ensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="428f6-293">Quando si tenta di registrare il gateway, viene visualizzato l'errore seguente: "Impossibile registrare la chiave del gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-293">When you try to register the gateway, you receive the following error: "Failed to register the gateway key.</span></span> <span data-ttu-id="428f6-294">Prima di provare di nuovo a registrare la chiave del gateway, verificare che lo stato di Gateway di gestione dati sia Connesso e che il servizio host di Gateway di gestione dati sia avviato".</span><span class="sxs-lookup"><span data-stu-id="428f6-294">Before trying to register the gateway key again, confirm that the data management gateway is in a connected state and the Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="428f6-295">Quando si apre Gestione configurazione, lo stato del gateway visualizzato può essere "Disconnesso" o "Connessione".</span><span class="sxs-lookup"><span data-stu-id="428f6-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="428f6-296">Quando si visualizzano i registri eventi di Windows, in "Visualizzatore eventi" > "Registri applicazioni e servizi" > "Gateway di gestione dati", vengono visualizzati messaggi di errore simili al seguente: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="428f6-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as the following error: `Unable to connect to the remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="428f6-297">Aprire la porta 8050 per la crittografia delle credenziali</span><span class="sxs-lookup"><span data-stu-id="428f6-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="428f6-298">L'applicazione **Impostazione credenziali** usa la porta in ingresso **8050** per inoltrare le credenziali al gateway quando si configura un servizio collegato locale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-298">The **Setting Credentials** application uses the inbound port **8050** to relay credentials to the gateway when you set up an on-premises linked service in the Azure portal.</span></span> <span data-ttu-id="428f6-299">Durante la configurazione del gateway, l'installazione del gateway apre la porta nel computer gateway per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="428f6-299">During gateway setup, by default, the gateway installation opens it on the gateway machine.</span></span>

<span data-ttu-id="428f6-300">Se si usa un firewall di terze parti, è possibile aprire manualmente la porta 8050.</span><span class="sxs-lookup"><span data-stu-id="428f6-300">If you are using a third-party firewall, you can manually open the port 8050.</span></span> <span data-ttu-id="428f6-301">In caso di problemi del firewall durante la configurazione del gateway, è possibile provare a usare il comando seguente per installare il gateway senza configurare il firewall.</span><span class="sxs-lookup"><span data-stu-id="428f6-301">If you run into firewall issue during gateway setup, you can try using the following command to install the gateway without configuring the firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="428f6-302">Se si sceglie di non aprire la porta 8050 nel computer gateway, usare meccanismi diversi dall'uso dell'applicazione **Impostazione credenziali** per configurare le credenziali dell'archivio dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-302">If you choose not to open the port 8050 on the gateway machine, use mechanisms other than using the **Setting Credentials** application to configure data store credentials.</span></span> <span data-ttu-id="428f6-303">È ad esempio possibile usare il cmdlet di PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="428f6-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="428f6-304">Per informazioni su come impostare le credenziali dell'archivio dati, vedere la sezione [Impostare le credenziali e la sicurezza](#set-credentials-and-securityy) .</span><span class="sxs-lookup"><span data-stu-id="428f6-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="428f6-305">Aggiornare</span><span class="sxs-lookup"><span data-stu-id="428f6-305">Update</span></span>
<span data-ttu-id="428f6-306">Per impostazione predefinita, il gateway di gestione dati viene aggiornato automaticamente quando è disponibile una versione più recente del gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-306">By default, data management gateway is automatically updated when a newer version of the gateway is available.</span></span> <span data-ttu-id="428f6-307">Il gateway non viene aggiornato finché non vengono eseguite tutte le operazioni pianificate.</span><span class="sxs-lookup"><span data-stu-id="428f6-307">The gateway is not updated until all the scheduled tasks are done.</span></span> <span data-ttu-id="428f6-308">Nessun'altra attività viene elaborata dal gateway fino al completamento dell'operazione di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="428f6-308">No further tasks are processed by the gateway until the update operation is completed.</span></span> <span data-ttu-id="428f6-309">Se l'aggiornamento non riesce, viene eseguito il rollback del gateway alla versione precedente.</span><span class="sxs-lookup"><span data-stu-id="428f6-309">If the update fails, gateway is rolled back to the old version.</span></span>

<span data-ttu-id="428f6-310">L'ora dell'aggiornamento pianificato viene visualizzata nelle posizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="428f6-310">You see the scheduled update time in the following places:</span></span>

* <span data-ttu-id="428f6-311">Pagina delle proprietà del gateway nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-311">The gateway properties page in the Azure portal.</span></span>
* <span data-ttu-id="428f6-312">Home page di Gestione configurazione di Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="428f6-312">Home page of the Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="428f6-313">Messaggi di notifica dell'aria di notifica</span><span class="sxs-lookup"><span data-stu-id="428f6-313">System tray notification message.</span></span>

<span data-ttu-id="428f6-314">La scheda Home di Gestione configurazione di Gateway di gestione dati mostra la pianificazione dell'aggiornamento, nonché la data e l'ora dell'ultima installazione o dell'ultimo aggiornamento del gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-314">The Home tab of the Data Management Gateway Configuration Manager displays the update schedule and the last time the gateway was installed/updated.</span></span>

![Pianificare gli aggiornamenti](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="428f6-316">È possibile installare l'aggiornamento immediatamente o attendere che il gateway venga aggiornato automaticamente all'ora pianificata.</span><span class="sxs-lookup"><span data-stu-id="428f6-316">You can install the update right away or wait for the gateway to be automatically updated at the scheduled time.</span></span> <span data-ttu-id="428f6-317">Ad esempio, l'immagine seguente mostra il messaggio di notifica in Gestione configurazione del gateway con il pulsante Aggiorna su cui è possibile fare clic per avviare immediatamente l'installazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-317">For example, the following image shows you the notification message shown in the Gateway Configuration Manager along with the Update button that you can click to install it immediately.</span></span>

![Aggiorna in Gestione configurazione di Gateway di gestione dati](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="428f6-319">Il messaggio di notifica nell'area di notifica sarà simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-319">The notification message in the system tray would look as shown in the following image:</span></span>

![Messaggio nell'area di notifica](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="428f6-321">Lo stato dell'operazione di aggiornamento, manuale o automatica, viene visualizzato nell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="428f6-321">You see the status of update operation (manual or automatic) in the system tray.</span></span> <span data-ttu-id="428f6-322">Alla successiva apertura di Gestione configurazione del gateway verrà visualizzato un messaggio sulla barra di notifica per indicare che il gateway è stato aggiornato, insieme a un collegamento [all'argomento Novità](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="428f6-322">When you launch Gateway Configuration Manager next time, you see a message on the notification bar that the gateway has been updated along with a link to [what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="to-disableenable-auto-update-feature"></a><span data-ttu-id="428f6-323">Per abilitare o disabilitare la funzionalità di aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="428f6-323">To disable/enable auto-update feature</span></span>
<span data-ttu-id="428f6-324">È possibile abilitare/disabilitare la funzionalità di aggiornamento automatico con la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="428f6-324">You can disable/enable the auto-update feature by doing the following steps:</span></span>

<span data-ttu-id="428f6-325">[Per gateway a nodo singolo]</span><span class="sxs-lookup"><span data-stu-id="428f6-325">[For single node gateway]</span></span>
1. <span data-ttu-id="428f6-326">Avviare Windows PowerShell nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-326">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="428f6-327">Passare alla cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="428f6-327">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="428f6-328">Eseguire il comando seguente per disattivare (disabilitare) la funzionalità di aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="428f6-328">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="428f6-329">Per riattivarla:</span><span class="sxs-lookup"><span data-stu-id="428f6-329">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="428f6-330">[[Per gateway a più nodi a disponibilità e scalabilità elevate (anteprima)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="428f6-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="428f6-331">Avviare Windows PowerShell nel computer gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-331">Launch Windows PowerShell on the gateway machine.</span></span>
2. <span data-ttu-id="428f6-332">Passare alla cartella C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript.</span><span class="sxs-lookup"><span data-stu-id="428f6-332">Switch to the C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="428f6-333">Eseguire il comando seguente per disattivare (disabilitare) la funzionalità di aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="428f6-333">Run the following command to turn the auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="428f6-334">Per il gateway con funzionalità di disponibilità elevata (anteprima), è necessario un parametro di AuthKey aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="428f6-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="428f6-335">Per riattivarla:</span><span class="sxs-lookup"><span data-stu-id="428f6-335">To turn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install the gateway, you can launch Data Management Gateway Configuration Manager in one of the following ways:

1. In the **Search** window, type **Data Management Gateway** to access this utility.
2. Run the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
The Home page allows you to do the following actions:

* View status of the gateway (connected to the cloud service etc.).
* **Register** using a key from the portal.
* **Stop** and start the **Data Management Gateway Host service** on the gateway machine.
* **Schedule updates** at a specific time of the days.
* View the date when the gateway was **last updated**.

### Settings page
The Settings page allows you to do the following actions:

* View, change, and export **certificate** used by the gateway. This certificate is used to encrypt data source credentials.
* Change **HTTPS port** for the endpoint. The gateway opens a port for setting the data source credentials.
* **Status** of the endpoint
* View **SSL certificate** is used for SSL communication between portal and the gateway to set credentials for data sources.  

### Diagnostics page
The Diagnostics page allows you to do the following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs to Microsoft if there was a failure.
* **Test connection** to a data source.  

### Help page
The Help page displays the following information:  

* Brief description of the gateway
* Version number
* Links to online help, privacy statement, and license agreement.  

## Monitor gateway in the portal
In the Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate to the home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select the **gateway** in the **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In the **Gateway** page, you can see the memory and CPU usage of the gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** to see more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

The following table provides descriptions of columns in the **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of the logical gateway and nodes associated with the gateway. Node is an on-premises Windows machine that has the gateway installed on it. For information on having more than one node (up to four nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of the logical gateway and the gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows the version of the logical gateway and each gateway node. The version of the logical gateway is determined based on version of majority of nodes in the group. If there are nodes with different versions in the logical gateway setup, only the nodes with the same version number as the logical gateway function properly. Others are in the limited mode and need to be manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies the maximum concurrent jobs for each node. This value is defined based on the machine size. You can increase the limit to scale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when the scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used to execute jobs. There is only one dispatcher node, which is used to pull tasks/jobs from cloud services and dispatch them to different worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in the gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
The following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected to Data Factory service.
Offline | Node is offline.
Upgrading | The node is being auto-updated.
Limited | Due to Connectivity issue. May be due to HTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from the configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect to other nodes. 


The following table provides possible statuses of a **logical gateway**. The gateway status depends on statuses of the gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered to this logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due to credential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure the number of **concurrent data movement jobs** that can run on a node to scale up the capability of moving data between on-premises and cloud data stores. 

When the available memory and CPU are not utilized well, but the idle capacity is 0, you should scale up by increasing the number of concurrent jobs that can run on a node. You may also want to scale up when activities are timing out because the gateway is overloaded. In the advanced settings of a gateway node, you can increase the maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using the data management gateway.  

## Move gateway from one machine to another
This section provides steps for moving gateway client from one machine to another machine.

1. In the portal, navigate to the **Data Factory home page**, and click the **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in the **DATA GATEWAYS** section of the **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In the **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In the **Configure** page, click **Download and install data gateway**, and follow instructions to install the data gateway on the machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep the **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In the **Configure** page in the portal, click **Recreate key** on the command bar, and click **Yes** for the warning message. Click **copy button** next to key text that copies the key to the clipboard. The gateway on the old machine stops functioning as soon you recreate the key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste the **key** into text box in the **Register Gateway** page of the **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box to see the key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** to register the gateway with the cloud service.
9. On the **Settings** tab, click **Change** to select the same certificate that was used with the old gateway, enter the **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from the old gateway by doing the following steps: launch Data Management Gateway Configuration Manager on the old machine, switch to the **Certificate** tab, click **Export** button and follow the instructions.
10. After successful registration of the gateway, you should see the **Registration** set to **Registered** and **Status** set to **Started** on the Home page of the Gateway Configuration Manager.

## Encrypting credentials
To encrypt credentials in the Data Factory Editor, do the following steps:

1. Launch web browser on the **gateway machine**, navigate to [Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in the **DATA FACTORY** page and then click **Author & Deploy** to launch Data Factory Editor.   
2. Click an existing **linked service** in the tree view to see its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In the JSON editor, for the **gatewayName** property, enter the name of the gateway.
4. Enter server name for the **Data Source** property in the **connectionString**.
5. Enter database name for the **Initial Catalog** property in the **connectionString**.    
6. Click **Encrypt** button on the command bar that launches the click-once **Credential Manager** application. You should see the **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In the **Setting Credentials** dialog box, do the following steps:
   1. Select **authentication** that you want the Data Factory service to use to connect to the database.
   2. Enter name of the user who has access to the database for the **USERNAME** setting.
   3. Enter password for the user for the **PASSWORD** setting.  
   4. Click **OK** to encrypt credentials and close the dialog box.
8. You should see a **encryptedCredential** property in the **connectionString** now.

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
<span data-ttu-id="428f6-336">Se si accede al portale da un computer diverso dal computer del gateway, è necessario assicurarsi che l'applicazione di gestione credenziali possa connettersi al computer del gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-336">If you access the portal from a machine that is different from the gateway machine, you must make sure that the Credentials Manager application can connect to the gateway machine.</span></span> <span data-ttu-id="428f6-337">Se l'applicazione non riesce a raggiungere il computer gateway, non è possibile impostare le credenziali per l'origine dati e testare la connessione all'origine dati.</span><span class="sxs-lookup"><span data-stu-id="428f6-337">If the application cannot reach the gateway machine, it does not allow you to set credentials for the data source and to test connection to the data source.</span></span>  

<span data-ttu-id="428f6-338">Quando si usa l'applicazione di **Impostazione credenziali**, il portale crittografa le credenziali usando il certificato specificato nella scheda **Certificato** di **Gestione configurazione di Gateway** del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-338">When you use the **Setting Credentials** application, the portal encrypts the credentials with the certificate specified in the **Certificate** tab of the **Gateway Configuration Manager** on the gateway machine.</span></span>

<span data-ttu-id="428f6-339">Se si vuole un approccio basato su API per crittografare le credenziali, è possibile usare il cmdlet di PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="428f6-339">If you are looking for an API-based approach for encrypting the credentials, you can use the [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet to encrypt credentials.</span></span> <span data-ttu-id="428f6-340">Questo cmdlet consente di crittografare le credenziali mediante il certificato usato dal gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-340">The cmdlet uses the certificate that gateway is configured to use to encrypt the credentials.</span></span> <span data-ttu-id="428f6-341">Aggiungere le credenziali crittografate all'elemento **EncryptedCredential** di **connectionString** nell'oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="428f6-341">You add encrypted credentials to the **EncryptedCredential** element of the **connectionString** in the JSON.</span></span> <span data-ttu-id="428f6-342">Usare l'oggetto JSON con il cmdlet [New AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) o nell'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-342">You use the JSON with the [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in the Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="428f6-343">Esiste un altro approccio per impostare le credenziali usando l'editor delle data factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="428f6-344">Se si crea un servizio collegato di SQL Server usando l'editor e si immettono le credenziali in testo normale, le credenziali vengono crittografate tramite un certificato che appartiene al servizio Data Factory,</span><span class="sxs-lookup"><span data-stu-id="428f6-344">If you create a SQL Server linked service by using the editor and you enter credentials in plain text, the credentials are encrypted using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="428f6-345">NON tramite il certificato usato dal gateway.</span><span class="sxs-lookup"><span data-stu-id="428f6-345">It does NOT use the certificate that gateway is configured to use.</span></span> <span data-ttu-id="428f6-346">Anche se questo approccio può apparire leggermente più veloce, in alcuni casi risulta meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="428f6-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="428f6-347">È pertanto consigliabile seguire questo approccio solo per scopi di sviluppo o di test.</span><span class="sxs-lookup"><span data-stu-id="428f6-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="428f6-348">Cmdlet PowerShell</span><span class="sxs-lookup"><span data-stu-id="428f6-348">PowerShell cmdlets</span></span>
<span data-ttu-id="428f6-349">Questa sezione descrive come creare e registrare un gateway con i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="428f6-349">This section describes how to create and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="428f6-350">Avviare **Azure PowerShell** in modalità di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="428f6-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="428f6-351">Accedere all'account Azure eseguendo il comando seguente e immettendo le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-351">Log in to your Azure account by running the following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="428f6-352">Usare il cmdlet **New-AzureRmDataFactoryGateway** per creare un gateway logico come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="428f6-352">Use the **New-AzureRmDataFactoryGateway** cmdlet to create a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="428f6-353">**Comando di esempio e output**:</span><span class="sxs-lookup"><span data-stu-id="428f6-353">**Example command and output**:</span></span>

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

1. <span data-ttu-id="428f6-354">In Azure PowerShell, passare alla cartella: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="428f6-354">In Azure PowerShell, switch to the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="428f6-355">Eseguire **RegisterGateway.ps1** associato alla variabile locale **$Key** come illustrato nel comando seguente.</span><span class="sxs-lookup"><span data-stu-id="428f6-355">Run **RegisterGateway.ps1** associated with the local variable **$Key** as shown in the following command.</span></span> <span data-ttu-id="428f6-356">Lo script registra l'agente client installato nel computer con il gateway logico creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="428f6-356">This script registers the client agent installed on your machine with the logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="428f6-357">È possibile registrare il gateway in un computer remoto usando il parametro IsRegisterOnRemoteMachine.</span><span class="sxs-lookup"><span data-stu-id="428f6-357">You can register the gateway on a remote machine by using the IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="428f6-358">Esempio:</span><span class="sxs-lookup"><span data-stu-id="428f6-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="428f6-359">È possibile usare il cmdlet **Get-AzureRmDataFactoryGateway** per ottenere l'elenco di gateway nell'istanza di Data factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-359">You can use the **Get-AzureRmDataFactoryGateway** cmdlet to get the list of Gateways in your data factory.</span></span> <span data-ttu-id="428f6-360">Quando lo **stato** è **online**, il gateway è pronto per essere usato.</span><span class="sxs-lookup"><span data-stu-id="428f6-360">When the **Status** shows **online**, it means your gateway is ready to use.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="428f6-361">È possibile rimuovere un gateway con il cmdlet **Remove-AzureRmDataFactoryGateway** e aggiornare la descrizione per un gateway usando i cmdlet **Set-AzureRmDataFactoryGateway**.</span><span class="sxs-lookup"><span data-stu-id="428f6-361">You can remove a gateway using the **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using the **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="428f6-362">Per la sintassi e altri dettagli relativi a questi cmdlet, vedere Riferimento ai cmdlet di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="428f6-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="428f6-363">Elencare i gateway usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="428f6-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="428f6-364">Rimuovere il gateway usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="428f6-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="428f6-365">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="428f6-365">Next steps</span></span>
* <span data-ttu-id="428f6-366">Vedere l'articolo [Spostare dati tra archivi dati locali e cloud](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="428f6-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="428f6-367">In questa procedura dettagliata viene creata una pipeline che usa il gateway per spostare i dati da un database di SQL Server locale a un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="428f6-367">In the walkthrough, you create a pipeline that uses the gateway to move data from an on-premises SQL Server database to an Azure blob.</span></span>  
