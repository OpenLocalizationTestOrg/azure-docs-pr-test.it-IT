---
title: aaaDevelop localmente con hello Azure Cosmos DB emulatore | Documenti Microsoft
description: "Utilizza hello Azure Cosmos DB emulatore, è possibile sviluppare e testare l'applicazione in locale per gratuito, senza creare una sottoscrizione di Azure."
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
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="963fb-104">Utilizzare hello Azure Cosmos DB emulatore per sviluppo locale e il test</span><span class="sxs-lookup"><span data-stu-id="963fb-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="963fb-105"><strong>File binari</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="963fb-106">Scarica MSI</span><span class="sxs-lookup"><span data-stu-id="963fb-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="963fb-108">Hub docker</span><span class="sxs-lookup"><span data-stu-id="963fb-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-109"><strong>Origine docker</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="963fb-110">Github</span><span class="sxs-lookup"><span data-stu-id="963fb-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="963fb-111">Hello Azure Cosmos DB emulatore offre un ambiente locale che emula hello Azure Cosmos DB servizio a scopo di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="963fb-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="963fb-112">Utilizza hello Azure Cosmos DB emulatore, è possibile sviluppare e testare l'applicazione localmente, senza creare una sottoscrizione di Azure o eventuali costi.</span><span class="sxs-lookup"><span data-stu-id="963fb-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="963fb-113">Quando si è soddisfatti delle modalità di funzionamento dell'applicazione nell'emulatore di Azure Cosmos DB hello, è possibile passare un account Azure Cosmos DB nel cloud hello toousing.</span><span class="sxs-lookup"><span data-stu-id="963fb-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="963fb-114">Questo articolo descrive hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="963fb-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="963fb-115">L'installazione dell'emulatore hello</span><span class="sxs-lookup"><span data-stu-id="963fb-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="963fb-116">Esecuzione hello emulatore in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="963fb-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="963fb-117">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="963fb-117">Authenticating requests</span></span>
> * <span data-ttu-id="963fb-118">Utilizzando Esplora dati Ciao hello emulatore</span><span class="sxs-lookup"><span data-stu-id="963fb-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="963fb-119">Esportazione di certificati SSL</span><span class="sxs-lookup"><span data-stu-id="963fb-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="963fb-120">La chiamata di hello emulatore dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="963fb-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="963fb-121">Raccolta dei file di traccia</span><span class="sxs-lookup"><span data-stu-id="963fb-121">Collecting trace files</span></span>

<span data-ttu-id="963fb-122">Si consiglia di iniziare, è possibile guardare hello seguente video, in cui Kirill Gavrylyuk viene illustrata la modalità di avvio tooget con hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="963fb-123">Si noti che video hello fa riferimento toohello emulatore come hello DocumentDB emulatore, ma è stato rinominato hello dello strumento hello Azure Cosmos DB emulatore dal toccare video hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="963fb-124">Tutte le informazioni hello video siano ancora corrette per hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="963fb-125">Funzionamento di hello emulatore</span><span class="sxs-lookup"><span data-stu-id="963fb-125">How hello Emulator works</span></span>
<span data-ttu-id="963fb-126">Hello Azure Cosmos DB emulatore fornisce un'emulazione ad alta fedeltà del servizio Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="963fb-127">Supporta le stesse funzionalità di Azure Cosmos DB, incluso il supporto per la creazione e l'esecuzione di query su documenti JSON, il provisioning e la scalabilità delle raccolte e l'esecuzione di stored procedure e trigger.</span><span class="sxs-lookup"><span data-stu-id="963fb-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="963fb-128">È possibile sviluppare e testare applicazioni utilizzando l'emulatore di Azure Cosmos DB hello e distribuirli tooAzure su scala globale apportando solo una singola configurazione modificare toohello endpoint della connessione per il database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="963fb-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="963fb-129">Quando abbiamo creato un'emulazione locale ad alta fedeltà del servizio Azure Cosmos DB effettivo hello, l'implementazione di hello di hello Azure Cosmos DB emulatore è diverso da quello del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="963fb-130">Ad esempio, hello Azure Cosmos DB emulatore utilizza i componenti del sistema operativo standard, ad esempio hello file system locale per la persistenza e stack del protocollo HTTPS per la connettività.</span><span class="sxs-lookup"><span data-stu-id="963fb-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="963fb-131">Ciò significa che alcune funzionalità che si basa sull'infrastruttura di Azure come globale, la latenza di millisecondo cifra di letture/scritture, i livelli di coerenza e non sono disponibili tramite hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="963fb-132">In questo Ciao ora Esplora dati hello emulatore supporta solo la creazione di hello di API DocumentDB raccolte e raccolte di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="963fb-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="963fb-133">Hello Esplora dati nell'emulatore hello non supporta attualmente la creazione di hello di tabelle e grafici.</span><span class="sxs-lookup"><span data-stu-id="963fb-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="963fb-134">Requisiti di sistema</span><span class="sxs-lookup"><span data-stu-id="963fb-134">System requirements</span></span>
<span data-ttu-id="963fb-135">Hello Azure Cosmos DB emulatore ha hello requisiti hardware e software seguenti:</span><span class="sxs-lookup"><span data-stu-id="963fb-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="963fb-136">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="963fb-136">Software requirements</span></span>
  * <span data-ttu-id="963fb-137">Windows Server 2012 R2, Windows Server 2016 o Windows Server 10</span><span class="sxs-lookup"><span data-stu-id="963fb-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="963fb-138">Requisiti hardware minimi</span><span class="sxs-lookup"><span data-stu-id="963fb-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="963fb-139">2 GB di RAM</span><span class="sxs-lookup"><span data-stu-id="963fb-139">2 GB RAM</span></span>
  * <span data-ttu-id="963fb-140">10 GB di spazio su disco disponibile</span><span class="sxs-lookup"><span data-stu-id="963fb-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="963fb-141">Installazione</span><span class="sxs-lookup"><span data-stu-id="963fb-141">Installation</span></span>
