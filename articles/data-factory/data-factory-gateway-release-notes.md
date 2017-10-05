---
title: Note sulla versione del gateway di gestione dati | Microsoft Docs
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
ms.openlocfilehash: c052d7e9f757164429ce867201b96305e405dce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="52ece-103">Note sulla versione di Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="52ece-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="52ece-104">Una delle maggiori difficoltà relative all'integrazione moderna dei dati consiste nello spostamento di dati da ambienti locali al cloud e viceversa.</span><span class="sxs-lookup"><span data-stu-id="52ece-104">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="52ece-105">Data Factory esegue questa integrazione con Gateway di gestione dati, un agente che è possibile installare in locale per abilitare lo spostamento di dati ibridi.</span><span class="sxs-lookup"><span data-stu-id="52ece-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="52ece-106">Vedere gli articoli seguenti per informazioni dettagliate su Gateway di gestione dati e su come usarlo:</span><span class="sxs-lookup"><span data-stu-id="52ece-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="52ece-107">Gateway di gestione dati</span><span class="sxs-lookup"><span data-stu-id="52ece-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="52ece-108">Spostare dati tra un ambiente locale e il cloud mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="52ece-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="52ece-109">VERSIONE CORRENTE (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="52ece-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="52ece-110">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-110">Enhancements-</span></span>
- <span data-ttu-id="52ece-111">È possibile aggiungere le voci DNS per aggiungere il bus di servizio all'elenco elementi consentiti, invece di inserire in tale elenco tutti gli indirizzi IP di Azure IP dal firewall (se necessario).</span><span class="sxs-lookup"><span data-stu-id="52ece-111">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="52ece-112">È possibile trovare la rispettiva voce DNS nel portale di Azure (Data Factory -> "Creare e distribuire" -> "Gateway" -> "serviceUrls" (in JSON)</span><span class="sxs-lookup"><span data-stu-id="52ece-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="52ece-113">Il connettore HDFS supporta ora il certificato pubblico autofirmato, consentendo di saltare la convalida SSL.</span><span class="sxs-lookup"><span data-stu-id="52ece-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="52ece-114">Corretto: problema relativo al gateway offline durante l'aggiornamento (a causa di uno sfasamento del clock)</span><span class="sxs-lookup"><span data-stu-id="52ece-114">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="52ece-115">Versioni precedenti</span><span class="sxs-lookup"><span data-stu-id="52ece-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="52ece-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="52ece-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="52ece-117">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-117">Enhancements-</span></span>
-   <span data-ttu-id="52ece-118">È possibile aggiungere le voci DNS per aggiungere il bus di servizio all'elenco elementi consentiti, invece di inserire in tale elenco tutti gli indirizzi IP di Azure IP dal firewall (se necessario).</span><span class="sxs-lookup"><span data-stu-id="52ece-118">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="52ece-119">Altri dettagli sono disponibili qui.</span><span class="sxs-lookup"><span data-stu-id="52ece-119">More details here.</span></span>
-   <span data-ttu-id="52ece-120">È ora possibile copiare i dati in/da un singolo BLOB in blocchi fino a 4,75 TB, che corrisponde alle dimensioni massime supportate per i BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="52ece-120">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="52ece-121">Il limite precedente era di 195 GB.</span><span class="sxs-lookup"><span data-stu-id="52ece-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="52ece-122">Corretto: problema relativo alla memoria esaurita durante la decompressione di alcuni file di piccole dimensioni durante l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="52ece-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="52ece-123">Corretto: problema relativo all'indice non compreso nell'intervallo durante la copia da Document DB a un'istanza locale di SQL Server con funzionalità di idempotenza.</span><span class="sxs-lookup"><span data-stu-id="52ece-123">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="52ece-124">Corretto: lo script di pulizia di SQL non funziona con l'istanza locale di SQL Server dalla Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="52ece-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="52ece-125">Corretto: il nome di colonna con uno spazio finale non funziona nell'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="52ece-125">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="52ece-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="52ece-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="52ece-127">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-127">Enhancements-</span></span>
- <span data-ttu-id="52ece-128">Corretto: problema relativo alle credenziali mancanti al riavvio del computer gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="52ece-129">Corretto: problema relativo alla registrazione durante il ripristino del gateway tramite un file di backup.</span><span class="sxs-lookup"><span data-stu-id="52ece-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="52ece-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="52ece-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="52ece-131">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-131">Enhancements-</span></span>
- <span data-ttu-id="52ece-132">Corretto: lettura non corretta del valore Null decimale da Oracle come origine.</span><span class="sxs-lookup"><span data-stu-id="52ece-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="52ece-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="52ece-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="52ece-134">Novità</span><span class="sxs-lookup"><span data-stu-id="52ece-134">What’s new</span></span>
- <span data-ttu-id="52ece-135">Gli utenti possono fornire commenti e suggerimenti sull'esperienza di registrazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="52ece-136">Supporta il nuovo formato di compressione ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="52ece-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="52ece-137">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-137">Enhancements-</span></span>
- <span data-ttu-id="52ece-138">Miglioramento delle prestazioni per Oracle Sink, origine HDFS.</span><span class="sxs-lookup"><span data-stu-id="52ece-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="52ece-139">Correzione di bug per l'aggiornamento automatico del gateway, capacità di elaborazione parallela del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="52ece-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="52ece-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="52ece-141">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-141">Enhancements</span></span>
- <span data-ttu-id="52ece-142">Esperienza di registrazione del gateway migliorata e più affidabile. L'esperienza risulta più efficiente grazie alla possibilità di tenere traccia dello stato di avanzamento durante il processo di registrazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-142">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="52ece-143">Miglioramento del processo di ripristino del gateway. Con questo aggiornamento è possibile ripristinare il gateway anche se non si ha il relativo file di backup.</span><span class="sxs-lookup"><span data-stu-id="52ece-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="52ece-144">Sarà necessario reimpostare le credenziali del servizio collegato nel portale.</span><span class="sxs-lookup"><span data-stu-id="52ece-144">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="52ece-145">Correzione di bug.</span><span class="sxs-lookup"><span data-stu-id="52ece-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="52ece-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="52ece-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="52ece-147">Novità</span><span class="sxs-lookup"><span data-stu-id="52ece-147">What’s new</span></span>

