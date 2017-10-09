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
# <a name="get-started-with-relay-hybrid-connections"></a>Introduzione alle connessioni ibride di inoltro
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

In questa esercitazione viene fornita un'introduzione troppo[connessioni ibride di inoltro Azure](relay-what-is-it.md#hybrid-connections)e viene illustrato come toouse .NET toocreate un'applicazione client che invia messaggi tooa corrispondente dell'applicazione di listener. 

## <a name="what-will-be-accomplished"></a>Contenuto dell'esercitazione
Poiché le connessioni ibride richiede sia un client e un componente server, hello esercitazione consente di creare due applicazioni console. Ecco i passaggi di hello:

1. Creare uno spazio dei nomi, inoltro utilizzando hello portale di Azure.
2. Creare una connessione ibrida nello spazio dei nomi utilizzando hello portale di Azure.
3. Scrivere una console di server (listener) tooreceive messaggi dell'applicazione.
4. Scrivere una console client (mittente) toosend messaggi dell'applicazione.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

1. [Visual Studio 2015 o versione successiva](http://www.visualstudio.com). esempi di Hello in questa esercitazione usano Visual Studio 2017.
2. Una sottoscrizione di Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Creare uno spazio dei nomi utilizzando hello portale di Azure
Se è già stato creato uno spazio dei nomi di inoltro, passare toohello [creare una connessione ibrida tramite il portale di Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) sezione.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Creare una connessione ibrida tramite hello portale di Azure
Se una connessione ibrida è già stato creato, passare toohello [creare un'applicazione server](#3-create-a-server-application-listener) sezione.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Creare un'applicazione server (listener)
toolisten e ricevere messaggi da hello inoltro, viene illustrato come scrivere un'applicazione console c# con Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Creare un'applicazione client (mittente)
Inoltro toosend messaggi toohello, viene illustrato come scrivere un'applicazione console c# con Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Eseguire applicazioni hello
1. Eseguire un'applicazione server hello.
2. Eseguire un'applicazione client hello e immettere il testo.
3. Assicurarsi che nel server hello applicazione console output hello testo immesso in un'applicazione hello client.

![applicazioni in esecuzione](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

A questo punto è stata creata un'applicazione per le connessioni ibride end-to-end.

## <a name="next-steps"></a>Passaggi successivi:
* [Domande frequenti sul servizio di inoltro](relay-faq.md)
* [Creare uno spazio dei nomi](relay-create-namespace-portal.md)
* [Introduzione all'applicazione Node](relay-hybrid-connections-node-get-started.md)

