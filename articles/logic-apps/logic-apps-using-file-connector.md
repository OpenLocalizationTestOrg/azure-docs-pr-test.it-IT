---
title: aaaConnect tooon locale file System da Azure logica App | Documenti Microsoft
description: Connettere i sistemi di file locali tooon dal flusso di lavoro logica app tramite gateway dati locale di hello e connettore File System
keywords: file system
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="b0bf9-104">Connettere i sistemi di file locale tooon logica App con connettore File System hello</span><span class="sxs-lookup"><span data-stu-id="b0bf9-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="b0bf9-105">Connettività di cloud ibrido è App toologic centrale, in tal caso toomanage dati e in modo sicuro l'accesso risorse locali, App per la logica è possibile usare gateway dati locale di hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="b0bf9-106">In questo articolo viene illustrata la modalità tooconnect tooan locale file system con uno scenario di base: copiare un file che tooa tooDropbox caricato condivisione file, quindi inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0bf9-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b0bf9-107">Prerequisites</span></span>

- <span data-ttu-id="b0bf9-108">Installare e configurare più recente hello [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="b0bf9-109">Installare hello gateway dati più recenti in locale, versione 1.15.6150.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="b0bf9-110">[Connessione gateway dati locale di toohello](http://aka.ms/logicapps-gateway) elenchi hello passaggi.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="b0bf9-111">gateway di Hello deve essere installato in un computer locale prima di continuare con il resto di hello dei passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="b0bf9-112">Aggiungere trigger e le azioni per la connessione a system file tooyour</span><span class="sxs-lookup"><span data-stu-id="b0bf9-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="b0bf9-113">Creare un'app per la logica e aggiungere il trigger Dropbox: **Quando viene creato un file**</span><span class="sxs-lookup"><span data-stu-id="b0bf9-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="b0bf9-114">In trigger hello, scegliere **passaggio successivo** > **aggiungere un'azione**.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="b0bf9-115">Nella casella di ricerca hello, immettere `file system` in modo da visualizzare azioni tutte supportate per il connettore File System hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Cercare il connettore file](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="b0bf9-117">Scegliere hello **crea file** action e creare un file system tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="b0bf9-118">Se non si dispone di una connessione esistente, verrà richiesta toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="b0bf9-119">Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="b0bf9-120">Vengono visualizzare altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-120">More properties appear.</span></span>
   2. <span data-ttu-id="b0bf9-121">Selezionare la cartella radice per il file system.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="b0bf9-122">cartella radice Hello è la cartella padre principale di hello, che viene utilizzata per i percorsi relativi per tutte le azioni relative ai file.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="b0bf9-123">È possibile specificare una cartella locale nel computer di hello in cui è installato gateway dati locale di hello o cartella hello può essere una condivisione di rete che hello computer può accedere.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="b0bf9-124">Immettere nome utente hello e una password per gateway hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="b0bf9-125">Selezionare il gateway hello installata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-125">Select hello gateway that you previously installed.</span></span>

       ![Configurare la connessione](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="b0bf9-127">Dopo aver fornito tutti i dettagli di hello, scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="b0bf9-128">Logica App Configura e testa la connessione, assicurarsi che la connessione hello funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="b0bf9-129">Se la connessione hello è configurata correttamente, si noterà opzioni per l'azione di hello selezionata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="b0bf9-130">connettore file system di Hello è ora pronto per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="b0bf9-131">Specificare che si desidera file toocopy Dropbox toohello nella cartella radice per la condivisione di file locale.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Azione Crea file](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="b0bf9-133">Dopo la logica app copie hello file, aggiungere un'azione di Outlook che invia un messaggio di posta elettronica in modo che gli utenti sul nuovo file hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="b0bf9-134">Immettere i destinatari hello, titolo e il corpo del messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="b0bf9-135">Nel selettore contenuto dinamico hello, è possibile scegliere gli output di dati dal connettore file hello, pertanto è possibile aggiungere ulteriori posta elettronica toohello di dettagli.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![Azione Invia e-mail](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="b0bf9-137">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-137">Save your logic app.</span></span> <span data-ttu-id="b0bf9-138">Testare l'app caricando un file tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="b0bf9-139">file Hello deve ottenere toohello copiati in una condivisione locale e dovrebbe essere visualizzato un messaggio di posta elettronica sull'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="b0bf9-140">Informazioni su come troppo[monitorare App per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="b0bf9-141">Congratulazioni, ora è un'app di logica di lavoro che può connettersi tooyour nel file sistema locale.</span><span class="sxs-lookup"><span data-stu-id="b0bf9-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="b0bf9-142">Provare a esplorare altre funzionalità che hello connettore offerte, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b0bf9-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="b0bf9-143">Crea file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-143">Create file</span></span>
- <span data-ttu-id="b0bf9-144">Elenca i file nella cartella</span><span class="sxs-lookup"><span data-stu-id="b0bf9-144">List files in folder</span></span>
- <span data-ttu-id="b0bf9-145">Aggiungi file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-145">Append file</span></span>
- <span data-ttu-id="b0bf9-146">Elimina file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-146">Delete file</span></span>
- <span data-ttu-id="b0bf9-147">Recupera contenuto di file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-147">Get file content</span></span>
- <span data-ttu-id="b0bf9-148">Recupera contenuto di file tramite percorso</span><span class="sxs-lookup"><span data-stu-id="b0bf9-148">Get file content using path</span></span>
- <span data-ttu-id="b0bf9-149">Recupera metadati di file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-149">Get file metadata</span></span>
- <span data-ttu-id="b0bf9-150">Recupera metadati di file tramite percorso</span><span class="sxs-lookup"><span data-stu-id="b0bf9-150">Get file metadata using path</span></span>
- <span data-ttu-id="b0bf9-151">Elenca i file nella cartella radice</span><span class="sxs-lookup"><span data-stu-id="b0bf9-151">List files in root folder</span></span>
- <span data-ttu-id="b0bf9-152">Aggiorna file</span><span class="sxs-lookup"><span data-stu-id="b0bf9-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="b0bf9-153">Swagger hello vista</span><span class="sxs-lookup"><span data-stu-id="b0bf9-153">View hello swagger</span></span>
<span data-ttu-id="b0bf9-154">Vedere hello [swagger dettagli](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="b0bf9-155">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="b0bf9-155">Get help</span></span>

<span data-ttu-id="b0bf9-156">rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="b0bf9-157">toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b0bf9-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0bf9-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0bf9-158">Next steps</span></span>

- <span data-ttu-id="b0bf9-159">[Connettere i dati locali tooon](../logic-apps/logic-apps-gateway-connection.md) da logica App</span><span class="sxs-lookup"><span data-stu-id="b0bf9-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="b0bf9-160">Informazioni su [Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b0bf9-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
