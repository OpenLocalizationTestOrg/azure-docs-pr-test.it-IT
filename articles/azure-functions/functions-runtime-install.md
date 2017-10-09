---
title: Funzioni di Runtime Installation aaaAzure | Documenti Microsoft
description: Come tooInstall hello Azure funzioni di Runtime
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
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="30e04-103">Installare l'anteprima del Runtime di Azure funzioni hello</span><span class="sxs-lookup"><span data-stu-id="30e04-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="30e04-104">Se si desidera anteprima di Azure funzioni Runtime hello tooinstall, è necessario seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="30e04-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="30e04-105">Verificare che il computer passa i requisiti minimi di hello</span><span class="sxs-lookup"><span data-stu-id="30e04-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="30e04-106">Scaricare hello [programma di installazione di Azure funzioni Runtime Preview](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="30e04-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="30e04-107">Installare l'anteprima di Azure funzioni Runtime hello</span><span class="sxs-lookup"><span data-stu-id="30e04-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="30e04-108">Configurazione di hello completa dell'anteprima di Azure funzioni Runtime hello</span><span class="sxs-lookup"><span data-stu-id="30e04-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30e04-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="30e04-109">Prerequisites</span></span>

<span data-ttu-id="30e04-110">Prima di installare l'anteprima di Azure funzioni Runtime hello, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="30e04-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="30e04-111">Un computer che esegue Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).</span><span class="sxs-lookup"><span data-stu-id="30e04-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="30e04-112">Un'istanza di SQL Server in esecuzione all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="30e04-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="30e04-113">L'edizione minima richiesta è SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="30e04-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="30e04-114">Installare l'anteprima del Runtime di Azure funzioni hello</span><span class="sxs-lookup"><span data-stu-id="30e04-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="30e04-115">il programma di installazione di Hello Azure funzioni Runtime preview semplificato installazione hello di anteprima di Azure funzioni Runtime hello gestione e i ruoli di lavoro.</span><span class="sxs-lookup"><span data-stu-id="30e04-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="30e04-116">È possibile tooinstall hello gestione e il ruolo di lavoro su hello nello stesso computer.</span><span class="sxs-lookup"><span data-stu-id="30e04-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="30e04-117">Tuttavia, quando si aggiungono altre funzioni, è necessario distribuire più ruoli di lavoro su computer aggiuntivi toobe in grado di tooscale delle funzioni in più thread di lavoro.</span><span class="sxs-lookup"><span data-stu-id="30e04-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="30e04-118">Installare Gestione hello e ruolo di lavoro in hello nello stesso computer</span><span class="sxs-lookup"><span data-stu-id="30e04-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="30e04-119">Eseguire installazione di anteprima di Azure funzioni Runtime hello.</span><span class="sxs-lookup"><span data-stu-id="30e04-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure][1]

1. <span data-ttu-id="30e04-121">**Fare clic su Avanti** avanzare oltre hello prima fase del programma di installazione hello</span><span class="sxs-lookup"><span data-stu-id="30e04-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="30e04-122">Dopo avere letto le condizioni di hello di hello **EULA**, **hello casella di controllo** termini hello tooaccept e **fare clic su Avanti** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="30e04-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="30e04-123">Ora selezionare hello ruoli si desidera tooinstall su questo computer **ruolo di gestione delle funzioni** e/o **il ruolo di lavoro funzioni** e **fare clic su Avanti**</span><span class="sxs-lookup"><span data-stu-id="30e04-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Selezione del ruolo][3]

    > [!NOTE]
    > <span data-ttu-id="30e04-125">È possibile installare hello **il ruolo di lavoro funzioni** in molti altri toodo macchine in tal caso, seguire queste istruzioni e selezionare solo **il ruolo di lavoro funzioni** nel programma di installazione hello.</span><span class="sxs-lookup"><span data-stu-id="30e04-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="30e04-126">**Fare clic su Avanti** toohave hello **il programma di installazione di Azure funzioni Runtime** installare nel computer.</span><span class="sxs-lookup"><span data-stu-id="30e04-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="30e04-127">Dopo l'installazione completa di hello avvierà hello **dello strumento di configurazione di Runtime di Azure funzioni**.</span><span class="sxs-lookup"><span data-stu-id="30e04-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Completato][5]

    > [!NOTE]
    > <span data-ttu-id="30e04-129">Se si sta installando in **Windows 10** hello e **contenitore** funzionalità non è stata precedentemente abilitata, hello **Azure funzioni Runtime** programma di installazione richiederà tooreboot installare il hello toocomplete macchina.</span><span class="sxs-lookup"><span data-stu-id="30e04-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="30e04-130">Configurare hello Azure funzioni di Runtime</span><span class="sxs-lookup"><span data-stu-id="30e04-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="30e04-131">toocomplete hello Azure funzioni Runtime installazione è necessario completare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="30e04-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="30e04-132">Hello **strumento di configurazione di Azure funzioni Runtime** Mostra quali ruoli sono installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="30e04-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Strumento di configurazione][6]

1. <span data-ttu-id="30e04-134">Fare clic su hello **Database** , immettere hello **dettagli di connessione per l'istanza di SQL Server** e **fare clic su Applica**.</span><span class="sxs-lookup"><span data-stu-id="30e04-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="30e04-135">Questa operazione è necessaria in ordine toohello Azure funzioni Runtime toocreate un hello toosupport database Runtime.</span><span class="sxs-lookup"><span data-stu-id="30e04-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Anteprima del runtime di Funzioni di Azure - Configurazione del database][7]

1. <span data-ttu-id="30e04-137">Fare clic su hello **credenziali** scheda.  In questa schermata è necessario creare due nuove credenziali per l'uso con una condivisione file per l'hosting di tutte le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="30e04-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="30e04-138">**Specificare nome utente e Password** combinazioni per hello **proprietario condivisione File** e per hello **utente condivisione File** e fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="30e04-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Credenziali][8]

1. <span data-ttu-id="30e04-140">Fare clic su hello **condivisione File** scheda.  In questa schermata è necessario specificare i dettagli di hello di hello **percorso di condivisione File**.</span><span class="sxs-lookup"><span data-stu-id="30e04-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="30e04-141">È possibile creare la condivisione file o usare una condivisione file esistente e fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="30e04-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="30e04-142">Se si seleziona un nuovo percorso di condivisione File, è necessario specificare una directory per l'utilizzo da hello Azure funzioni di Runtime.</span><span class="sxs-lookup"><span data-stu-id="30e04-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Anteprima del runtime di Funzioni di Azure - Condivisione file][9]

1. <span data-ttu-id="30e04-144">Fare clic su hello **IIS** scheda.  Questa scheda Mostra i dettagli di hello di siti Web di hello in IIS che hello Azure funzioni Runtime installazione creeranno.</span><span class="sxs-lookup"><span data-stu-id="30e04-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="30e04-145">**Fare clic su Applica** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="30e04-145">**Click Apply** toocomplete.</span></span>

    ![Anteprima del runtime di Funzioni di Azure - IIS][10]

1. <span data-ttu-id="30e04-147">Fare clic su hello **servizi** scheda.  Questa scheda Mostra stato hello dei servizi di hello nell'installazione di Runtime di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="30e04-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="30e04-148">Se dopo hello configurazione iniziale **servizio di attivazione di Azure funzioni Host** non è in esecuzione fare clic su **avvio del servizio**</span><span class="sxs-lookup"><span data-stu-id="30e04-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Anteprima del runtime di Funzioni di Azure - Configurazione completata][11]

1. <span data-ttu-id="30e04-150">Passare infine toohello **portale di Azure funzioni Runtime** come`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="30e04-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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