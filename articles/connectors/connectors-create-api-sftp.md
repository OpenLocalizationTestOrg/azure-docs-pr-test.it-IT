---
title: Informazioni su come usare il connettore SFTP nelle app per la logica | Documentazione Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi all'API SFTP per inviare e ricevere file. È possibile eseguire varie operazioni come creare, aggiornare, recuperare o eliminare file."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="aaea8-105">Introduzione al connettore SFTP</span><span class="sxs-lookup"><span data-stu-id="aaea8-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="aaea8-106">Usare il connettore SFTP per accedere a un account SFTP al fine di inviare e ricevere file.</span><span class="sxs-lookup"><span data-stu-id="aaea8-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="aaea8-107">È possibile eseguire varie operazioni come creare, aggiornare, recuperare o eliminare file.</span><span class="sxs-lookup"><span data-stu-id="aaea8-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="aaea8-108">Per usare [qualsiasi connettore](apis-list.md), è necessario innanzitutto creare un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="aaea8-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="aaea8-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="aaea8-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="aaea8-110">Connettersi a SFTP</span><span class="sxs-lookup"><span data-stu-id="aaea8-110">Connect to SFTP</span></span>
<span data-ttu-id="aaea8-111">Perché l'app per la logica possa accedere a qualsiasi servizio, è necessario creare una *connessione* al servizio.</span><span class="sxs-lookup"><span data-stu-id="aaea8-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="aaea8-112">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="aaea8-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="aaea8-113">Creare una connessione a SFTP</span><span class="sxs-lookup"><span data-stu-id="aaea8-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="aaea8-114">Usare un trigger SFTP</span><span class="sxs-lookup"><span data-stu-id="aaea8-114">Use an SFTP trigger</span></span>
<span data-ttu-id="aaea8-115">Un trigger è un evento che può essere usato per avviare il flusso di lavoro definito in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="aaea8-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="aaea8-116">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aaea8-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="aaea8-117">In questo esempio il trigger **SFTP - Quando viene aggiunto o modificato un file** viene usato per avviare un flusso di lavoro dell'app per la logica quando viene aggiunto o modificato un file in un server SFTP.</span><span class="sxs-lookup"><span data-stu-id="aaea8-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="aaea8-118">Viene aggiunta anche una condizione che controlla il contenuto del file nuovo o modificato e decide di estrarre il file se il relativo contenuto indica che il file deve essere estratto prima di usare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="aaea8-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="aaea8-119">Viene infine aggiunta un'azione per estrarre il contenuto di un file e inserire il contenuto estratto in una cartella sul server SFTP.</span><span class="sxs-lookup"><span data-stu-id="aaea8-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="aaea8-120">In un esempio riguardante un'organizzazione si potrebbe usare questo trigger per monitorare una cartella SFTP per nuovi file di ordini dei clienti.</span><span class="sxs-lookup"><span data-stu-id="aaea8-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="aaea8-121">È quindi possibile usare un'azione connettore SFTP come **Recuperare i contenuti del file** per recuperare il contenuto dell'ordine per elaborarlo ulteriormente e archiviarlo nel database degli ordini.</span><span class="sxs-lookup"><span data-stu-id="aaea8-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="aaea8-122">Add a condition</span><span class="sxs-lookup"><span data-stu-id="aaea8-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="aaea8-123">Usare un'azione SFTP</span><span class="sxs-lookup"><span data-stu-id="aaea8-123">Use an SFTP action</span></span>
<span data-ttu-id="aaea8-124">Un'azione è un'operazione eseguita dal flusso di lavoro e definita in un'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="aaea8-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="aaea8-125">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aaea8-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="aaea8-126">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="aaea8-126">Connector-specific details</span></span>

<span data-ttu-id="aaea8-127">Per visualizzare eventuali azioni e trigger definiti in Swagger ed eventuali limiti, vedere i [dettagli del connettore](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="aaea8-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="aaea8-128">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="aaea8-128">More connectors</span></span>
<span data-ttu-id="aaea8-129">Tornare all' [elenco di API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="aaea8-129">Go back to the [APIs list](apis-list.md).</span></span>