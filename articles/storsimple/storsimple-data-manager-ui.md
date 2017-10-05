---
title: Interfaccia utente di Microsoft Azure StorSimple Data Manager | Documentazione Microsoft
description: Questo articolo descrive come usare l'interfaccia utente del servizio StorSimple Data Manager (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 53a8599df2c647613122cd791b680e2e658586b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-using-the-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="02aba-103">Gestire tramite l'interfaccia utente del servizio StorSimple Data Manager (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="02aba-103">Manage using the StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="02aba-104">Questo articolo illustra come usare l'interfaccia utente di StorSimple Data Manager per eseguire la trasformazione dei dati che risiedono sui dispositivi StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="02aba-104">This article explains how you can use the StorSimple Data Manager UI to perform data transformation on data residing on the StorSimple 8000 series devices.</span></span> <span data-ttu-id="02aba-105">I dati trasformati possono quindi essere impiegati da altri servizi di Azure, ad esempio Servizi multimediali di Azure, Azure HDInsight, Azure Machine Learning e Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="02aba-105">The transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="02aba-106">Usare la trasformazione dati di StorSimple</span><span class="sxs-lookup"><span data-stu-id="02aba-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="02aba-107">StorSimple Data Manager è la risorsa all'interno della quale è possibile creare istanze di trasformazione dati.</span><span class="sxs-lookup"><span data-stu-id="02aba-107">The StorSimple Data Manager is the resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="02aba-108">Il servizio di trasformazione dei dati consente di spostare dati dal dispositivo StorSimple locale ai BLOB in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="02aba-108">The Data Transformation service lets you move data from your StorSimple on-premises device to blobs in Azure storage.</span></span> <span data-ttu-id="02aba-109">Di conseguenza, nel flusso di lavoro è necessario specificare i dettagli relativi al dispositivo StorSimple e i dati di interesse da spostare nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="02aba-109">Hence, in workflow you need to specify the details about your StorSimple device and the data of interest that you want to move to the storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="02aba-110">Creare un servizio StorSimple Data Manager</span><span class="sxs-lookup"><span data-stu-id="02aba-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="02aba-111">Eseguire la procedura seguente per creare un servizio StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="02aba-111">Perform the following steps to create a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="02aba-112">Per creare un servizio StorSimple Data Manager, fare riferimento a [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="02aba-112">To create a StorSimple Data Manager service, go to [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="02aba-113">Fare clic sull'icona **+** e ricercare StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="02aba-113">Click the **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="02aba-114">Fare clic sul servizio StorSimple Data Manager, quindi su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="02aba-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="02aba-115">Se la sottoscrizione è abilitata per la creazione di questo servizio, viene visualizzato il pannello seguente.</span><span class="sxs-lookup"><span data-stu-id="02aba-115">If your subscription is enabled for creating this service, you see the following blade.</span></span>

    ![Creare una risorsa StorSimple Data Manager](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="02aba-117">Immettere i dati necessari e fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="02aba-117">Enter the inputs and click **Create**.</span></span> <span data-ttu-id="02aba-118">Il percorso specificato deve essere quello che ospita gli account di archiviazione e il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="02aba-118">The specified location should be the one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="02aba-119">Attualmente sono supportate solo le aree Europa occidentale e Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="02aba-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="02aba-120">Di conseguenza, il servizio StorSimple Manager, il servizio Data Manager e l'account di archiviazione associato devono essere tutti nelle aree supportate indicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="02aba-120">Hence, your StorSimple Manager service, Data Manager service, and the associated storage account should all be in the preceding supported regions.</span></span> <span data-ttu-id="02aba-121">La creazione del servizio richiede circa un minuto.</span><span class="sxs-lookup"><span data-stu-id="02aba-121">It takes about a minute to create the service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="02aba-122">Creare una definizione di processo di trasformazione dati</span><span class="sxs-lookup"><span data-stu-id="02aba-122">Create a data transformation job definition</span></span>

<span data-ttu-id="02aba-123">All'interno di un servizio StorSimple Data Manager è necessario creare una definizione di processo di trasformazione dati.</span><span class="sxs-lookup"><span data-stu-id="02aba-123">Within a StorSimple Data Manager service, you need to create a data transformation job definition.</span></span> <span data-ttu-id="02aba-124">Tale definizione specifica i dettagli dei dati da spostare in un account di archiviazione nel formato nativo.</span><span class="sxs-lookup"><span data-stu-id="02aba-124">A job definition specifies details of the data that you are interested in moving into a storage account in the native format.</span></span> 

<span data-ttu-id="02aba-125">Eseguire la procedura seguente per creare una nuova definizione di processo di trasformazione dati.</span><span class="sxs-lookup"><span data-stu-id="02aba-125">Perform the following steps to create a new data transformation job definition.</span></span>

1.  <span data-ttu-id="02aba-126">Passare al servizio creato.</span><span class="sxs-lookup"><span data-stu-id="02aba-126">Navigate to the service that you created.</span></span> <span data-ttu-id="02aba-127">Fare clic su **+ Job Definition** (+ Definizione processo).</span><span class="sxs-lookup"><span data-stu-id="02aba-127">Click **+ Job Definition**.</span></span>

    ![Fare clic su + Definizione processo](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="02aba-129">Si apre il pannello della nuova definizione processo.</span><span class="sxs-lookup"><span data-stu-id="02aba-129">The new job definition blade opens up.</span></span> <span data-ttu-id="02aba-130">Assegnare un nome alla definizione di processo e fare clic su **Origine**.</span><span class="sxs-lookup"><span data-stu-id="02aba-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="02aba-131">Nel pannello **Configure data source** (Configura origine dati) specificare i dettagli del dispositivo StorSimple e i dati di interesse.</span><span class="sxs-lookup"><span data-stu-id="02aba-131">In the **Configure data source** blade, specify the details of your StorSimple device and the data of interest.</span></span>

    ![Creare la definizione di processo](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="02aba-133">Poiché si tratta di un nuovo servizio Data Manager, non sono presenti repository di dati configurati.</span><span class="sxs-lookup"><span data-stu-id="02aba-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="02aba-134">Per aggiungere il servizio StorSimple Manager come un repository di dati, fare clic su **Aggiungi nuovo** nell'elenco a discesa dei repository di dati e quindi fare clic su **Add Data Repository** (Aggiungi repository di dati).</span><span class="sxs-lookup"><span data-stu-id="02aba-134">To add your StorSimple Manager as a data repository, click **Add new** in the data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="02aba-135">Scegliere **StorSimple Manager serie 8000** come tipo di repository e immettere le proprietà del servizio **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="02aba-135">Choose **StorSimple 8000 series Manager** as the repository type and enter the properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="02aba-136">Nel campo **ID risorsa** è necessario immettere il numero che precede **:** nella chiave di registrazione del servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="02aba-136">For the **Resource Id** field, you need to enter the number before the **:** in the registration key of your StorSimple manager.</span></span>

    ![Creare un'origine dati](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="02aba-138">Fare clic su **OK** al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="02aba-138">Click **OK** when done.</span></span> <span data-ttu-id="02aba-139">In questo modo sarà possibile salvare il repository di dati e usare questo servizio StorSimple Manager in altre definizioni di processo senza dover immettere nuovamente tali parametri.</span><span class="sxs-lookup"><span data-stu-id="02aba-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="02aba-140">Dopo aver fatto clic su **OK** attendere pochi secondi prima che StorSimple Manager venga visualizzato nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="02aba-140">It takes a few seconds after you click **OK** for the StorSimple Manager to show up in the dropdown.</span></span>

6.  <span data-ttu-id="02aba-141">Nel pannello **Configure data source** (Configura origine dati) immettere il nome del dispositivo e il nome del volume contenente i dati di interesse.</span><span class="sxs-lookup"><span data-stu-id="02aba-141">In the **Configure data source** blade, enter the device name and the volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="02aba-142">Nella sottosezione **Filtro** immettere la directory radice contenente i dati di interesse (questo campo deve iniziare con `\`).</span><span class="sxs-lookup"><span data-stu-id="02aba-142">In the **Filter** subsection, enter the root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="02aba-143">È inoltre possibile aggiungere qualsiasi filtro file qui.</span><span class="sxs-lookup"><span data-stu-id="02aba-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="02aba-144">Il servizio di trasformazione dati funziona sui dati inseriti in Azure tramite snapshot.</span><span class="sxs-lookup"><span data-stu-id="02aba-144">The data transformation service works on the data that is pushed up to the Azure via snapshots.</span></span> <span data-ttu-id="02aba-145">Quando si esegue questo processo, è possibile scegliere di completare un backup a ogni esecuzione del processo (per lavorare sui dati più recenti) o usare l'ultimo backup esistente nel cloud (se si lavora con alcuni dati archiviati).</span><span class="sxs-lookup"><span data-stu-id="02aba-145">When running this job, you can choose to take a backup every time this job is run (to work on latest data) or to use the last existing backup in the cloud (if you are working on some archived data).</span></span>

    ![Dettagli nuova origine dati](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="02aba-147">Successivamente, è necessario configurare le impostazioni di destinazione.</span><span class="sxs-lookup"><span data-stu-id="02aba-147">Next, the Target settings need to be configured.</span></span> <span data-ttu-id="02aba-148">Sono previsti 2 tipi di destinazioni supportate: account di Archiviazione di Azure e account di Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="02aba-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="02aba-149">Scegliere gli account di archiviazione per l'inserimento dei file nei BLOB di tale account.</span><span class="sxs-lookup"><span data-stu-id="02aba-149">Choose storage accounts to put files into blobs in that account.</span></span> <span data-ttu-id="02aba-150">Scegliere l'account dei servizi multimediali per l'inserimento dei file negli asset di tale account.</span><span class="sxs-lookup"><span data-stu-id="02aba-150">Choose media services account to put files into assets in that account.</span></span> <span data-ttu-id="02aba-151">Anche in questo caso è necessario aggiungere un repository.</span><span class="sxs-lookup"><span data-stu-id="02aba-151">Again, we need to add a repository.</span></span> <span data-ttu-id="02aba-152">Nell'elenco a discesa selezionare **Aggiungi nuovo** e quindi **Configura impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="02aba-152">In the dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Creare un sink dati](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="02aba-154">In questo caso, è possibile selezionare il tipo di repository che si desidera aggiungere e gli altri parametri a esso associati.</span><span class="sxs-lookup"><span data-stu-id="02aba-154">Here, you can select the type of repository you want to add and the other parameters associated with the repository.</span></span> <span data-ttu-id="02aba-155">In entrambi i casi, quando viene eseguito il processo, viene creata una coda di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="02aba-155">In both cases, a storage queue is created when the job runs.</span></span> <span data-ttu-id="02aba-156">Questa coda viene popolata con i messaggi relativi ai BLOB trasformati non appena pronti.</span><span class="sxs-lookup"><span data-stu-id="02aba-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="02aba-157">Il nome di questa coda corrisponde a quello della definizione di processo.</span><span class="sxs-lookup"><span data-stu-id="02aba-157">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="02aba-158">Se si seleziona **Servizi multimediali** come tipo di repository, è quindi possibile immettere anche le credenziali dell'account di archiviazione in cui viene creata la coda.</span><span class="sxs-lookup"><span data-stu-id="02aba-158">If you select **Media Services** as the repo type, then you can also enter storage account credentials where the queue is created.</span></span>

    ![Dettagli nuovo sink dati](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="02aba-160">Dopo aver aggiunto il repository di dati, operazione che richiede alcuni secondi, questo verrà incluso nell'elenco a discesa nel **nome dell'account di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="02aba-160">After adding the data repository (which takes a few seconds), you will find the repo in the dropdown in the **Target account name**.</span></span>  <span data-ttu-id="02aba-161">Scegliere la destinazione desiderata.</span><span class="sxs-lookup"><span data-stu-id="02aba-161">Choose the target that you need.</span></span>

12. <span data-ttu-id="02aba-162">Fare clic su **OK** per creare la definizione di processo.</span><span class="sxs-lookup"><span data-stu-id="02aba-162">Click **OK** to create the job definition.</span></span> <span data-ttu-id="02aba-163">La definizione di processo è ora impostata.</span><span class="sxs-lookup"><span data-stu-id="02aba-163">Your job definition is now set up.</span></span> <span data-ttu-id="02aba-164">È possibile usare questa definizione più volte tramite l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="02aba-164">You can use this job definition multiple times via the UI.</span></span>

    ![Aggiungere una nuova definizione di processo](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-the-job-definition"></a><span data-ttu-id="02aba-166">Eseguire la definizione di processo</span><span class="sxs-lookup"><span data-stu-id="02aba-166">Run the job definition</span></span>

<span data-ttu-id="02aba-167">Quando si desidera spostare i dati da StorSimple all'account di archiviazione specificato nella definizione di processo, è necessario richiamarlo.</span><span class="sxs-lookup"><span data-stu-id="02aba-167">Whenever you need to move data from StorSimple to the storage account that you have specified in the job definition, you will need to invoke it.</span></span> <span data-ttu-id="02aba-168">Ogni volta che si richiama il processo, è prevista una determinata flessibilità di modifica dei parametri.</span><span class="sxs-lookup"><span data-stu-id="02aba-168">There is some flexibility in changing the parameters every time you invoke the job.</span></span> <span data-ttu-id="02aba-169">Attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="02aba-169">The steps are as follows:</span></span>

1. <span data-ttu-id="02aba-170">Fare clic sul servizio StorSimple Data Manager e passare a **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="02aba-170">Select your StorSimple Data Manager service and go to **Monitoring**.</span></span> <span data-ttu-id="02aba-171">Fare clic su **Esegui adesso**.</span><span class="sxs-lookup"><span data-stu-id="02aba-171">Click **Run Now**.</span></span>

    ![Attivare la definizione di processo](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="02aba-173">Scegliere la definizione di processo che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="02aba-173">Choose the job definition that you want to run.</span></span> <span data-ttu-id="02aba-174">Fare clic su **Impostazioni di esecuzione** per modificare le impostazioni che si desidera cambiare per l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="02aba-174">Click **Run settings** to modify any settings that you might want to change for this job run.</span></span>

    ![Impostazioni di esecuzione del processo](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="02aba-176">Fare clic su **OK** quindi fare clic su **Esegui** per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="02aba-176">Click **OK** and then click **Run** to launch your job.</span></span> <span data-ttu-id="02aba-177">Per monitorare il processo, passare alla pagina **Processi** in StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="02aba-177">To monitor this job, go to the **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Elenco e stato dei processi](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="02aba-179">Oltre al monitoraggio nel pannello **Processi** è possibile anche restare in ascolto sulla coda di archiviazione in cui viene aggiunto un messaggio ogni volta che un file viene spostato da StorSimple all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="02aba-179">In addition to monitoring in the **Jobs** blade, you can also listen on the storage queue where a message is added every time a file is moved from StorSimple to the storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="02aba-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="02aba-180">Next steps</span></span>

<span data-ttu-id="02aba-181">[Usare .NET SDK per avviare i processi di StorSimple Data Manager](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="02aba-181">[Use .NET SDK to launch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>