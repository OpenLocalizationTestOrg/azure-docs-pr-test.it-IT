---
title: aaaLearn come toouse hello connettore FTP in App per la logica | Documenti Microsoft
description: "Creare app per la logica con Servizio app di Azure. Connettersi tooFTP server toomanage i file. Nel server FTP è possibile eseguire varie azioni, ad esempio creare, aggiornare, ottenere ed eliminare file."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Iniziare con connettore FTP hello
Utilizzare toomonitor connettore hello FTP, gestire e creare file in un server FTP. 

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Connettersi tooFTP
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio. Una [connessione](connectors-overview.md) fornisce la connettività tra un'app per la logica e un altro servizio.  

### <a name="create-a-connection-tooftp"></a>Creare una connessione tooFTP
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Usare un trigger FTP
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> connettore FTP Hello richiede un server FTP che sia accessibile da Internet hello e sia configurato toooperate con la modalità passiva. Inoltre, il connettore hello FTP è **non è compatibile con implicita FTPS (FTP su SSL)**. connettore FTP Hello supporta solo esplicita FTPS (FTP su SSL).  
> 
> 

In questo esempio, verrà spiegato come hello toouse **FTP: quando un file viene aggiunto o modificato** attivare un flusso di lavoro logica app tooinitiate quando un file viene aggiunto o modificato in, un server FTP. In un esempio di enterprise, è possibile utilizzare questo toomonitor trigger, una cartella FTP per i nuovi file che rappresentano gli ordini dei clienti.  È quindi possibile utilizzare un'azione di connettore FTP, ad esempio **ottenere contenuto del file** contenuto hello tooget dell'ordine di hello per un'ulteriore elaborazione e archiviazione del database orders.

1. Immettere *ftp* nella casella di ricerca hello nella finestra di progettazione di hello logica App, quindi selezionare hello **FTP: quando un file viene aggiunto o modificato** trigger   
   ![Immagine di trigger FTP 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Hello **quando un file viene aggiunto o modificato** apre controllo  
   ![Immagine di trigger FTP 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Seleziona hello **...**  si trova sul lato destro hello del controllo hello. Verrà visualizzata di controllo di selezione cartella hello  
   ![Immagine di trigger FTP 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Seleziona hello  **>**  (freccia destra) e cartella toofind hello che si vuole toomonitor per file nuovi o modificati. Selezionare la cartella hello e cartella hello viene ora visualizzato nella hello **cartella** controllo.  
   ![Immagine di trigger FTP 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

A questo punto, l'app di logica è stato configurato con un trigger che verrà avviata un'esecuzione di hello altre azioni nel flusso di lavoro hello e il trigger quando un file viene modificato o creato nella cartella FTP specifico hello. 

> [!NOTE]
> Per un toobe di app logica funzionale, deve contenere almeno un trigger e un'azione. Seguire passaggi hello hello successiva sezione tooadd un'azione.  
> 
> 

## <a name="use-a-ftp-action"></a>Usare un'azione FTP
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Dopo avere aggiunto un trigger, seguire questi tooadd passaggi un'azione che verrà visualizzato contenuto hello del file hello nuove o modificate, è stato trovato dal trigger hello.    

1. Selezionare **+ nuovo passaggio** tooadd hello hello azione tooget hello contenuto file hello sul server FTP hello  
2. Seleziona hello **aggiungere un'azione** collegamento.  
   ![Immagine di azione FTP 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Immettere *FTP* toosearch per tutte le azioni correlate tooFTP.
4. Selezionare **FTP - ottenere il contenuto di file** come hello tootake azione quando viene trovato un file nuovo o modificato nella cartella hello FTP.      
   ![Immagine di azione FTP 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Hello **ottenere contenuto del file** controllo viene visualizzata. **Nota**: si sarà richiesta tooauthorize il tooaccess app logica al server FTP account se si è già stato in precedenza.  
   ![Immagine di azione FTP 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Seleziona hello **File** controllo (sotto lo spazio vuoto hello **FILE***). In questo caso, è possibile utilizzare uno qualsiasi dei hello varie proprietà dal file nuovi o modificati hello trovato nel server FTP hello.  
6. Seleziona hello **il contenuto di File** opzione.  
   ![Immagine di azione FTP 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. controllo di Hello viene aggiornato, indicante che hello **FTP - ottenere il contenuto di file** azione verrà visualizzato hello *il contenuto di file* file hello nuovi o modificati nel server FTP hello.      
   ![Immagine di azione FTP 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Salvare il lavoro, quindi aggiungere un tootest cartella FTP di file toohello il flusso di lavoro.    

A questo punto, hello logica app è stato configurato con toomonitor un trigger una cartella su un server FTP e un flusso di lavoro avviare hello a quando trova un nuovo file o un file modificato nel server FTP hello. 

Hello logica app è stato configurato con un contenuto di hello azione tooget file hello nuove o modificate.

È ora possibile aggiungere un'altra azione, ad esempio hello [SQL Server - Inserisci riga](connectors-create-api-sqlazure.md) contenuto hello tooinsert di azione del file hello di nuove o modificate in una tabella di database SQL.  

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)

