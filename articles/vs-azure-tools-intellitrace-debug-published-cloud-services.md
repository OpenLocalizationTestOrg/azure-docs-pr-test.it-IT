---
title: Debug di un servizio cloud di Azure pubblicato con Visual Studio e IntelliTrace| Microsoft Docs
description: Informazioni su come eseguire il debug di un servizio cloud con Visual Studio e IntelliTrace
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
ms.openlocfilehash: 7905dfb97cbd7578a8422567fe674839d00c21ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="84e1a-103">Debug di un servizio cloud di Azure pubblicato con Visual Studio e IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="84e1a-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="84e1a-104">Con IntelliTrace è possibile registrare informazioni di debug approfondite per un'istanza del ruolo quando è in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="84e1a-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="84e1a-105">Se è necessario individuare la causa di un problema, è possibile usare i log di IntelliTrace per esaminare il codice da Visual Studio come se fosse in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="84e1a-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="84e1a-106">In effetti, IntelliTrace registra i dati fondamentali dell’esecuzione del codice e dell’ambiente quando l'applicazione Azure è in esecuzione come servizio cloud in Azure e consente di riprodurre i dati registrati da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84e1a-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span></span> 

<span data-ttu-id="84e1a-107">È possibile usare IntelliTrace se Visual Studio Enterprise è installato e l'applicazione Azure è destinata a .NET Framework 4 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="84e1a-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="84e1a-108">IntelliTrace raccoglie informazioni per i ruoli Azure.</span><span class="sxs-lookup"><span data-stu-id="84e1a-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="84e1a-109">Le macchine virtuali per questi ruoli eseguono sempre sistemi operativi a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="84e1a-109">The virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="84e1a-110">In alternativa, è possibile usare il [debug remoto](http://go.microsoft.com/fwlink/p/?LinkId=623041) per connettersi direttamente a un servizio cloud in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="84e1a-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84e1a-111">IntelliTrace è destinato esclusivamente a scenari di debug e non deve essere usato per una distribuzione di produzione.</span><span class="sxs-lookup"><span data-stu-id="84e1a-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="84e1a-112">Configurare un'applicazione Azure per IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="84e1a-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="84e1a-113">Per abilitare IntelliTrace per un'applicazione Azure, è necessario creare e pubblicare l'applicazione da un progetto Azure di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84e1a-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span></span> <span data-ttu-id="84e1a-114">È necessario configurare IntelliTrace per l'applicazione Azure prima di pubblicarla in Azure.</span><span class="sxs-lookup"><span data-stu-id="84e1a-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span></span> <span data-ttu-id="84e1a-115">Se si pubblica l'applicazione senza configurare IntelliTrace, è necessario ripubblicare il progetto.</span><span class="sxs-lookup"><span data-stu-id="84e1a-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span></span> <span data-ttu-id="84e1a-116">Per altre informazioni, vedere [Pubblicazione di progetti di servizi cloud di Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="84e1a-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="84e1a-117">Quando si è pronti distribuire l'applicazione Azure, verificare che le destinazioni di compilazione del progetto siano impostate su **Debug**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span></span>

1. <span data-ttu-id="84e1a-118">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="84e1a-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="84e1a-119">Nella finestra di dialogo **Pubblica applicazione Azure** selezionare la sottoscrizione di Azure e scegliere **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="84e1a-120">Nella pagina **Impostazioni** selezionare la scheda **Impostazioni avanzate**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-120">In the **Settings** page, select the **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="84e1a-121">Per raccogliere i log di IntelliTrace per l'applicazione quando viene pubblicata nel cloud, selezionare l'opzione **Abilita IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span></span>
   
1. <span data-ttu-id="84e1a-122">Per personalizzare la configurazione di base di IntelliTrace, selezionare **Impostazioni** accanto ad **Abilita IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span></span>

    ![Collegamento alle impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="84e1a-124">Nella finestra di dialogo **Impostazioni di IntelliTrace** è possibile specificare gli eventi da registrare, se si desidera raccogliere informazioni sulle chiamate, i moduli e i processi di cui raccogliere i log e quanto spazio allocare per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="84e1a-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span></span> <span data-ttu-id="84e1a-125">Per ulteriori informazioni su IntelliTrace, vedere [Debug con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="84e1a-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Impostazioni di IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="84e1a-127">Il log di IntelliTrace è un file di log circolare delle dimensioni massime specificate nelle impostazioni di IntelliTrace (le dimensioni predefinite sono 250 MB).</span><span class="sxs-lookup"><span data-stu-id="84e1a-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span></span> <span data-ttu-id="84e1a-128">I log di IntelliTrace vengono raccolti in un file nel file system della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="84e1a-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span></span> <span data-ttu-id="84e1a-129">Quando si richiedono i log, a questo punto uno snapshot viene creato e scaricato nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="84e1a-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span></span>

<span data-ttu-id="84e1a-130">Dopo che il servizio cloud di Azure è stato pubblicato in Azure, è possibile determinare se IntelliTrace è stato abilitato dal nodo di Azure in **Esplora server**, come illustrato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="84e1a-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span></span>

![Esplora server - IntelliTrace abilitato](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="84e1a-132">Scaricare i log di IntelliTrace per un'istanza del ruolo</span><span class="sxs-lookup"><span data-stu-id="84e1a-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="84e1a-133">Tramite Visual Studio, è possibile scaricare i log di IntelliTrace per un'istanza del ruolo attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="84e1a-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="84e1a-134">In **Esplora Server**, espandere il nodo **Servizi cloud** e quindi individuare l'istanza del ruolo di cui si desidera scaricare i log.</span><span class="sxs-lookup"><span data-stu-id="84e1a-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span></span> 

1. <span data-ttu-id="84e1a-135">Fare clic con il pulsante destro del mouse sull'istanza del ruolo e dal menu di scelta rapida scegliere **Visualizza log IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Opzione del menu Visualizza log IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="84e1a-137">I log di IntelliTrace vengono scaricati in un file in una directory nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="84e1a-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span></span> <span data-ttu-id="84e1a-138">Ogni volta che si richiedono i log di IntelliTrace, viene creato un nuovo snapshot.</span><span class="sxs-lookup"><span data-stu-id="84e1a-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="84e1a-139">Quando i log vengono scaricati, Visual Studio mostra lo stato di avanzamento dell'operazione nella finestra **Log attività di Azure**.</span><span class="sxs-lookup"><span data-stu-id="84e1a-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span></span> <span data-ttu-id="84e1a-140">Come illustrato nella figura riportata di seguito, è possibile espandere la voce dell'operazione per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="84e1a-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="84e1a-142">È possibile continuare a lavorare in Visual Studio durante il download dei log di IntelliTrace.</span><span class="sxs-lookup"><span data-stu-id="84e1a-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span></span> <span data-ttu-id="84e1a-143">Quando il download del log è terminato si apre automaticamente in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84e1a-143">When the log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="84e1a-144">I log di IntelliTrace possono contenere eccezioni generate e poi gestite dal framework.</span><span class="sxs-lookup"><span data-stu-id="84e1a-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span></span> <span data-ttu-id="84e1a-145">Codice interno del framework genera queste eccezioni come parte normale di avvio di un ruolo, pertanto può essere ignorato.</span><span class="sxs-lookup"><span data-stu-id="84e1a-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="84e1a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="84e1a-146">Next steps</span></span>
- [<span data-ttu-id="84e1a-147">Opzioni per il debug dei servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="84e1a-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="84e1a-148">Pubblicazione di un servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84e1a-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)