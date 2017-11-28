---
title: note sulla aaaRelease per Gateway di gestione dati | Documenti Microsoft
description: Note sulla versione di Gateway di gestione dati
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="348d6-103">Note sulla versione di Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="348d6-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="348d6-104">Una delle sfide hello per l'integrazione di dati più recenti è toomove dati tooand da toocloud locale.</span><span class="sxs-lookup"><span data-stu-id="348d6-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="348d6-105">Data Factory rende l'integrazione con i Gateway di gestione dati, ovvero un agente che è possibile installare lo spostamento di dati locale tooenable ibrido.</span><span class="sxs-lookup"><span data-stu-id="348d6-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="348d6-106">Vedere i seguenti articoli per informazioni dettagliate su Gateway di gestione dati hello e come toouse è:</span><span class="sxs-lookup"><span data-stu-id="348d6-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="348d6-107">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="348d6-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="348d6-108">Spostare dati tra un ambiente locale e il cloud mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="348d6-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="348d6-109">VERSIONE CORRENTE (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="348d6-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="348d6-110">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-110">Enhancements-</span></span>
- <span data-ttu-id="348d6-111">È possibile aggiungere bus di servizio toowhitelist le voci DNS anziché whitelist tutti gli indirizzi IP di Azure da un firewall (se necessario).</span><span class="sxs-lookup"><span data-stu-id="348d6-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="348d6-112">È possibile trovare la rispettiva voce DNS nel portale di Azure (Data Factory -> "Creare e distribuire" -> "Gateway" -> "serviceUrls" (in JSON)</span><span class="sxs-lookup"><span data-stu-id="348d6-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="348d6-113">Il connettore HDFS supporta ora il certificato pubblico autofirmato, consentendo di saltare la convalida SSL.</span><span class="sxs-lookup"><span data-stu-id="348d6-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="348d6-114">Problema risolto: Problema con gateway offline durante l'aggiornamento (in scadenza inclinazione tooclock)</span><span class="sxs-lookup"><span data-stu-id="348d6-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="348d6-115">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="348d6-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="348d6-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="348d6-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="348d6-117">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-117">Enhancements-</span></span>
-   <span data-ttu-id="348d6-118">È possibile aggiungere toowhitelist le voci DNS Service Bus anziché whitelist tutti gli indirizzi IP di Azure da un firewall (se necessario).</span><span class="sxs-lookup"><span data-stu-id="348d6-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="348d6-119">Altri dettagli sono disponibili qui.</span><span class="sxs-lookup"><span data-stu-id="348d6-119">More details here.</span></span>
-   <span data-ttu-id="348d6-120">È ora possibile copiare dati da e verso un blob in blocchi singolo backup too4.75 TB, ovvero dimensioni hello massimo supportato di blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="348d6-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="348d6-121">Il limite precedente era di 195 GB.</span><span class="sxs-lookup"><span data-stu-id="348d6-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="348d6-122">Corretto: problema relativo alla memoria esaurita durante la decompressione di alcuni file di piccole dimensioni durante l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="348d6-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="348d6-123">Problema risolto: Indice fuori problema intervallo durante la copia da DB documento tooan SQL Server locale con funzionalità idempotenza.</span><span class="sxs-lookup"><span data-stu-id="348d6-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="348d6-124">Corretto: lo script di pulizia di SQL non funziona con l'istanza locale di SQL Server dalla Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="348d6-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="348d6-125">Problema risolto: Nome della colonna con lo spazio alla fine di hello non funziona nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="348d6-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="348d6-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="348d6-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="348d6-127">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-127">Enhancements-</span></span>
- <span data-ttu-id="348d6-128">Corretto: problema relativo alle credenziali mancanti al riavvio del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="348d6-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="348d6-129">Corretto: problema relativo alla registrazione durante il ripristino del gateway tramite un file di backup.</span><span class="sxs-lookup"><span data-stu-id="348d6-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="348d6-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="348d6-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="348d6-131">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-131">Enhancements-</span></span>
- <span data-ttu-id="348d6-132">Corretto: lettura non corretta del valore Null decimale da Oracle come origine.</span><span class="sxs-lookup"><span data-stu-id="348d6-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="348d6-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="348d6-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="348d6-134">Novità</span><span class="sxs-lookup"><span data-stu-id="348d6-134">What’s new</span></span>
- <span data-ttu-id="348d6-135">Gli utenti possono fornire commenti e suggerimenti sull'esperienza di registrazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="348d6-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="348d6-136">Supporta il nuovo formato di compressione ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="348d6-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="348d6-137">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-137">Enhancements-</span></span>
- <span data-ttu-id="348d6-138">Miglioramento delle prestazioni per Oracle Sink, origine HDFS.</span><span class="sxs-lookup"><span data-stu-id="348d6-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="348d6-139">Correzione di bug per l'aggiornamento automatico del gateway, capacità di elaborazione parallela del gateway.</span><span class="sxs-lookup"><span data-stu-id="348d6-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="348d6-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="348d6-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="348d6-141">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-141">Enhancements</span></span>
- <span data-ttu-id="348d6-142">Migliore e più affidabile Gateway registrazione esperienza-ora è possibile monitorare lo stato di avanzamento durante il processo di registrazione Gateway hello, che rende la registrazione di hello esperienza più reattiva.</span><span class="sxs-lookup"><span data-stu-id="348d6-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="348d6-143">Miglioramento Gateway ripristino configurazione di processo, è comunque possibile ripristinare i gateway anche se i file di backup gateway hello con questo aggiornamento non si dispone.</span><span class="sxs-lookup"><span data-stu-id="348d6-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="348d6-144">In questo caso è necessario tooreset le credenziali di servizio collegato nel portale.</span><span class="sxs-lookup"><span data-stu-id="348d6-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="348d6-145">Correzione di bug.</span><span class="sxs-lookup"><span data-stu-id="348d6-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="348d6-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="348d6-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="348d6-147">Novità</span><span class="sxs-lookup"><span data-stu-id="348d6-147">What’s new</span></span>

