---
title: aaaConnect tooan locale sistema SAP in Azure logica App | Documenti Microsoft
description: La connessione di sistema SAP locale di tooan dal flusso di lavoro logica app tramite gateway dati locale di hello
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
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="5bff5-103">Connettersi sistema SAP di tooan locale da App per la logica con connettore SAP hello</span><span class="sxs-lookup"><span data-stu-id="5bff5-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="5bff5-104">gateway dati locale di Hello consente dati toomanage e accedere in modo sicuro le risorse in locale.</span><span class="sxs-lookup"><span data-stu-id="5bff5-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="5bff5-105">In questo argomento viene illustrato come collegare il sistema SAP locale di logica App tooan.</span><span class="sxs-lookup"><span data-stu-id="5bff5-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="5bff5-106">In questo esempio, la logica app richiede un IDOC su HTTP e Invia risposta hello.</span><span class="sxs-lookup"><span data-stu-id="5bff5-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="5bff5-107">Limitazioni correnti:</span><span class="sxs-lookup"><span data-stu-id="5bff5-107">Current limitations:</span></span> 
> - <span data-ttu-id="5bff5-108">Logica app timeout se tutti i passaggi necessari per la risposta hello non completano entro hello [il limite di timeout della richiesta](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="5bff5-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="5bff5-109">In questo scenario, è possibile che le richieste vengano bloccate.</span><span class="sxs-lookup"><span data-stu-id="5bff5-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="5bff5-110">selettore file Hello non vengono visualizzati tutti i campi disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="5bff5-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="5bff5-111">In questo scenario, è possibile aggiungere manualmente i percorsi.</span><span class="sxs-lookup"><span data-stu-id="5bff5-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bff5-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5bff5-112">Prerequisites</span></span>

- <span data-ttu-id="5bff5-113">Installare e configurare più recente hello [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127) versione 1.15.6150.1 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5bff5-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="5bff5-114">[Come tooconnect toohello sul gateway dati locale in un'app di logica](http://aka.ms/logicapps-gateway) elenchi hello passaggi.</span><span class="sxs-lookup"><span data-stu-id="5bff5-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="5bff5-115">gateway di Hello deve essere installato in un computer locale prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="5bff5-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="5bff5-116">Download e installazione hello più recente SAP libreria client in hello stesso computer in cui è installato gateway dati hello.</span><span class="sxs-lookup"><span data-stu-id="5bff5-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="5bff5-117">Utilizzare una delle seguenti versioni SAP hello:</span><span class="sxs-lookup"><span data-stu-id="5bff5-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="5bff5-118">Server SAP</span><span class="sxs-lookup"><span data-stu-id="5bff5-118">SAP Server</span></span>
        - <span data-ttu-id="5bff5-119">Qualsiasi Server SAP che hello supporto .NET Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="5bff5-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="5bff5-120">Client SAP</span><span class="sxs-lookup"><span data-stu-id="5bff5-120">SAP Client</span></span>
        - <span data-ttu-id="5bff5-121">SAP Connettore .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="5bff5-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="5bff5-122">Aggiungere i trigger e le azioni per la connessione del sistema SAP tooyour</span><span class="sxs-lookup"><span data-stu-id="5bff5-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="5bff5-123">connettore SAP Hello ha azioni, ma non i trigger.</span><span class="sxs-lookup"><span data-stu-id="5bff5-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="5bff5-124">In tal caso, abbiamo toouse un altro trigger all'inizio di hello del flusso di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="5bff5-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="5bff5-125">Aggiungere trigger di richiesta/risposta hello e quindi selezionare **nuovo passaggio**.</span><span class="sxs-lookup"><span data-stu-id="5bff5-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="5bff5-126">Selezionare **aggiungere un'azione**, quindi selezionare il connettore SAP hello digitando `SAP` nel campo di ricerca hello:</span><span class="sxs-lookup"><span data-stu-id="5bff5-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Selezionare il server applicazioni o il server di messaggistica SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="5bff5-128">Selezionare il [**server applicazioni SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) o il [**server di messaggistica SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), in base alla configurazione SAP.</span><span class="sxs-lookup"><span data-stu-id="5bff5-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="5bff5-129">Se non si dispone di una connessione esistente, verrà richiesta toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="5bff5-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="5bff5-130">Selezionare **Connetti tramite il gateway dati locale**e immettere i dettagli di hello per il sistema SAP:</span><span class="sxs-lookup"><span data-stu-id="5bff5-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Aggiungere tooSAP di stringa di connessione](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="5bff5-132">In **Gateway**, selezionare un gateway esistente o un nuovo gateway tooinstall, **installare Gateway**.</span><span class="sxs-lookup"><span data-stu-id="5bff5-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Installare un nuovo gateway](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="5bff5-134">Dopo avere immesso tutti i dettagli di hello, selezionare **crea**.</span><span class="sxs-lookup"><span data-stu-id="5bff5-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="5bff5-135">Logica App Configura e testa connessione hello, assicurandosi che la connessione hello funziona correttamente.</span><span class="sxs-lookup"><span data-stu-id="5bff5-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="5bff5-136">Inserire un nome per la connessione SAP.</span><span class="sxs-lookup"><span data-stu-id="5bff5-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="5bff5-137">diverse opzioni di SAP Hello sono ora disponibili.</span><span class="sxs-lookup"><span data-stu-id="5bff5-137">hello different SAP options are now available.</span></span> <span data-ttu-id="5bff5-138">toofind la categoria IDOC, seleziona dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="5bff5-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="5bff5-139">O digitare manualmente il percorso di hello e risposta hello selezionare HTTP nell'hello **corpo** campo:</span><span class="sxs-lookup"><span data-stu-id="5bff5-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Azione SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="5bff5-141">Aggiungere l'azione di hello per la creazione di un **risposta HTTP**.</span><span class="sxs-lookup"><span data-stu-id="5bff5-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="5bff5-142">messaggio di risposta Hello deve essere dall'output di hello SAP.</span><span class="sxs-lookup"><span data-stu-id="5bff5-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="5bff5-143">Salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="5bff5-143">Save your logic app.</span></span> <span data-ttu-id="5bff5-144">Test inviando un IDOC tramite URL trigger hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="5bff5-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="5bff5-145">Dopo la hello che viene inviato l'IDOC, attendere la risposta hello da hello logica app:</span><span class="sxs-lookup"><span data-stu-id="5bff5-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="5bff5-146">Estrarre come troppo[monitorare App per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="5bff5-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="5bff5-147">Connettore SAP hello viene aggiunta la tooyour logica app, iniziare a esplorare altre funzionalità:</span><span class="sxs-lookup"><span data-stu-id="5bff5-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="5bff5-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="5bff5-148">BAPI</span></span>
- <span data-ttu-id="5bff5-149">RFC</span><span class="sxs-lookup"><span data-stu-id="5bff5-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="5bff5-150">Ottenere aiuto</span><span class="sxs-lookup"><span data-stu-id="5bff5-150">Get help</span></span>

<span data-ttu-id="5bff5-151">rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="5bff5-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="5bff5-152">toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="5bff5-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bff5-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5bff5-153">Next steps</span></span>

- <span data-ttu-id="5bff5-154">Informazioni su come toovalidate, trasformazione e altre funzioni simili a BizTalk hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bff5-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="5bff5-155">[Connettere i dati locali tooon](../logic-apps/logic-apps-gateway-connection.md) da logica App</span><span class="sxs-lookup"><span data-stu-id="5bff5-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
