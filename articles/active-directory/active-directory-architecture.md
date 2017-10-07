---
title: architettura di Azure Active Directory aaaUnderstand | Documenti Microsoft
description: "Spiega che cos'è un tenant di Azure AD e come toomanage Azure tramite Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Informazioni sull'architettura di Azure Active Directory
Consente di Azure Active Directory (Azure AD) è toosecurely gestire servizi di accesso tooAzure e risorse per gli utenti. In Azure AD è inclusa una suite completa di funzionalità di gestione delle identità. Per informazioni sulle funzionalità di Azure AD, vedere [Informazioni su Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis).

Con Azure AD, è possibile creare e gestire utenti e gruppi e abilitare tooallow autorizzazioni e negare l'accesso alle risorse tooenterprise. Per informazioni sulla gestione delle identità, vedere [hello nozioni di base della gestione delle identità di Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Architettura di Azure AD
Architettura distribuita geograficamente di Azure AD combina un controllo esteso, il reindirizzamento automatico, failover e funzionalità di recupero consentono toodeliver-disponibilità e prestazioni tooour clienti aziendali.

in questo articolo viene trattato i seguenti elementi dell'architettura Hello:
 *  Progettazione dell'architettura del servizio
 *  Scalabilità 
 *  Disponibilità continua
 *  Data center

### <a name="service-architecture-design"></a>Progettazione dell'architettura del servizio
Hello più comuni modo toobuild è un sistema di dati, a disponibilità elevata, scalabile tramite blocchi indipendenti o unità di scala per il livello di dati hello Azure AD, unità di scala vengono chiamate *partizioni*. 

livello dati Hello dispone di diversi servizi front-end che forniscono funzionalità di lettura / scrittura. diagramma di Hello seguente viene illustrato come i componenti di una partizione singola directory hello vengono distribuiti geograficamente distribuite data center. 

  ![Partizioni di directory singola](./media/active-directory-architecture/active-directory-architecture.png)

i componenti dell'architettura di Azure AD Hello includono una replica primaria e le repliche secondarie.

**Replica primaria**

Hello *replica primaria* riceve tutti *scrive* per partizione hello a cui appartiene. Qualsiasi operazione di scrittura tooa replicate immediatamente la replica secondaria in un altro Data Center prima della restituzione chiamante toohello esito positivo, assicurando con ridondanza geografica durabilità delle scritture.

**Repliche secondarie**

Tutte le *operazioni di lettura* delle directory vengono gestite dalle *repliche secondarie*, che si trovano in data center situati fisicamente in aree geografiche diverse. Esistono molte repliche secondarie perché i dati vengono replicati in modo asincrono. Letture di directory, ad esempio le richieste di autenticazione, vengono gestite i centri dati che sono i clienti tooour Chiudi. repliche secondarie Hello sono responsabili per la scalabilità di lettura.

### <a name="scalability"></a>Scalabilità

La scalabilità rappresenta il possibilità hello di un toomeet tooexpand servizio l'aumento di richieste di prestazioni. Scrivere la scalabilità è ottenuta tramite il partizionamento dati hello. La scalabilità di lettura è necessario replicare i dati da una partizione toomultiple le repliche secondarie distribuite in tutto il mondo hello.

Le richieste di applicazioni di directory sono in genere indirizzato toohello datacenter che sono fisicamente più vicini alla. Operazioni di scrittura sono coerenza di lettura / scrittura tooprovide replica primaria toohello reindirizzato in modo trasparente. Repliche secondarie estendono in modo significativo la scala hello di partizioni perché directory hello è sono in genere letture a soddisfare la maggior parte del tempo di hello.

Le applicazioni di directory connettersi toohello più vicino al Data Center. migliorando le prestazioni e rendendo quindi possibile l'aumento del numero di istanze. Poiché una partizione di directory può avere molti repliche secondarie, repliche secondarie possono essere inserite i client di directory toohello più vicino. Solo interno componenti del servizio di replica primaria di destinazione elevato della scrittura hello active direttamente.

### <a name="continuous-availability"></a>Disponibilità continua

Disponibilità (o tempi di attività) definisce il possibilità hello di un sistema di tooperform senza interruzioni. Hello chiave tooAzure AD elevata disponibilità è che i nostri servizi possono diventare in fretta il traffico tra più centri dati distribuiti geograficamente. Ogni data center è indipendente e ciò abilita le modalità di errore con annullamento della correlazione.

Progettazione delle partizioni di Azure AD è semplificata toohello confrontati enterprise struttura di Active Directory che è fondamentale per la scalabilità verticale sistema hello. È stato adottato uno schema master singolo che include un processo di failover della replica primaria deterministico e orchestrato con attenzione.

**Tolleranza di errore**

Un sistema è più disponibile in caso di errori di tolleranza d'errore toohardware, rete e software. Per ogni partizione di directory hello, esiste una replica master a disponibilità elevata: replica primaria hello. Solo operazioni di scrittura toohello partizione vengono eseguite in questa replica. La replica è viene continuamente monitorata e scritture possono essere spostate immediatamente tooanother replica (che diventa hello nuovo database primario) se viene rilevato un errore. Durante il failover, è possibile che si verifichi una perdita di disponibilità in scrittura, in genere per 1-2 minuti. La disponibilità in lettura non è invece interessata durante questo intervallo di tempo.

