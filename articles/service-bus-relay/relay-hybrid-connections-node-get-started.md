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
# <a name="get-started-with-relay-hybrid-connections"></a>Introduzione alle connessioni ibride di inoltro

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

In questa esercitazione viene fornita un'introduzione troppo[connessioni ibride di inoltro Azure](relay-what-is-it.md#hybrid-connections)e viene illustrato come toouse Node.js toocreate un'applicazione client che invia messaggi tooa corrispondente dell'applicazione di listener. 

## <a name="what-will-be-accomplished"></a>Contenuto dell'esercitazione

Dato che le connessioni ibride richiedono sia un componente client che un componente server, in questa esercitazione verranno create due applicazioni console. Ecco i passaggi di hello:

1. Creare uno spazio dei nomi, inoltro utilizzando hello portale di Azure.
2. Creare una connessione ibrida, hello portale di Azure.
3. Scrittura di un server tooreceive messaggi dell'applicazione console.
4. Scrivere un client toosend messaggi dell'applicazione console.

## <a name="prerequisites"></a>Prerequisiti

1. [Node.js](https://nodejs.org/en/).
2. Una sottoscrizione di Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Creare uno spazio dei nomi utilizzando hello portale di Azure

Se si dispone già di uno spazio dei nomi di inoltro creato, passare toohello [creare una connessione ibrida tramite il portale di Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sezione.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Creare una connessione ibrida tramite hello portale di Azure

Se si dispone già di una connessione ibrida creata, passare toohello [creare un'applicazione server](#3-create-a-server-application-listener) sezione.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Creare un'applicazione server (listener)

toolisten e ricevere messaggi da hello inoltro, viene illustrato come scrivere un'applicazione console Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Creare un'applicazione client (mittente)

toosend messaggi toohello inoltro, viene illustrato come scrivere un'applicazione console Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Eseguire applicazioni hello

1. Eseguire un'applicazione server hello: da un tipo di prompt dei comandi di Node.js `node listener.js`.
2. Eseguire un'applicazione client hello: da un tipo di prompt dei comandi di Node.js `node sender.js`e immettere il testo.
3. Assicurarsi che nel server hello applicazione console output hello testo immesso in un'applicazione hello client.

![applicazioni in esecuzione](./media/relay-hybrid-connections-node-get-started/running-applications.png)

A questo punto è stata creata un'applicazione per le connessioni ibride end-to-end con Node.js.

## <a name="next-steps"></a>Passaggi successivi:

* [Domande frequenti sul servizio di inoltro](relay-faq.md)
* [Creare uno spazio dei nomi](relay-create-namespace-portal.md)
* [Introduzione a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introduzione a Node](relay-hybrid-connections-node-get-started.md)

