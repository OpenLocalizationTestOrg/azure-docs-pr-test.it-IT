---
title: aaaUse tootrigger di automazione di Azure un processo | Documenti Microsoft
description: Informazioni su come toouse automazione di Azure per l'attivazione dei processi di gestione di dati di StorSimple (anteprima privata)
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="f9ea9-103">Utilizzare tootrigger di automazione di Azure (anteprima privata) un processo</span><span class="sxs-lookup"><span data-stu-id="f9ea9-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="f9ea9-104">In questo articolo viene descritto come toouse tootrigger di automazione di Azure un processo di gestione di dati di StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9ea9-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f9ea9-105">Prerequisites</span></span>

<span data-ttu-id="f9ea9-106">Prima di iniziare, assicurarsi di disporre di:</span><span class="sxs-lookup"><span data-stu-id="f9ea9-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="f9ea9-107">Azure Powershell installato.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-107">Azure Powershell installed.</span></span> <span data-ttu-id="f9ea9-108">[Scaricare Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="f9ea9-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="f9ea9-109">Configurazione processo impostazioni di tooinitialize hello la trasformazione dei dati (istruzioni tooobtain queste impostazioni sono incluse in questo caso).</span><span class="sxs-lookup"><span data-stu-id="f9ea9-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="f9ea9-110">Una definizione del processo configurata correttamente in una risorsa dati ibrida all'interno di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="f9ea9-111">Scaricare `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="f9ea9-112">Scaricare `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="f9ea9-113">Scaricare `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="f9ea9-114">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="f9ea9-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="f9ea9-115">Ottenere le autorizzazioni di Azure Active Directory per la definizione di processo hello hello automazione processo toorun</span><span class="sxs-lookup"><span data-stu-id="f9ea9-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="f9ea9-116">parametri di configurazione di hello tooretrieve per Active Directory, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f9ea9-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="f9ea9-117">Aprire Windows PowerShell nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="f9ea9-118">Assicurarsi che [Azure PowerShell](https://azure.microsoft.com/downloads/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="f9ea9-119">Eseguire hello `Get-ConfigurationParams.ps1` script (nella cartella hello è stato scaricato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="f9ea9-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="f9ea9-120">Digitare hello comando nella finestra di PowerShell hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f9ea9-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="f9ea9-121">Hello ActiveDirectoryKey è una password in uso in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="f9ea9-122">Immettere una password a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-122">Enter a password of your choice.</span></span> <span data-ttu-id="f9ea9-123">AppName può essere una stringa qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-123">AppName can be any string.</span></span>

2. <span data-ttu-id="f9ea9-124">Questo script genera hello seguente i valori che devono essere utilizzati durante l'attivazione di hello runbook di automazione.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="f9ea9-125">Prendere nota dei valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-125">Make a note of these values.</span></span>

    - <span data-ttu-id="f9ea9-126">ID Client</span><span class="sxs-lookup"><span data-stu-id="f9ea9-126">Client ID</span></span>
    - <span data-ttu-id="f9ea9-127">ID tenant</span><span class="sxs-lookup"><span data-stu-id="f9ea9-127">Tenant ID</span></span>
    - <span data-ttu-id="f9ea9-128">Chiave di Directory attiva (quella hello uno sopra specificato)</span><span class="sxs-lookup"><span data-stu-id="f9ea9-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="f9ea9-129">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="f9ea9-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="f9ea9-130">Configurare Account di automazione hello</span><span class="sxs-lookup"><span data-stu-id="f9ea9-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="f9ea9-131">Accedere a tooAzure e aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="f9ea9-132">Fare clic su **asset** riquadro tooopen hello elenco degli asset.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="f9ea9-133">Fare clic su **moduli** riquadro tooopen hello elenco dei moduli.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="f9ea9-134">Fare clic su **+ Aggiungi un modulo** Pannello di modulo Aggiungi pulsante e hello viene avviata.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="f9ea9-136">Dopo aver selezionato hello `DataTransformationApp.zip` file dal computer locale, fare clic su **OK** modulo hello tooimport.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="f9ea9-137">Quando un account tooyour modulo di importazione di automazione di Azure, estrae i metadati relativi a modulo hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="f9ea9-138">Questa operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-138">This operation may take a couple of minutes.</span></span>

   ![Impostazioni dell'account di automazione](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="f9ea9-140">Si riceve una notifica viene distribuito il modulo hello e un'altra notifica al termine il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="f9ea9-141">È inoltre possibile verificare lo stato di hello in **moduli** riquadro.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="f9ea9-142">runbook hello tooimport che attiva la definizione di processo hello</span><span class="sxs-lookup"><span data-stu-id="f9ea9-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="f9ea9-143">Nel portale di Azure hello, aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="f9ea9-144">Fare clic su **runbook** riquadro tooopen hello elenco di runbook.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="f9ea9-145">Fare clic su **+ Aggiungi runbook** e poi **Importa un runbook esistente**.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Importare un runbook esistente](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="f9ea9-147">Fare clic su **file Runbook** e hello selezionare file tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="f9ea9-148">Fare clic su **crea** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="f9ea9-149">Hello nuovo runbook verrà visualizzato nell'elenco di hello di runbook per hello account di automazione.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="f9ea9-150">Fare clic sul runbook **Trigger-DataTransformation-Job** quindi su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="f9ea9-151">Fare clic su **Pubblica** quindi su **Sì** quando viene richiesta la conferma.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="f9ea9-152">runbook hello toorun:</span><span class="sxs-lookup"><span data-stu-id="f9ea9-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="f9ea9-153">Nel portale di Azure hello, aprire l'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="f9ea9-154">Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="f9ea9-155">Fare clic su **Trigger-DataTransformation-Job**.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="f9ea9-156">Fare clic su **avviare** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-156">Click **Start** toostart hello runbook.</span></span>

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="f9ea9-158">In hello **avviare runbook** pannello, immettere tutti i parametri di hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="f9ea9-159">Fare clic su **OK** processo di trasformazione dei dati toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="f9ea9-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Avvia runbook](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="f9ea9-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9ea9-161">Next steps</span></span>

<span data-ttu-id="f9ea9-162">[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="f9ea9-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
