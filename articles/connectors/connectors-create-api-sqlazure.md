---
title: connettore di Database SQL di Azure hello aaaAdd nelle App logica | Documenti Microsoft
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
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="3aead-103">Iniziare con il connettore di Database SQL di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3aead-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="3aead-104">Utilizzando il connettore di Database SQL di Azure hello, creare i flussi di lavoro per l'organizzazione che gestiscono i dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="3aead-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="3aead-105">Con il database SQL è possibile:</span><span class="sxs-lookup"><span data-stu-id="3aead-105">With SQL Database, you:</span></span>

* <span data-ttu-id="3aead-106">Compilare il flusso di lavoro aggiungendo un nuovo database di clienti tooa cliente o l'aggiornamento di un ordine in un database orders.</span><span class="sxs-lookup"><span data-stu-id="3aead-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="3aead-107">Utilizzare azioni tooget una riga di dati, inserire una nuova riga e di eliminare.</span><span class="sxs-lookup"><span data-stu-id="3aead-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="3aead-108">Ad esempio, quando viene creato un record in Dynamics CRM Online (trigger), inserire una riga in un database SQL di Azure (azione).</span><span class="sxs-lookup"><span data-stu-id="3aead-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="3aead-109">Questo argomento viene illustrato come toouse hello connettore del Database SQL in un'app di logica e anche gli elenchi di hello azioni.</span><span class="sxs-lookup"><span data-stu-id="3aead-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="3aead-110">toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aead-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="3aead-111">Connettersi tooAzure Database SQL</span><span class="sxs-lookup"><span data-stu-id="3aead-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="3aead-112">Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="3aead-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="3aead-113">Una connessione fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="3aead-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="3aead-114">Ad esempio, tooconnect tooSQL Database, si crea un Database SQL *connessione*.</span><span class="sxs-lookup"><span data-stu-id="3aead-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="3aead-115">toocreate una connessione, immettere credenziali hello utilizzato normalmente il servizio di hello tooaccess a che ci si connette.</span><span class="sxs-lookup"><span data-stu-id="3aead-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="3aead-116">In tal caso, nel Database SQL, immettere la connessione al Database di SQL credenziali toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="3aead-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="3aead-117">Creare una connessione hello</span><span class="sxs-lookup"><span data-stu-id="3aead-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="3aead-118">Usare un trigger</span><span class="sxs-lookup"><span data-stu-id="3aead-118">Use a trigger</span></span>
<span data-ttu-id="3aead-119">Questo connettore non include trigger.</span><span class="sxs-lookup"><span data-stu-id="3aead-119">This connector does not have any triggers.</span></span> <span data-ttu-id="3aead-120">Usare altri trigger toostart hello logica app, ad esempio un trigger di ricorrenza, un trigger HTTP Webhook, i trigger disponibili con altri connettori e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="3aead-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="3aead-121">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.</span><span class="sxs-lookup"><span data-stu-id="3aead-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="3aead-122">Usare un'azione</span><span class="sxs-lookup"><span data-stu-id="3aead-122">Use an action</span></span>
<span data-ttu-id="3aead-123">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="3aead-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="3aead-124">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="3aead-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="3aead-125">Selezionare hello sul segno più.</span><span class="sxs-lookup"><span data-stu-id="3aead-125">Select hello plus sign.</span></span> <span data-ttu-id="3aead-126">Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.</span><span class="sxs-lookup"><span data-stu-id="3aead-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="3aead-127">Selezionare **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="3aead-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="3aead-128">Nella casella di testo hello, digitare "sql" tooget un elenco di tutte le azioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="3aead-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="3aead-129">Nell'esempio scegliere **SQL Server - Ottieni riga**.</span><span class="sxs-lookup"><span data-stu-id="3aead-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="3aead-130">Se esiste già una connessione, quindi selezionare hello **nome tabella** dall'elenco a discesa hello elenco e immettere hello **ID riga** desiderato tooreturn.</span><span class="sxs-lookup"><span data-stu-id="3aead-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="3aead-131">Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="3aead-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="3aead-132">[Creare una connessione hello](connectors-create-api-sqlazure.md#create-the-connection) in questo argomento vengono descritte queste proprietà.</span><span class="sxs-lookup"><span data-stu-id="3aead-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="3aead-133">In questo esempio si restituisce una riga da una tabella.</span><span class="sxs-lookup"><span data-stu-id="3aead-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="3aead-134">dati di hello toosee in questa riga, aggiungere un'altra operazione che crea un file utilizzando i campi di hello dalla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="3aead-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="3aead-135">Ad esempio, aggiungere un'azione di OneDrive che utilizza hello FirstName e LastName campi toocreate un nuovo file nell'account di archiviazione cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3aead-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="3aead-136">**Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello).</span><span class="sxs-lookup"><span data-stu-id="3aead-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="3aead-137">L'app per la logica viene salvata e può essere attivata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="3aead-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="3aead-138">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="3aead-138">Connector-specific details</span></span>

<span data-ttu-id="3aead-139">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="3aead-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3aead-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3aead-140">Next steps</span></span>
<span data-ttu-id="3aead-141">[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3aead-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3aead-142">Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3aead-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

