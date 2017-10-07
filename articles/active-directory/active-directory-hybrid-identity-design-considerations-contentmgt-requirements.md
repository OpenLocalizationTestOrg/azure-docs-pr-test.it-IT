---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di gestione del contenuto | Documenti Microsoft"
description: "Fornisce informazioni approfondite come toodetermine hello requisiti di gestione dei contenuti dell'azienda. In genere quando un utente ha il proprio dispositivo potrebbe essere anche più credenziali che verranno essere alternati applicazione toohello in base che utilizza. È importante toodifferentiate il contenuto è stato creato utilizzando le credenziali personali rispetto a quelli creati utilizzando le credenziali aziendale hello. La soluzione di identità deve essere in grado di toointeract con cloud services tooprovide un utente finale di esperienza toohello durante garantire la privacy e aumentare la protezione di hello da perdita di dati."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Determinare i requisiti di gestione dei contenuti per una soluzione di identità ibrida
Informazioni sui requisiti di gestione dei contenuti hello per l'azienda può indirizzare influire sulla decisione su quale toouse soluzione di identità ibride. Con hello proliferazione di più dispositivi e dalla capacità di hello di utenti toobring i propri dispositivi ([BYOD](http://aka.ms/byodcg)), società hello devono proteggere i propri dati ma anche necessario tenere privacy dell'utente intatto. In genere quando un utente ha il proprio dispositivo potrebbe essere anche più credenziali che verranno essere alternati applicazione toohello in base che utilizza. È importante toodifferentiate il contenuto è stato creato utilizzando le credenziali personali rispetto a quelli creati utilizzando le credenziali aziendale hello. La soluzione di identità deve essere in grado di toointeract con cloud services tooprovide un utente finale di esperienza toohello durante garantire la privacy e aumentare la protezione di hello da perdita di dati. 

La soluzione di identità verrà utilizzata dai diversi controlli tecnici nella gestione dei contenuti tooprovide ordine come illustrato nella figura hello seguente:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Controlli di protezione che interessano il sistema di gestione delle identità**

In generale, i requisiti di gestione dei contenuti verranno utilizzati il sistema di gestione di identità in hello seguenti aree:

* Privacy: identificazione utente hello che possiede una risorsa e applicare l'integrità toomaintain hello controlli appropriati.
* Classificazione dei dati: identificare l'utente hello o gruppo e il livello di oggetto tooan accesso in base tooits classificazione. 
* Protezione di perdita di dati: i controlli di sicurezza responsabili della protezione tooavoid perdita dei dati saranno necessario toointeract con hello identità sistema toovalidate hello identità dell'utente. Questo aspetto è importante anche per eventuali esigenze di auditing.

> [!NOTE]
> Leggere l'articolo sulla [classificazione dei dati per la conformità al cloud](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) per maggiori informazioni sulle linee guida e le procedure consigliate per la classificazione dei dati.
> 
> 

Quando pianificazione della soluzione di identità ibrida accertarsi che hello seguenti domande in base ai requisiti dell'organizzazione tooyour:

* L'azienda prevede dei controlli di sicurezza in luogo tooenforce privacy dei dati?
  * In caso affermativo, i controlli di sicurezza sarà in grado di toointegrate con una soluzione con identità ibrida hello siano tooadopt corso?
* È presente in azienda un sistema di classificazione dei dati?
  * In caso affermativo, è toointegrate hello corrente soluzione in grado di soluzione con identità ibrida hello siano tooadopt corso?
* È presente in azienda un sistema di protezione contro la perdita di dati? 
  * In caso affermativo, è toointegrate hello corrente soluzione in grado di soluzione con identità ibrida hello siano tooadopt corso?
* L'azienda necessita di tooaudit accesso tooresources?
  * In caso affermativo, che tipo di risorse?
  * Quale livello di informazioni è necessario?
  * In caso affermativo, in cui deve risiedere il log di controllo di hello? Locale o nel cloud hello?
* L'azienda necessita tooencrypt eventuali messaggi di posta elettronica che contengono dati riservati (SSNs, i numeri di carta di credito e così via)?
* L'azienda necessita tooencrypt tutti i documenti o contenuto condiviso con i partner commerciali esterni?
* L'azienda necessita di criteri aziendali di tooenforce su determinati tipi di messaggi di posta elettronica (non Rispondi a tutti, non inoltrare)?

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Definire la strategia di protezione dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esaminerà le opzioni di hello disponibili e i vantaggi e svantaggi di ogni opzione.  Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Determinare i requisiti di controllo di accesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

