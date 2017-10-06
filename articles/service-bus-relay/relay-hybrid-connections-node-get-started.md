---
title: aaaGet avviato con le connessioni ibride di inoltro di Azure nel nodo | Documenti Microsoft
description: Scrivere un'applicazione console Node.js per le connessioni ibride di inoltro di Azure.
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="91ff7-103">Introduzione alle connessioni ibride di inoltro</span><span class="sxs-lookup"><span data-stu-id="91ff7-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="91ff7-104">In questa esercitazione viene fornita un'introduzione troppo[connessioni ibride di inoltro Azure](relay-what-is-it.md#hybrid-connections)e viene illustrato come toouse Node.js toocreate un'applicazione client che invia messaggi tooa corrispondente dell'applicazione di listener.</span><span class="sxs-lookup"><span data-stu-id="91ff7-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="91ff7-105">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="91ff7-105">What will be accomplished</span></span>

<span data-ttu-id="91ff7-106">Dato che le connessioni ibride richiedono sia un componente client che un componente server, in questa esercitazione verranno create due applicazioni console.</span><span class="sxs-lookup"><span data-stu-id="91ff7-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="91ff7-107">Ecco i passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="91ff7-107">Here are hello steps:</span></span>

1. <span data-ttu-id="91ff7-108">Creare uno spazio dei nomi, inoltro utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="91ff7-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="91ff7-109">Creare una connessione ibrida, hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="91ff7-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="91ff7-110">Scrittura di un server tooreceive messaggi dell'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="91ff7-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="91ff7-111">Scrivere un client toosend messaggi dell'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="91ff7-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91ff7-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="91ff7-112">Prerequisites</span></span>

1. <span data-ttu-id="91ff7-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="91ff7-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="91ff7-114">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="91ff7-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="91ff7-115">1. Creare uno spazio dei nomi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="91ff7-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="91ff7-116">Se si dispone già di uno spazio dei nomi di inoltro creato, passare toohello [creare una connessione ibrida tramite il portale di Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sezione.</span><span class="sxs-lookup"><span data-stu-id="91ff7-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="91ff7-117">2. Creare una connessione ibrida tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="91ff7-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="91ff7-118">Se si dispone già di una connessione ibrida creata, passare toohello [creare un'applicazione server](#3-create-a-server-application-listener) sezione.</span><span class="sxs-lookup"><span data-stu-id="91ff7-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="91ff7-119">3. Creare un'applicazione server (listener)</span><span class="sxs-lookup"><span data-stu-id="91ff7-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="91ff7-120">toolisten e ricevere messaggi da hello inoltro, viene illustrato come scrivere un'applicazione console Node.js.</span><span class="sxs-lookup"><span data-stu-id="91ff7-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="91ff7-121">4. Creare un'applicazione client (mittente)</span><span class="sxs-lookup"><span data-stu-id="91ff7-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="91ff7-122">toosend messaggi toohello inoltro, viene illustrato come scrivere un'applicazione console Node.js.</span><span class="sxs-lookup"><span data-stu-id="91ff7-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="91ff7-123">5. Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="91ff7-123">5. Run hello applications</span></span>

1. <span data-ttu-id="91ff7-124">Eseguire un'applicazione server hello: da un tipo di prompt dei comandi di Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="91ff7-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="91ff7-125">Eseguire un'applicazione client hello: da un tipo di prompt dei comandi di Node.js `node sender.js`e immettere il testo.</span><span class="sxs-lookup"><span data-stu-id="91ff7-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="91ff7-126">Assicurarsi che nel server hello applicazione console output hello testo immesso in un'applicazione hello client.</span><span class="sxs-lookup"><span data-stu-id="91ff7-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![applicazioni in esecuzione](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="91ff7-128">A questo punto è stata creata un'applicazione per le connessioni ibride end-to-end con Node.js.</span><span class="sxs-lookup"><span data-stu-id="91ff7-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="91ff7-129">Passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="91ff7-129">Next steps:</span></span>

* [<span data-ttu-id="91ff7-130">Domande frequenti sul servizio di inoltro</span><span class="sxs-lookup"><span data-stu-id="91ff7-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="91ff7-131">Creare uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="91ff7-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="91ff7-132">Introduzione a .NET</span><span class="sxs-lookup"><span data-stu-id="91ff7-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="91ff7-133">Introduzione a Node</span><span class="sxs-lookup"><span data-stu-id="91ff7-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

