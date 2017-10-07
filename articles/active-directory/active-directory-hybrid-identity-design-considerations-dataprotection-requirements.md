---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - determinare i requisiti di protezione dati | Documenti Microsoft"
description: "Quando pianificazione della soluzione di identità ibride, identificare i requisiti di protezione dati hello per l'azienda e le opzioni sono disponibili toobest soddisfare questi requisiti."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Pianificare il potenziamento della sicurezza dei dati attraverso soluzioni d’identità avanzate
dati hello tooprotect Hello primo passaggio sono identificare chi può accedere a tali dati e come parte di questo processo è necessario toohave una soluzione di identità che si integra con le funzionalità di autenticazione e autorizzazione tooprovide sistema. L'autenticazione e l'autorizzazione vengono spesso confuse e i rispettivi ruoli fraintesi. In realtà sono molto diversi, come illustrato nella figura hello seguente:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Fasi del ciclo di vita di gestione dei dispositivi mobili**

Quando si pianifica la soluzione con identità ibrida è necessario comprendere i requisiti di protezione dati hello per l'azienda e le opzioni sono disponibili toobest soddisfano questi requisiti.

> [!NOTE]
> Dopo aver completato la pianificazione per la protezione dei dati, esaminare [determinare i requisiti di autenticazione a più fattori](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure che selezioni riguardanti i requisiti di autenticazione a più fattori non sono interessate dalle decisioni hello la apportate in questa sezione.
> 
> 

## <a name="determine-data-protection-requirements"></a>Determinare i requisiti di protezione dei dati
In età hello di mobilità, la maggior parte delle aziende hanno un obiettivo comune: abilitare le toobe utenti produttivi su dispositivi mobili in locale o in remoto da in qualsiasi punto della produttività tooincrease ordine. Anche se potrebbe trattarsi di un obiettivo comune, aziende che dispongono di tale requisito sarà anche preoccupazioni circa hello quantità delle minacce che devono essere affrontati in ordine tookeep dati aziendali sicura e mantenere la privacy dell'utente. Ogni società potrebbe avere requisiti diversi in questo senso; le regole di conformità diverso che variano in base della società di hello settore toowhich agisce verrà causare toodifferent decisioni di progettazione. 

Tuttavia, esistono alcuni aspetti di sicurezza che devono essere esaminate e convalidati, indipendentemente dal settore hello, che sono descritte nella sezione successiva hello.

## <a name="data-protection-paths"></a>Percorsi di protezione dei dati
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Percorsi di protezione dei dati**

In hello diagramma, il componente di identità hello sarà hello un primo toobe verificato prima dell'accesso a dati. Tuttavia, i dati possono essere in stati diversi durante la fase di hello che è avvenuto. Ogni numero del diagramma rappresenta un percorso in cui possono trovarsi i dati in un determinato momento nel tempo. I numeri vengono spiegati di seguito:

1. Protezione dei dati a livello di dispositivo hello.
2. Protezione dei dati in transito.
3. Protezione dei dati quando sono inattivi in locale.
4. Protezione dei dati inattivi nel cloud hello.

Anche se i controlli tecnici hello che consentono IT tooprotect hello dati su ognuno di tali fasi non sono disponibili direttamente da una soluzione con identità ibrida hello, è necessario che soluzione con identità ibrida hello è in grado di sfruttare sia in locale e cloud utente hello tooidentify delle risorse di gestione di identità prima di concedere accesso ai dati di toohello. Quando pianificazione della soluzione di identità ibrida accertarsi che hello seguenti domande in base ai requisiti dell'organizzazione tooyour:

## <a name="data-protection-at-rest"></a>Protezione dei dati inattivi
Indipendentemente dalla posizione dati hello inattivi (dispositivo, cloud o locale), è importante tooperform un'organizzazione di hello toounderstand di valutazione è necessario in questo senso. Per questa area, verificare che viene richiesto che hello seguenti domande:

* L'azienda necessita di tooprotect dati inattivi?
  * In caso affermativo, è toointegrate in grado di soluzioni di hello identità ibrida con l'infrastruttura locale esistente?
  * In caso affermativo, è toointegrate soluzione di identità ibrida hello in grado di carichi di lavoro che si trova nel cloud hello?
* È hello cloud identity management tooprotect in grado di hello credenziali dell'utente e altri dati archiviati nel cloud hello?

## <a name="data-protection-in-transit"></a>Protezione dei dati in transito
I dati in transito tra il dispositivo hello e Data Center hello o tra dispositivi hello e cloud hello devono essere protette. Il transito, tuttavia, non presuppone necessariamente un processo di comunicazione con un componente esterno al servizio cloud. È anche possibile, infatti, che i dati vengono spostati internamente, ad esempio tra due reti virtuali. Per questa area, verificare che viene richiesto che hello seguenti domande:

* L'azienda necessita di tooprotect dati in transito?
  * In caso affermativo, è toointegrate in grado di soluzioni di hello identità ibrida con controlli sicuri, ad esempio SSL/TLS?
* Gestione delle identità cloud hello mantiene hello traffico tooand all'interno dell'archivio di directory hello (all'interno e tra i Data Center) i firmato?

## <a name="compliance"></a>Conformità
Norme in materia di controllo e conformi ai requisiti normativi variano secondo settore toohello cui appartiene l'azienda. Le aziende in settori regolamentati elevate necessario risolvere problemi di toocompliance correlati problemi di gestione delle identità. Normative come Sarbanes-Oxley (SOX), hello Health Insurance Portability e Accountability Act (HIPAA), hello Gramm-Leach-Bliley Act (GLBA) e Payment Card Industry Data Security Standard (PCI DSS) hello sono molto rigidi relative identità e accessi. soluzione con identità ibrida Hello che verrà adottata la società deve disporre di funzionalità di base hello che verrà usata per soddisfare i requisiti di hello di uno o più di queste norme. Per questa area, verificare che viene richiesto che hello seguenti domande:

* È conforme ai requisiti normativi di hello per l'azienda soluzione con identità ibrida hello?
* Soluzione con identità ibrida hello fa incorpora una funzionalità che consentono a toobe conformi ai requisiti normativi ai requisiti della società? 

> [!NOTE]
> Annotare i tootake che ogni risposta e comprendere motivazioni hello delle risposte hello. [Definire la strategia di protezione dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) esaminerà le opzioni di hello disponibili e i vantaggi e svantaggi di ogni opzione.  Una volta fornite le risposte a queste domande, sarà possibile selezionare l'opzione più adatta in base alle esigenze aziendali.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
 [Determinare i requisiti di gestione dei contenuti](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Vedere anche
[Panoramica delle considerazioni di progettazione](active-directory-hybrid-identity-design-considerations-overview.md)