<span data-ttu-id="963fb-142">È possibile scaricare e installare l'emulatore di Azure Cosmos DB hello da hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="963fb-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="963fb-143">tooinstall, configurare ed eseguire hello Azure Cosmos DB emulatore, è necessario disporre dei privilegi amministrativi nel computer di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="963fb-144">Esecuzione in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="963fb-144">Running on Docker for Windows</span></span>

<span data-ttu-id="963fb-145">Hello Azure Cosmos DB emulatore può essere eseguito in Docker per Windows.</span><span class="sxs-lookup"><span data-stu-id="963fb-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="963fb-146">Hello emulatore non funzionano in Docker per Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="963fb-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="963fb-147">Dopo aver [Docker per Windows](https://www.docker.com/docker-windows) installato, è possibile effettuare il pull immagine dell'emulatore hello dall'Hub Docker eseguendo hello comando seguente dalla shell preferite (cmd.exe, PowerShell, ecc.).</span><span class="sxs-lookup"><span data-stu-id="963fb-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="963fb-148">immagine di hello toostart, eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="963fb-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="963fb-149">risposta Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="963fb-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="963fb-150">Chiudere la shell interattiva hello quando hello è stato avviato l'emulatore verrà contenitore dell'emulatore di arresto hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="963fb-151">Utilizzare endpoint hello e la chiave master dalla risposta hello nel client e importare il certificato SSL hello nell'host.</span><span class="sxs-lookup"><span data-stu-id="963fb-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="963fb-152">hello hello tooimport certificato SSL, seguito da un prompt dei comandi di amministratore:</span><span class="sxs-lookup"><span data-stu-id="963fb-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="963fb-153">Avviare l'emulatore hello</span><span class="sxs-lookup"><span data-stu-id="963fb-153">Start hello Emulator</span></span>

<span data-ttu-id="963fb-154">toostart hello Azure Cosmos DB emulatore, selezionare il pulsante di avvio di hello o premere tasto Windows hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="963fb-155">Iniziare a digitare **Azure Cosmos DB emulatore**e l'emulatore hello selezionare dall'elenco di hello delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="963fb-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Selezionare hello o preme hello Windows chiave di avvio, iniziare a digitare * * Azure Cosmos DB emulatore * * ed emulatore hello selezionare dall'elenco di hello delle applicazioni](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="963fb-157">Quando l'emulatore di hello è in esecuzione, si noterà un'icona nell'area di notifica della barra delle applicazioni di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Notifica della barra delle applicazioni dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="963fb-159">Hello Azure Cosmos DB emulatore per impostazione predefinita viene eseguito nel computer locale a hello ("localhost") in ascolto sulla porta 8081.</span><span class="sxs-lookup"><span data-stu-id="963fb-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="963fb-160">Hello Cosmos DB emulatore Azure è installato per impostazione predefinita toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="963fb-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="963fb-161">È possibile anche avviare e arrestare l'emulatore hello dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="963fb-162">Per altre informazioni, vedere le [informazioni di riferimento sullo strumento da riga di comando](#command-line).</span><span class="sxs-lookup"><span data-stu-id="963fb-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="963fb-163">Avviare Esplora dati</span><span class="sxs-lookup"><span data-stu-id="963fb-163">Start Data Explorer</span></span>

<span data-ttu-id="963fb-164">Avvio dell'emulatore di Azure Cosmos DB hello hello Azure Cosmos DB Data Explorer verrà automaticamente aperta nel browser.</span><span class="sxs-lookup"><span data-stu-id="963fb-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="963fb-165">indirizzo Hello verrà visualizzato come [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="963fb-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="963fb-166">Se si chiudere hello explorer e si desidera toore aperta è in un secondo momento, è possibile aprire hello URL nel browser o avviarlo da hello Azure Cosmos DB emulatore nell'icona di Windows hello, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="963fb-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Utilità di avvio di Esplora dati dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="963fb-168">Preparazione per gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="963fb-168">Checking for updates</span></span>
<span data-ttu-id="963fb-169">Esplora dati indica se è disponibile un nuovo aggiornamento per il download.</span><span class="sxs-lookup"><span data-stu-id="963fb-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="963fb-170">Dati creati in una versione di hello Azure Cosmos DB emulatore non sono garantiti toobe accessibili quando si utilizza una versione diversa.</span><span class="sxs-lookup"><span data-stu-id="963fb-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="963fb-171">Se è necessario toopersist i dati a lungo termine hello, è consigliabile archiviare i dati in un account Azure Cosmos DB anziché nell'emulatore di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="963fb-172">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="963fb-172">Authenticating requests</span></span>
<span data-ttu-id="963fb-173">Proprio come con DB Cosmos Azure nel cloud hello, tutte le richieste effettuate su hello Azure Cosmos DB emulatore devono essere autenticata.</span><span class="sxs-lookup"><span data-stu-id="963fb-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="963fb-174">Hello Azure Cosmos DB emulatore supporta un singolo account fisso e una chiave di autenticazione noto per l'autenticazione chiave master.</span><span class="sxs-lookup"><span data-stu-id="963fb-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="963fb-175">Questo account e questa chiave sono hello uniche credenziali consentite per l'utilizzo con hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="963fb-176">Sono:</span><span class="sxs-lookup"><span data-stu-id="963fb-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="963fb-177">chiave master di Hello supportati da hello Azure Cosmos DB emulatore deve essere utilizzato solo con l'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="963fb-178">È possibile utilizzare l'account di Azure Cosmos DB produzione e la chiave con hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="963fb-179">Se è stato avviato l'emulatore hello con opzione /Key hello, quindi utilizzare il tasto di hello generato invece di "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="963fb-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="963fb-180">Inoltre, esattamente come hello Azure Cosmos DB servizio hello Azure Cosmos DB emulatore supporta solo le comunicazioni protette tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="963fb-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="963fb-181">Emulatore hello in esecuzione in una rete locale</span><span class="sxs-lookup"><span data-stu-id="963fb-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="963fb-182">È possibile eseguire l'emulatore hello in una rete locale.</span><span class="sxs-lookup"><span data-stu-id="963fb-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="963fb-183">tooenable l'accesso alla rete, specificare l'opzione /AllowNetworkAccess hello hello [riga di comando](#command-line-syntax), che richiede di specificare /Key = key_string o /KeyFile = nome_file.</span><span class="sxs-lookup"><span data-stu-id="963fb-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="963fb-184">È possibile utilizzare /GenKeyFile = nome_file toogenerate un file con una chiave casuale sin dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="963fb-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="963fb-185">Non è possibile passare tale troppo/KeyFile = nome_file o /Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="963fb-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="963fb-186">accesso alla rete tooenable per hello hello utente devono arresta emulatore hello ed Elimina directory dei dati dell'emulatore hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="963fb-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="963fb-187">Lo sviluppo con hello emulatore</span><span class="sxs-lookup"><span data-stu-id="963fb-187">Developing with hello Emulator</span></span>
<span data-ttu-id="963fb-188">Una volta che si sono hello Azure Cosmos DB dell'emulatore in esecuzione sul desktop, è possibile utilizzare qualsiasi tipo supportato [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) o hello [API REST di Azure Cosmos DB](/rest/api/documentdb/) toointeract con hello emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="963fb-189">Hello Azure Cosmos DB emulatore include anche una finestra di esplorazione dati incorporato che consente di creare raccolte per DocumentDB hello e MongoDB APIs e visualizzare e modificare i documenti senza scrivere alcun codice.</span><span class="sxs-lookup"><span data-stu-id="963fb-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="963fb-190">Se si utilizza [Azure Cosmos DB supporto del protocollo per MongoDB](mongodb-introduction.md), utilizzare hello seguente stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="963fb-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="963fb-191">È possibile utilizzare strumenti esistenti come [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="963fb-192">È inoltre possibile migrare i dati tra hello Azure Cosmos DB emulatore e il servizio di Azure Cosmos DB hello utilizzando hello [utilità di migrazione di dati di Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="963fb-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="963fb-193">Se è stato avviato l'emulatore hello con opzione /Key hello, quindi utilizzare il tasto di hello generato invece di "C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="963fb-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="963fb-194">Utilizzando l'emulatore di Azure Cosmos DB hello, per impostazione predefinita, è possibile creare raccolte con partizione singola too25 o raccolta partizionata 1.</span><span class="sxs-lookup"><span data-stu-id="963fb-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="963fb-195">Per ulteriori informazioni sulla modifica di questo valore, vedere [impostazione hello PartitionCount valore](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="963fb-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="963fb-196">Esportare il certificato SSL di hello</span><span class="sxs-lookup"><span data-stu-id="963fb-196">Export hello SSL certificate</span></span>

<span data-ttu-id="963fb-197">Linguaggi .NET e runtime utilizzare hello archivio certificati Windows toosecurely connettersi toohello emulatore locale di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="963fb-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="963fb-198">Gli altri linguaggi hanno il proprio metodo di gestione e uso dei certificati.</span><span class="sxs-lookup"><span data-stu-id="963fb-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="963fb-199">Java usa il proprio [archivio certificati](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), mentre Python usa i [wrapper per i socket](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="963fb-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="963fb-200">In ordine tooobtain toouse un certificato con linguaggi e Runtime che non si integrano con l'archivio certificati Windows hello è necessario tooexport utilizzando Gestione certificati di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="963fb-201">È possibile avviarlo eseguendo certlm.msc o seguire le istruzioni dettagliate hello in [esportare i certificati dell'emulatore di hello Azure Cosmos DB](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="963fb-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="963fb-202">Quando il gestore di certificati hello è in esecuzione, aprire hello dei certificati personali come illustrato di seguito e l'esportazione hello certificato con il nome descrittivo di hello "DocumentDBEmulatorCertificate" come file x. 509 (. cer) con codifica BASE 64.</span><span class="sxs-lookup"><span data-stu-id="963fb-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificato SSL dell'emulatore locale di Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="963fb-204">certificato x. 509 Hello può essere importato nell'archivio di certificati di Java hello seguendo le istruzioni hello [aggiunta di un certificato toohello archivio certificati Autorità di certificazione Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="963fb-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="963fb-205">Una volta hello certificato viene importato nell'archivio certificati hello, le applicazioni Java e MongoDB saranno in grado di tooconnect toohello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="963fb-206">Durante la connessione dell'emulatore toohello da Python e Node.js SDK, verifica SSL è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="963fb-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="963fb-207"><a id="command-line"></a>Riferimenti allo strumento da riga di comando</span><span class="sxs-lookup"><span data-stu-id="963fb-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="963fb-208">Dal percorso di installazione di hello, si può utilizzare toostart della riga di comando hello e arresta emulatore hello, configurare le opzioni ed eseguire altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="963fb-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="963fb-209">Sintassi della riga di comando</span><span class="sxs-lookup"><span data-stu-id="963fb-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="963fb-210">elenco di hello tooview di opzioni, digitare `CosmosDB.Emulator.exe /?` al prompt dei comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="963fb-211"><strong>Opzione</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="963fb-212"><strong>Descrizione</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="963fb-213"><strong>Comando</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="963fb-214"><strong>Argomenti</strong></span><span class="sxs-lookup"><span data-stu-id="963fb-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-215">[Nessun argomento]</span><span class="sxs-lookup"><span data-stu-id="963fb-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="963fb-216">Avvio hello Azure Cosmos DB emulatore con le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="963fb-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="963fb-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="963fb-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="963fb-218">[Help]</span></span></td>
  <td><span data-ttu-id="963fb-219">Visualizza l'elenco di hello supportati gli argomenti della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="963fb-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="963fb-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="963fb-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="963fb-221">Shutdown</span></span></td>
  <td><span data-ttu-id="963fb-222">Arresta l'emulatore di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="963fb-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="963fb-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="963fb-224">DataPath</span></span></td>
  <td><span data-ttu-id="963fb-225">Specifica il percorso di hello nei file di dati quali toostore.</span><span class="sxs-lookup"><span data-stu-id="963fb-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="963fb-226">Il valore predefinito è %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="963fb-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="963fb-227">CosmosDB.Emulator.exe /DataPath=&lt;percorsodati&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="963fb-228">&lt;percorsodati&gt;: percorso accessibile</span><span class="sxs-lookup"><span data-stu-id="963fb-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-229">Porta</span><span class="sxs-lookup"><span data-stu-id="963fb-229">Port</span></span></td>
  <td><span data-ttu-id="963fb-230">Specifica toouse numero di porta hello per emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="963fb-231">Il valore predefinito è 8081.</span><span class="sxs-lookup"><span data-stu-id="963fb-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="963fb-232">CosmosDB.Emulator.exe /Port=&lt;porta&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="963fb-233">&lt;porta&gt;: numero di porta singolo</span><span class="sxs-lookup"><span data-stu-id="963fb-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="963fb-234">MongoPort</span></span></td>
  <td><span data-ttu-id="963fb-235">Specifica hello toouse numero di porta per la compatibilità di MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="963fb-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="963fb-236">Il valore predefinito è 10255.</span><span class="sxs-lookup"><span data-stu-id="963fb-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="963fb-237">CosmosDB.Emulator.exe /MongoPort=&lt;portaMongo&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="963fb-238">&lt;portaMongo&gt;: numero di porta singolo</span><span class="sxs-lookup"><span data-stu-id="963fb-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="963fb-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="963fb-240">Specifica hello toouse di porte per la connessione diretta.</span><span class="sxs-lookup"><span data-stu-id="963fb-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="963fb-241">I valori predefiniti sono 10251, 10252, 10253 e 10254.</span><span class="sxs-lookup"><span data-stu-id="963fb-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="963fb-242">CosmosDB.Emulator.exe /DirectPorts:&lt;portedirette&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="963fb-243">&lt;portedirette&gt;: elenco delimitato da virgole di 4 porte.</span><span class="sxs-lookup"><span data-stu-id="963fb-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-244">Chiave</span><span class="sxs-lookup"><span data-stu-id="963fb-244">Key</span></span></td>
  <td><span data-ttu-id="963fb-245">Chiave di autorizzazione per l'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="963fb-246">La chiave deve essere hello codifica base 64 di un vettore di 64 byte.</span><span class="sxs-lookup"><span data-stu-id="963fb-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="963fb-247">CosmosDB.Emulator.exe /Key:&lt;chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="963fb-248">&lt;chiave&gt;: chiave deve essere hello codifica base 64 di un vettore di 64 byte</span><span class="sxs-lookup"><span data-stu-id="963fb-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="963fb-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="963fb-250">Specifica che il comportamento di limitazione della frequenza è abilitato.</span><span class="sxs-lookup"><span data-stu-id="963fb-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="963fb-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="963fb-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="963fb-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="963fb-253">Specifica che il comportamento di limitazione della frequenza è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="963fb-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="963fb-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="963fb-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="963fb-255">NoUI</span></span></td>
  <td><span data-ttu-id="963fb-256">Non visualizzare emulatore hello interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="963fb-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="963fb-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="963fb-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="963fb-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="963fb-259">Non mostra Esplora documenti all'avvio.</span><span class="sxs-lookup"><span data-stu-id="963fb-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="963fb-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="963fb-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="963fb-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="963fb-262">Specifica hello il numero massimo di raccolte partizionate.</span><span class="sxs-lookup"><span data-stu-id="963fb-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="963fb-263">Vedere [modificare hello numero di raccolte](#set-partitioncount) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="963fb-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="963fb-264">CosmosDB.Emulator.exe /PartitionCount=&lt;conteggiopartizioni&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="963fb-265">&lt;partitioncount&gt;: numero massimo di raccolte con partizione singola consentite.</span><span class="sxs-lookup"><span data-stu-id="963fb-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="963fb-266">Il valore predefinito è 25.</span><span class="sxs-lookup"><span data-stu-id="963fb-266">Default is 25.</span></span> <span data-ttu-id="963fb-267">Il valore massimo consentito è 250.</span><span class="sxs-lookup"><span data-stu-id="963fb-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="963fb-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="963fb-269">Specifica il numero predefinito di hello di partizioni per una raccolta partizionata.</span><span class="sxs-lookup"><span data-stu-id="963fb-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="963fb-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;numeropredefinitopartizioni&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="963fb-271">&lt;numeropredefinitopartizioni&gt; Il valore predefinito è 25.</span><span class="sxs-lookup"><span data-stu-id="963fb-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="963fb-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="963fb-273">Abilita accesso emulatore toohello in rete.</span><span class="sxs-lookup"><span data-stu-id="963fb-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="963fb-274">È necessario passare anche /Key =&lt;key_string&gt; /KeyFile o =&lt;file_name&gt; tooenable accesso alla rete.</span><span class="sxs-lookup"><span data-stu-id="963fb-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="963fb-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;stringa_chiave&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="963fb-276">oppure</span><span class="sxs-lookup"><span data-stu-id="963fb-276">or</span></span><br><br><span data-ttu-id="963fb-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;nome_file&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="963fb-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="963fb-279">Non modificare le regole del firewall quando si usa /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="963fb-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="963fb-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="963fb-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="963fb-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="963fb-282">Generare una nuova chiave di autorizzazione e salvare toohello file specificato.</span><span class="sxs-lookup"><span data-stu-id="963fb-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="963fb-283">chiave Hello generato può essere utilizzato con hello /Key o /KeyFile opzioni.</span><span class="sxs-lookup"><span data-stu-id="963fb-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="963fb-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey percorso file&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-285">Coerenza</span><span class="sxs-lookup"><span data-stu-id="963fb-285">Consistency</span></span></td>
  <td><span data-ttu-id="963fb-286">Impostare livello di coerenza hello predefinito per l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="963fb-287">CosmosDB.Emulator.exe /Consistency=&lt;coerenza&gt;</span><span class="sxs-lookup"><span data-stu-id="963fb-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="963fb-288">&lt;coerenza&gt;: valore deve essere uno dei seguenti hello [livelli di coerenza](consistency-levels.md): BoundedStaleness, sicuro, eventuale o sessione.</span><span class="sxs-lookup"><span data-stu-id="963fb-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="963fb-289">valore predefinito di Hello è sessione.</span><span class="sxs-lookup"><span data-stu-id="963fb-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="963fb-290">?</span><span class="sxs-lookup"><span data-stu-id="963fb-290">?</span></span></td>
  <td><span data-ttu-id="963fb-291">Mostra messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="963fb-292">Differenze tra hello Azure Cosmos DB emulatore e Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="963fb-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="963fb-293">Poiché hello Azure Cosmos DB emulatore fornisce un ambiente di emulato in esecuzione in una workstation di sviluppo locale, esistono alcune differenze nelle funzionalità tra emulatore hello e un account Azure Cosmos DB nel cloud hello:</span><span class="sxs-lookup"><span data-stu-id="963fb-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="963fb-294">Hello Azure Cosmos DB emulatore supporta solo un singolo account fisso e una chiave master del nota.</span><span class="sxs-lookup"><span data-stu-id="963fb-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="963fb-295">Rigenerazione della chiave non è possibile in hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="963fb-296">Hello Azure Cosmos DB emulatore non è un servizio scalabile e non supporta un numero elevato di raccolte.</span><span class="sxs-lookup"><span data-stu-id="963fb-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="963fb-297">Hello Azure Cosmos DB emulatore non simula diverse [livelli di coerenza Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="963fb-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="963fb-298">Hello Azure Cosmos DB emulatore non viene simulata [multiarea replica](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="963fb-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="963fb-299">Hello Azure Cosmos DB emulatore non supporta l'override di quota hello servizio che sono disponibili nel servizio di Azure Cosmos DB hello (ad esempio i limiti di dimensioni di documento, archiviazione della raccolta partizionata maggiore).</span><span class="sxs-lookup"><span data-stu-id="963fb-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="963fb-300">Come la copia di hello Azure Cosmos DB emulatore potrebbe non essere backup toodate con le modifiche più recenti di hello con il servizio di Azure Cosmos DB hello, eseguire [pianificazione della capacità di Azure Cosmos DB](https://www.documentdb.com/capacityplanner) velocità effettiva di produzione stima di tooaccurately (RUs) requisiti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="963fb-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="963fb-301"><a id="set-partitioncount"></a>Modificare il numero di hello di raccolte</span><span class="sxs-lookup"><span data-stu-id="963fb-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="963fb-302">Per impostazione predefinita, è possibile creare raccolte con partizione singola too25 o 1 raccolta partizionata utilizzando hello Azure Cosmos DB emulatore.</span><span class="sxs-lookup"><span data-stu-id="963fb-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="963fb-303">Modificando hello **PartitionCount** valore, è possibile creare raccolte con partizione singola too250 o le raccolte partizionate 10 o qualsiasi combinazione di due che non superano 250 singolo hello partizioni (in cui 1 partizionata raccolta = raccolta singola partizione 25).</span><span class="sxs-lookup"><span data-stu-id="963fb-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="963fb-304">Se si tenta di toocreate una raccolta dopo che è stato superato il numero di partizione corrente hello, emulatore hello genera un'eccezione ServiceUnavailable, con successivo messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="963fb-305">numero di hello toochange di raccolte disponibili toohello Azure Cosmos DB emulatore, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="963fb-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="963fb-306">Eliminare tutti i dati di Azure Cosmos DB emulatore locali facendo clic su hello **emulatore di Azure Cosmos DB** icona sulla barra delle applicazioni hello, quindi fare clic su **Reimposta dati...** .</span><span class="sxs-lookup"><span data-stu-id="963fb-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="963fb-307">Eliminare tutti i dati dell'emulatore dalla cartella C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="963fb-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="963fb-308">Chiudere tutte le istanze aperte facendo clic su hello **emulatore di Azure Cosmos DB** icona sulla barra delle applicazioni hello, quindi fare clic su **uscita**.</span><span class="sxs-lookup"><span data-stu-id="963fb-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="963fb-309">Potrebbe richiedere un minuto per tutte le istanze tooexit.</span><span class="sxs-lookup"><span data-stu-id="963fb-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="963fb-310">Installare una versione più recente di hello di hello [emulatore di Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="963fb-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="963fb-311">Avvia emulatore di hello con flag PartitionCount hello impostando un valore < = 250.</span><span class="sxs-lookup"><span data-stu-id="963fb-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="963fb-312">Ad esempio: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="963fb-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="963fb-313">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="963fb-313">Troubleshooting</span></span>

<span data-ttu-id="963fb-314">Utilizzare hello toohelp di risolvere i problemi riscontrati con l'emulatore di Azure Cosmos DB hello suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="963fb-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="963fb-315">Se è installata una nuova versione di hello emulatore e segnalano errori, assicurarsi che ripristinare i dati.</span><span class="sxs-lookup"><span data-stu-id="963fb-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="963fb-316">È possibile ripristinare i dati facendo clic sull'icona di Azure Cosmos DB emulatore hello sulla barra delle applicazioni hello, e quindi fare clic su Reimposta dati...</span><span class="sxs-lookup"><span data-stu-id="963fb-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="963fb-317">Se non viene risolto errori hello, è possibile disinstallare e reinstallare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="963fb-318">Vedere [disinstallare emulatore locale hello](#uninstall) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="963fb-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="963fb-319">Se si blocca l'emulatore di Azure Cosmos DB hello, raccogliere i file di dump dalla cartella c:\Users\user_name\AppData\Local\CrashDumps comprimerli e collegarli tramite posta elettronica tooan troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="963fb-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="963fb-320">Se si verificano arresti anomali del sistema in CosmosDB.StartupEntryPoint.exe, eseguire hello comando seguente da un prompt dei comandi di amministratore:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="963fb-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="963fb-321">Se si verifica un problema di connettività, [raccogliere i file di traccia](#trace-files)comprimerli e collegarli tramite posta elettronica tooan troppo[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="963fb-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="963fb-322">Se si riceve un **servizio non disponibile** dei messaggi, hello emulatore potrebbe essersi verificato un errore dello stack di rete hello tooinitialize.</span><span class="sxs-lookup"><span data-stu-id="963fb-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="963fb-323">Toosee di controllo se si dispone di hello Pulse secure Juniper reti client o installati, come i driver di filtro rete potrebbero causare il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="963fb-324">La disinstallazione di driver di filtro di rete di terze parti in genere consente di correggere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="963fb-325"><a id="trace-files"></a>Raccogliere i file di traccia</span><span class="sxs-lookup"><span data-stu-id="963fb-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="963fb-326">toocollect debug tracce, eseguire hello dopo i comandi da un prompt dei comandi amministrativo:</span><span class="sxs-lookup"><span data-stu-id="963fb-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="963fb-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="963fb-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="963fb-328">Espressioni di controllo hello sistema toomake che hello programma è arrestato, potrebbe richiedere un minuto.</span><span class="sxs-lookup"><span data-stu-id="963fb-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="963fb-329">È anche possibile fare clic **uscita** nell'interfaccia utente dell'emulatore di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="963fb-330">Riprodurre il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-330">Reproduce hello problem.</span></span> <span data-ttu-id="963fb-331">Se Esplora dati non funziona, è necessario solo toowait per hello browser tooopen per pochi secondi toocatch hello correggere l'errore.</span><span class="sxs-lookup"><span data-stu-id="963fb-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="963fb-332">Passare troppo`%ProgramFiles%\Azure Cosmos DB Emulator` e trovare il file docdbemulator_000001.etl hello.</span><span class="sxs-lookup"><span data-stu-id="963fb-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="963fb-333">Inviare file con estensione etl hello insieme ai passaggi ripetizione bug troppo[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) per il debug.</span><span class="sxs-lookup"><span data-stu-id="963fb-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="963fb-334"><a id="uninstall"></a>Disinstallare hello emulatore locale</span><span class="sxs-lookup"><span data-stu-id="963fb-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="963fb-335">Chiudere tutte le istanze aperte di hello emulatore locale facendo clic sull'icona di Azure Cosmos DB emulatore hello sulla barra delle applicazioni hello, e quindi fare clic su Esci.</span><span class="sxs-lookup"><span data-stu-id="963fb-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="963fb-336">Potrebbe richiedere un minuto per tutte le istanze tooexit.</span><span class="sxs-lookup"><span data-stu-id="963fb-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="963fb-337">Nella casella di ricerca di Windows hello, digitare **App e funzionalità** e fare clic su hello **App e funzionalità (impostazioni di sistema)** risultato.</span><span class="sxs-lookup"><span data-stu-id="963fb-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="963fb-338">Nell'elenco di App hello scorrere troppo**emulatore di Azure Cosmos DB**, selezionarla, fare clic su **Disinstalla**, confermare, quindi fare clic su **Disinstalla** nuovamente.</span><span class="sxs-lookup"><span data-stu-id="963fb-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="963fb-339">Quando viene disinstallata l'applicazione hello, passare tooC:\Users\<utente > cartella hello \AppData\Local\CosmosDBEmulator e delete.</span><span class="sxs-lookup"><span data-stu-id="963fb-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="963fb-340">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="963fb-340">Next steps</span></span>

<span data-ttu-id="963fb-341">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="963fb-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="963fb-342">Installato hello emulatore locale</span><span class="sxs-lookup"><span data-stu-id="963fb-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="963fb-343">Rand hello emulatore in Docker per Windows</span><span class="sxs-lookup"><span data-stu-id="963fb-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="963fb-344">Autenticazione delle richieste</span><span class="sxs-lookup"><span data-stu-id="963fb-344">Authenticated requests</span></span>
> * <span data-ttu-id="963fb-345">Ciao Esplora dati hello emulatore utilizzato</span><span class="sxs-lookup"><span data-stu-id="963fb-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="963fb-346">Esportazione dei certificati SSL</span><span class="sxs-lookup"><span data-stu-id="963fb-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="963fb-347">Chiamata hello emulatore dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="963fb-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="963fb-348">Raccolta dei file di traccia</span><span class="sxs-lookup"><span data-stu-id="963fb-348">Collected trace files</span></span>

<span data-ttu-id="963fb-349">In questa esercitazione, si è appreso come toouse hello emulatore locale di sviluppo locale disponibile.</span><span class="sxs-lookup"><span data-stu-id="963fb-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="963fb-350">È possibile continuare l'esercitazione successiva toohello e informazioni su come i certificati SSL emulatore tooexport.</span><span class="sxs-lookup"><span data-stu-id="963fb-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="963fb-351">Esportare i certificati di Azure Cosmos DB emulatore hello</span><span class="sxs-lookup"><span data-stu-id="963fb-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
