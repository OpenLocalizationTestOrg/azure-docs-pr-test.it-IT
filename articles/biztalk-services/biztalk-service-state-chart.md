---
title: aaaTasks consentiti in stati diversi o gli Stati nei servizi BizTalk | Documenti Microsoft
description: 'Hello azioni o operazioni consentite in stato MABS diverso: arresta, avvia, riavviare, sospendere, riprendere, eliminare, ridimensionare, aggiornare la configurazione e il supporto di'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Informazioni che è possibile eseguire utilizzando hello lo stato di BizTalk Service

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

A seconda dello stato corrente di hello di hello servizio BizTalk, sono presenti operazioni che è possibile o non è possibile eseguire hello servizio BizTalk.

Ad esempio, viene eseguito il provisioning di un nuovo servizio BizTalk nel portale di Azure classico hello. Quando viene completato correttamente, hello servizio BizTalk è in `active` stato. Stato attivo hello, puoi arrestare, sospendere ed eliminare il servizio BizTalk hello. Se si arresta il servizio di BizTalk hello, si verifica un errore di arresto, quindi hello servizio BizTalk passa tooa `StopFailed` stato. In hello `StopFailed` stato, è possibile riavviare il servizio di BizTalk hello. Se si tenta un'operazione che non è consentita, ad esempio ripresa, si verifica hello errore seguente:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Possibili stati di visualizzazione hello

nelle tabelle seguenti Hello sono operazioni hello elenco o le azioni che possono essere eseguite quando hello BizTalk Service è in uno stato specifico. Un ✔ significa hello operazione è consentita mentre è in tale stato. Una voce vuota significa hello operazione non può essere eseguita in tale stato.

| Stato del servizio | Inizia | Arresto | Riavvio | Sospensione | Riprendi | Eliminazione | Scalabilità | Aggiornamento <br/> Configurazione | Backup |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Attivo |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Disabled |  |  |  |  |  | ✔ | |  |  | 
| Suspended |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Arrestato | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Service Update Failed |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Vedere anche
* [Creare un BizTalk Service utilizzando hello portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Operazioni possibili in schede del dashboard, monitor e scale hello nei servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Il risultato con le edizioni Developer, Basic, Standard e Premium hello nei servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Come tooback di backup e ripristino di un BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Le limitazioni spiegate nei servizi BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Recuperare hello Bus di servizio e il controllo di accesso dell'autorità di certificazione dell'autorità di certificazione e di nome valori della chiave per il BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