- <span data-ttu-id="52ece-148">È ora possibile archiviare localmente le credenziali dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="52ece-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="52ece-149">Le credenziali vengono crittografate.</span><span class="sxs-lookup"><span data-stu-id="52ece-149">The credentials are encrypted.</span></span> <span data-ttu-id="52ece-150">Le credenziali dell'origine dati possono essere recuperate e ripristinate usando il file di backup che può essere esportato dal gateway esistente, operando in locale.</span><span class="sxs-lookup"><span data-stu-id="52ece-150">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="52ece-151">Miglioramenti</span><span class="sxs-lookup"><span data-stu-id="52ece-151">Enhancements-</span></span>

- <span data-ttu-id="52ece-152">Esperienza di registrazione gateway migliorata e più affidabile.</span><span class="sxs-lookup"><span data-stu-id="52ece-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="52ece-153">Supporto del rilevamento automatico della configurazione QuoteChar per il formato di testo in copia guidata e aumento dell'accuratezza di rilevamento del formato generale.</span><span class="sxs-lookup"><span data-stu-id="52ece-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="52ece-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="52ece-154">2.3.6100.2</span></span>

- <span data-ttu-id="52ece-155">Support del rilevamento automatico di firstRowAsHeader e SkipLineCount nella copia guidata per i file di testo in HDFS e nel file system locale.</span><span class="sxs-lookup"><span data-stu-id="52ece-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="52ece-156">Miglioramento della stabilità della connessione di rete tra il gateway e il bus di servizio</span><span class="sxs-lookup"><span data-stu-id="52ece-156">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="52ece-157">Alcune correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="52ece-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="52ece-158">2.2.6072.1</span></span>

