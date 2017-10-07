---
title: "Considerazioni sulla progettazione di aaaAzure Active Directory ibrido identità - Panoramica | Documenti Microsoft"
description: "Panoramica e mappa dei contenuti della guida alle considerazioni sulla progettazione di identità ibrida"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Considerazioni di progettazione dell'identità ibrida di Azure Active Directory 
Proliferazione sono dispositivi basati su consumer HelloWorld aziendali e applicazioni basate su cloud di software-as-a-service (SaaS) sono tooadopt semplice. Come risultato, mantenere il controllo sull’accesso alle applicazioni degli utenti tra centri dati interni e piattaforme cloud è arduo.  

Soluzioni di gestione identità Microsoft span locale e le funzionalità basate su cloud, la creazione di una singola identità utente per l'autenticazione e autorizzazione tooall risorse, indipendentemente dalla posizione. Tutto questo viene chiamato Identità ibrida. Esistono diverse opzioni di progettazione e configurazione per Gestione identità ibride con le soluzioni Microsoft, e in alcuni casi potrebbe essere difficile toodetermine quale combinazione soddisfi meglio alle esigenze di hello dell'organizzazione. 

Questa Guida di considerazioni sulla progettazione di identità ibride consentono toounderstand come una soluzione con identità ibrida che meglio si adatta a tecnologia e business hello toodesign necessario per l'organizzazione.  Questa guida illustra in dettaglio una serie di passaggi e attività che è possibile seguire toohelp si progetta una soluzione con identità ibrida che soddisfi requisiti specifici dell'organizzazione. Nei passaggi hello e nelle attività Guida hello verrà presentate le tecnologie rilevanti hello e funzionalità opzioni disponibile tooorganizations toomeet funzionale e qualità del servizio (ad esempio disponibilità, scalabilità, prestazioni, gestibilità e sicurezza) requisiti del livello. 

In particolare, gli obiettivi di Guida Considerazioni sulla progettazione identità ibrida hello sono hello tooanswer seguenti domande: 

* Operazioni di domande necessarie tooask e rispondere toodrive una progettazione specifica identità ibrida per una tecnologia o il dominio problematico che meglio soddisfa i requisiti?
* La sequenza di attività deve è possibile completare toodesign una soluzione con identità ibrida per hello tecnologia o il dominio problematico? 
* Quali opzioni di configurazione e di tecnologia di identità ibrida sono disponibili toohelp me soddisfare i requisiti? Quali sono i compromessi tra tali opzioni hello in modo che è possibile selezionare l'opzione migliore hello per la mia azienda?

## <a name="who-is-this-guide-intended-for"></a>A chi si rivolge questa guida?
 CIO, CITO, Chief Identity Architects, Enterprise Architects e IT Architects responsabili per la progettazione di una soluzione con identità ibrida per medie o grandi organizzazioni.

## <a name="how-can-this-guide-help-you"></a>Come può essere d’aiuto questa guida?
È possibile usare questa guida toounderstand toodesign una soluzione con identità ibrida che è in grado di toointegrate un cloud basati su sistema di gestione identità con corrente identità soluzione locale. 

Hello seguente grafico mostra un esempio di una soluzione con identità ibrida che consente agli amministratori IT toomanage toointegrate corrente Windows Server Active Directory soluzione locale con Microsoft Azure Active Directory tooenable utenti toouse singolo Sign-On (SSO) in applicazioni che si trovano nel cloud hello e in locale.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Hello sopra illustrazione è riportato un esempio di una soluzione con identità ibrida che si avvale di cloud services toointegrate con funzionalità locali in ordine tooprovide un processo di autenticazione degli utenti finali di esperienza single toohello e toofacilitate IT gestione tali risorse. Anche se può trattarsi di uno scenario molto comune, progettazione identità ibrida di ogni organizzazione è probabilmente toobe diversa hello esempio illustrato nella figura 1 a causa di requisiti toodifferent. 

Questa guida fornisce una serie di passaggi e attività che è possibile seguire toodesign una soluzione con identità ibrida che soddisfi requisiti specifici dell'organizzazione. Nel corso di hello seguenti passaggi e attività, funzionalità e tecnologie pertinenti hello Visualizza Guida hello opzioni disponibile tooyou toomeet funzionali e di servizio requisiti di qualità per l'organizzazione.

**Presupposti**: Avere esperienza con Windows Server, Servizi di Dominio di Active Directory e Azure Active Directory. In questo documento, si presuppone che il lettore cerchi il modo in cui queste soluzioni possano soddisfare le proprie necessità commerciali nella propria soluzione o in una soluzione integrata.

## <a name="design-considerations-overview"></a>Panoramica delle considerazioni di progettazione
Questo documento fornisce un set di passaggi e attività che è possibile seguire toodesign una soluzione con identità ibrida che meglio soddisfa le esigenze. Hello passaggi sono presentati in una sequenza ordinata. Considerazioni sulla progettazione che apprese nei passaggi successivi potrebbero richiedere toochange decisioni che prese nei passaggi precedenti, tuttavia, a causa di tooconflicting scelte di progettazione. Viene eseguito ogni tentativo di tooalert di conflitti di progettazione toopotential documento hello. 

Arriverà a progettazione hello che meglio soddisfa le esigenze solo dopo l'iterazione nei passaggi hello come numero di volte necessario tooincorporate tutte hello considerazioni illustrate nel documento hello. 

| Fase identità ibrida | Elenco argomenti |
| --- | --- |
| Determinazione dei requisiti d’identità |[Determinare le esigenze aziendali](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Determinare i requisiti di sincronizzazione della directory](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Determinare i requisiti di autenticazione a più fattori](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Definizione di una strategia di adozione dell’identità ibrida](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Pianificare il potenziamento della sicurezza dei dati attraverso soluzioni d’identità avanzate |[Determinare i requisiti di protezione dati](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Determinare i requisiti di gestione del contenuto](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Determinare i requisiti di controllo di accesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Determinare i requisiti di risposta agli eventi imprevisti](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Definire la strategia di protezione dei dati](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Pianificare il ciclo di vita dell’identità ibrida |[Determinare le attività per la soluzione ibrida di gestione delle identità](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Gestione della sincronizzazione](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Determinare la strategia di adozione di una soluzione per la gestione di un'identità ibrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Scaricare questa guida
È possibile scaricare una versione in formato pdf della Guida di considerazioni sulla progettazione di identità ibrida hello da hello [raccolta Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

