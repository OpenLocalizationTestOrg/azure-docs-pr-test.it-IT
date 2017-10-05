---
title: Risolvere i problemi relativi a Servizi BizTalk usando i log operazioni | Documentazione Microsoft
description: Informazioni su come risolvere i problemi relativi ai Servizi BizTalk mediante i log operazioni. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c0c83361f94ffd9c30d7fcc551ff4b85ad7d6fa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Servizi BizTalk: Risoluzione dei problemi mediante i log operazioni

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-the-operation-logs"></a>Cosa sono i log operazioni
I log operazioni costituiscono una funzionalità dei servizi di gestione disponibile sul portale di Azure classico che consente di visualizzare log cronologici delle operazioni eseguite nei servizi di Azure, inclusi i servizi BizTalk. La funzionalità consente di visualizzare i dati cronologici relativi alle operazioni di gestione nella sottoscrizione del servizio BizTalk eseguite negli ultimi 180 giorni.

> [!NOTE]
> Si tratta di una funzionalità che acquisisce i log unicamente per operazioni di gestione sui Servizi BizTalk, ad esempio quando il servizio è stato avviato, sottoposto a backup e così via. Viene tenuta traccia di queste operazioni a prescindere dal fatto che vengano eseguite dal portale di Azure classico o mediante le [API REST del servizio BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Per un elenco completo delle operazioni di cui viene tenuta traccia tramite i servizi di gestione, vedere [Operazioni di cui viene tenuta traccia tramite i servizi di gestione di Azure](#bizops).<br/><br/>
> Non vengono acquisiti log delle attività correlate al runtime del servizio BizTalk (ad esempio un messaggio elaborato da bridge e così via). Per visualizzare tali log, è utilizzare la visualizzazione Rilevamento del portale di Servizi BizTalk. Per ulteriori informazioni, vedere [Rilevamento di messaggi](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Visualizzazione dei log operazioni di Servizi BizTalk
1. Nel portale di Azure classico selezionare **Servizi di gestione**, quindi selezionare la scheda **Log operazioni**.
2. È possibile filtrare i log in base a diversi parametri quali sottoscrizione, intervallo di date, tipo di servizio (ad esempio Servizi BizTalk), nome del servizio o stato dell'operazione (Completata, Non riuscita).
3. Fare clic sul segno di spunta per visualizzare l'elenco filtrato. L'immagine seguente illustra le attività correlate a testbiztalkservice: ![Visualizzare i log delle operazioni][ViewLogs] 
4. Per visualizzare informazioni più dettagliate su una specifica operazione, selezionare la riga e fare clic su **Dettagli** nella barra delle attività nella parte inferiore.

## <a name="bizops"></a>Operazioni di cui viene tenuta traccia tramite i servizi di gestione di Azure
Nella tabella seguente sono elencate le operazioni di cui viene tenuta traccia tramite i servizi di gestione di Azure:

| Nome operazione | Attività |
| --- | --- |
| CreateBizTalkService |Operazione di creazione di un nuovo servizio BizTalk |
| DeleteBizTalkService |Operazione di eliminazione di un servizio BizTalk |
| RestartBizTalkService |Operazione di riavvio di un servizio BizTalk |
| StartBizTalkService |Operazione di avvio di un servizio BizTalk |
| StopBizTalkService |Operazione di arresto di un servizio BizTalk |
| DisableBizTalkService |Operazione di disabilitazione di un servizio BizTalk |
| EnableBizTalkService |Operazione di abilitazione di un servizio BizTalk |
| BackupBizTalkService |Operazione di backup di un servizio BizTalk |
| RestoreBizTalkService |Operazione di ripristino di un servizio BizTalk dal backup specificato |
| SuspendBizTalkService |Operazione di sospensione di un servizio BizTalk |
| ResumeBizTalkService |Operazione di ripresa di un servizio BizTalk |
| ScaleBizTalkService |Operazione di scalabilità orizzontale o verticale di un servizio BizTalk |
| ConfigUpdateBizTalkService |Operazione di aggiornamento della configurazione di un servizio BizTalk |
| ServiceUpdateBizTalkService |Operazione di aggiornamento o downgrade di un servizio BizTalk a una versione diversa |
| PurgeBackupBizTalkService |Operazione di cancellazione dei backup del servizio BizTalk che non rientrano nel periodo di conservazione |

## <a name="see-also"></a>Vedere anche
* [Backup del servizio BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Ripristino del servizio BizTalk da un backup](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Servizi BizTalk: Tabella degli stati del servizio](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Servizi BizTalk: limitazione](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Servizi BizTalk: nome e chiave dell'autorità emittente](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Come iniziare a usare l'SDK di Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