*  <span data-ttu-id="52ece-159">Supporta l'impostazione proxy HTTP per il gateway tramite Gestione configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-159">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="52ece-160">Se configurato, l'accesso tramite proxy HTTP è disponibile per il BLOB di Azure, le tabelle di Azure, Azure Data Lake e Document DB.</span><span class="sxs-lookup"><span data-stu-id="52ece-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="52ece-161">Supporta la gestione delle intestazioni per il formato di testo quando si copiano dati da e verso BLOB di Azure, Azure Data Lake Store, File System locale e HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="52ece-161">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="52ece-162">Supporta la copia di dati dal BLOB di accodamento e BLOB di pagine, oltre al BLOB in blocchi già supportato.</span><span class="sxs-lookup"><span data-stu-id="52ece-162">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="52ece-163">Introduce un nuovo stato del gateway **Online (Limited)**(Online (limitato)), che indica che la funzionalità principale del gateway funziona ad eccezione del supporto delle operazioni interattive per la copia guidata.</span><span class="sxs-lookup"><span data-stu-id="52ece-163">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="52ece-164">Migliora la solidità della registrazione del gateway con la chiave di registrazione.</span><span class="sxs-lookup"><span data-stu-id="52ece-164">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="52ece-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="52ece-165">2.1.6040.</span></span>

*  <span data-ttu-id="52ece-166">Il driver DB2 è ora incluso nel pacchetto di installazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-166">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="52ece-167">Non è necessario installarlo separatamente.</span><span class="sxs-lookup"><span data-stu-id="52ece-167">You do not need to install it separately.</span></span>
*  <span data-ttu-id="52ece-168">Il driver DB2 supporta ora z/OS e DB2 for i (AS/400) oltre alle piattaforme già supportate (Linux, Unix e Windows).</span><span class="sxs-lookup"><span data-stu-id="52ece-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="52ece-169">Supporta l'uso di Azure Cosmos DB come origine o destinazione per gli archivi dati locali.</span><span class="sxs-lookup"><span data-stu-id="52ece-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="52ece-170">Supporta la copia di dati da e nell'archivio BLOB ad accesso frequente o sporadico con l'account di archiviazione di uso generico già supportato.</span><span class="sxs-lookup"><span data-stu-id="52ece-170">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="52ece-171">Consente di connettersi a SQL Server locale tramite il gateway con privilegi di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="52ece-171">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="52ece-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="52ece-172">2.0.6013.1</span></span>

*  <span data-ttu-id="52ece-173">È possibile selezionare la lingua/cultura che verrà usata da un gateway durante l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="52ece-173">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="52ece-174">Quando il gateway non funziona come previsto, è possibile scegliere di inviare a Microsoft i log di gateway degli ultimi sette giorni per agevolare la risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="52ece-174">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="52ece-175">Se il gateway non è connesso al servizio cloud, è possibile scegliere di salvare e archiviare i log del gateway.</span><span class="sxs-lookup"><span data-stu-id="52ece-175">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="52ece-176">Miglioramenti all'interfaccia utente per la gestione della configurazione gateway:</span><span class="sxs-lookup"><span data-stu-id="52ece-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="52ece-177">Stato del gateway più visibile sulla scheda Home.</span><span class="sxs-lookup"><span data-stu-id="52ece-177">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="52ece-178">Controlli riorganizzati e semplificati.</span><span class="sxs-lookup"><span data-stu-id="52ece-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="52ece-179">È possibile copiare dati da un archivio tramite lo [strumento di anteprima della copia senza codice](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="52ece-179">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="52ece-180">Per informazioni generiche su questa funzionalità, vedere [Copia di staging](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="52ece-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="52ece-181">Gateway di gestione dati consente di inserire i dati direttamente da un database di SQL Server locale in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="52ece-181">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="52ece-182">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-182">Performance improvements</span></span>

    * <span data-ttu-id="52ece-183">Prestazioni di visualizzazione migliorate dello schema e dell'anteprima in SQL Server nello strumento di anteprima della copia senza codice.</span><span class="sxs-lookup"><span data-stu-id="52ece-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="52ece-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="52ece-184">1.12.5953.1</span></span>

