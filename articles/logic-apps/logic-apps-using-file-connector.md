---
title: aaaConnect tooon locale file System da Azure logica App | Documenti Microsoft
description: Connettere i sistemi di file locali tooon dal flusso di lavoro logica app tramite gateway dati locale di hello e connettore File System
keywords: file system
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Connettere i sistemi di file locale tooon logica App con connettore File System hello

Connettività di cloud ibrido è App toologic centrale, in tal caso toomanage dati e in modo sicuro l'accesso risorse locali, App per la logica è possibile usare gateway dati locale di hello. In questo articolo viene illustrata la modalità tooconnect tooan locale file system con uno scenario di base: copiare un file che tooa tooDropbox caricato condivisione file, quindi inviare un messaggio di posta elettronica.

## <a name="prerequisites"></a>Prerequisiti

- Installare e configurare più recente hello [gateway dati locale](https://www.microsoft.com/download/details.aspx?id=53127).
- Installare hello gateway dati più recenti in locale, versione 1.15.6150.1 o versione successiva. [Connessione gateway dati locale di toohello](http://aka.ms/logicapps-gateway) elenchi hello passaggi. gateway di Hello deve essere installato in un computer locale prima di continuare con il resto di hello dei passaggi di hello.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Aggiungere trigger e le azioni per la connessione a system file tooyour

1. Creare un'app per la logica e aggiungere il trigger Dropbox: **Quando viene creato un file** 
2. In trigger hello, scegliere **passaggio successivo** > **aggiungere un'azione**. 
3. Nella casella di ricerca hello, immettere `file system` in modo da visualizzare azioni tutte supportate per il connettore File System hello.

   ![Cercare il connettore file](media/logic-apps-using-file-connector/search-file-connector.png)

2. Scegliere hello **crea file** action e creare un file system tooyour di connessione.

   Se non si dispone di una connessione esistente, verrà richiesta toocreate uno.

   1. Selezionare **Connect via on-premises data gateway** (Connetti tramite gateway dati locale). Vengono visualizzare altre proprietà.
   2. Selezionare la cartella radice per il file system.
      
       > [!NOTE]
       > cartella radice Hello è la cartella padre principale di hello, che viene utilizzata per i percorsi relativi per tutte le azioni relative ai file. È possibile specificare una cartella locale nel computer di hello in cui è installato gateway dati locale di hello o cartella hello può essere una condivisione di rete che hello computer può accedere.

   3. Immettere nome utente hello e una password per gateway hello.
   4. Selezionare il gateway hello installata in precedenza.

       ![Configurare la connessione](media/logic-apps-using-file-connector/create-file.png)

3. Dopo aver fornito tutti i dettagli di hello, scegliere **crea**. 

   Logica App Configura e testa la connessione, assicurarsi che la connessione hello funziona correttamente. 
   Se la connessione hello è configurata correttamente, si noterà opzioni per l'azione di hello selezionata in precedenza. 
   connettore file system di Hello è ora pronto per l'utilizzo.

4. Specificare che si desidera file toocopy Dropbox toohello nella cartella radice per la condivisione di file locale.

   ![Azione Crea file](media/logic-apps-using-file-connector/create-file-filled.png)

5. Dopo la logica app copie hello file, aggiungere un'azione di Outlook che invia un messaggio di posta elettronica in modo che gli utenti sul nuovo file hello. Immettere i destinatari hello, titolo e il corpo del messaggio di posta elettronica hello. 

   Nel selettore contenuto dinamico hello, è possibile scegliere gli output di dati dal connettore file hello, pertanto è possibile aggiungere ulteriori posta elettronica toohello di dettagli.

   ![Azione Invia e-mail](media/logic-apps-using-file-connector/send-email.png)

6. Salvare l'app per la logica. Testare l'app caricando un file tooDropbox. file Hello deve ottenere toohello copiati in una condivisione locale e dovrebbe essere visualizzato un messaggio di posta elettronica sull'operazione hello.

   > [!TIP] 
   > Informazioni su come troppo[monitorare App per la logica](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Congratulazioni, ora è un'app di logica di lavoro che può connettersi tooyour nel file sistema locale. Provare a esplorare altre funzionalità che hello connettore offerte, ad esempio:

- Crea file
- Elenca i file nella cartella
- Aggiungi file
- Elimina file
- Recupera contenuto di file
- Recupera contenuto di file tramite percorso
- Recupera metadati di file
- Recupera metadati di file tramite percorso
- Elenca i file nella cartella radice
- Aggiorna file

## <a name="view-hello-swagger"></a>Swagger hello vista
Vedere hello [swagger dettagli](/connectors/fileconnector/). 

## <a name="get-help"></a>Ottenere aiuto

rispondere alle domande di domande tooask, e informazioni su quali altri logica app di Azure in caso di utenti, visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare Azure logica App e connettori, votare o inviare idee in hello [sito commenti e suggerimenti dell'utente di Azure logica app](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

- [Connettere i dati locali tooon](../logic-apps/logic-apps-gateway-connection.md) da logica App
- Informazioni su [Enterprise Integration](../logic-apps/logic-apps-enterprise-integration-overview.md)