- <span data-ttu-id="348d6-148">È ora possibile archiviare localmente le credenziali dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="348d6-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="348d6-149">Hello credenziali vengono crittografate.</span><span class="sxs-lookup"><span data-stu-id="348d6-149">hello credentials are encrypted.</span></span> <span data-ttu-id="348d6-150">le credenziali dell'origine dati Hello possono essere ripristinate e ripristino i file di backup hello che possono essere esportati da hello locale tutti i Gateway esistente.</span><span class="sxs-lookup"><span data-stu-id="348d6-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="348d6-151">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="348d6-151">Enhancements-</span></span>

- <span data-ttu-id="348d6-152">Esperienza di registrazione gateway migliorata e più affidabile.</span><span class="sxs-lookup"><span data-stu-id="348d6-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="348d6-153">Supporta il rilevamento automatico della configurazione QuoteChar di formato di testo in copia guidata e migliorare hello accuratezza di rilevamento di formato generale.</span><span class="sxs-lookup"><span data-stu-id="348d6-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="348d6-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="348d6-154">2.3.6100.2</span></span>

- <span data-ttu-id="348d6-155">Support del rilevamento automatico di firstRowAsHeader e SkipLineCount nella copia guidata per i file di testo in HDFS e nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="348d6-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="348d6-156">Migliorare la stabilità di hello della connessione di rete tra i gateway e Bus di servizio</span><span class="sxs-lookup"><span data-stu-id="348d6-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="348d6-157">Alcune correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="348d6-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="348d6-158">2.2.6072.1</span></span>

*  <span data-ttu-id="348d6-159">Supporta l'impostazione proxy HTTP per l'utilizzo di gateway hello hello Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="348d6-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="348d6-160">Se configurato, l'accesso tramite proxy HTTP è disponibile per il BLOB di Azure, le tabelle di Azure, Azure Data Lake e Document DB.</span><span class="sxs-lookup"><span data-stu-id="348d6-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="348d6-161">Intestazione supporta gestione TextFormat quando si copiano dati dal File System locale tooAzure Blob, archivio Azure Data Lake e HDFS in locale.</span><span class="sxs-lookup"><span data-stu-id="348d6-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="348d6-162">Supporta la copia dei dati da Blob di accodamento e Blob di pagine insieme hello già supportati Blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="348d6-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="348d6-163">Introduce un nuovo stato del gateway **Online (limitato)**, che indica che le funzionalità principali di hello del gateway hello funziona ad eccezione di supporto delle operazioni interattive hello per la copia guidata.</span><span class="sxs-lookup"><span data-stu-id="348d6-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="348d6-164">Migliora l'affidabilità di hello di registrazione del gateway mediante la chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="348d6-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="348d6-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="348d6-165">2.1.6040.</span></span>

*  <span data-ttu-id="348d6-166">Driver DB2 è incluso nel pacchetto di installazione di gateway hello ora.</span><span class="sxs-lookup"><span data-stu-id="348d6-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="348d6-167">Non è necessario tooinstall è separatamente.</span><span class="sxs-lookup"><span data-stu-id="348d6-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="348d6-168">Driver DB2 supporta ora z/OS e DB2 per i (AS / 400) insieme a piattaforme di hello già supportate (Windows, Linux e Unix).</span><span class="sxs-lookup"><span data-stu-id="348d6-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="348d6-169">Supporta l'uso di Azure Cosmos DB come origine o destinazione per gli archivi dati locali.</span><span class="sxs-lookup"><span data-stu-id="348d6-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="348d6-170">Supporta la copia di archiviazione dei dati blob da/toocold/hot insieme hello già supportati account di archiviazione generico.</span><span class="sxs-lookup"><span data-stu-id="348d6-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="348d6-171">Consente di tooconnect tooon locale SQL Server tramite il gateway con privilegi di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="348d6-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="348d6-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="348d6-172">2.0.6013.1</span></span>