*  <span data-ttu-id="52ece-185">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="52ece-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="52ece-186">1.11.5918.1</span></span>

*  <span data-ttu-id="52ece-187">La dimensione massima del registro eventi del gateway è aumentata da 1 MB a 40 MB.</span><span class="sxs-lookup"><span data-stu-id="52ece-187">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="52ece-188">Nel caso in cui sia necessario un riavvio durante l'aggiornamento automatico del gateway, viene visualizzata una finestra di dialogo di avviso.</span><span class="sxs-lookup"><span data-stu-id="52ece-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="52ece-189">È possibile scegliere di riavviare subito o in un secondo tempo.</span><span class="sxs-lookup"><span data-stu-id="52ece-189">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="52ece-190">In caso di errore dell'aggiornamento automatico, il programma di installazione del gateway ritenta l'aggiornamento automatico al massimo tre volte.</span><span class="sxs-lookup"><span data-stu-id="52ece-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="52ece-191">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-191">Performance improvements</span></span>

    * <span data-ttu-id="52ece-192">È possibile migliorare le prestazioni in caso di caricamento di tabelle di grandi dimensioni dal server locale in uno scenario di copia senza codice.</span><span class="sxs-lookup"><span data-stu-id="52ece-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="52ece-193">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="52ece-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="52ece-194">1.10.5892.1</span></span>

*  <span data-ttu-id="52ece-195">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-195">Performance improvements</span></span>

*  <span data-ttu-id="52ece-196">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="52ece-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="52ece-197">1.9.5865.2</span></span>

*  <span data-ttu-id="52ece-198">Funzionalità di aggiornamento automatico senza intervento dell'utente</span><span class="sxs-lookup"><span data-stu-id="52ece-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="52ece-199">Nuova icona dell'area di notifica con indicatori di stato del gateway</span><span class="sxs-lookup"><span data-stu-id="52ece-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="52ece-200">Possibilità di scegliere "Aggiorna adesso" dal client</span><span class="sxs-lookup"><span data-stu-id="52ece-200">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="52ece-201">Possibilità di impostare l'ora di pianificazione dell'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="52ece-201">Ability to set update schedule time</span></span>
*  <span data-ttu-id="52ece-202">Script di PowerShell per attivare o disattivare l'aggiornamento automatico</span><span class="sxs-lookup"><span data-stu-id="52ece-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="52ece-203">Supporto per il formato JSON</span><span class="sxs-lookup"><span data-stu-id="52ece-203">Support for JSON format</span></span>  
*  <span data-ttu-id="52ece-204">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-204">Performance improvements</span></span>
*  <span data-ttu-id="52ece-205">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="52ece-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="52ece-206">1.8.5822.1</span></span>

*  <span data-ttu-id="52ece-207">Miglioramento dell'esperienza di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="52ece-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="52ece-208">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-208">Performance improvements</span></span>
*  <span data-ttu-id="52ece-209">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="52ece-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="52ece-210">1.7.5795.1</span></span>

*  <span data-ttu-id="52ece-211">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-211">Performance improvements</span></span>
*  <span data-ttu-id="52ece-212">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="52ece-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="52ece-213">1.7.5764.1</span></span>

*  <span data-ttu-id="52ece-214">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-214">Performance improvements</span></span>
*  <span data-ttu-id="52ece-215">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="52ece-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="52ece-216">1.6.5735.1</span></span>

*  <span data-ttu-id="52ece-217">Supporto di origine/sink HDFS in locale</span><span class="sxs-lookup"><span data-stu-id="52ece-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="52ece-218">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-218">Performance improvements</span></span>
*  <span data-ttu-id="52ece-219">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="52ece-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="52ece-220">1.6.5696.1</span></span>

*  <span data-ttu-id="52ece-221">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-221">Performance improvements</span></span>
*  <span data-ttu-id="52ece-222">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="52ece-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="52ece-223">1.6.5676.1</span></span>

