---
title: 'Analisi di flusso: Ruotare le credenziali di accesso per input e output | Documentazione Microsoft'
description: Informazioni su come hello tooupdate le credenziali per l'output e input flusso Analitica.
keywords: credenziali di accesso
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Ruotare le credenziali di accesso per input e output nei processi di analisi di flusso
## <a name="abstract"></a>Sunto
Analitica di flusso di Azure attualmente non consente sostituendo le credenziali di hello su un input/output durante il processo di hello è in esecuzione.

Mentre Analitica di flusso di Azure supporta la ripresa di un processo dall'ultimo output, Desideravamo intero processo di hello tooshare per ridurre al minimo ritardo hello tra hello l'arresto e avvio del processo di hello e la rotazione di credenziali di accesso hello.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Parte 1: preparare nuovo set di credenziali di hello:
Questa parte è applicabile toohello degli input/output seguente:

* Archiviazione BLOB
* Hub eventi
* Database SQL
* Archiviazione tabelle

Per altri input/output, andare alla Parte 2.

### <a name="blob-storagetable-storage"></a>Archiviazione BLOB/Archiviazione tabelle
1. Visitare toohello dell'estensione di archiviazione nel portale di gestione di Azure hello:  
   ![graphic1][graphic1]
2. Individuare utilizzato dal processo di archiviazione di hello e passare al suo interno:  
   ![graphic2][graphic2]
3. Fare clic sul comando Gestisci chiavi di accesso hello:  
   ![graphic3][graphic3]
4. Tra hello chiave di accesso primaria e chiave di accesso secondaria, hello **pick hello non utilizzato dal processo di**.
5. Premere l’opzione di rigenerazione:   
   ![graphic4][graphic4]
6. Copiare la chiave hello appena generato:  
   ![graphic5][graphic5]
7. Continuare tooPart 2.

### <a name="event-hubs"></a>Hub eventi
1. Passare l'estensione di Service Bus toohello nel portale di gestione di Azure hello:  
   ![graphic6][graphic6]
2. Individuare hello Namespace Bus di servizio utilizzato per il processo e passare al suo interno:  
   ![graphic7][graphic7]
3. Se il processo utilizza un criterio di accesso condiviso su hello Service Bus Namespace, passare toostep 6  
4. Consente di passare toohello scheda di hub eventi:  
   ![graphic8][graphic8]
5. Individuare hello utilizzato dal processo di Hub di eventi e passare al suo interno:  
   ![graphic9][graphic9]
6. Consente di passare toohello scheda Configura:  
   ![graphic10][graphic10]
7. Nel menu a discesa Nome criterio hello, individuare i criteri di accesso condiviso hello utilizzato dal processo di:  
   ![graphic11][graphic11]
8. Tra hello chiave primaria e chiave secondaria, hello **pick hello non utilizzato dal processo di**.  
9. Premere l’opzione di rigenerazione:   
   ![graphic12][graphic12]
10. Copiare la chiave hello appena generato:  
   ![graphic13][graphic13]
11. Continuare tooPart 2.  

### <a name="sql-database"></a>Database SQL
> [!NOTE]
> Nota: è necessario tooconnect toohello servizio Database SQL. Verrà tooshow come toodo questo utilizzando hello esperienza di gestione nel portale di gestione di Azure hello ma è possibile scegliere toouse nonché uno strumento sul lato client, ad esempio SQL Server Management Studio.
>
> 

1. Passare l'estensione database SQL toohello nel portale di gestione di Azure hello:  
   ![graphic14][graphic14]
2. Individuare i Database SQL utilizzato dal processo di hello e **fare clic su server hello** collegamento su hello stessa riga:  
   ![graphic15][graphic15]
3. Fare clic sul comando Gestisci hello:  
   ![graphic16][graphic16]
4. Digitare master del database:   
   ![graphic17][graphic17]
5. Immettere il nome utente, la password e fare clic su Accedi:   
   ![graphic18][graphic18]
6. Fare clic su Nuova query:   
   ![graphic19][graphic19]
7. Tipo di hello seguente query sostituendo < login_name > con il nome utente e la sostituzione <enterStrongPasswordHere> con la nuova password:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Fare clic su Esegui:   
   ![graphic20][graphic20]
9. Tornare indietro toostep 2 e questa volta scegliere database hello:  
   ![graphic21][graphic21]
10. Fare clic sul comando Gestisci hello:  
   ![graphic22][graphic22]
