---
title: Eseguire lo sviluppo in locale con l'emulatore di Azure Cosmos DB | Microsoft Docs
description: "Usare l'emulatore di Azure Cosmos DB, è possibile sviluppare e testare gratuitamente l'applicazione in locale, senza creare una sottoscrizione di Azure."
services: cosmos-db
documentationcenter: 
keywords: Emulatore di Azure Cosmos DB
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="56c48-104">Usare l'emulatore di Azure Cosmos DB per sviluppo e test locali</span><span class="sxs-lookup"><span data-stu-id="56c48-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="56c48-105"><strong>File binari</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="56c48-106">Scarica MSI</span><span class="sxs-lookup"><span data-stu-id="56c48-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="56c48-108">Hub docker</span><span class="sxs-lookup"><span data-stu-id="56c48-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-109"><strong>Origine docker</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="56c48-110">Github</span><span class="sxs-lookup"><span data-stu-id="56c48-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="56c48-111">L'emulatore di Azure Cosmos DB fornisce un ambiente locale che emula il servizio Azure Cosmos DB a fini di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="56c48-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="56c48-112">Usando l'emulatore di Azure Cosmos DB, è possibile sviluppare e testare l'applicazione in locale, senza creare una sottoscrizione di Azure né sostenere costi.</span><span class="sxs-lookup"><span data-stu-id="56c48-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="56c48-113">Quando si è soddisfatti del funzionamento dell'applicazione nell'emulatore di Azure Cosmos DB, è possibile iniziare a usare l'account Azure Cosmos DB nel cloud.</span><span class="sxs-lookup"><span data-stu-id="56c48-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="56c48-114">Questo articolo illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c48-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="56c48-115">Installazione dell'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-115">Installing the Emulator</span></span>
> * <span data-ttu-id="56c48-116">Esecuzione dell'emulatore in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="56c48-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="56c48-117">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="56c48-117">Authenticating requests</span></span>
> * <span data-ttu-id="56c48-118">Uso di Esplora dati nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="56c48-119">Esportazione di certificati SSL</span><span class="sxs-lookup"><span data-stu-id="56c48-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="56c48-120">Chiamata dell'emulatore dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="56c48-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="56c48-121">Raccolta dei file di traccia</span><span class="sxs-lookup"><span data-stu-id="56c48-121">Collecting trace files</span></span>

<span data-ttu-id="56c48-122">È consigliabile guardare prima di tutto il video seguente, in cui Kirill Gavrylyuk illustra come iniziare a usare l'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="56c48-123">Si noti che il video fa riferimento all'emulatore come emulatore di DocumentDB, ma lo strumento stesso è stato rinominato Emulatore Azure Cosmos DB dopo la registrazione del video.</span><span class="sxs-lookup"><span data-stu-id="56c48-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="56c48-124">Tutte le informazioni del video sono ancora corrette per l'emulatore Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="56c48-125">Come funziona l'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-125">How the Emulator works</span></span>
<span data-ttu-id="56c48-126">L'emulatore Azure Cosmos DB offre un'emulazione ultra fedele del servizio Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="56c48-127">Supporta le stesse funzionalità di Azure Cosmos DB, incluso il supporto per la creazione e l'esecuzione di query su documenti JSON, il provisioning e la scalabilità delle raccolte e l'esecuzione di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="56c48-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="56c48-128">È possibile sviluppare e testare le applicazioni usando l'emulatore di Azure Cosmos DB e distribuirle in Azure su scala globale semplicemente apportando una singola modifica di configurazione all'endpoint di connessione per Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="56c48-129">Anche se è stata creata un'emulazione locale estremamente fedele del servizio Azure Cosmos DB effettivo, l'implementazione dell'emulatore di Azure Cosmos DB è diversa da quella del servizio.</span><span class="sxs-lookup"><span data-stu-id="56c48-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="56c48-130">L'emulatore di Azure Cosmos DB, ad esempio, usa i componenti del sistema operativo standard, ad esempio il file system locale per la persistenza e lo stack di protocolli HTTPS per la connettività.</span><span class="sxs-lookup"><span data-stu-id="56c48-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="56c48-131">Di conseguenza alcune funzionalità basate sull'infrastruttura di Azure, ad esempio la replica globale, la latenza in millisecondi a cifra singola per le operazioni di lettura/scrittura e i livelli di coerenza regolabili, non sono disponibili nell'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="56c48-132">Esplora dati nell'emulatore supporta attualmente solo la creazione di raccolte di API DocumentDB e raccolte di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="56c48-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="56c48-133">Esplora dati nell'emulatore non supporta attualmente la creazione di tabelle e grafici.</span><span class="sxs-lookup"><span data-stu-id="56c48-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="56c48-134">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="56c48-134">System requirements</span></span>
<span data-ttu-id="56c48-135">L'emulatore di Azure Cosmos DB presenta i requisiti hardware e software seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c48-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="56c48-136">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="56c48-136">Software requirements</span></span>
  * <span data-ttu-id="56c48-137">Windows Server 2012 R2, Windows Server 2016 o Windows Server 10</span><span class="sxs-lookup"><span data-stu-id="56c48-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="56c48-138">Requisiti hardware minimi</span><span class="sxs-lookup"><span data-stu-id="56c48-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="56c48-139">2 GB di RAM</span><span class="sxs-lookup"><span data-stu-id="56c48-139">2 GB RAM</span></span>
  * <span data-ttu-id="56c48-140">10 GB di spazio su disco disponibile</span><span class="sxs-lookup"><span data-stu-id="56c48-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="56c48-141">Installare</span><span class="sxs-lookup"><span data-stu-id="56c48-141">Installation</span></span>
