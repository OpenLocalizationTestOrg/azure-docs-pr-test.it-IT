---
title: aaaLearn sulla limitazione delle richieste nei servizi BizTalk | Documenti Microsoft
description: "Informazioni sulle soglie di limitazione delle richieste e sui relativi comportamenti di runtime per Servizi BizTalk. La limitazione delle richieste è basata sull'utilizzo della memoria e sul numero di messaggi. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>Servizi BizTalk: limitazione

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servizi BizTalk di Azure implementa una limitazione del servizio in base alle due condizioni: numero di hello e utilizzo della memoria di elaborazione di messaggi simultanei. In questo argomento vengono elencate le soglie di limitazione hello e viene descritto il comportamento di Runtime hello quando si verifica una condizione di limitazione.

## <a name="throttling-thresholds"></a>Soglie di limitazione
Nella seguente sono elencati nella tabella Hello hello origine limitazione delle richieste e le soglie:

|  | Descrizione | Soglia inferiore | Soglia superiore |
| --- | --- | --- | --- |
| Memoria |Percentuale di memoria totale del sistema disponibile/byte file di paging. <p><p>PageFileBytes disponibile totale è circa 2 volte hello RAM di sistema hello. |60% |70% |
| Elaborazione di messaggi |Numero di messaggi elaborati simultaneamente |40 * numero di memorie centrali |100 * numero di memorie centrali |

Quando viene raggiunta una soglia elevata, i servizi BizTalk di Azure avvia toothrottle. Interrompe la limitazione delle richieste quando viene raggiunta la soglia inferiore hello. Se ad esempio il servizio utilizza il 65% della memoria di sistema, In questo caso, il servizio di hello non rallenta. Se invece il servizio inizia a utilizzare il 70% della memoria di sistema, In questo caso, il servizio di hello limita e continua toothrottle fino a quando il servizio di hello utilizza memoria di sistema di 60% (soglia inferiore).

Servizi BizTalk di Azure tiene traccia hello la limitazione delle richieste di stato (stato normale e lo stato di limitato) e la limitazione della durata hello.

## <a name="runtime-behavior"></a>Comportamento in fase di esecuzione
Quando i servizi BizTalk di Azure passa allo stato di limitazione delle richieste, si verifica hello segue:

* La limitazione viene applicata a ogni istanza del ruolo, Ad esempio:<br/>
  IstanzaRuoloA è limitata. IstanzaRuoloB non è limitata. In questa situazione, i messaggi in IstanzaRuoloB vengono elaborati come previsto. I messaggi di RoleInstanceA vengono ignorati e non riuscire con hello errore seguente:<br/><br/>
  **Il server è occupato. Riprovare più tardi.**<br/><br/>
* Nessuna origine di pull esegue il polling o scarica un messaggio, Ad esempio:<br/>
  Una pipeline effettua il pull dei messaggi da un'origine FTP esterna. istanza del ruolo Hello esegue il pull di hello ottiene in uno stato di limitazione delle richieste. In questo caso, la pipeline hello arresta download altri messaggi fino a quando l'istanza del ruolo hello arresta la limitazione delle richieste.
* Una risposta viene inviata toohello client in modo da client hello è possibile inviare di nuovo il messaggio hello.
* È necessario attendere fino a quando la limitazione delle richieste di hello viene risolto. In particolare, è necessario attendere fino a quando non viene raggiunta la soglia inferiore hello.

## <a name="important-notes"></a>Note importanti
* Non è possibile disabilitare la limitazione.
* Non è possibile modificare le soglie di limitazione.
* La limitazione viene implementata nell'intero sistema.
* Hello Server di Database SQL di Azure dispone anche di limitazione incorporato.

## <a name="additional-azure-biztalk-services-topics"></a>Argomenti aggiuntivi su Servizi BizTalk di Azure
* [L'installazione di hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Servizi BizTalk: Esercitazioni ed esempi](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Vedere anche
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Servizi BizTalk: Tabella degli stati del servizio](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Servizi BizTalk: Schede Dashboard, Monitoraggio, Scalabilità](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Servizi BizTalk: backup e ripristino](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Servizi BizTalk: nome e chiave dell'autorità emittente](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