Le operazioni di lettura (che sono maggiori di scritture di molti ordini di grandezza) passare solo toosecondary repliche. Poiché le repliche secondarie sono idempotenti, perdita di una qualsiasi replica in una determinata partizione viene compensata facilmente indirizzando hello letture tooanother replica, in genere hello stesso Data Center.

**Durabilità dei dati**

Un'operazione di scrittura è tooat duraturo almeno due data center tooit precedente riconosciuto. Ciò avviene per l'esecuzione del commit prima scrittura hello hello primario e quindi immediatamente la replica hello scrittura tooat almeno un altro data center. Ciò garantisce che un potenziale di perdita irreversibile di hello data center hosting hello primario non comporta la perdita di dati.

Azure AD gestisce uno zero [obiettivo tempo di ripristino (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) per l'emissione di token e di directory legge e scrive i in ordine di hello di minuti (5 minuti) RTO per directory. Viene anche mantenuto un [obiettivo del punto di ripristino (RPO, Recovery Point Objective)](https://en.wikipedia.org/wiki/Recovery_point_objective) pari a zero e non si verificheranno perdite di dati in caso di failover.

### <a name="data-centers"></a>Data center

Le repliche di Azure AD vengono archiviate in dislocati in tutto il mondo hello. Per altre informazioni, vedere [Data center Azure](https://azure.microsoft.com/en-us/overview/datacenters).

Azure AD opera tra data center con hello seguenti caratteristiche:

 * L'autenticazione, grafico e altri servizi di Active Directory si trovano dietro il servizio Gateway hello. Hello Gateway gestisce il bilanciamento del carico di questi servizi. Verrà eseguito il failover automatico se viene rilevato che server non integri usano probe di integrità transazionali. In base a questi probe di integrità, hello Gateway instrada in modo dinamico il traffico toohealthy data center.
 * Per *legge*, hello directory dispone di repliche e i servizi front-end corrispondenti in una configurazione attivo-attivo opera in più data center. In caso di errore di un intero data center, il traffico sarà automaticamente indirizzato tooa altro Data Center.
 *  Per *scrive*, hello directory verrà failover (master) replica primaria tra i data Center tramite pianificato (nuovo database primario è sincronizzata tooold primario) o procedure di failover di emergenza. Durabilità dei dati avviene mediante la replica di qualsiasi commit tooat almeno due data center.

**Coerenza dei dati**

modello di directory Hello è uno dei coerenza finale. Uno dei problemi tipici dei sistemi distribuiti di replica in modo asincrono è che i dati di hello restituiti da una replica "specifica" potrebbero non essere backup toodate. 

Azure Active Directory fornisce la coerenza di lettura / scrittura per applicazioni destinate a una replica secondaria tramite la replica primaria toohello di scritture di routing e in modo sincrono pull hello riscrive toohello replica secondaria.

Applicazione scrive utilizzando hello API Graph di Azure AD vengono ricavati dalla gestione di replica directory tooa di affinità per la coerenza di lettura / scrittura. servizio di Azure AD Graph Hello gestisce una sessione logica, che include replica secondaria tooa di affinità utilizzato per le letture; l'affinità viene acquisita in un "replica token" hello cache servizio grafico utilizzando una cache distribuita. Questo token viene quindi utilizzato per le operazioni successive hello stessa sessione logica. 

 >[!NOTE]
 >Operazioni di scrittura vengono replicate immediatamente letture toohello replica secondaria toowhich hello logico della sessione sono state rilasciate.
 >

**Protezione dei backup**

directory Hello implementa eliminazioni reversibili, invece di eliminazioni di disco rigide, per gli utenti e i tenant per il ripristino semplice in caso di eliminazione accidentale di un cliente. Se l'amministratore del tenant accidentalmente eliminati gli utenti possono annullare e ripristinare gli utenti di hello eliminato. 

Azure AD implementa backup giornalieri di tutti i dati e quindi può ripristinare autorevolmente i dati in caso di eliminazioni logiche o danneggiamenti. Il livello dati usa i codici di correzione degli errori e può quindi verificare la presenza di errori e correggere automaticamente determinati tipi di errori del disco.

**Metriche e monitoraggio**

L'esecuzione di un servizio a disponibilità elevata richiede funzionalità di monitoraggio e metriche di alto livello. Azure AD analizza e segnala ininterrottamente le principali metriche sull'integrità del servizio e i criteri di successo per ogni servizio. Vengono continuamente sviluppate e ottimizzate metriche e funzionalità di monitoraggio e avviso per ogni scenario, in ogni singolo servizio di Azure AD e nell'insieme di tutti i servizi.

Se qualsiasi servizio di Azure AD non funziona come previsto, è immediatamente richiedere funzionalità toorestore azione più rapidamente possibile. Hello tracce più importanti di metrica Azure AD è rapidità con cui è possibile rilevare e limitare un cliente o live problema del sito. È investire molto in Monitoraggio e avvisi toominimize ora toodetect (destinazione TTD: < 5 minuti) e conformità operational toominimize ora toomitigate (destinazione TTM: < 30 minuti).

**Operazioni sicure**

Vengono usati controlli operativi, ad esempio Multi-Factor Authentication (MFA), per tutte le operazioni, oltre al controllo di tutte le operazioni. Inoltre, è usare un elevazione just-in-time sistema toogrant necessarie temporaneo l'accesso per qualsiasi attività su richiesta operativa in tempo reale. Per ulteriori informazioni, vedere [hello attendibili Cloud](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Passaggi successivi
[Guida per gli sviluppatori di Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