<span data-ttu-id="56c48-142">È possibile scaricare e installare l'emulatore di Azure Cosmos DB dall'[Area download Microsoft](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="56c48-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="56c48-143">Per installare, configurare ed eseguire l'emulatore di Azure Cosmos DB, è necessario avere i privilegi di amministratore nel computer.</span><span class="sxs-lookup"><span data-stu-id="56c48-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="56c48-144">Esecuzione in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="56c48-144">Running on Docker for Windows</span></span>

<span data-ttu-id="56c48-145">L'emulatore di Azure Cosmos DB può essere eseguito in Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="56c48-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="56c48-146">L'emulatore non funziona su Docker per Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="56c48-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="56c48-147">Dopo aver installato [Docker per Windows](https://www.docker.com/docker-windows) è possibile caricare l'immagine dell'emulatore da Docker Hub eseguendo il comando seguente dalla shell preferita: cmd.exe, PowerShell e così via.</span><span class="sxs-lookup"><span data-stu-id="56c48-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="56c48-148">Per avviare l'immagine, eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="56c48-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="56c48-149">La risposta sarà simile a quanto riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="56c48-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="56c48-150">Se si chiude la shell interattiva una volta avviato l'emulatore, il contenitore dell'emulatore verrà arrestato.</span><span class="sxs-lookup"><span data-stu-id="56c48-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="56c48-151">Usare l'endpoint e la chiave master dalla risposta nel client e importare il certificato SSL nell'host.</span><span class="sxs-lookup"><span data-stu-id="56c48-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="56c48-152">Per importare il certificato SSL, eseguire le operazioni seguenti da un prompt dei comandi di amministratore:</span><span class="sxs-lookup"><span data-stu-id="56c48-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="56c48-153">Avviare l'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-153">Start the Emulator</span></span>

<span data-ttu-id="56c48-154">Per avviare l'emulatore di Azure Cosmos DB, selezionare il pulsante Start o premere WINDOWS sulla tastiera.</span><span class="sxs-lookup"><span data-stu-id="56c48-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="56c48-155">Iniziare a digitare **emulatore di Azure Cosmos DB**e selezionare l'emulatore nell'elenco di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="56c48-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Selezionare il pulsante Start o premere il tasto WINDOWS, iniziare a digitare **emulatore di Azure Cosmos DB** e selezionare l'emulatore nell'elenco di applicazioni](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="56c48-157">Quando l'emulatore è in esecuzione, verrà visualizzata un'icona nell'area di notifica della barra delle applicazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="56c48-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Notifica della barra delle applicazioni dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="56c48-159">Per impostazione predefinita, l'emulatore di Azure Cosmos DB viene eseguito nel computer locale ("localhost") in ascolto sulla porta 8081.</span><span class="sxs-lookup"><span data-stu-id="56c48-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="56c48-160">Per impostazione predefinita, l'emulatore di Azure Cosmos DB viene installato nella directory `C:\Program Files\Azure Cosmos DB Emulator`.</span><span class="sxs-lookup"><span data-stu-id="56c48-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="56c48-161">È anche possibile avviare e arrestare l'emulatore dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="56c48-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="56c48-162">Per altre informazioni, vedere le [informazioni di riferimento sullo strumento da riga di comando](#command-line).</span><span class="sxs-lookup"><span data-stu-id="56c48-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="56c48-163">Avviare Esplora dati</span><span class="sxs-lookup"><span data-stu-id="56c48-163">Start Data Explorer</span></span>

<span data-ttu-id="56c48-164">Quando l'emulatore di Azure Cosmos DB viene avviato, apre automaticamente Esplora dati di Azure Cosmos DB nel browser.</span><span class="sxs-lookup"><span data-stu-id="56c48-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="56c48-165">L'indirizzo visualizzato sarà [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="56c48-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="56c48-166">Se si chiude lo strumento di esplorazione e lo si vuole riaprire in seguito, è possibile aprire l'URL nel browser o avviarlo dall'emulatore di Azure Cosmos DB usando l'icona dell'area di notifica di Windows, come illustrato sotto.</span><span class="sxs-lookup"><span data-stu-id="56c48-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Utilità di avvio di Esplora dati dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="56c48-168">Preparazione per gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="56c48-168">Checking for updates</span></span>
<span data-ttu-id="56c48-169">Esplora dati indica se è disponibile un nuovo aggiornamento per il download.</span><span class="sxs-lookup"><span data-stu-id="56c48-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="56c48-170">I dati creati in una versione dell'emulatore di Azure Cosmos DB non sono necessariamente accessibili quando si usa una versione diversa.</span><span class="sxs-lookup"><span data-stu-id="56c48-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="56c48-171">Se è necessario rendere persistenti i dati a lungo termine, si consiglia di archiviare i dati in un account di Azure Cosmos DB invece che nell'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="56c48-172">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="56c48-172">Authenticating requests</span></span>
<span data-ttu-id="56c48-173">Come per Azure Cosmos DB nel cloud, tutte le richieste effettuate nell'emulatore di Azure Cosmos DB devono essere autenticate.</span><span class="sxs-lookup"><span data-stu-id="56c48-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="56c48-174">L'emulatore di Azure Cosmos DB supporta un singolo account fisso e una chiave di autenticazione nota per l'autenticazione della chiave master.</span><span class="sxs-lookup"><span data-stu-id="56c48-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="56c48-175">Questo account e questa chiave sono le uniche credenziali consentite per l'uso con l'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="56c48-176">Sono:</span><span class="sxs-lookup"><span data-stu-id="56c48-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="56c48-177">La chiave master supportata dall'emulatore di Azure Cosmos DB deve essere usata solo con l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="56c48-178">È possibile utilizzare l'account Azure Cosmos DB di produzione e la chiave con l'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="56c48-179">Se l'emulatore è stato avviato con l'opzione /Key, usare la chiave generata anziché "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="56c48-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="56c48-180">Proprio come il servizio Azure Cosmos DB, anche l'emulatore di Azure Cosmos DB supporta solo la comunicazione sicura tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="56c48-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="56c48-181">Esecuzione dell'emulatore in una rete locale</span><span class="sxs-lookup"><span data-stu-id="56c48-181">Running the emulator on a local network</span></span>

<span data-ttu-id="56c48-182">È possibile eseguire l'emulatore in una rete locale.</span><span class="sxs-lookup"><span data-stu-id="56c48-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="56c48-183">Per abilitare l'accesso alla rete, specificare l'opzione /AllowNetworkAccess nella [riga di comando](#command-line-syntax), che richiede di specificare anche /Key=stringa_chiave o /KeyFile=nome_file.</span><span class="sxs-lookup"><span data-stu-id="56c48-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="56c48-184">È possibile usare /GenKeyFile=nome_file per generare un file con una chiave casuale sin dall'inizio,</span><span class="sxs-lookup"><span data-stu-id="56c48-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="56c48-185">per poi passarlo a /KeyFile=nome_file o /Key=contenuto_del_file.</span><span class="sxs-lookup"><span data-stu-id="56c48-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="56c48-186">Per abilitare l'accesso alla rete per la prima volta, l'utente deve arrestare l'emulatore ed eliminare la directory dei dati dell'emulatore (C:\Users\nome_utente\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="56c48-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="56c48-187">Sviluppo con l'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-187">Developing with the Emulator</span></span>
<span data-ttu-id="56c48-188">Quando l'emulatore di Azure Cosmos DB è in esecuzione sul desktop, è possibile usare qualsiasi [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) supportato o l'[API REST di Azure Cosmos DB](/rest/api/documentdb/) per interagire con l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="56c48-189">L'emulatore Azure Cosmos DB include anche l'utilità Esplora dati predefinita che consente di creare raccolte per API DocumentDB e MongoDB e di visualizzare e modificare documenti senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="56c48-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="56c48-190">Se si usa il [supporto del protocollo Azure Cosmos DB per MongoDB](mongodb-introduction.md), usare la stringa di connessione seguente:</span><span class="sxs-lookup"><span data-stu-id="56c48-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="56c48-191">È possibile usare gli strumenti esistenti, ad esempio [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio), per connettersi all'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="56c48-192">È anche possibile eseguire la migrazione dei dati tra l'emulatore di Azure Cosmos DB e il servizio Azure Cosmos DB usando lo [strumento per la migrazione dei dati di Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="56c48-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="56c48-193">Se l'emulatore è stato avviato con l'opzione /Key, usare la chiave generata anziché "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="56c48-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="56c48-194">Usando l'emulatore di Azure Cosmos DB, per impostazione predefinita è possibile creare fino a 25 raccolte con partizione singola o una raccolta partizionata.</span><span class="sxs-lookup"><span data-stu-id="56c48-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="56c48-195">Per altre informazioni sulla modifica di questo valore, vedere la sezione su come [impostare il valore PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="56c48-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="56c48-196">Esportare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="56c48-196">Export the SSL certificate</span></span>

<span data-ttu-id="56c48-197">I linguaggi e il runtime .NET usano l'archivio certificati Windows per connettersi in modo sicuro all'emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="56c48-198">Gli altri linguaggi hanno il proprio metodo di gestione e uso dei certificati.</span><span class="sxs-lookup"><span data-stu-id="56c48-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="56c48-199">Java usa il proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), mentre Python usa i [wrapper per i socket](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="56c48-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="56c48-200">Per ottenere un certificato da usare con i linguaggi e i runtime che non si integrano con l'archivio certificati Windows, sarà necessario esportarlo usando Gestione certificati di Windows.</span><span class="sxs-lookup"><span data-stu-id="56c48-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="56c48-201">Per avviarlo, eseguire certlm.msc o seguire le istruzioni dettagliate nel post [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md) (Esportare i certificati dell'emulatore di Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="56c48-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="56c48-202">Quando Gestione certificati è in esecuzione, aprire i certificati personali, come illustrato sotto, ed esportare il certificato con il nome descrittivo "DocumentDBEmulatorCertificate" come file Codificato Base 64 X.509 (.CER).</span><span class="sxs-lookup"><span data-stu-id="56c48-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificato SSL dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="56c48-204">Per importare il certificato X.509 nell'archivio certificati Java, seguire le istruzioni disponibili in [Aggiunta di un certificato all'archivio certificati CA Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="56c48-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="56c48-205">Dopo l'importazione del certificato nell'archivio certificati, le applicazioni Java e MongoDB, potranno connettersi all'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="56c48-206">Quando ci si connette all'emulatore da Python e Node.js SDK, la verifica SSL è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="56c48-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="56c48-207"><a id="command-line"></a>Riferimenti allo strumento da riga di comando</span><span class="sxs-lookup"><span data-stu-id="56c48-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="56c48-208">Dal percorso di installazione è possibile usare la riga di comando per avviare e arrestare l'emulatore, configurare le opzioni ed eseguire altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="56c48-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="56c48-209">Sintassi della riga di comando</span><span class="sxs-lookup"><span data-stu-id="56c48-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="56c48-210">Per visualizzare l'elenco di opzioni, digitare `CosmosDB.Emulator.exe /?` al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="56c48-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="56c48-211"><strong>Opzione</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="56c48-212"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="56c48-213"><strong>Comando</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="56c48-214"><strong>Argomenti</strong></span><span class="sxs-lookup"><span data-stu-id="56c48-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-215">[Nessun argomento]</span><span class="sxs-lookup"><span data-stu-id="56c48-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="56c48-216">Avvia l'emulatore di Azure Cosmos DB con le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="56c48-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="56c48-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="56c48-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="56c48-218">[Help]</span></span></td>
  <td><span data-ttu-id="56c48-219">Visualizza l'elenco di argomenti della riga di comando supportati.</span><span class="sxs-lookup"><span data-stu-id="56c48-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="56c48-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="56c48-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="56c48-221">Shutdown</span></span></td>
  <td><span data-ttu-id="56c48-222">Arresta l'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="56c48-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="56c48-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="56c48-224">DataPath</span></span></td>
  <td><span data-ttu-id="56c48-225">Specifica il percorso in cui archiviare i file di dati.</span><span class="sxs-lookup"><span data-stu-id="56c48-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="56c48-226">Il valore predefinito è %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="56c48-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="56c48-227">CosmosDB.Emulator.exe /DataPath=&lt;percorsodati&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="56c48-228">&lt;percorsodati&gt;: percorso accessibile</span><span class="sxs-lookup"><span data-stu-id="56c48-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-229">Porta</span><span class="sxs-lookup"><span data-stu-id="56c48-229">Port</span></span></td>
  <td><span data-ttu-id="56c48-230">Specifica il numero di porta da usare per l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="56c48-231">Il valore predefinito è 8081.</span><span class="sxs-lookup"><span data-stu-id="56c48-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="56c48-232">CosmosDB.Emulator.exe /Port=&lt;porta&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="56c48-233">&lt;porta&gt;: numero di porta singolo</span><span class="sxs-lookup"><span data-stu-id="56c48-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="56c48-234">MongoPort</span></span></td>
  <td><span data-ttu-id="56c48-235">Specifica il numero di porta da usare per l'API di compatibilità MongoDB.</span><span class="sxs-lookup"><span data-stu-id="56c48-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="56c48-236">Il valore predefinito è 10255.</span><span class="sxs-lookup"><span data-stu-id="56c48-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="56c48-237">CosmosDB.Emulator.exe /MongoPort=&lt;portaMongo&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="56c48-238">&lt;portaMongo&gt;: numero di porta singolo</span><span class="sxs-lookup"><span data-stu-id="56c48-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="56c48-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="56c48-240">Specifica le porte da usare per la connettività diretta.</span><span class="sxs-lookup"><span data-stu-id="56c48-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="56c48-241">I valori predefiniti sono 10251, 10252, 10253 e 10254.</span><span class="sxs-lookup"><span data-stu-id="56c48-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="56c48-242">CosmosDB.Emulator.exe /DirectPorts:&lt;portedirette&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="56c48-243">&lt;portedirette&gt;: elenco delimitato da virgole di 4 porte.</span><span class="sxs-lookup"><span data-stu-id="56c48-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-244">Chiave</span><span class="sxs-lookup"><span data-stu-id="56c48-244">Key</span></span></td>
  <td><span data-ttu-id="56c48-245">Chiave di autorizzazione per l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-245">Authorization key for the emulator.</span></span> <span data-ttu-id="56c48-246">La chiave deve essere la codifica Base 64 di un vettore a 64 byte.</span><span class="sxs-lookup"><span data-stu-id="56c48-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="56c48-247">CosmosDB.Emulator.exe /Key:&lt;chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="56c48-248">&lt;chiave&gt;: la chiave deve essere la codifica Base 64 di un vettore a 64 byte.</span><span class="sxs-lookup"><span data-stu-id="56c48-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="56c48-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="56c48-250">Specifica che il comportamento di limitazione della frequenza è abilitato.</span><span class="sxs-lookup"><span data-stu-id="56c48-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="56c48-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="56c48-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="56c48-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="56c48-253">Specifica che il comportamento di limitazione della frequenza è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="56c48-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="56c48-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="56c48-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="56c48-255">NoUI</span></span></td>
  <td><span data-ttu-id="56c48-256">Non mostra l'interfaccia utente dell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="56c48-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="56c48-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="56c48-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="56c48-259">Non mostra Esplora documenti all'avvio.</span><span class="sxs-lookup"><span data-stu-id="56c48-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="56c48-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="56c48-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="56c48-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="56c48-262">Specifica il numero massimo di raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="56c48-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="56c48-263">Per altre informazioni vedere [Modificare il numero di raccolte](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="56c48-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="56c48-264">CosmosDB.Emulator.exe /PartitionCount=&lt;conteggiopartizioni&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="56c48-265">&lt;partitioncount&gt;: numero massimo di raccolte con partizione singola consentite.</span><span class="sxs-lookup"><span data-stu-id="56c48-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="56c48-266">Il valore predefinito è 25.</span><span class="sxs-lookup"><span data-stu-id="56c48-266">Default is 25.</span></span> <span data-ttu-id="56c48-267">Il valore massimo consentito è 250.</span><span class="sxs-lookup"><span data-stu-id="56c48-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="56c48-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="56c48-269">Specifica il numero predefinito di partizioni per una raccolta partizionata.</span><span class="sxs-lookup"><span data-stu-id="56c48-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="56c48-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;numeropredefinitopartizioni&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="56c48-271">&lt;numeropredefinitopartizioni&gt; Il valore predefinito è 25.</span><span class="sxs-lookup"><span data-stu-id="56c48-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="56c48-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="56c48-273">Consente l'accesso all'emulatore tramite una rete.</span><span class="sxs-lookup"><span data-stu-id="56c48-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="56c48-274">È necessario passare anche /Key=&lt;stringa_chiave&gt; o /KeyFile=&lt;nome_file&gt; per abilitare l'accesso alla rete.</span><span class="sxs-lookup"><span data-stu-id="56c48-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="56c48-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;stringa_chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="56c48-276">oppure</span><span class="sxs-lookup"><span data-stu-id="56c48-276">or</span></span><br><br><span data-ttu-id="56c48-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;nome_file&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="56c48-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="56c48-279">Non modificare le regole del firewall quando si usa /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="56c48-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="56c48-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="56c48-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="56c48-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="56c48-282">Genera una nuova chiave di autorizzazione e la salva nel file specificato.</span><span class="sxs-lookup"><span data-stu-id="56c48-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="56c48-283">La chiave generata può essere usata con le opzioni /Key o /KeyFile.</span><span class="sxs-lookup"><span data-stu-id="56c48-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="56c48-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;percorso del file della chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-285">Consistency</span><span class="sxs-lookup"><span data-stu-id="56c48-285">Consistency</span></span></td>
  <td><span data-ttu-id="56c48-286">Imposta il livello di coerenza per l'account.</span><span class="sxs-lookup"><span data-stu-id="56c48-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="56c48-287">CosmosDB.Emulator.exe /Consistency=&lt;coerenza&gt;</span><span class="sxs-lookup"><span data-stu-id="56c48-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="56c48-288">&lt;coerenza&gt;: il valore deve essere uno dei seguenti [livelli di coerenza](consistency-levels.md): Session, Strong, Eventual o BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="56c48-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="56c48-289">Il valore predefinito è Session.</span><span class="sxs-lookup"><span data-stu-id="56c48-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="56c48-290">?</span><span class="sxs-lookup"><span data-stu-id="56c48-290">?</span></span></td>
  <td><span data-ttu-id="56c48-291">Mostra il messaggio della Guida.</span><span class="sxs-lookup"><span data-stu-id="56c48-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="56c48-292">Differenze tra l'emulatore di Azure Cosmos DB e Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56c48-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="56c48-293">Poiché l'emulatore di Azure Cosmos DB fornisce un ambiente emulato eseguito in una workstation di sviluppo locale, esistono alcune differenze a livello di funzionalità tra l'emulatore e un account Azure Cosmos DB nel cloud:</span><span class="sxs-lookup"><span data-stu-id="56c48-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="56c48-294">L'emulatore di Azure Cosmos DB supporta solo un singolo account fisso e una chiave master nota.</span><span class="sxs-lookup"><span data-stu-id="56c48-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="56c48-295">La rigenerazione della chiave non è possibile nell'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="56c48-296">L'emulatore di Azure Cosmos DB non è un servizio scalabile e non supporta un numero elevato di raccolte.</span><span class="sxs-lookup"><span data-stu-id="56c48-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="56c48-297">L'emulatore di Azure Cosmos DB non simula [livelli di coerenza di Azure Cosmos DB](consistency-levels.md) diversi.</span><span class="sxs-lookup"><span data-stu-id="56c48-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="56c48-298">L'emulatore di Azure Cosmos DB non simula la [replica tra più aree](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="56c48-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="56c48-299">L'emulatore di Azure Cosmos DB non supporta gli override della quota del servizio disponibili nel servizio Azure Cosmos DB, ad esempio i limiti di dimensioni dei documenti e lo spazio di archiviazione per le raccolte aumentato.</span><span class="sxs-lookup"><span data-stu-id="56c48-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="56c48-300">Poiché la copia dell'emulatore di Azure Cosmos DB potrebbe non essere aggiornata con le modifiche più recenti del servizio Azure Cosmos DB, vedere [Capacity Planner di Azure Cosmos DB](https://www.documentdb.com/capacityplanner) per stimare con precisione le esigenze di produttività (UR) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="56c48-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="56c48-301"><a id="set-partitioncount"></a>Modificare il numero di raccolte</span><span class="sxs-lookup"><span data-stu-id="56c48-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="56c48-302">Per impostazione predefinita, è possibile creare fino a 25 raccolte con partizione singola o una raccolta partizionata usando l'emulatore di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="56c48-303">Modificando il valore **PartitionCount**, è possibile creare fino a 250 raccolte a partizione singola o 10 raccolte partizionate o qualsiasi combinazione delle due che non contenga più di 250 raccolte a partizione singola (dove una raccolta partizionata = 25 raccolte a partizione singola).</span><span class="sxs-lookup"><span data-stu-id="56c48-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="56c48-304">Se si tenta di creare una raccolta dopo il superamento di questi limiti, l'emulatore genera un'eccezione ServiceUnavailable con il messaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="56c48-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="56c48-305">Per modificare il numero di raccolte disponibili nell'emulatore di Azure Cosmos DB, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="56c48-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="56c48-306">Eliminare tutti i dati locali dell'emulatore di Azure Cosmos DB facendo clic sull'icona dell'**emulatore di Azure Cosmos DB**  sull'area di notifica e quindi su **Reset data** (Reimposta dati).</span><span class="sxs-lookup"><span data-stu-id="56c48-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="56c48-307">Eliminare tutti i dati dell'emulatore dalla cartella C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="56c48-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="56c48-308">Chiudere tutte le istanze aperte facendo clic con il pulsante destro del mouse sull'icona dell'**emulatore di Azure Cosmos DB** sull'area di notifica, quindi fare clic su **Esci**.</span><span class="sxs-lookup"><span data-stu-id="56c48-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="56c48-309">La chiusura di tutte le istanze può richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="56c48-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="56c48-310">Installare la versione più recente dell'[emulatore di Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="56c48-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="56c48-311">Avviare l'emulatore con il flag PartitionCount impostando un valore <= 250.</span><span class="sxs-lookup"><span data-stu-id="56c48-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="56c48-312">Ad esempio: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="56c48-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="56c48-313">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="56c48-313">Troubleshooting</span></span>

<span data-ttu-id="56c48-314">Usa i suggerimenti seguenti per aiutare a risolvere i problemi dell'emulatore di Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="56c48-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="56c48-315">Se è stata installata una nuova versione dell'emulatore e si verificano errori, provare a ripristinare i dati.</span><span class="sxs-lookup"><span data-stu-id="56c48-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="56c48-316">Per ripristinare i dati, fare clic con il pulsante destro del mouse sull'icona dell'emulatore di Azure Cosmos DB nell'area di notifica e quindi fare clic su Reset Data (Ripristina dati).</span><span class="sxs-lookup"><span data-stu-id="56c48-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="56c48-317">Se gli errori persistono, è possibile provare a disinstallare e reinstallare l'app.</span><span class="sxs-lookup"><span data-stu-id="56c48-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="56c48-318">Per istruzioni, vedere [Disinstallare l'emulatore locale](#uninstall).</span><span class="sxs-lookup"><span data-stu-id="56c48-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="56c48-319">In caso di arresto anomalo dell'emulatore di Azure Cosmos DB, raccogliere file di dump dalla cartella c:\Users\nome_utente\AppData\Local\CrashDumps, comprimerli e allegarli a un messaggio di posta elettronica da inviare all'indirizzo [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="56c48-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="56c48-320">In caso di arresti anomali del sistema in CosmosDB.StartupEntryPoint.exe, eseguire il comando seguente da un prompt dei comandi di amministratore: `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="56c48-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="56c48-321">In caso di problemi di connettività, [raccogliere i file di traccia](#trace-files), comprimerli e allegarli a un messaggio di posta elettronica da inviare all'indirizzo [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="56c48-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="56c48-322">Se si riceve un messaggio di tipo **Servizio non disponibile**, è possibile che l'emulatore non riesca a inizializzare lo stack di rete.</span><span class="sxs-lookup"><span data-stu-id="56c48-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="56c48-323">Controllare per verificare se è stato installato il client sicuro Pulse o il client di rete Juniper, perché è possibile che i rispettivi driver del filtro di rete provochino il problema.</span><span class="sxs-lookup"><span data-stu-id="56c48-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="56c48-324">La disinstallazione dei driver filtro di rete di terze parti consente in genere di risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="56c48-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="56c48-325"><a id="trace-files"></a>Raccogliere i file di traccia</span><span class="sxs-lookup"><span data-stu-id="56c48-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="56c48-326">Per raccogliere le tracce di debug, eseguire i comandi seguenti da un prompt dei comandi amministrativi:</span><span class="sxs-lookup"><span data-stu-id="56c48-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="56c48-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="56c48-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="56c48-328">Verificare l'area di notifica per assicurarsi che il programma sia stato arrestato. Potrebbe essere necessario qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="56c48-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="56c48-329">È anche possibile fare semplicemente clic su **Esci** nell'interfaccia utente dell'emulatore Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="56c48-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="56c48-330">Riprodurre il problema.</span><span class="sxs-lookup"><span data-stu-id="56c48-330">Reproduce the problem.</span></span> <span data-ttu-id="56c48-331">Se Esplora dati non funziona, è sufficiente attendere qualche secondo per l'apertura del browser e il rilevamento dell'errore.</span><span class="sxs-lookup"><span data-stu-id="56c48-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="56c48-332">Passare a `%ProgramFiles%\Azure Cosmos DB Emulator` e individuare il file docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="56c48-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="56c48-333">Inviare il file con estensione etl insieme alla procedura per la riproduzione all'indirizzo [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) per il debug.</span><span class="sxs-lookup"><span data-stu-id="56c48-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="56c48-334"><a id="uninstall"></a>Disinstallare l'emulatore locale</span><span class="sxs-lookup"><span data-stu-id="56c48-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="56c48-335">Chiudere tutte le istanze aperte dell'emulatore locale facendo clic con il pulsante destro del mouse sull'icona dell'emulatore di Azure Cosmos DB nell'area di notifica e quindi fare clic su Esci.</span><span class="sxs-lookup"><span data-stu-id="56c48-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="56c48-336">La chiusura di tutte le istanze può richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="56c48-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="56c48-337">Nella casella di ricerca di Windows digitare **Apps & features** (App e funzionalità) e fare clic sul risultato **Apps & features (System settings)** (App e funzionalità - Impostazioni di sistema).</span><span class="sxs-lookup"><span data-stu-id="56c48-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="56c48-338">Nell'elenco di app scorrere fino a **Azure Cosmos DB Emulator** (Emulatore di Azure Cosmos DB), selezionarla, fare clic su **Disinstalla**, confermare e quindi fare clic nuovamente su **Disinstalla**.</span><span class="sxs-lookup"><span data-stu-id="56c48-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="56c48-339">Quando l'app è disinstallata, passare a C:\Users\<user>\AppData\Local\CosmosDBEmulator ed eliminare la cartella.</span><span class="sxs-lookup"><span data-stu-id="56c48-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="56c48-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56c48-340">Next steps</span></span>

<span data-ttu-id="56c48-341">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56c48-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="56c48-342">Installazione dell'emulatore locale</span><span class="sxs-lookup"><span data-stu-id="56c48-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="56c48-343">Esecuzione dell'emulatore in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="56c48-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="56c48-344">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="56c48-344">Authenticated requests</span></span>
> * <span data-ttu-id="56c48-345">Uso di Esplora dati nell'emulatore</span><span class="sxs-lookup"><span data-stu-id="56c48-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="56c48-346">Esportazione dei certificati SSL</span><span class="sxs-lookup"><span data-stu-id="56c48-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="56c48-347">Chiamata dell'emulatore dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="56c48-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="56c48-348">Raccolta dei file di traccia</span><span class="sxs-lookup"><span data-stu-id="56c48-348">Collected trace files</span></span>

<span data-ttu-id="56c48-349">In questa esercitazione, si è appresso come usare l'emulatore locale per sviluppo locale libero.</span><span class="sxs-lookup"><span data-stu-id="56c48-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="56c48-350">È ora possibile passare all'esercitazione successiva e apprendere come esportare i certificati SSL dell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="56c48-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="56c48-351">Esportare i certificati dell'emulatore Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="56c48-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
