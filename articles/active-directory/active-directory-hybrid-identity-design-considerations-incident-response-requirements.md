---
title: "aaaAzure considerazioni di progettazione di Active Directory ibrido identità - determinare i requisiti di eventi imprevisti rResponse | Documenti Microsoft"
description: "Determinare le funzionalità di monitoraggio e reporting per la soluzione con identità ibrida hello che può essere utilizzato da IT tootake azioni tooidentify e un potenziali minacce"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Determinare i requisiti di risposta agli eventi imprevisti per una soluzione di identità ibrida
Le organizzazioni di medie o grandi dimensioni saranno probabilmente necessario un [risposta agli eventi imprevisti di protezione](https://technet.microsoft.com/library/cc700825.aspx) in luogo toohelp IT agire di conseguenza toohello livello di evento imprevisto. sistema di gestione di identità Hello è un importante componente nel processo di risposta agli eventi imprevisti hello poiché può essere utilizzato toohelp identificare chi ha eseguito un'azione specifica rispetto a destinazione hello. soluzione con identità ibrida Hello deve essere in grado di tooprovide monitoraggio e reporting di funzionalità che possono essere sfruttate da IT tootake azioni tooidentify e contrastare una minaccia potenziale. In un piano di risposta tipica è hello seguenti fasi come parte del piano di hello:

1. Valutazione iniziale.
2. Comunicazione dell'evento.
3. Controllo dei danni e riduzione dei rischi.
4. Identificazione degli elementi danneggiati e livello di gravità.
5. Conservazione delle prove.
6. Parti tooappropriate di notifica.
7. Ripristino del sistema.
8. Documentazione.
9. Valutazione dei danni e dei costi.
10. Revisione del piano e del processo.

Durante l'identificazione di hello di quello a cui è stato compromesso e in fase di gravità, sarà necessario tooidentify hello i sistemi che sono stati compromessi, i file che sono stati eseguiti e determinano la sensibilità hello di tali file. Il sistema di identità ibrida deve essere in grado di toofulfill tooassist questi requisiti si identificazione utente hello apportate le modifiche. 

## <a name="monitoring-and-reporting"></a>Monitoraggio e reporting
Sistema di identità hello molte volte può inoltre aiutare nella fase di valutazione iniziale principalmente se sistema hello è compilato il controllo e funzionalità di creazione di report. Durante la valutazione iniziale hello, amministratore IT deve essere in grado di tooidentify un'attività sospetta, o di sistema hello deve essere in grado di tootrigger che automaticamente in base a un'attività configurata in precedenza. Molte attività potrebbe indicare un possibile attacco, ma in altri casi, un sistema configurato in modo errato potrebbe provocare tooa numero di falsi positivi in un sistema di rilevamento delle intrusioni. 

sistema di gestione di identità Hello deve assistere tooidentify gli amministratori IT e segnalare le attività sospette. In genere, è possibile soddisfare questi requisiti tecnici monitorando tutti i sistemi e adottando una funzionalità di reporting in grado di evidenziare potenziali minacce. Usa domande di hello sotto toohelp si progetta la soluzione con identità ibrida tenendo in requisiti di risposta agli eventi imprevisti considerazione:

* L'azienda ha già definito una risposta ad eventi imprevisti in materia di sicurezza?
  * In caso affermativo, viene hello corrente sistema di gestione di identità usato come parte del processo di hello?
* L'azienda necessita tooidentify tentativi di accesso sospetti dagli utenti in diversi dispositivi?
* L'azienda necessita di toodetect potenziali compromesso credenziali dell'utente?
* L'azienda necessita l'accesso e l'azione dell'utente tooaudit?
* L'azienda necessita tooknow quando un utente di Reimposta la password?

## <a name="policy-enforcement"></a>Imposizione dei criteri
Durante il controllo dei danni e la fase di riduzione dei rischi, è importante tooquickly ridurre gli effetti effettive e potenziali hello di un attacco. L'operazione che avranno a questo punto può fare hello differenza tra un minore e uno degli strumenti principale. la risposta esatta Hello dipenderà dall'organizzazione e la natura hello di attacco hello che trovano ad affrontare. Se la valutazione iniziale hello concluso che è stato compromesso un account, è necessario tooenforce criteri tooblock questo account. Che è solo un esempio in cui verrà utilizzato il sistema di gestione delle identità di hello. Usa domande di hello sotto toohelp che è progettare la soluzione con identità ibrida prendendo in considerazione la modalità con cui sarà criteri applicati tooreact tooan in corso incidente:

* L'azienda prevede dei criteri degli utenti di tooblock sul posto da accesso rete hello se necessario?
  * In caso affermativo, hello corrente soluzione esegue l'integrazione con sistema di gestione identità ibride hello siano tooadopt corso?
* L'azienda necessita di accesso condizionale tooenforce per gli utenti che sono in quarantena? 

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Definire la strategia di protezione dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esaminerà le opzioni di hello disponibili e i vantaggi e svantaggi di ogni opzione.  Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
[Definire la strategia di protezione dei dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

