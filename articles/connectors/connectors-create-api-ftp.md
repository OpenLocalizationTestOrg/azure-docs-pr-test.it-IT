---
title: aaaLearn come toouse hello connettore FTP in App per la logica | Documenti Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi tooFTP server toomanage i file. Nel server FTP è possibile eseguire varie azioni, ad esempio creare, aggiornare, ottenere ed eliminare file."
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
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="1e185-105">Iniziare con connettore FTP hello</span><span class="sxs-lookup"><span data-stu-id="1e185-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="1e185-106">Utilizzare toomonitor connettore hello FTP, gestire e creare file in un server FTP.</span><span class="sxs-lookup"><span data-stu-id="1e185-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="1e185-107">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="1e185-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="1e185-108">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="1e185-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="1e185-109">Connettersi tooFTP</span><span class="sxs-lookup"><span data-stu-id="1e185-109">Connect tooFTP</span></span>
<span data-ttu-id="1e185-110">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="1e185-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="1e185-111">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="1e185-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="1e185-112">Creare una connessione tooFTP</span><span class="sxs-lookup"><span data-stu-id="1e185-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="1e185-113">Usare un trigger FTP</span><span class="sxs-lookup"><span data-stu-id="1e185-113">Use a FTP trigger</span></span>
<span data-ttu-id="1e185-114">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="1e185-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="1e185-115">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1e185-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1e185-116">connettore FTP Hello richiede un server FTP che sia accessibile da Internet hello e sia configurato toooperate con la modalità passiva.</span><span class="sxs-lookup"><span data-stu-id="1e185-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="1e185-117">Inoltre, il connettore hello FTP è **non è compatibile con implicita FTPS (FTP su SSL)**.</span><span class="sxs-lookup"><span data-stu-id="1e185-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="1e185-118">connettore FTP Hello supporta solo esplicita FTPS (FTP su SSL).</span><span class="sxs-lookup"><span data-stu-id="1e185-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="1e185-119">In questo esempio, verrà spiegato come hello toouse **FTP: quando un file viene aggiunto o modificato** attivare un flusso di lavoro logica app tooinitiate quando un file viene aggiunto o modificato in, un server FTP.</span><span class="sxs-lookup"><span data-stu-id="1e185-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="1e185-120">In un esempio di enterprise, è possibile utilizzare questo toomonitor trigger, una cartella FTP per i nuovi file che rappresentano gli ordini dei clienti.</span><span class="sxs-lookup"><span data-stu-id="1e185-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="1e185-121">È quindi possibile utilizzare un'azione di connettore FTP, ad esempio **ottenere contenuto del file** contenuto hello tooget dell'ordine di hello per un'ulteriore elaborazione e archiviazione del database orders.</span><span class="sxs-lookup"><span data-stu-id="1e185-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="1e185-122">Immettere *ftp* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **FTP: quando un file viene aggiunto o modificato** trigger</span><span class="sxs-lookup"><span data-stu-id="1e185-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="1e185-123">![Immagine di trigger FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="1e185-124">Hello **quando un file viene aggiunto o modificato** apre controllo</span><span class="sxs-lookup"><span data-stu-id="1e185-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="1e185-125">![Immagine di trigger FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="1e185-126">Seleziona hello **...**  si trova sul lato destro hello del controllo hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="1e185-127">Verrà visualizzata di controllo di selezione cartella hello</span><span class="sxs-lookup"><span data-stu-id="1e185-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="1e185-128">![Immagine di trigger FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="1e185-129">Seleziona hello  **>**  (freccia destra) e cartella toofind hello che si vuole toomonitor per file nuovi o modificati.</span><span class="sxs-lookup"><span data-stu-id="1e185-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="1e185-130">Selezionare la cartella hello e cartella hello viene ora visualizzato nella hello **cartella** controllo.</span><span class="sxs-lookup"><span data-stu-id="1e185-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="1e185-131">![Immagine di trigger FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="1e185-132">A questo punto, l'app di logica è stato configurato con un trigger che verrà avviata un'esecuzione di hello altre azioni nel flusso di lavoro hello e il trigger quando un file viene modificato o creato nella cartella FTP specifico hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="1e185-133">Per un toobe di app logica funzionale, deve contenere almeno un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="1e185-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="1e185-134">Seguire passaggi hello hello successiva sezione tooadd un'azione.</span><span class="sxs-lookup"><span data-stu-id="1e185-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="1e185-135">Usare un'azione FTP</span><span class="sxs-lookup"><span data-stu-id="1e185-135">Use a FTP action</span></span>
<span data-ttu-id="1e185-136">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="1e185-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="1e185-137">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="1e185-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="1e185-138">Dopo avere aggiunto un trigger, seguire questi tooadd passaggi un'azione che verrà visualizzato contenuto hello del file hello nuove o modificate, è stato trovato dal trigger hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="1e185-139">Selezionare **+ nuovo passaggio** tooadd hello hello azione tooget hello contenuto file hello sul server FTP hello</span><span class="sxs-lookup"><span data-stu-id="1e185-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="1e185-140">Seleziona hello **aggiungere un'azione** collegamento.</span><span class="sxs-lookup"><span data-stu-id="1e185-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="1e185-141">![Immagine di azione FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="1e185-142">Immettere *FTP* toosearch per tutte le azioni correlate tooFTP.</span><span class="sxs-lookup"><span data-stu-id="1e185-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="1e185-143">Selezionare **FTP - ottenere il contenuto di file** come hello tootake azione quando viene trovato un file nuovo o modificato nella cartella hello FTP.</span><span class="sxs-lookup"><span data-stu-id="1e185-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="1e185-144">![Immagine di azione FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="1e185-145">Hello **ottenere contenuto del file** controllo viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="1e185-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="1e185-146">**Nota**: si sarà richiesta tooauthorize il tooaccess app logica al server FTP account se si è già stato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1e185-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="1e185-147">![Immagine di azione FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="1e185-148">Seleziona hello **File** controllo (sotto lo spazio vuoto hello **FILE***).</span><span class="sxs-lookup"><span data-stu-id="1e185-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="1e185-149">In questo caso, è possibile utilizzare uno qualsiasi dei hello varie proprietà dal file nuovi o modificati hello trovato nel server FTP hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="1e185-150">Seleziona hello **il contenuto di File** opzione.</span><span class="sxs-lookup"><span data-stu-id="1e185-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="1e185-151">![Immagine di azione FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="1e185-152">controllo di Hello viene aggiornato, indicante che hello **FTP - ottenere il contenuto di file** azione verrà visualizzato hello *il contenuto di file* file hello nuovi o modificati nel server FTP hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="1e185-153">![Immagine di azione FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="1e185-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="1e185-154">Salvare il lavoro, quindi aggiungere un tootest cartella FTP di file toohello il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1e185-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="1e185-155">A questo punto, hello logica app è stato configurato con toomonitor un trigger una cartella su un server FTP e un flusso di lavoro avviare hello a quando trova un nuovo file o un file modificato nel server FTP hello.</span><span class="sxs-lookup"><span data-stu-id="1e185-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="1e185-156">Hello logica app è stato configurato con un contenuto di hello azione tooget file hello nuove o modificate.</span><span class="sxs-lookup"><span data-stu-id="1e185-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="1e185-157">È ora possibile aggiungere un'altra azione, ad esempio hello [SQL Server - Inserisci riga](connectors-create-api-sqlazure.md) contenuto hello tooinsert di azione del file hello di nuove o modificate in una tabella di database SQL.</span><span class="sxs-lookup"><span data-stu-id="1e185-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="1e185-158">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="1e185-158">Connector-specific details</span></span>

<span data-ttu-id="1e185-159">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="1e185-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1e185-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e185-160">Next Steps</span></span>
[<span data-ttu-id="1e185-161">Creare un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1e185-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

