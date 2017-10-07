---
title: "aaaAdministration e l'elenco di attività di sviluppo nei servizi BizTalk | Documenti Microsoft"
description: Pianificazione e processo di aiuto per la distribuzione di servizi BizTalk di Azure.
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Elenco dell’attività di Amministrazione e Sviluppo in Servizi BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Introduzione
Quando si lavora con i servizi BizTalk di Microsoft Azure, esistono diverse tooconsider componenti basati su cloud e locali. tooget avviato, prendere in considerazione hello flusso del processo seguente:  

| Passaggio | Chi è il responsabile | Attività | Collegamenti correlati |
| --- | --- | --- | --- |
| 1. |Amministratore |Creare hello utilizzando un account Microsoft o un account aziendale di sottoscrizione di Microsoft Azure |[portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Amministratore |Creare o eseguire il provisioning di un servizio BizTalk |[Creare un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Amministratore |Registrazione della distribuzione dei servizi BizTalk dell’azienda |[Registrazione e aggiornamento di una distribuzione del servizio BizTalk nel portale dei servizi BizTalk di hello](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Amministratore |Si applica se un'applicazione hello utilizzi il sistema Line-of-Business (LOB) locale di servizio Adapter BizTalk tooconnect tooan o una destinazione coda o argomento.  Creare hello Azure Service Bus Namespace. Assegnare questo spazio dei nomi, nome dell'autorità di certificazione del Bus di servizio e developer di toohello valori di chiave dell'autorità emittente Bus di servizio. |[Procedura: Creare o modificare uno spazio dei nomi del servizio Bus di servizio](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) e [Ottenere il Nome dell'autorità emittente e i Valori della chiave dell'autorità emittente](biztalk-issuer-name-issuer-key.md) |
| 5. |Developer |Installare SDK hello e creare il progetto BizTalk Service hello in Visual Studio. |[Installare Azure BizTalk Services SDK](https://msdn.microsoft.com/library/azure/hh689760.aspx) e [Creare endpoint di messaggistica avanzate in Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Developer |Distribuire il tooyour progetto BizTalk Service che BizTalk Service ospitato in Azure. |[Distribuzione e aggiornamento hello progetto di servizi BizTalk](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Amministratore |Si applica se usa EDI:  È possibile aggiungere partner e creare contratti nel portale di Microsoft Azure BizTalk Services hello. Quando si crea un contratto, è possibile aggiungere bridge hello e/o nelle trasformazioni create per le impostazioni dell'accordo toohello hello developer. |[Configurazione di EDI, AS2 ed EDIFACT nel portale dei Servizi BizTalk](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Amministratore |Utilizza hello portale di Azure classico, monitorare l'integrità di hello di BizTalk Service, incluse le metriche delle prestazioni. |[Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Amministratore |Tramite il portale Microsoft Azure BizTalk Services hello, gestire gli elementi di hello utilizzati dai servizi BizTalk e tenere traccia dei messaggi man mano che vengono elaborati dai file bridge hello. |[Utilizzo di hello portale dei servizi BizTalk](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Amministratore |Creare un piano di backup di tooback backup hello BizTalk Service. |[Continuità aziendale e ripristino di emergenza nei servizi BizTalk](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Passaggi successivi
[Esercitazioni ed esempi](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Creare il progetto hello in Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Installare l’SDK dei Servizi BizTalk di Azure](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Concetti
[Creare il progetto hello in Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 ed EDIFACT (Business tooBusiness) di messaggistica](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Altre risorse
[Aggiungere endpoint di messaggistica di origine, destinazione e bridge](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Imparare a usare e creare mappe e trasformazioni dei messaggi](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[Utilizzo di hello servizio Adapter BizTalk (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)