11. Digitare il nome utente, la password e fare clic su Accedi:   
   ![graphic23][graphic23]
12. Fare clic su Nuova query:   
   ![graphic24][graphic24]
13. Digitare nella seguente query sostituendo < nome_utente > con un nome con cui si desidera tooidentify hello questo account di accesso nel contesto di hello del database (è possibile fornire hello stesso valore scelto per < login_name >, ad esempio) e sostituendo < login_name > con il nuovo nome utente:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Fare clic su Esegui:   
   ![graphic25][graphic25]
15. A questo punto è necessario fornire un nuovo utente hello stessi ruoli e i privilegi assegnati all'utente originale.
16. Continuare tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Parte 2: Arresto hello Analitica del processo di flusso
1. Visitare estensione Analitica flusso toohello nel portale di gestione di Azure hello:  
   ![graphic26][graphic26]
2. Individuare il processo e accedervi:   
   ![graphic27][graphic27]
3. Passare toohello input scheda o hello output in base a rotazione se credenziali hello su un Input o su un Output.  
   ![graphic28][graphic28]
4. Fare clic sul comando di arresto hello e confermare processo hello è stato arrestato.  
   ![graphic29][graphic29] attendere toostop processo hello.
5. Individuare hello input/output desiderato credenziali toorotate on e passare al suo interno:  
   ![graphic30][graphic30]
6. Procedere tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Parte 3: Modifica delle credenziali di hello nel processo di flusso Analitica hello
### <a name="blob-storagetable-storage"></a>Archiviazione BLOB/Archiviazione tabelle
1. Trovare il campo chiave dell'Account di archiviazione hello e incollare la chiave appena generata:  
   ![graphic31][graphic31]
2. Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:  
   ![graphic32][graphic32]
3. Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.
4. Procedere tooPart 4.

### <a name="event-hubs"></a>Hub eventi
1. Trovare il campo chiave criterio Hub eventi hello e incollare la chiave appena generata:  
   ![graphic33][graphic33]
2. Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:  
   ![graphic34][graphic34]
3. Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.
4. Procedere tooPart 4.

### <a name="power-bi"></a>Power BI
1. Fare clic su autorizzazione rinnovo hello:  

   ![graphic35][graphic35]
2. Verrà visualizzato hello seguito conferma:  

   ![graphic36][graphic36]
3. Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:  
   ![graphic37][graphic37]
4. Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.
5. Procedere tooPart 4.

### <a name="sql-database"></a>Database SQL
1. Trovare i campi nome utente e Password di hello e incollare l'insieme di credenziali appena creato:  
   ![graphic38][graphic38]
2. Fare clic sul comando Salva hello e confermare il salvataggio delle modifiche:  
   ![graphic39][graphic39]
3. Al salvataggio delle modifiche, verrà automaticamente avviato un test di connessione. Assicurarsi che abbia esito positivo.  
4. Procedere tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Parte 4: avvio del processo dall’ora dell’ultimo arresto
1. Abbandona hello Input/Output:  
   ![graphic40][graphic40]
2. Fare clic sul comando di avvio hello:  
   ![graphic41][graphic41]
3. Selezionare ora ultimo arresto hello e fare clic su OK:  
   ![graphic42][graphic42]
4. Procedere tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Parte 5: Rimozione di hello precedente set di credenziali
Questa parte è applicabile toohello degli input/output seguente:

* Archiviazione BLOB
* Hub eventi
* Database SQL
* Archiviazione tabelle

### <a name="blob-storagetable-storage"></a>Archiviazione BLOB/Archiviazione tabelle
Ripetere parte 1 per la chiave di accesso utilizzato dal processo di hello toorenew hello ora inutilizzati chiave di accesso.

### <a name="event-hubs"></a>Hub eventi
Ripetere parte 1 per la chiave utilizzata per il processo di hello toorenew hello chiave ora inutilizzati.

### <a name="sql-database"></a>Database SQL
1. Tornare indietro toohello finestra di query da parte 1 passaggio 7 e tipo di query seguente, sostituendo < previous_login_name > con il nome utente utilizzato in precedenza per il processo di hello di hello:  
   `DROP LOGIN <previous_login_name>`  
2. Fare clic su Esegui:   
   ![graphic43][graphic43]  

È necessario ottenere hello seguito conferma: 

    Command(s) completed successfully.

## <a name="get-help"></a>Ottenere aiuto
Per assistenza, provare il [Forum di Analisi di flusso di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

