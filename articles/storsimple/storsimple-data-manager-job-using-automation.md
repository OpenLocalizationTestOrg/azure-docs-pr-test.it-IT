---
title: Attivare un processo tramite Automazione di Azure | Microsoft Docs
description: Informazioni su come usare Automazione di Azure per attivare i processi di Gestore dati StorSimple (anteprima privata)
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
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="c47ed-103">Attivare un processo tramite Automazione di Azure (anteprima privata)</span><span class="sxs-lookup"><span data-stu-id="c47ed-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="c47ed-104">In questo articolo viene descritto come usare Automazione di Azure per attivare un processo di Gestore dati StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c47ed-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c47ed-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c47ed-105">Prerequisites</span></span>

<span data-ttu-id="c47ed-106">Prima di iniziare, assicurarsi di disporre di:</span><span class="sxs-lookup"><span data-stu-id="c47ed-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="c47ed-107">Azure Powershell installato.</span><span class="sxs-lookup"><span data-stu-id="c47ed-107">Azure Powershell installed.</span></span> <span data-ttu-id="c47ed-108">[Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="c47ed-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="c47ed-109">Impostazioni di configurazione per l'inizializzazione del processo di trasformazione dei dati (le istruzioni per ottenere queste impostazioni sono incluse qui).</span><span class="sxs-lookup"><span data-stu-id="c47ed-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="c47ed-110">Una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c47ed-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="c47ed-111">Scaricare il file [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) `DataTransformationApp.zip` dal repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="c47ed-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="c47ed-112">Scaricare lo [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) `Get-ConfigurationParams.ps1` dal repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="c47ed-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="c47ed-113">Scaricare lo [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) `Trigger-DataTransformation-Job.ps1` dal repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="c47ed-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="c47ed-114">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="c47ed-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="c47ed-115">Ottenere le autorizzazioni di Azure Active Directory per il processo di automazione in modo da eseguire la definizione del processo</span><span class="sxs-lookup"><span data-stu-id="c47ed-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="c47ed-116">Per recuperare i parametri di configurazione di Active Directory, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c47ed-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="c47ed-117">Aprire Windows PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="c47ed-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="c47ed-118">Assicurarsi che [Azure PowerShell](https://azure.microsoft.com/downloads/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="c47ed-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="c47ed-119">Eseguire lo script `Get-ConfigurationParams.ps1` (nella cartella scaricata in precedenza).</span><span class="sxs-lookup"><span data-stu-id="c47ed-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="c47ed-120">Digitare il comando seguente nella finestra di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c47ed-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="c47ed-121">ActiveDirectoryKey è una password da usare successivamente.</span><span class="sxs-lookup"><span data-stu-id="c47ed-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="c47ed-122">Immettere una password a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="c47ed-122">Enter a password of your choice.</span></span> <span data-ttu-id="c47ed-123">AppName può essere una stringa qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="c47ed-123">AppName can be any string.</span></span>

2. <span data-ttu-id="c47ed-124">Questo script restituisce come output i valori seguenti che devono essere usati durante l'attivazione del runbook dell'automazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="c47ed-125">Prendere nota dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="c47ed-125">Make a note of these values.</span></span>

    - <span data-ttu-id="c47ed-126">ID Client</span><span class="sxs-lookup"><span data-stu-id="c47ed-126">Client ID</span></span>
    - <span data-ttu-id="c47ed-127">ID tenant</span><span class="sxs-lookup"><span data-stu-id="c47ed-127">Tenant ID</span></span>
    - <span data-ttu-id="c47ed-128">Chiave di Active Directory (uguale a quella immessa in precedenza)</span><span class="sxs-lookup"><span data-stu-id="c47ed-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="c47ed-129">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="c47ed-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="c47ed-130">Configurare l'account di automazione</span><span class="sxs-lookup"><span data-stu-id="c47ed-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="c47ed-131">Accedere ad Azure e aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="c47ed-132">Fare clic sul riquadro **Asset** per aprire l'elenco degli asset.</span><span class="sxs-lookup"><span data-stu-id="c47ed-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="c47ed-133">Fare clic nel riquadro **Moduli** per aprire l'elenco dei moduli.</span><span class="sxs-lookup"><span data-stu-id="c47ed-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="c47ed-134">Fare clic sul pulsante **+ Aggiungi un modulo** per avviare il pannello Aggiungi modulo.</span><span class="sxs-lookup"><span data-stu-id="c47ed-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="c47ed-136">Dopo aver selezionato il file `DataTransformationApp.zip` dal computer locale, fare clic su **OK** per importare il modulo.</span><span class="sxs-lookup"><span data-stu-id="c47ed-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="c47ed-137">Quando Automazione di Azure esegue l'importazione del modulo nell'account, estrae anche i metadati relativi al modulo.</span><span class="sxs-lookup"><span data-stu-id="c47ed-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="c47ed-138">Questa operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="c47ed-138">This operation may take a couple of minutes.</span></span>

   ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="c47ed-140">Si riceverà una notifica per indicare che è in corso la distribuzione del modulo e un'altra notifica al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="c47ed-141">È inoltre possibile controllare lo stato nel riquadro **Moduli**.</span><span class="sxs-lookup"><span data-stu-id="c47ed-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="c47ed-142">Per importare il runbook che attiva la definizione del processo</span><span class="sxs-lookup"><span data-stu-id="c47ed-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="c47ed-143">Nel portale di Azure aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="c47ed-144">Fare clic nel riquadro **Runbook** per aprire l'elenco dei runbook.</span><span class="sxs-lookup"><span data-stu-id="c47ed-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="c47ed-145">Fare clic su **+ Aggiungi runbook** e poi **Importa un runbook esistente**.</span><span class="sxs-lookup"><span data-stu-id="c47ed-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importare un runbook esistente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="c47ed-147">Fare clic su **File di runbook** e selezionare il file da importare `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c47ed-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="c47ed-148">Per importare il runbook fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c47ed-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="c47ed-149">Il nuovo runbook verrà visualizzato nell'elenco dei runbook dell'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="c47ed-150">Fare clic sul runbook **Trigger-DataTransformation-Job** quindi su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="c47ed-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="c47ed-151">Fare clic su **Pubblica** quindi su **Sì** quando viene richiesta la conferma.</span><span class="sxs-lookup"><span data-stu-id="c47ed-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="c47ed-152">Per eseguire il runbook:</span><span class="sxs-lookup"><span data-stu-id="c47ed-152">To run the runbook:</span></span>
1. <span data-ttu-id="c47ed-153">Nel portale di Azure aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="c47ed-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="c47ed-154">Fare clic nel pannello **Runbook** per aprire l'elenco dei runbook.</span><span class="sxs-lookup"><span data-stu-id="c47ed-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="c47ed-155">Fare clic su **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="c47ed-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="c47ed-156">Fare clic su **Avvia** per avviare il runbook.</span><span class="sxs-lookup"><span data-stu-id="c47ed-156">Click **Start** to start the runbook.</span></span>

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="c47ed-158">Nel pannello **Avvia runbook** immettere tutti i parametri.</span><span class="sxs-lookup"><span data-stu-id="c47ed-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="c47ed-159">Fare clic su **OK** per inviare il processo di trasformazione dati.</span><span class="sxs-lookup"><span data-stu-id="c47ed-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="c47ed-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c47ed-161">Next steps</span></span>

<span data-ttu-id="c47ed-162">[Usare l'interfaccia utente di StorSimple Data Manager per la trasformazione dei dati](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="c47ed-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>