*  <span data-ttu-id="348d6-173">È possibile selezionare hello lingua toobe utilizzato da un gateway durante l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="348d6-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="348d6-174">Quando il gateway non funziona come previsto, è possibile scegliere toosend registri del gateway di ultimi sette giorni tooMicrosoft toofacilitate risoluzione dei problemi di rilascio hello.</span><span class="sxs-lookup"><span data-stu-id="348d6-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="348d6-175">Se il gateway non è connesso toohello servizio cloud, è possibile scegliere toosave e archiviare i registri del gateway.</span><span class="sxs-lookup"><span data-stu-id="348d6-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="348d6-176">Miglioramenti all'interfaccia utente per la gestione della configurazione gateway:</span><span class="sxs-lookup"><span data-stu-id="348d6-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="348d6-177">Rendere più visibile nella scheda Home di hello lo stato del gateway.</span><span class="sxs-lookup"><span data-stu-id="348d6-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="348d6-178">Controlli riorganizzati e semplificati.</span><span class="sxs-lookup"><span data-stu-id="348d6-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="348d6-179">È possibile copiare dati da un archivio utilizzando hello [strumento anteprima senza codice copia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="348d6-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="348d6-180">Per informazioni generiche su questa funzionalità, vedere [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="348d6-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="348d6-181">È possibile utilizzare dati tooingress Gateway di gestione dati direttamente da un database di SQL Server locale in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="348d6-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="348d6-182">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-182">Performance improvements</span></span>

    * <span data-ttu-id="348d6-183">Prestazioni di visualizzazione migliorate dello schema e dell'anteprima in SQL Server nello strumento di anteprima della copia senza codice.</span><span class="sxs-lookup"><span data-stu-id="348d6-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="348d6-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="348d6-184">1.12.5953.1</span></span>

*  <span data-ttu-id="348d6-185">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="348d6-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="348d6-186">1.11.5918.1</span></span>

*  <span data-ttu-id="348d6-187">Dimensione massima del registro eventi del gateway hello è stato aumentato da 1 MB too40 MB.</span><span class="sxs-lookup"><span data-stu-id="348d6-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="348d6-188">Nel caso in cui sia necessario un riavvio durante l'aggiornamento automatico del gateway, viene visualizzata una finestra di dialogo di avviso.</span><span class="sxs-lookup"><span data-stu-id="348d6-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="348d6-189">È possibile scegliere toorestart destra quindi o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="348d6-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="348d6-190">In caso di errore dell'aggiornamento automatico, il programma di installazione del gateway ritenta l'aggiornamento automatico al massimo tre volte.</span><span class="sxs-lookup"><span data-stu-id="348d6-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="348d6-191">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-191">Performance improvements</span></span>

    * <span data-ttu-id="348d6-192">È possibile migliorare le prestazioni in caso di caricamento di tabelle di grandi dimensioni dal server locale in uno scenario di copia senza codice.</span><span class="sxs-lookup"><span data-stu-id="348d6-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="348d6-193">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="348d6-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="348d6-194">1.10.5892.1</span></span>

*  <span data-ttu-id="348d6-195">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-195">Performance improvements</span></span>

*  <span data-ttu-id="348d6-196">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="348d6-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="348d6-197">1.9.5865.2</span></span>

*  <span data-ttu-id="348d6-198">Funzionalità di aggiornamento automatico senza intervento dell'utente</span><span class="sxs-lookup"><span data-stu-id="348d6-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="348d6-199">Nuova icona dell'area di notifica con indicatori di stato del gateway</span><span class="sxs-lookup"><span data-stu-id="348d6-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="348d6-200">Capacità troppo "Aggiorna" da client hello</span><span class="sxs-lookup"><span data-stu-id="348d6-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="348d6-201">Ora pianificazione dell'aggiornamento tooset possibilità</span><span class="sxs-lookup"><span data-stu-id="348d6-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="348d6-202">Script di PowerShell per attivare o disattivare l'aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="348d6-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="348d6-203">Supporto per il formato JSON</span><span class="sxs-lookup"><span data-stu-id="348d6-203">Support for JSON format</span></span>  
*  <span data-ttu-id="348d6-204">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-204">Performance improvements</span></span>
*  <span data-ttu-id="348d6-205">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="348d6-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="348d6-206">1.8.5822.1</span></span>

*  <span data-ttu-id="348d6-207">Miglioramento dell'esperienza di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="348d6-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="348d6-208">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-208">Performance improvements</span></span>
*  <span data-ttu-id="348d6-209">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="348d6-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="348d6-210">1.7.5795.1</span></span>

*  <span data-ttu-id="348d6-211">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-211">Performance improvements</span></span>
*  <span data-ttu-id="348d6-212">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="348d6-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="348d6-213">1.7.5764.1</span></span>

*  <span data-ttu-id="348d6-214">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-214">Performance improvements</span></span>
*  <span data-ttu-id="348d6-215">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="348d6-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="348d6-216">1.6.5735.1</span></span>

*  <span data-ttu-id="348d6-217">Supporto di origine/sink HDFS in locale</span><span class="sxs-lookup"><span data-stu-id="348d6-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="348d6-218">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-218">Performance improvements</span></span>
*  <span data-ttu-id="348d6-219">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="348d6-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="348d6-220">1.6.5696.1</span></span>

*  <span data-ttu-id="348d6-221">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-221">Performance improvements</span></span>
*  <span data-ttu-id="348d6-222">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="348d6-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="348d6-223">1.6.5676.1</span></span>

*  <span data-ttu-id="348d6-224">Supporto degli strumenti di diagnostica in Gestione configurazione</span><span class="sxs-lookup"><span data-stu-id="348d6-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="348d6-225">Supporto delle colonne di tabella per le origini dati tabulari per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-226">Supporto di SQL DW per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-227">Supporto dell'isolamento in BlobSource e FileSource per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-228">Supporto di CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy in BlobSink e FileSink con copia binaria per Data Factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-229">Supporto dello stato di avanzamento della creazione di report per l'attività di copia per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-230">Supporto della convalida della connettività dell'origine dati per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-231">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="348d6-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="348d6-232">1.6.5672.1</span></span>

*  <span data-ttu-id="348d6-233">Supporto del nome di tabella per l'origine dati ODBC per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-234">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-234">Performance improvements</span></span>
*  <span data-ttu-id="348d6-235">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="348d6-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="348d6-236">1.6.5658.1</span></span>

*  <span data-ttu-id="348d6-237">Supporto del sink dei file per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-238">Supporto del mantenimento della gerarchia nella copia binaria per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-239">Supporto dell'idempotenza dell'attività di copia per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-240">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="348d6-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="348d6-241">1.6.5640.1</span></span>

*  <span data-ttu-id="348d6-242">Supporto di altre 3 origini dati per Data factory di Azure (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="348d6-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="348d6-243">Supporto delle virgolette nel parser CSV per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-244">Supporto della compressione (BZip2)</span><span class="sxs-lookup"><span data-stu-id="348d6-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="348d6-245">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="348d6-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="348d6-246">1.5.5612.1</span></span>

*  <span data-ttu-id="348d6-247">Supporto di cinque database relazionali per Data Factory di Azure (MySQL, PostgreSQL, DB2, Teradata e Sybase)</span><span class="sxs-lookup"><span data-stu-id="348d6-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="348d6-248">Supporto della compressione (Gzip e Deflate)</span><span class="sxs-lookup"><span data-stu-id="348d6-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="348d6-249">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-249">Performance improvements</span></span>
*  <span data-ttu-id="348d6-250">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="348d6-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="348d6-251">1.4.5549.1</span></span>

*  <span data-ttu-id="348d6-252">Aggiunta del supporto dell'origine dati Oracle per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="348d6-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="348d6-253">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="348d6-253">Performance improvements</span></span>
*  <span data-ttu-id="348d6-254">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="348d6-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="348d6-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="348d6-255">1.4.5492.1</span></span>

*  <span data-ttu-id="348d6-256">File binario unificato che supporta il servizio Data factory di Microsoft Azure e il servizio Power BI di Office 365</span><span class="sxs-lookup"><span data-stu-id="348d6-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="348d6-257">Ridefinire il processo di registrazione e l'interfaccia utente di configurazione hello</span><span class="sxs-lookup"><span data-stu-id="348d6-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="348d6-258">Data Factory di Azure: supporto di ingresso e uscita in Azure per l'origine dati SQL Server</span><span class="sxs-lookup"><span data-stu-id="348d6-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="348d6-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="348d6-259">1.2.5303.1</span></span>

*  <span data-ttu-id="348d6-260">Correggere timeout problema toosupport più connessioni a origini dati richiede molto tempo.</span><span class="sxs-lookup"><span data-stu-id="348d6-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="348d6-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="348d6-261">1.1.5526.8</span></span>

*  <span data-ttu-id="348d6-262">Richiede .NET Framework 4.5.1 come prerequisito durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="348d6-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="348d6-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="348d6-263">1.0.5144.2</span></span>

*  <span data-ttu-id="348d6-264">Nessuna modifica che interessi gli scenari di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="348d6-264">No changes that affect Azure Data Factory scenarios.</span></span>
