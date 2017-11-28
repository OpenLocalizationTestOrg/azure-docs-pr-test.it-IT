---
title: Connettersi a file system locali dalle app per la logica di Azure | Microsoft Docs
description: Connettersi a file system locali dal flusso di lavoro dell'app per la logica tramite il gateway dati locale e il connettore File System
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
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="86a39-104">Connettersi a file system locali dalle app per la logica con il connettore File System</span><span class="sxs-lookup"><span data-stu-id="86a39-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="86a39-105">La connettività cloud ibrida è basilare per le app per la logica. In questo modo le app per la logica possono gestire i dati e accedere in modo sicuro alla risorse locali usando il gateway dati locale.</span><span class="sxs-lookup"><span data-stu-id="86a39-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="86a39-106">Questo articolo descrive come connettersi a un file system locale presentando uno scenario semplice: copiare un file caricato in Dropbox in una condivisione file e successivamente inviare un messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="86a39-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a39-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="86a39-107">Prerequisites</span></span>

- <span data-ttu-id="86a39-108">Installare e configurare il [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127) più recente.</span><span class="sxs-lookup"><span data-stu-id="86a39-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="86a39-109">Installare il gateway dati locale più recente, versione 1.15.6150.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="86a39-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="86a39-110">[Connessione al gateway dati locale](http://aka.ms/logicapps-gateway) elenca i passaggi.</span><span class="sxs-lookup"><span data-stu-id="86a39-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="86a39-111">Prima di procedere con il resto della procedura, è necessario installare il gateway in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="86a39-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="86a39-112">Aggiungere trigger e azioni per la connessione al file system</span><span class="sxs-lookup"><span data-stu-id="86a39-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="86a39-113">Creare un'app per la logica e aggiungere il trigger Dropbox: **Quando viene creato un file**</span><span class="sxs-lookup"><span data-stu-id="86a39-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="86a39-114">Nel trigger scegliere **Passaggio successivo** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="86a39-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="86a39-115">Nella casella di ricerca, immettere `file system` in modo da visualizzare tutte le azioni supportate per il connettore File System.</span><span class="sxs-lookup"><span data-stu-id="86a39-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Cercare il connettore file](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="86a39-117">Scegliere l'azione **Crea file** e creare una connessione al file system.</span><span class="sxs-lookup"><span data-stu-id="86a39-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="86a39-118">Se non è già disponibile una connessione, verrà richiesto di crearne una.</span><span class="sxs-lookup"><span data-stu-id="86a39-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="86a39-119">Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale).</span><span class="sxs-lookup"><span data-stu-id="86a39-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="86a39-120">Vengono visualizzare altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="86a39-120">More properties appear.</span></span>
   2. <span data-ttu-id="86a39-121">Selezionare la cartella radice per il file system.</span><span class="sxs-lookup"><span data-stu-id="86a39-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="86a39-122">La cartella radice è la cartella principale che verrà usata per i percorsi relativi di tutte le azioni correlate ai file.</span><span class="sxs-lookup"><span data-stu-id="86a39-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="86a39-123">È possibile specificare una cartella locale del computer in cui è installato il gateway dati locale oppure la cartella può essere una condivisione di rete a cui il computer ha accesso.</span><span class="sxs-lookup"><span data-stu-id="86a39-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="86a39-124">Immettere il nome utente e la password del gateway.</span><span class="sxs-lookup"><span data-stu-id="86a39-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="86a39-125">Selezionare il gateway installato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86a39-125">Select the gateway that you previously installed.</span></span>

       ![Configurare la connessione](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="86a39-127">Dopo aver specificato tutti i dettagli, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="86a39-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="86a39-128">Le app per la logica configurano ed eseguono il test della connessione, assicurandosi che funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="86a39-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="86a39-129">Se la connessione è configurata correttamente, vengono visualizzate le opzioni per l'azione selezionata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="86a39-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="86a39-130">Il connettore del file system sarà pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="86a39-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="86a39-131">Specificare che si desidera copiare i file da Dropbox nella cartella radice per la condivisione di file locale.</span><span class="sxs-lookup"><span data-stu-id="86a39-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Azione Crea file](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="86a39-133">Dopo che l'app per la logica ha copiato il file, aggiungere un'azione di Outlook che invia un messaggio di posta elettronica che informa gli utenti del nuovo file.</span><span class="sxs-lookup"><span data-stu-id="86a39-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="86a39-134">Immettere i destinatari, il titolo e il corpo del messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="86a39-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="86a39-135">Nel selettore di contenuto dinamico, è possibile scegliere output di dati dal connettore di file per aggiungere altri dettagli al messaggio di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="86a39-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Azione Invia e-mail](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="86a39-137">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="86a39-137">Save your logic app.</span></span> <span data-ttu-id="86a39-138">Eseguire il test dell'app caricando un file in Dropbox.</span><span class="sxs-lookup"><span data-stu-id="86a39-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="86a39-139">Il file dovrebbe essere copiato nella condivisione di file locale e si dovrebbe ricevere il relativo messaggio di posta elettronica di notifica.</span><span class="sxs-lookup"><span data-stu-id="86a39-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="86a39-140">Informazioni su come [monitorare le app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="86a39-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="86a39-141">A questo punto, si disporrà di un'app per la logica funzionante che può connettersi al file system locale.</span><span class="sxs-lookup"><span data-stu-id="86a39-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="86a39-142">Provare a esplorare altre funzionalità del connettore, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="86a39-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="86a39-143">Crea file</span><span class="sxs-lookup"><span data-stu-id="86a39-143">Create file</span></span>
- <span data-ttu-id="86a39-144">Elenca i file nella cartella</span><span class="sxs-lookup"><span data-stu-id="86a39-144">List files in folder</span></span>
- <span data-ttu-id="86a39-145">Aggiungi file</span><span class="sxs-lookup"><span data-stu-id="86a39-145">Append file</span></span>
- <span data-ttu-id="86a39-146">Elimina file</span><span class="sxs-lookup"><span data-stu-id="86a39-146">Delete file</span></span>
- <span data-ttu-id="86a39-147">Recupera contenuto di file</span><span class="sxs-lookup"><span data-stu-id="86a39-147">Get file content</span></span>
- <span data-ttu-id="86a39-148">Recupera contenuto di file tramite percorso</span><span class="sxs-lookup"><span data-stu-id="86a39-148">Get file content using path</span></span>
- <span data-ttu-id="86a39-149">Recupera metadati di file</span><span class="sxs-lookup"><span data-stu-id="86a39-149">Get file metadata</span></span>
- <span data-ttu-id="86a39-150">Recupera metadati di file tramite percorso</span><span class="sxs-lookup"><span data-stu-id="86a39-150">Get file metadata using path</span></span>
- <span data-ttu-id="86a39-151">Elenca i file nella cartella radice</span><span class="sxs-lookup"><span data-stu-id="86a39-151">List files in root folder</span></span>
- <span data-ttu-id="86a39-152">Aggiorna file</span><span class="sxs-lookup"><span data-stu-id="86a39-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="86a39-153">Visualizzare il file Swagger</span><span class="sxs-lookup"><span data-stu-id="86a39-153">View the swagger</span></span>
<span data-ttu-id="86a39-154">Vedere i [dettagli del file Swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="86a39-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="86a39-155">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="86a39-155">Get help</span></span>

<span data-ttu-id="86a39-156">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti di App per la logica di Azure, vedere il [forum su App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="86a39-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="86a39-157">Per contribuire al miglioramento delle App per la logica di Azure e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti di App per la logica di Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="86a39-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a39-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86a39-158">Next steps</span></span>

- <span data-ttu-id="86a39-159">[Connettersi ai dati locali](../logic-apps/logic-apps-gateway-connection.md) dalle app per la logica</span><span class="sxs-lookup"><span data-stu-id="86a39-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="86a39-160">Informazioni su [Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="86a39-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
