---
title: Informazioni su come usare il connettore FTP nelle app per la logica | Documentazione Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi a un server FTP per gestire i file. Nel server FTP è possibile eseguire varie azioni, ad esempio creare, aggiornare, ottenere ed eliminare file."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="dae2b-105">Introduzione al connettore FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-105">Get started with the FTP connector</span></span>
<span data-ttu-id="dae2b-106">Usare il connettore FTP per monitorare, gestire e creare file in un server FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="dae2b-107">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="dae2b-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="dae2b-108">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dae2b-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="dae2b-109">Connettersi a FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-109">Connect to FTP</span></span>
<span data-ttu-id="dae2b-110">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="dae2b-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="dae2b-111">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="dae2b-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="dae2b-112">Creare una connessione a FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="dae2b-113">Usare un trigger FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-113">Use a FTP trigger</span></span>
<span data-ttu-id="dae2b-114">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="dae2b-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="dae2b-115">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="dae2b-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="dae2b-116">Il connettore FTP richiede un server FTP che sia accessibile da Internet e sia configurato per operare con la modalità passiva.</span><span class="sxs-lookup"><span data-stu-id="dae2b-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="dae2b-117">Il connettore FTP, inoltre, **non è compatibile con FTPS implicito (FTP su SSL)**.</span><span class="sxs-lookup"><span data-stu-id="dae2b-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="dae2b-118">Il connettore FTP supporta solo FTPS esplicito (FTP su SSL).</span><span class="sxs-lookup"><span data-stu-id="dae2b-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="dae2b-119">Questo esempio spiega come usare il trigger **FTP - Quando viene aggiunto o modificato un file** per avviare un flusso di lavoro dell'app per la logica quando viene aggiunto o modificato un file in un server FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="dae2b-120">In un esempio riguardante un'organizzazione si potrebbe usare questo trigger per monitorare una cartella FTP per nuovi file di ordini dei clienti.</span><span class="sxs-lookup"><span data-stu-id="dae2b-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="dae2b-121">È quindi possibile usare un'azione connettore FTP come **Recuperare i contenuti del file** per recuperare il contenuto dell'ordine per elaborarlo ulteriormente e archiviarlo nel database degli ordini.</span><span class="sxs-lookup"><span data-stu-id="dae2b-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="dae2b-122">Immettere *ftp* nella casella di ricerca della finestra di progettazione delle app per la logica, quindi selezionare il trigger **FTP - Quando viene aggiunto o modificato un file**</span><span class="sxs-lookup"><span data-stu-id="dae2b-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="dae2b-123">![Immagine di trigger FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="dae2b-124">Il controllo **Quando viene aggiunto o modificato un file** viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="dae2b-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="dae2b-125">![Immagine di trigger FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="dae2b-126">Selezionare **...** sul lato destro del controllo.</span><span class="sxs-lookup"><span data-stu-id="dae2b-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="dae2b-127">Viene visualizzato il controllo di selezione della cartella.</span><span class="sxs-lookup"><span data-stu-id="dae2b-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="dae2b-128">![Immagine di trigger FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="dae2b-129">Selezionare **>** (freccia destra) e individuare la cartella da monitorare per rilevare i file nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="dae2b-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="dae2b-130">Selezionare la cartella e notare che ora è visualizzata nel controllo **Cartella**.</span><span class="sxs-lookup"><span data-stu-id="dae2b-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="dae2b-131">![Immagine di trigger FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="dae2b-132">A questo punto, l’app per la logica è stata configurata con un trigger che avvierà l'esecuzione di altri trigger e altre azioni nel flusso di lavoro quando un file viene modificato o creato nella cartella FTP specificata.</span><span class="sxs-lookup"><span data-stu-id="dae2b-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="dae2b-133">Affinché sia funzionale, l'app per la logica deve contenere almeno un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="dae2b-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="dae2b-134">Seguire i passaggi nella sezione successiva per aggiungere un'azione.</span><span class="sxs-lookup"><span data-stu-id="dae2b-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="dae2b-135">Usare un'azione FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-135">Use a FTP action</span></span>
<span data-ttu-id="dae2b-136">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="dae2b-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="dae2b-137">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="dae2b-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="dae2b-138">Dopo aver aggiunto un trigger, seguire questi passaggi per aggiungere un'azione che otterrà il contenuto del file nuovo o modificato individuato dal trigger.</span><span class="sxs-lookup"><span data-stu-id="dae2b-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="dae2b-139">Selezionare **+ Nuovo passaggio** per aggiungere l'azione che recupera il contenuto del file sul server FTP</span><span class="sxs-lookup"><span data-stu-id="dae2b-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="dae2b-140">Selezionare il collegamento **Aggiungi un'azione** .</span><span class="sxs-lookup"><span data-stu-id="dae2b-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="dae2b-141">![Immagine di azione FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="dae2b-142">Immettere *FTP* per cercare tutte le azioni correlate a FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="dae2b-143">Selezionare **FTP - Recuperare i contenuti del file** come azione da eseguire quando viene individuato un file nuovo o modificato nella cartella FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="dae2b-144">![Immagine di azione FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="dae2b-145">Si apre il controllo **Recuperare i contenuti del file**.</span><span class="sxs-lookup"><span data-stu-id="dae2b-145">The **Get file content** control opens.</span></span> <span data-ttu-id="dae2b-146">**Nota**: verrà richiesto di autorizzare l'app per la logica ad accedere all'account sul server FTP, se non lo si è già fatto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dae2b-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="dae2b-147">![Immagine di azione FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="dae2b-148">Selezionare il controllo **File** (lo spazio vuoto sotto **FILE***).</span><span class="sxs-lookup"><span data-stu-id="dae2b-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="dae2b-149">In questo caso è possibile usare le varie proprietà dal file nuovo o modificato individuato sul server FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="dae2b-150">Selezionare l'opzione **Contenuto file**.</span><span class="sxs-lookup"><span data-stu-id="dae2b-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="dae2b-151">![Immagine di azione FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="dae2b-152">Il controllo viene aggiornato e indica che l'azione **FTP - Recuperare i contenuti del file** recupererà il *contenuto del file* nuovo o modificato nel server FTP.</span><span class="sxs-lookup"><span data-stu-id="dae2b-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="dae2b-153">![Immagine di azione FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="dae2b-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="dae2b-154">Salvare il lavoro e poi aggiungere un file nella cartella FTP per testare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="dae2b-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="dae2b-155">A questo punto l'app per la logica è stata configurata con un trigger per monitorare una cartella su un server FTP e avviare il flusso di lavoro quando viene individuato un nuovo file o un file modificato sul server FTP stesso.</span><span class="sxs-lookup"><span data-stu-id="dae2b-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="dae2b-156">L'app per la logica è stata configurata con un'azione per ottenere il contenuto del file nuovo o modificato.</span><span class="sxs-lookup"><span data-stu-id="dae2b-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="dae2b-157">È ora possibile aggiungere un'altra azione, come [SQL Server - Inserisci riga](connectors-create-api-sqlazure.md), per inserire il contenuto del file nuovo o modificato in una tabella di database SQL.</span><span class="sxs-lookup"><span data-stu-id="dae2b-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="dae2b-158">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="dae2b-158">Connector-specific details</span></span>

<span data-ttu-id="dae2b-159">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="dae2b-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dae2b-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dae2b-160">Next Steps</span></span>
[<span data-ttu-id="dae2b-161">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="dae2b-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

