---
title: Connessione a un sistema SAP locale nelle App per la logica di Azure | Microsoft Docs
description: Connessione a un sistema SAP locale nel flusso di lavoro delle app per la logica attraverso il gateway dati locale
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="270f3-103">Connessione a un sistema SAP locale dalle app per la logica con il connettore SAP</span><span class="sxs-lookup"><span data-stu-id="270f3-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="270f3-104">Il gateway dati locale consente di gestire i dati e accedere in modo sicuro alle risorse presenti in locale.</span><span class="sxs-lookup"><span data-stu-id="270f3-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="270f3-105">Questo argomento illustra come collegare le app per la logica a un sistema SAP locale.</span><span class="sxs-lookup"><span data-stu-id="270f3-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="270f3-106">In questo esempio, l'app per la logica richiede un IDOC su HTTP e invia la risposta.</span><span class="sxs-lookup"><span data-stu-id="270f3-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="270f3-107">Limitazioni correnti:</span><span class="sxs-lookup"><span data-stu-id="270f3-107">Current limitations:</span></span> 
> - <span data-ttu-id="270f3-108">L'app per la logica va in timeout se tutti i passaggi necessari per la risposta non terminano entro il [limite di timeout della richiesta](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="270f3-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="270f3-109">In questo scenario, è possibile che le richieste vengano bloccate.</span><span class="sxs-lookup"><span data-stu-id="270f3-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="270f3-110">Il selettore file non consente di visualizzare tutti i campi disponibili.</span><span class="sxs-lookup"><span data-stu-id="270f3-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="270f3-111">In questo scenario, è possibile aggiungere manualmente i percorsi.</span><span class="sxs-lookup"><span data-stu-id="270f3-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="270f3-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="270f3-112">Prerequisites</span></span>

- <span data-ttu-id="270f3-113">Installare e configurare il [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127) più recente, versione 1.15.6150.1 o superiore.</span><span class="sxs-lookup"><span data-stu-id="270f3-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="270f3-114">L'articolo sulla [connessione al gateway dati locale in un'app per la logica](http://aka.ms/logicapps-gateway) elenca i passaggi da seguire.</span><span class="sxs-lookup"><span data-stu-id="270f3-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="270f3-115">Prima di procedere, è necessario installare il gateway in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="270f3-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="270f3-116">Scaricare e installare la libreria client SAP più recente nello stesso computer in cui è stato installato il gateway dati.</span><span class="sxs-lookup"><span data-stu-id="270f3-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="270f3-117">È possibile usare una delle versioni SAP seguenti:</span><span class="sxs-lookup"><span data-stu-id="270f3-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="270f3-118">Server SAP</span><span class="sxs-lookup"><span data-stu-id="270f3-118">SAP Server</span></span>
        - <span data-ttu-id="270f3-119">Qualsiasi Server SAP che supporti il connettore .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="270f3-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="270f3-120">Client SAP</span><span class="sxs-lookup"><span data-stu-id="270f3-120">SAP Client</span></span>
        - <span data-ttu-id="270f3-121">SAP Connettore .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="270f3-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="270f3-122">Aggiungere trigger e azioni per la connessione al sistema SAP</span><span class="sxs-lookup"><span data-stu-id="270f3-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="270f3-123">Il connettore SAP ha azioni, ma non trigger.</span><span class="sxs-lookup"><span data-stu-id="270f3-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="270f3-124">Di conseguenza, è necessario usare un altro trigger all'inizio del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="270f3-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="270f3-125">Aggiungere il trigger di richiesta/risposta e quindi selezionare **Nuovo passaggio**.</span><span class="sxs-lookup"><span data-stu-id="270f3-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="270f3-126">Selezionare **Aggiungi un'azione**, quindi selezionare il connettore SAP digitando `SAP` nel campo di ricerca:</span><span class="sxs-lookup"><span data-stu-id="270f3-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![Selezionare il server applicazioni o il server di messaggistica SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="270f3-128">Selezionare il [**server applicazioni SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o il [**server di messaggistica SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), in base alla configurazione SAP.</span><span class="sxs-lookup"><span data-stu-id="270f3-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="270f3-129">Se non è già disponibile una connessione, verrà richiesto di crearne una.</span><span class="sxs-lookup"><span data-stu-id="270f3-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="270f3-130">Selezionare **Connect via on-premises data gateway** (Connessione tramite gateway dati locale) e immettere i dettagli del sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="270f3-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Aggiungere la stringa di connessione a SAP](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="270f3-132">In **Gateway**, selezionare un gateway esistente o per installare un nuovo gateway, selezionare **Installa Gateway**.</span><span class="sxs-lookup"><span data-stu-id="270f3-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Installare un nuovo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="270f3-134">Dopo aver inserito tutti i dettagli, selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="270f3-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="270f3-135">Le app per la logica configurano ed eseguono il test della connessione, assicurandosi che funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="270f3-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="270f3-136">Inserire un nome per la connessione SAP.</span><span class="sxs-lookup"><span data-stu-id="270f3-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="270f3-137">Sono ora disponibili le diverse opzioni SAP.</span><span class="sxs-lookup"><span data-stu-id="270f3-137">The different SAP options are now available.</span></span> <span data-ttu-id="270f3-138">Per trovare la categoria IDOC, selezionarla dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="270f3-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="270f3-139">oppure digitare manualmente il percorso e selezionare la risposta HTTP nel campo **corpo**:</span><span class="sxs-lookup"><span data-stu-id="270f3-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![Azione SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="270f3-141">Aggiungere l'azione per la creazione di una **risposta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="270f3-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="270f3-142">Il messaggio di risposta deve derivare dall'output SAP.</span><span class="sxs-lookup"><span data-stu-id="270f3-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="270f3-143">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="270f3-143">Save your logic app.</span></span> <span data-ttu-id="270f3-144">Testarla inviando un IDOC tramite l'URL del trigger HTTP.</span><span class="sxs-lookup"><span data-stu-id="270f3-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="270f3-145">Dopo l'invio dell'IDOC, attendere la risposta dall'app per la logica:</span><span class="sxs-lookup"><span data-stu-id="270f3-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="270f3-146">Scoprire come [monitorare le app per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="270f3-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="270f3-147">Ora che il connettore SAP è stato aggiunto all'app per la logica, iniziare a esplorare altre funzionalità:</span><span class="sxs-lookup"><span data-stu-id="270f3-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="270f3-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="270f3-148">BAPI</span></span>
- <span data-ttu-id="270f3-149">RFC</span><span class="sxs-lookup"><span data-stu-id="270f3-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="270f3-150">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="270f3-150">Get help</span></span>

<span data-ttu-id="270f3-151">Per porre domande, fornire risposte e ottenere informazioni sulle attività degli altri utenti di App per la logica di Azure, vedere il [forum su App per la logica di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="270f3-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="270f3-152">Per contribuire al miglioramento delle App per la logica di Azure e dei connettori, votare o inviare idee al [sito dei commenti e suggerimenti degli utenti di App per la logica di Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="270f3-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="270f3-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="270f3-153">Next steps</span></span>

- <span data-ttu-id="270f3-154">Informazioni su come convalidare, trasformare e altre funzioni simili a BizTalk di [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="270f3-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="270f3-155">[Connettersi ai dati locali](../logic-apps/logic-apps-gateway-connection.md) dalle app per la logica</span><span class="sxs-lookup"><span data-stu-id="270f3-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
