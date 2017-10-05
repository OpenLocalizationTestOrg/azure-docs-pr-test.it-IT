---
title: Aggiungere il connettore del database SQL di Azure alle app per la logica | Microsoft Docs
description: Panoramica del connettore del database SQL di Azure con i parametri dell'API REST
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="f7a6b-103">Introduzione al connettore del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="f7a6b-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="f7a6b-104">Usando il connettore del database SQL di Azure, creare flussi di lavoro per l'organizzazione che gestiscano i dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="f7a6b-105">Con il database SQL è possibile:</span><span class="sxs-lookup"><span data-stu-id="f7a6b-105">With SQL Database, you:</span></span>

* <span data-ttu-id="f7a6b-106">Creare il flusso di lavoro aggiungendo un nuovo cliente in un database di clienti o aggiornando un ordine in un database di ordini.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="f7a6b-107">Usare le azioni per ottenere una riga di dati, inserire una nuova riga e persino eliminare una riga.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="f7a6b-108">Ad esempio, quando viene creato un record in Dynamics CRM Online (trigger), inserire una riga in un database SQL di Azure (azione).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="f7a6b-109">Questo argomento illustra come usare il connettore database SQL in un'app per la logica ed elenca le azioni.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="f7a6b-110">Per altre informazioni sulle app per la logica, vedere [Cosa sono le app per la logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="f7a6b-111">Connettersi al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="f7a6b-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="f7a6b-112">Prima che l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="f7a6b-113">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f7a6b-114">Ad esempio, per connettersi al database SQL, si crea una *connessione* al database SQL.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="f7a6b-115">Per creare una connessione, immettere le credenziali che si usano normalmente per accedere al servizio a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="f7a6b-116">Pertanto, per creare la connessione al database SQL, immettere le credenziali del database SQL.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="f7a6b-117">Creare la connessione</span><span class="sxs-lookup"><span data-stu-id="f7a6b-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="f7a6b-118">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="f7a6b-118">Use a trigger</span></span>
<span data-ttu-id="f7a6b-119">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-119">This connector does not have any triggers.</span></span> <span data-ttu-id="f7a6b-120">Usare altri trigger per avviare l'app per la logica, come un trigger di ricorrenza, un trigger Webhook HTTP, i trigger disponibili con altri connettori e altri ancora.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="f7a6b-121">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="f7a6b-122">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="f7a6b-122">Use an action</span></span>
<span data-ttu-id="f7a6b-123">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="f7a6b-124">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="f7a6b-125">Selezionare il segno più.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-125">Select the plus sign.</span></span> <span data-ttu-id="f7a6b-126">Sono disponibili varie opzioni: **Aggiungi un'azione**, **Aggiungi una condizione** e le opzioni in **Altro**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="f7a6b-127">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f7a6b-128">Nella casella di testo digitare "sql" per ottenere l'elenco di tutte le azioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="f7a6b-129">Nell'esempio scegliere **SQL Server - Ottieni riga**.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="f7a6b-130">Se esiste già una connessione, selezionare il **nome della tabella** dall'elenco a discesa e immettere l'**ID riga** che si vuole restituire.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="f7a6b-131">Se viene richiesto di inserire le informazioni di connessione, immettere i dettagli per creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="f7a6b-132">La sezione [Creare la connessione](connectors-create-api-sqlazure.md#create-the-connection) di questo argomento descrive queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f7a6b-133">In questo esempio si restituisce una riga da una tabella.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="f7a6b-134">Per visualizzare i dati in questa riga aggiungere un'altra azione che crea un file usando i campi della tabella.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="f7a6b-135">Ad esempio, aggiungere un'azione OneDrive che usa i campi Nome e Cognome per creare un nuovo file nell'account di archiviazione cloud.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="f7a6b-136">Scegliere **Salva** nell'angolo in alto a sinistra della barra degli strumenti per salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="f7a6b-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f7a6b-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f7a6b-138">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="f7a6b-138">Connector-specific details</span></span>

<span data-ttu-id="f7a6b-139">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f7a6b-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7a6b-140">Next steps</span></span>
<span data-ttu-id="f7a6b-141">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f7a6b-142">Esplorare gli altri connettori disponibili nelle app per la logica nell' [elenco delle API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f7a6b-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

