---
title: aaaLearn come toouse hello connettore SFTP in App per la logica | Documenti Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi toosend tooSFTP API e ricevere file. È possibile eseguire varie operazioni come creare, aggiornare, recuperare o eliminare file."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="7f468-105">Iniziare con connettore SFTP hello</span><span class="sxs-lookup"><span data-stu-id="7f468-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="7f468-106">Utilizzare hello SFTP connettore tooaccess un toosend account SFTP e ricevere file.</span><span class="sxs-lookup"><span data-stu-id="7f468-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="7f468-107">È possibile eseguire varie operazioni come creare, aggiornare, recuperare o eliminare file.</span><span class="sxs-lookup"><span data-stu-id="7f468-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="7f468-108">toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="7f468-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="7f468-109">Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7f468-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="7f468-110">Connettersi tooSFTP</span><span class="sxs-lookup"><span data-stu-id="7f468-110">Connect tooSFTP</span></span>
<span data-ttu-id="7f468-111">Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="7f468-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="7f468-112">Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.</span><span class="sxs-lookup"><span data-stu-id="7f468-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="7f468-113">Creare una connessione tooSFTP</span><span class="sxs-lookup"><span data-stu-id="7f468-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="7f468-114">Usare un trigger SFTP</span><span class="sxs-lookup"><span data-stu-id="7f468-114">Use an SFTP trigger</span></span>
<span data-ttu-id="7f468-115">Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="7f468-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="7f468-116">[Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7f468-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="7f468-117">In questo esempio hello **SFTP - quando un file viene aggiunto o modificato** trigger è tooinitiate usato un flusso di lavoro logica app quando un file viene aggiunto o modificato in, un server SFTP.</span><span class="sxs-lookup"><span data-stu-id="7f468-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="7f468-118">È inoltre possibile aggiungere una condizione che controlla il contenuto di hello del file nuovo o modificato hello e lo rende un file di hello tooextract decisione se il relativo contenuto indica che devono essere estratti prima di usare contenuto hello.</span><span class="sxs-lookup"><span data-stu-id="7f468-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="7f468-119">Infine, aggiungere un contenuto di hello tooextract azione di un file e inserire contenuto hello estratto in una cartella nel server SFTP hello.</span><span class="sxs-lookup"><span data-stu-id="7f468-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="7f468-120">In un esempio di enterprise, è possibile utilizzare questo toomonitor trigger, una cartella SFTP per i nuovi file che rappresentano gli ordini dei clienti.</span><span class="sxs-lookup"><span data-stu-id="7f468-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="7f468-121">È quindi possibile utilizzare un'azione di connettore SFTP, ad esempio **ottenere contenuto del file**, contenuto hello tooget dell'ordine di hello per un'ulteriore elaborazione e archiviazione in un database orders.</span><span class="sxs-lookup"><span data-stu-id="7f468-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="7f468-122">Add a condition</span><span class="sxs-lookup"><span data-stu-id="7f468-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="7f468-123">Usare un'azione SFTP</span><span class="sxs-lookup"><span data-stu-id="7f468-123">Use an SFTP action</span></span>
<span data-ttu-id="7f468-124">Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="7f468-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="7f468-125">[Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7f468-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="7f468-126">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="7f468-126">Connector-specific details</span></span>

<span data-ttu-id="7f468-127">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="7f468-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7f468-128">Altri connettori</span><span class="sxs-lookup"><span data-stu-id="7f468-128">More connectors</span></span>
<span data-ttu-id="7f468-129">Tornare indietro toohello [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7f468-129">Go back toohello [APIs list](apis-list.md).</span></span>
