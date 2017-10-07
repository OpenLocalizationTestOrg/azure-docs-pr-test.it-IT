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
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Iniziare con il connettore di Database SQL di Azure hello
Utilizzando il connettore di Database SQL di Azure hello, creare i flussi di lavoro per l'organizzazione che gestiscono i dati nelle tabelle. 

Con il database SQL è possibile:

* Compilare il flusso di lavoro aggiungendo un nuovo database di clienti tooa cliente o l'aggiornamento di un ordine in un database orders.
* Utilizzare azioni tooget una riga di dati, inserire una nuova riga e di eliminare. Ad esempio, quando viene creato un record in Dynamics CRM Online (trigger), inserire una riga in un database SQL di Azure (azione). 

Questo argomento viene illustrato come toouse hello connettore del Database SQL in un'app di logica e anche gli elenchi di hello azioni.

toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Connettersi tooAzure Database SQL
Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, tooconnect tooSQL Database, si crea un Database SQL *connessione*. toocreate una connessione, immettere credenziali hello utilizzato normalmente il servizio di hello tooaccess a che ci si connette. In tal caso, nel Database SQL, immettere la connessione al Database di SQL credenziali toocreate hello. 

#### <a name="create-hello-connection"></a>Creare una connessione hello
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Usare un trigger
Questo connettore non include trigger. Usare altri trigger toostart hello logica app, ad esempio un trigger di ricorrenza, un trigger HTTP Webhook, i trigger disponibili con altri connettori e altro ancora. [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.

## <a name="use-an-action"></a>Usare un'azione
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selezionare hello sul segno più. Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di testo hello, digitare "sql" tooget un elenco di tutte le azioni disponibili hello.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Nell'esempio scegliere **SQL Server - Ottieni riga**. Se esiste già una connessione, quindi selezionare hello **nome tabella** dall'elenco a discesa hello elenco e immettere hello **ID riga** desiderato tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello. [Creare una connessione hello](connectors-create-api-sqlazure.md#create-the-connection) in questo argomento vengono descritte queste proprietà. 
   
   > [!NOTE]
   > In questo esempio si restituisce una riga da una tabella. dati di hello toosee in questa riga, aggiungere un'altra operazione che crea un file utilizzando i campi di hello dalla tabella hello. Ad esempio, aggiungere un'azione di OneDrive che utilizza hello FirstName e LastName campi toocreate un nuovo file nell'account di archiviazione cloud hello. 
   > 
   > 
5. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/sql/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).

