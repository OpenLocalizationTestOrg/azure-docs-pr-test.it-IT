---
title: servizio con Visual Studio e IntelliTrace cloud di un report pubblicato un Azure aaaDebugging | Documenti Microsoft
description: Informazioni su come toodebug un cloud service con Visual Studio e IntelliTrace
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="9bcc9-103">Debug di un servizio cloud di Azure pubblicato con Visual Studio e IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="9bcc9-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="9bcc9-104">Con IntelliTrace è possibile registrare informazioni di debug approfondite per un'istanza del ruolo quando è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="9bcc9-105">Se è necessario a causa di hello toofind di un problema, è possibile utilizzare hello IntelliTrace registri toostep tramite il codice da Visual Studio come se fosse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="9bcc9-106">In effetti, i record codice chiave ambiente e sull'esecuzione dati IntelliTrace quando l'applicazione Azure è in esecuzione come servizio cloud in Azure e consente di riprodurre i dati di hello registrato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="9bcc9-107">È possibile usare IntelliTrace se Visual Studio Enterprise è installato e l'applicazione Azure è destinata a .NET Framework 4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="9bcc9-108">IntelliTrace raccoglie informazioni per i ruoli Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="9bcc9-109">macchine virtuali di Hello per questi ruoli sempre sistemi operativi a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="9bcc9-110">In alternativa, è possibile utilizzare [il debug remoto](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach direttamente tooa servizio cloud in cui è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9bcc9-111">IntelliTrace è destinato esclusivamente a scenari di debug e non deve essere usato per una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="9bcc9-112">Configurare un'applicazione Azure per IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="9bcc9-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="9bcc9-113">tooenable IntelliTrace per un'applicazione Azure, è necessario creare e pubblicare un'applicazione hello da un progetto Azure di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="9bcc9-114">È necessario configurare IntelliTrace per l'applicazione Azure prima di pubblicarla tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="9bcc9-115">Se si pubblica l'applicazione senza configurare IntelliTrace, è necessario progetto hello toorepublish.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="9bcc9-116">Per altre informazioni, vedere [Pubblicazione di progetti di servizi cloud di Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="9bcc9-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="9bcc9-117">Quando si è pronti a toodeploy l'applicazione Azure, verificare che le destinazioni di compilazione progetto siano impostate troppo**Debug**.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="9bcc9-118">In **Esplora**, fare clic sul progetto e selezionare il menu di scelta rapida hello **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="9bcc9-119">In hello **pubblica l'applicazione Azure** finestra di dialogo, seleziona hello sottoscrizione di Azure e scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="9bcc9-120">In hello **impostazioni** pagina, seleziona hello **impostazioni avanzate** scheda.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="9bcc9-121">Attivare hello **Abilita IntelliTrace** opzione toocollect i log di IntelliTrace per l'applicazione quando viene pubblicata nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="9bcc9-122">toocustomize hello IntelliTrace configurazione di base, selezionare **impostazioni** Avanti troppo**Abilita IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Collegamento alle impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="9bcc9-124">In hello **impostazioni IntelliTrace** finestra di dialogo, è possibile specificare quali toolog eventi, se toocollect chiamare informazioni, quali toocollect moduli e i processi di log per e quanta registrazione toohello tooallocate di spazio.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="9bcc9-125">Per ulteriori informazioni su IntelliTrace, vedere [Debug con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="9bcc9-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="9bcc9-127">log di IntelliTrace Hello è un file di log circolare delle dimensioni massime consentite di hello specificato nelle impostazioni di IntelliTrace hello (dimensione predefinita hello è 250 MB).</span><span class="sxs-lookup"><span data-stu-id="9bcc9-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="9bcc9-128">I log IntelliTrace vengono raccolti tooa file hello file System della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="9bcc9-129">Quando si richiedono i log di hello, uno snapshot viene portato a questo punto nel tempo e scaricati tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="9bcc9-130">Dopo è stato pubblicato tooAzure hello servizio cloud di Azure, è possibile determinare se è stato abilitato IntelliTrace da hello Azure nodo **Esplora Server**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="9bcc9-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Esplora server - IntelliTrace abilitato](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="9bcc9-132">Scaricare i log di IntelliTrace per un'istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="9bcc9-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="9bcc9-133">Tramite Visual Studio, è possibile scaricare i log di IntelliTrace per un'istanza del ruolo attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9bcc9-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="9bcc9-134">In **Esplora Server**, espandere hello **servizi Cloud** nodo, quindi individuare l'istanza del ruolo i cui log si desidera toodownload.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="9bcc9-135">Istanza del ruolo hello e dal menu di scelta rapida hello s, scegliere **Visualizza log IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Opzione del menu Visualizza log IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="9bcc9-137">i log di IntelliTrace Hello sono tooa scaricato i file in una directory sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="9bcc9-138">Ogni volta che si richiede il log di IntelliTrace hello, viene creato un nuovo snapshot.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="9bcc9-139">Mentre vengono scaricati i registri di hello, Visual Studio consente di visualizzare lo stato di avanzamento hello dell'operazione di hello in hello **Log attività Azure** finestra.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="9bcc9-140">Come illustrato nella seguente illustrazione hello, è possibile espandere voce di riga hello hello operazione toosee maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="9bcc9-142">È possibile continuare toowork in Visual Studio durante il download dei log di IntelliTrace hello.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="9bcc9-143">Quando il log di hello ha completato il download, viene aperto in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="9bcc9-144">Hello log IntelliTrace possono contenere eccezioni tale framework hello genera e gestisce in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="9bcc9-145">Codice interno del framework genera queste eccezioni come parte normale di avvio di un ruolo, pertanto può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="9bcc9-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9bcc9-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bcc9-146">Next steps</span></span>
- [<span data-ttu-id="9bcc9-147">Opzioni per il debug dei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="9bcc9-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="9bcc9-148">Pubblicazione di un servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9bcc9-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)