*  <span data-ttu-id="52ece-224">Supporto degli strumenti di diagnostica in Gestione configurazione</span><span class="sxs-lookup"><span data-stu-id="52ece-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="52ece-225">Supporto delle colonne di tabella per le origini dati tabulari per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-226">Supporto di SQL DW per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-227">Supporto dell'isolamento in BlobSource e FileSource per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-228">Supporto di CopyBehavior – MergeFiles, PreserveHierarchy e FlattenHierarchy in BlobSink e FileSink con copia binaria per Data Factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-229">Supporto dello stato di avanzamento della creazione di report per l'attività di copia per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-230">Supporto della convalida della connettività dell'origine dati per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-231">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="52ece-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="52ece-232">1.6.5672.1</span></span>

*  <span data-ttu-id="52ece-233">Supporto del nome di tabella per l'origine dati ODBC per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-234">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-234">Performance improvements</span></span>
*  <span data-ttu-id="52ece-235">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="52ece-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="52ece-236">1.6.5658.1</span></span>

*  <span data-ttu-id="52ece-237">Supporto del sink dei file per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-238">Supporto del mantenimento della gerarchia nella copia binaria per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-239">Supporto dell'idempotenza dell'attività di copia per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-240">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="52ece-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="52ece-241">1.6.5640.1</span></span>

*  <span data-ttu-id="52ece-242">Supporto di altre 3 origini dati per Data factory di Azure (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="52ece-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="52ece-243">Supporto delle virgolette nel parser CSV per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-244">Supporto della compressione (BZip2)</span><span class="sxs-lookup"><span data-stu-id="52ece-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="52ece-245">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="52ece-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="52ece-246">1.5.5612.1</span></span>

*  <span data-ttu-id="52ece-247">Supporto di cinque database relazionali per Data Factory di Azure (MySQL, PostgreSQL, DB2, Teradata e Sybase)</span><span class="sxs-lookup"><span data-stu-id="52ece-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="52ece-248">Supporto della compressione (Gzip e Deflate)</span><span class="sxs-lookup"><span data-stu-id="52ece-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="52ece-249">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-249">Performance improvements</span></span>
*  <span data-ttu-id="52ece-250">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="52ece-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="52ece-251">1.4.5549.1</span></span>

*  <span data-ttu-id="52ece-252">Aggiunta del supporto dell'origine dati Oracle per Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="52ece-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="52ece-253">Miglioramenti delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="52ece-253">Performance improvements</span></span>
*  <span data-ttu-id="52ece-254">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="52ece-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="52ece-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="52ece-255">1.4.5492.1</span></span>

*  <span data-ttu-id="52ece-256">File binario unificato che supporta il servizio Data factory di Microsoft Azure e il servizio Power BI di Office 365</span><span class="sxs-lookup"><span data-stu-id="52ece-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="52ece-257">Perfezionamento dell'interfaccia utente di configurazione e del processo di registrazione</span><span class="sxs-lookup"><span data-stu-id="52ece-257">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="52ece-258">Data Factory di Azure: supporto di ingresso e uscita in Azure per l'origine dati SQL Server</span><span class="sxs-lookup"><span data-stu-id="52ece-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="52ece-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="52ece-259">1.2.5303.1</span></span>

*  <span data-ttu-id="52ece-260">Risoluzione del problema di timeout per supportare connessioni alle origini dati più dispersive in termini di tempo.</span><span class="sxs-lookup"><span data-stu-id="52ece-260">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="52ece-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="52ece-261">1.1.5526.8</span></span>

*  <span data-ttu-id="52ece-262">Richiede .NET Framework 4.5.1 come prerequisito durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="52ece-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="52ece-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="52ece-263">1.0.5144.2</span></span>

*  <span data-ttu-id="52ece-264">Nessuna modifica che interessi gli scenari di Data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="52ece-264">No changes that affect Azure Data Factory scenarios.</span></span>
