---
title: Installazione del runtime di Funzioni di Azure | Documentazione Microsoft
description: Come installare il runtime di Funzioni di Azure
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="b6c24-103">Installare l'anteprima del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b6c24-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="b6c24-104">Se si desidera installare la versione di anteprima del runtime di Funzioni di Azure è necessario seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="b6c24-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="b6c24-105">Assicurarsi che il computer abbia i requisiti minimi</span><span class="sxs-lookup"><span data-stu-id="b6c24-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="b6c24-106">Scaricare il [programma di installazione dell'anteprima del runtime di Funzioni di Azure](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="b6c24-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="b6c24-107">Installare l'anteprima del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b6c24-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="b6c24-108">Completare la configurazione dell'anteprima del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b6c24-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6c24-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b6c24-109">Prerequisites</span></span>

<span data-ttu-id="b6c24-110">Prima di installare la versione di anteprima del runtime di Funzioni di Azure, è necessario avere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b6c24-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="b6c24-111">Un computer che esegue Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="b6c24-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="b6c24-112">Un'istanza di SQL Server in esecuzione all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="b6c24-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="b6c24-113">L'edizione minima richiesta è SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="b6c24-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="b6c24-114">Installare l'anteprima del runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b6c24-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="b6c24-115">Il programma di installazione dell'anteprima del runtime di Funzioni di Azure guida l'utente nell'installazione dei ruoli di gestione e di lavoro dell'anteprima del runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c24-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="b6c24-116">È possibile installare il ruolo di gestione e di lavoro nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="b6c24-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="b6c24-117">Tuttavia, quando si aggiungono altre funzioni, è necessario distribuire altri ruoli di lavoro nei computer aggiuntivi per poter scalare le funzioni su più thread di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b6c24-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="b6c24-118">Installare il ruolo di gestione e di lavoro nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="b6c24-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="b6c24-119">Eseguire il programma di installazione dell'anteprima del runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c24-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure][1]

1. <span data-ttu-id="b6c24-121">**Fare clic su Avanti** per procedere oltre la prima fase del programma di installazione</span><span class="sxs-lookup"><span data-stu-id="b6c24-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="b6c24-122">Dopo aver letto le condizioni dell'**EULA**, **selezionare la casella** per accettare le condizioni e **fare clic su Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="b6c24-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="b6c24-123">Selezionare i ruoli che si desidera installare nel computer **ruolo di gestione per le funzioni** e/o **ruolo di lavoro per le funzioni** e **fare clic su Avanti**</span><span class="sxs-lookup"><span data-stu-id="b6c24-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Selezione del ruolo][3]

    > [!NOTE]
    > <span data-ttu-id="b6c24-125">È possibile installare il **ruolo di lavoro per le funzioni** in molte altre macchine: a tale scopo, seguire queste istruzioni e selezionare solo il **ruolo di lavoro per le funzioni** nel programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="b6c24-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="b6c24-126">**Fare clic su Avanti** affinché il **programma di installazione del runtime di Funzioni di Azure** esegua l'installazione nel computer.</span><span class="sxs-lookup"><span data-stu-id="b6c24-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="b6c24-127">Al termine, il programma di installazione avvierà lo **strumento di configurazione del runtime di Funzioni di Azure**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Completato][5]

    > [!NOTE]
    > <span data-ttu-id="b6c24-129">Se si sta eseguendo l'installazione su **Windows 10** e la funzionalità **contenitore** non è stata abilitata in precedenza, il programma di installazione del **runtime di Funzioni di Azure** chiede di riavviare il computer per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="b6c24-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="b6c24-130">Configurare il runtime di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b6c24-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="b6c24-131">Per completare l'installazione del Runtime di funzioni di Azure è necessario completare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b6c24-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="b6c24-132">Lo **strumento di configurazione del runtime di Funzioni di Azure** mostra i ruoli che sono installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="b6c24-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Strumento di configurazione][6]

1. <span data-ttu-id="b6c24-134">Fare clic sulla scheda **Database**, immettere i **dettagli della connessione per l'istanza di SQL Server** e **fare clic su Applica**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="b6c24-135">Questo è necessario perché il runtime di Funzioni di Azure possa creare un database per supportare il runtime.</span><span class="sxs-lookup"><span data-stu-id="b6c24-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Anteprima del runtime di Funzioni di Azure - Configurazione del database][7]

1. <span data-ttu-id="b6c24-137">Fare clic sulla scheda **Credenziali**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="b6c24-138">In questa schermata è necessario creare due nuove credenziali per l'uso con una condivisione file per l'hosting di tutte le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c24-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="b6c24-139">**Specificare le combinazioni di nome utente e password** per il **proprietario della condivisione file** e per l'**utente della condivisione file** e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Credenziali][8]

1. <span data-ttu-id="b6c24-141">Fare clic sulla scheda **Condivisione file**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="b6c24-142">In questa schermata è necessario specificare i dettagli del **percorso della condivisione file**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="b6c24-143">È possibile creare la condivisione file o usare una condivisione file esistente e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="b6c24-144">Se si seleziona un nuovo percorso di condivisione file è necessario specificare una directory per l'uso da parte del runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c24-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Anteprima del runtime di Funzioni di Azure - Condivisione file][9]

1. <span data-ttu-id="b6c24-146">Fare clic sulla scheda **IIS**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="b6c24-147">Questa scheda mostra i dettagli dei siti Web in IIS che l'installazione del runtime di Funzioni di Azure creerà.</span><span class="sxs-lookup"><span data-stu-id="b6c24-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="b6c24-148">**Fare clic su Applica** per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="b6c24-148">**Click Apply** to complete.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - IIS][10]

1. <span data-ttu-id="b6c24-150">Fare clic sulla scheda **Servizi**.</span><span class="sxs-lookup"><span data-stu-id="b6c24-150">Click the **Services** tab.</span></span>  <span data-ttu-id="b6c24-151">Questa scheda mostra lo stato dei servizi nell'installazione del runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c24-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="b6c24-152">Se dopo la configurazione iniziale il **servizio di attivazione host di Funzioni di Azure** non è in esecuzione, fare clic su **avvio del servizio**</span><span class="sxs-lookup"><span data-stu-id="b6c24-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Configurazione completata][11]

1. <span data-ttu-id="b6c24-154">Passare infine al **portale di runtime di Funzioni di Azure** come `https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="b6c24-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Portale][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png