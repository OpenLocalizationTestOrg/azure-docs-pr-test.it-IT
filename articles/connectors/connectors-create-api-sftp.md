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
# <a name="get-started-with-hello-sftp-connector"></a>Iniziare con connettore SFTP hello
Utilizzare hello SFTP connettore tooaccess un toosend account SFTP e ricevere file. È possibile eseguire varie operazioni come creare, aggiornare, recuperare o eliminare file.  

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Connettersi tooSFTP
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio. Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.  

### <a name="create-a-connection-toosftp"></a>Creare una connessione tooSFTP
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Usare un trigger SFTP
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

In questo esempio hello **SFTP - quando un file viene aggiunto o modificato** trigger è tooinitiate usato un flusso di lavoro logica app quando un file viene aggiunto o modificato in, un server SFTP. È inoltre possibile aggiungere una condizione che controlla il contenuto di hello del file nuovo o modificato hello e lo rende un file di hello tooextract decisione se il relativo contenuto indica che devono essere estratti prima di usare contenuto hello. Infine, aggiungere un contenuto di hello tooextract azione di un file e inserire contenuto hello estratto in una cartella nel server SFTP hello. 

In un esempio di enterprise, è possibile utilizzare questo toomonitor trigger, una cartella SFTP per i nuovi file che rappresentano gli ordini dei clienti.  È quindi possibile utilizzare un'azione di connettore SFTP, ad esempio **ottenere contenuto del file**, contenuto hello tooget dell'ordine di hello per un'ulteriore elaborazione e archiviazione in un database orders.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Add a condition
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Usare un'azione SFTP
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).
