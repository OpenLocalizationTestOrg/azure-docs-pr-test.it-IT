---
title: aaaGet avviato con le connessioni ibride di inoltro di Azure in .NET | Documenti Microsoft
description: Scrivere un'applicazione console C# per le connessioni ibride di inoltro di Azure.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="ab756-103">Introduzione alle connessioni ibride di inoltro</span><span class="sxs-lookup"><span data-stu-id="ab756-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="ab756-104">In questa esercitazione viene fornita un'introduzione troppo[connessioni ibride di inoltro Azure](relay-what-is-it.md#hybrid-connections)e viene illustrato come toouse .NET toocreate un'applicazione client che invia messaggi tooa corrispondente dell'applicazione di listener.</span><span class="sxs-lookup"><span data-stu-id="ab756-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ab756-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="ab756-105">What will be accomplished</span></span>
<span data-ttu-id="ab756-106">Poiché le connessioni ibride richiede sia un client e un componente server, hello esercitazione consente di creare due applicazioni console.</span><span class="sxs-lookup"><span data-stu-id="ab756-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="ab756-107">Ecco i passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="ab756-107">Here are hello steps:</span></span>

1. <span data-ttu-id="ab756-108">Creare uno spazio dei nomi, inoltro utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab756-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="ab756-109">Creare una connessione ibrida nello spazio dei nomi utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab756-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="ab756-110">Scrivere una console di server (listener) tooreceive messaggi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab756-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="ab756-111">Scrivere una console client (mittente) toosend messaggi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ab756-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab756-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ab756-112">Prerequisites</span></span>

<span data-ttu-id="ab756-113">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="ab756-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="ab756-114">[Visual Studio 2015 o versione successiva](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ab756-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="ab756-115">esempi di Hello in questa esercitazione usano Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ab756-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="ab756-116">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab756-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="ab756-117">1. Creare uno spazio dei nomi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ab756-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="ab756-118">Se è già stato creato uno spazio dei nomi di inoltro, passare toohello [creare una connessione ibrida tramite il portale di Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sezione.</span><span class="sxs-lookup"><span data-stu-id="ab756-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="ab756-119">2. Creare una connessione ibrida tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ab756-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="ab756-120">Se una connessione ibrida è già stato creato, passare toohello [creare un'applicazione server](#3-create-a-server-application-listener) sezione.</span><span class="sxs-lookup"><span data-stu-id="ab756-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="ab756-121">3. Creare un'applicazione server (listener)</span><span class="sxs-lookup"><span data-stu-id="ab756-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="ab756-122">toolisten e ricevere messaggi da hello inoltro, viene illustrato come scrivere un'applicazione console c# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab756-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="ab756-123">4. Creare un'applicazione client (mittente)</span><span class="sxs-lookup"><span data-stu-id="ab756-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="ab756-124">Inoltro toosend messaggi toohello, viene illustrato come scrivere un'applicazione console c# con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab756-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="ab756-125">5. Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="ab756-125">5. Run hello applications</span></span>
1. <span data-ttu-id="ab756-126">Eseguire un'applicazione server hello.</span><span class="sxs-lookup"><span data-stu-id="ab756-126">Run hello server application.</span></span>
2. <span data-ttu-id="ab756-127">Eseguire un'applicazione client hello e immettere il testo.</span><span class="sxs-lookup"><span data-stu-id="ab756-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="ab756-128">Assicurarsi che nel server hello applicazione console output hello testo immesso in un'applicazione hello client.</span><span class="sxs-lookup"><span data-stu-id="ab756-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![applicazioni in esecuzione](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="ab756-130">A questo punto è stata creata un'applicazione per le connessioni ibride end-to-end.</span><span class="sxs-lookup"><span data-stu-id="ab756-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab756-131">Passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="ab756-131">Next steps:</span></span>
* [<span data-ttu-id="ab756-132">Domande frequenti sul servizio di inoltro</span><span class="sxs-lookup"><span data-stu-id="ab756-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="ab756-133">Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="ab756-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="ab756-134">Introduzione all'applicazione Node</span><span class="sxs-lookup"><span data-stu-id="ab756-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

