---
title: Servizi BizTalk aaaTroubleshoot usando log operazioni | Documenti Microsoft
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
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Servizi BizTalk: Risoluzione dei problemi mediante i log operazioni

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Quali sono i registri operazioni hello
Registri operazioni è una funzionalità di servizi di gestione disponibile in hello portale classico di Azure che consente di tooview log cronologico delle operazioni eseguite in servizi di Azure, ad esempio servizi BizTalk. In questo modo i dati cronologici tooview toomanagement operazioni per la sottoscrizione di BizTalk Service precedenti fino a 180 giorni correlate.

> [!NOTE]
> Questa funzionalità acquisisce solo i log per operazioni di gestione in servizi di BizTalk, ad esempio quando hello è stato avviato, eseguito verso l'alto, e così via. Tali operazioni vengono rilevate indipendentemente se vengono eseguite dal portale di Azure classico hello o tramite hello [API REST dei servizi BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Per un elenco completo delle operazioni di cui viene tenuta traccia tramite i servizi di gestione, vedere [Operazioni di cui viene tenuta traccia tramite i servizi di gestione di Azure](#bizops).<br/><br/>
> Questo non acquisire i log di hello per le attività correlate tooBizTalk runtime del servizio (ad esempio, i messaggi elaborati dal bridge e così via). tooview questi log, utilizzare hello vista relativa al rilevamento dal portale di servizi BizTalk di hello. Per ulteriori informazioni, vedere [Rilevamento di messaggi](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Visualizzazione dei log operazioni di Servizi BizTalk
1. Nel portale di Azure classico hello, selezionare **servizi di gestione**, quindi selezionare hello **registri operazioni** scheda.
2. È possibile filtrare i registri di hello in base ai diversi parametri come sottoscrizione, l'intervallo di date, il tipo di servizio (ad esempio servizi di BizTalk), nome del servizio o lo stato dell'operazione di hello (Succeeded, Failed).
3. Selezionare hello segno di spunta tooview hello elenco filtrato. Hello figura seguente vengono illustrate le attività correlate tootestbiztalkservice: ![visualizzare log operazioni][ViewLogs] 
4. tooview ulteriori informazioni su un'operazione specifica, selezionare la riga hello e fare clic su **dettagli** hello sulla barra delle applicazioni nella parte inferiore di hello.

## <a name="bizops"></a>Operazioni di cui viene tenuta traccia tramite i servizi di gestione di Azure
Hello nella tabella seguente sono elencate hello operazioni che vengono rilevate tramite servizi di gestione di Azure hello:

| Nome operazione | Attività |
| --- | --- |
| CreateBizTalkService |Operazione toocreate un nuovo di BizTalk Service |
| DeleteBizTalkService |Operazione toodelete un BizTalk Service |
| RestartBizTalkService |Operazione toorestart un BizTalk Service |
| StartBizTalkService |Operazione toostart un BizTalk Service |
| StopBizTalkService |Operazione toostop un BizTalk Service |
| DisableBizTalkService |Operazione toodisable un BizTalk Service |
| EnableBizTalkService |Operazione tooenable un BizTalk Service |
| BackupBizTalkService |Operazione tooback backup un BizTalk Service |
| RestoreBizTalkService |Operazione toorestore un BizTalk Service dal backup specificato |
| SuspendBizTalkService |Operazione toosuspend un BizTalk Service |
| ResumeBizTalkService |Operazione tooresume un BizTalk Service |
| ScaleBizTalkService |Operazione tooscale a BizTalk Service verso l'alto o verso il basso |
| ConfigUpdateBizTalkService |Configurazione di hello operazione tooupdate di un BizTalk Service |
| ServiceUpdateBizTalkService |Operazione tooupgrade o il downgrade a una versione diversa di BizTalk Service tooa |
| PurgeBackupBizTalkService |Backup toopurge operazione di hello BizTalk Service esterno hello periodo di memorizzazione |

## <a name="see-also"></a>Vedere anche
* [Backup del servizio BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Ripristino del servizio BizTalk da un backup](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Servizi BizTalk: Tabella degli stati del servizio](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Servizi BizTalk: limitazione](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Servizi BizTalk: nome e chiave dell'autorità emittente](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

