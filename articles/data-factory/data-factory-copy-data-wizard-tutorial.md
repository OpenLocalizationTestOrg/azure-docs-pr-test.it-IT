---
title: 'Esercitazione: Creare una pipeline usando la Copia guidata | Documentazione Microsoft'
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando la Copia guidata supportata da Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="f80ae-103">Esercitazione: Creare una pipeline con l'attività di copia usando la Copia guidata di Data Factory</span><span class="sxs-lookup"><span data-stu-id="f80ae-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f80ae-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f80ae-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="f80ae-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="f80ae-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="f80ae-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f80ae-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="f80ae-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f80ae-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="f80ae-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f80ae-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="f80ae-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f80ae-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="f80ae-110">API REST</span><span class="sxs-lookup"><span data-stu-id="f80ae-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="f80ae-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="f80ae-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="f80ae-112">Questa esercitazione illustra come usare la **copia guidata** per copiare i dati da un archivio BLOB di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f80ae-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="f80ae-113">La **copia guidata** di Azure Data Factory consente di creare rapidamente una pipeline di dati che copia i dati da un archivio dati di origine supportato a un archivio dati di destinazione supporto.</span><span class="sxs-lookup"><span data-stu-id="f80ae-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="f80ae-114">È quindi consigliabile usare la procedura guidata come primo passaggio per creare una pipeline di esempio per lo scenario di spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="f80ae-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="f80ae-115">Per un elenco degli archivi dati supportati come origini e come destinazioni, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f80ae-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="f80ae-116">Questa esercitazione illustra come creare una data factory di Azure, avviare la Copia guidata ed eseguire una serie di passaggi per specificare i dettagli relativi allo scenario di inserimento/spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="f80ae-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="f80ae-117">Al termine dei passaggi della procedura guidata, verrà creata automaticamente una pipeline con un'attività di copia per copiare i dati da un archivio BLOB di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f80ae-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="f80ae-118">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f80ae-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f80ae-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f80ae-119">Prerequisites</span></span>
<span data-ttu-id="f80ae-120">Prima di eseguire questa esercitazione, completare i prerequisiti indicati nella [panoramica dell'esercitazione](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .</span><span class="sxs-lookup"><span data-stu-id="f80ae-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="f80ae-121">Creare un'istanza di Data Factory</span><span class="sxs-lookup"><span data-stu-id="f80ae-121">Create data factory</span></span>
<span data-ttu-id="f80ae-122">In questo passaggio viene usato il portale di Azure per creare un'istanza di Azure Data Factory denominata **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="f80ae-123">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f80ae-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f80ae-124">Fare clic su **+ NUOVO** nell'angolo in alto a sinistra e quindi su **Dati e analisi** e su **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Nuovo->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="f80ae-126">Nel pannello **Nuova data factory** :</span><span class="sxs-lookup"><span data-stu-id="f80ae-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="f80ae-127">Immettere **ADFTutorialDataFactory** come **nome**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="f80ae-128">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f80ae-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="f80ae-129">Se viene visualizzato l'errore `Data factory name “ADFTutorialDataFactory” is not available`, modificare il nome della data factory, ad esempio, nomeutenteADFTutorialDataFactoryAAAAMMGG, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="f80ae-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="f80ae-130">Per informazioni sulle regole di denominazione per gli elementi di Data Factory, vedere l'argomento [Azure Data Factory - Regole di denominazione](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="f80ae-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Nome di data factory non disponibile](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="f80ae-132">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="f80ae-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="f80ae-133">In Gruppo di risorse eseguire una di queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="f80ae-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="f80ae-134">Selezionare **Usa esistente** per scegliere un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="f80ae-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="f80ae-135">Selezionare **Crea nuovo** per immettere un nome per un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f80ae-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="f80ae-136">Alcuni dei passaggi di questa esercitazione presuppongono l'uso del nome **ADFTutorialResourceGroup** per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f80ae-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="f80ae-137">Per informazioni sui gruppi di risorse, vedere l'articolo relativo all' [uso di gruppi di risorse per la gestione delle risorse di Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f80ae-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="f80ae-138">Selezionare una **località** per la data factory.</span><span class="sxs-lookup"><span data-stu-id="f80ae-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="f80ae-139">Selezionare la casella di controllo **Aggiungi al dashboard** nella parte inferiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="f80ae-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="f80ae-140">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-140">Click **Create**.</span></span>
      
       ![Pannello Nuova data factory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="f80ae-142">Al termine della creazione verrà visualizzato il pannello **Data factory**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="f80ae-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Home page di Data factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="f80ae-144">Avviare la Copia guidata</span><span class="sxs-lookup"><span data-stu-id="f80ae-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="f80ae-145">Nel pannello Data Factory fare clic su **Copia dati (ANTEPRIMA)** per avviare **Copy Wizard** (Copia guidata).</span><span class="sxs-lookup"><span data-stu-id="f80ae-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f80ae-146">Se il Web browser è bloccato su "Concessione autorizzazioni in corso...", disabilitare/deselezionare l'impostazione **Block third party cookies and site data** (Blocca cookie e dati del sito di terze parti) nelle impostazioni del browser oppure lasciarla abilitata e creare un'eccezione per **login.microsoftonline.com** e quindi provare di nuovo ad avviare la procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="f80ae-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="f80ae-147">Nella pagina **Proprietà** :</span><span class="sxs-lookup"><span data-stu-id="f80ae-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="f80ae-148">Immettere **CopyFromBlobToAzureSql** per **Nome attività**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="f80ae-149">Immettere una **descrizione** (facoltativo).</span><span class="sxs-lookup"><span data-stu-id="f80ae-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="f80ae-150">Modificare **Start date time** (Data e ora di inizio) ed **End date time** (Data e ora di fine) in modo che la data di fine corrisponda alla data odierna e la data di inizio a cinque giorni prima.</span><span class="sxs-lookup"><span data-stu-id="f80ae-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="f80ae-151">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-151">Click **Next**.</span></span>  
      
      ![Strumento di copia - Pagina Proprietà](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="f80ae-153">Nella pagina **Source data store** (Archivio dati di origine) fare clic sul riquadro **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="f80ae-154">Usare questa pagina per specificare l'archivio dati di origine per l'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="f80ae-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Strumento di copia - Pagina Archivio dati di origine](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="f80ae-156">Nella pagina **Specify the Azure Blob storage account** (Specificare l'account di archiviazione BLOB di Azure):</span><span class="sxs-lookup"><span data-stu-id="f80ae-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="f80ae-157">Immettere **AzureStorageLinkedService** per **Nome del servizio collegato**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="f80ae-158">Verificare che in **Account selection method** (Metodo di selezione dell'account) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="f80ae-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="f80ae-159">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="f80ae-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="f80ae-160">Selezionare un **Account di archiviazione di Azure** nell'elenco di quelli disponibili nella sottoscrizione selezionata.</span><span class="sxs-lookup"><span data-stu-id="f80ae-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="f80ae-161">È anche possibile scegliere di immettere manualmente le impostazioni dell'account di archiviazione, selezionando l'opzione **Immetti manualmente** per **Account selection method** (Metodo di selezione dell'account), quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Strumento di copia - Specificare l'account di archiviazione BLOB di Azure](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="f80ae-163">Nella pagina **Choose the input file or folder** (Scegliere il file o la cartella di input):</span><span class="sxs-lookup"><span data-stu-id="f80ae-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="f80ae-164">Fare doppio clic sulla cartella **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="f80ae-165">Selezionare **emp.txt** e fare clic su **Scegli**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Strumento di copia - Scegliere il file o la cartella di input](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="f80ae-167">Nella pagina **Choose the input file or folder** (Scegliere il file o la cartella di input) fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="f80ae-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="f80ae-168">Non selezionare **Binary copy**(Copia binaria).</span><span class="sxs-lookup"><span data-stu-id="f80ae-168">Do not select **Binary copy**.</span></span> 
   
    ![Strumento di copia - Scegliere il file o la cartella di input](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="f80ae-170">Nella pagina **File format settings** (Impostazioni di formato file) vengono visualizzati i delimitatori e lo schema rilevati automaticamente dalla procedura guidata analizzando il file.</span><span class="sxs-lookup"><span data-stu-id="f80ae-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="f80ae-171">È anche possibile immettere i delimitatori manualmente per sostituirli o interrompere il rilevamento automatico nella Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="f80ae-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="f80ae-172">Dopo aver esaminato i delimitatori e i dati di anteprima, fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="f80ae-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Strumento di copia - Impostazioni di formattazioni del file](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="f80ae-174">Nella pagina Destination data store (Archivio dati di destinazione) selezionare **Azure SQL Database** (Database SQL di Azure) e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="f80ae-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Strumento di copia - Scegliere l'archivio di destinazione](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="f80ae-176">Nella pagina **Specify the Azure SQL database** (Specificare il database SQL di Azure):</span><span class="sxs-lookup"><span data-stu-id="f80ae-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="f80ae-177">Immettere **AzureSqlLinkedService** nel campo **Connection name** (Nome connessione).</span><span class="sxs-lookup"><span data-stu-id="f80ae-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="f80ae-178">Verificare che in **Server / database selection method** (Metodo di selezione del server/database) sia selezionata l'opzione **From Azure subscriptions** (Da sottoscrizioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="f80ae-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="f80ae-179">Selezionare la **sottoscrizione**di Azure.</span><span class="sxs-lookup"><span data-stu-id="f80ae-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="f80ae-180">Selezionare **Nome server** e **Database**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="f80ae-181">Immettere un **Nome utente** e una **Password**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="f80ae-182">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-182">Click **Next**.</span></span>  
      
      ![Strumento di copia - Specificare il database SQL di Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="f80ae-184">Nella pagina **Mapping tabella** selezionare **emp** dall'elenco a discesa per il campo **Destinazione**, fare clic sulla **freccia giù** (facoltativo) per visualizzare lo schema e l'anteprima dei dati.</span><span class="sxs-lookup"><span data-stu-id="f80ae-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Strumento di copia - Mapping tabella](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="f80ae-186">Nella pagina **Mapping dello schema** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Strumento di copia - Mapping dello schema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="f80ae-188">Nella pagina **Prestazioni** fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Strumento di copia - Impostazioni relative alle prestazioni](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="f80ae-190">Verificare le informazioni nella pagina **Riepilogo** e fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="f80ae-191">La procedura guidata crea due servizi collegati, due set di dati (input e output) e una pipeline nella data factory da cui è stata avviata la Copia guidata.</span><span class="sxs-lookup"><span data-stu-id="f80ae-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Strumento di copia - Impostazioni relative alle prestazioni](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="f80ae-193">Avviare l'applicazione di monitoraggio e gestione</span><span class="sxs-lookup"><span data-stu-id="f80ae-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="f80ae-194">Nella pagina **Distribuzione** fare clic sul collegamento: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="f80ae-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Strumento di copia - La distribuzione è riuscita](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="f80ae-196">L'applicazione di monitoraggio viene avviata in una scheda separata del Web browser.</span><span class="sxs-lookup"><span data-stu-id="f80ae-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![App di monitoraggio](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="f80ae-198">Per visualizzare lo stato più recente delle sezioni orarie, fare clic sul pulsante **Aggiorna** nell'elenco **ACTIVITY WINDOWS** (Finestre attività) nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="f80ae-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="f80ae-199">Vengono visualizzate cinque finestre attività relative a cinque giorni compresi tra le ore di inizio e di fine della pipeline.</span><span class="sxs-lookup"><span data-stu-id="f80ae-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="f80ae-200">L'elenco non viene aggiornato automaticamente, quindi potrebbe essere necessario fare clic su Aggiorna un paio di volte prima di visualizzare tutte le finestre attività con lo stato Pronto.</span><span class="sxs-lookup"><span data-stu-id="f80ae-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="f80ae-201">Selezionare una finestra attività nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="f80ae-201">Select an activity window in the list.</span></span> <span data-ttu-id="f80ae-202">Visualizzarne i dettagli in **Activity Window Explorer** (Esplora finestre attività) a destra.</span><span class="sxs-lookup"><span data-stu-id="f80ae-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Dettagli finestra attività](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="f80ae-204">Si noti che le date 11, 12, 13, 14 e 15 sono di colore verde per indicare che le sezioni di output giornaliere di queste date sono già stata generate.</span><span class="sxs-lookup"><span data-stu-id="f80ae-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="f80ae-205">Questa codifica a colori viene usata anche nella pipeline e nel set di dati di output nella vista diagramma.</span><span class="sxs-lookup"><span data-stu-id="f80ae-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="f80ae-206">Nel passaggio precedente si noti che due sezioni sono già state generate, una sezione è attualmente in fase di elaborazione e le altre due sono in attesa di essere elaborate (in base alla codifica a colori).</span><span class="sxs-lookup"><span data-stu-id="f80ae-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="f80ae-207">Per altre informazioni sull'uso di questa applicazione, vedere l'articolo [Monitorare e gestire le pipeline di Azure Data Factory con l'app di monitoraggio e gestione](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="f80ae-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f80ae-208">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f80ae-208">Next steps</span></span>
<span data-ttu-id="f80ae-209">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="f80ae-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f80ae-210">La tabella seguente contiene un elenco degli archivi dati supportati come origini e come destinazioni dall'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="f80ae-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f80ae-211">Per informazioni dettagliate sui campi o sulle proprietà visualizzate durante la copia guidata di un archivio dati, fare clic sul collegamento relativo all'archivio dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="f80ae-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 