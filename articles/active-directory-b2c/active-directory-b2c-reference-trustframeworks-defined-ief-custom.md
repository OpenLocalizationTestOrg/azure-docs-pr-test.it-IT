---
title: "Azure Active Directory B2C: riferimenti - Framework attendibilità | Microsoft Docs"
description: "Un argomento sui criteri personalizzati di Azure Active Directory B2C e hello identità esperienza Framework"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Definizione dei framework attendibilità basati sul Framework dell'esperienza di gestione delle identità di Azure AD B2C

Azure Active B2C di Directory (Azure AD B2C) i criteri personalizzati che utilizzano hello identità esperienza Framework forniscono dell'organizzazione con un servizio centralizzato. Questo servizio consente di ridurre la complessità di hello di federazione delle identità in una grande community di interesse. la complessità di Hello è ridotta tooa singola relazione di trust e uno scambio di metadati singolo.

Criteri personalizzati di Azure Active Directory B2C che utilizzano tooenable identità esperienza Framework hello è tooanswer hello seguenti domande:

- Quali sono hello legale, sicurezza, privacy e i criteri di protezione dati che devono essere rispettati?
- Chi sono i contatti hello e quali sono i processi di hello per diventare un partecipante accreditato?
- Chi sono hello accredited provider di informazioni di identità (anche noto come "provider di attestazioni") e ciò che offrono?
- Chi sono hello accredited relying party (e, facoltativamente, cosa è necessario il)?
- Quali sono hello tecnico "in transito hello" requisiti di interoperabilità per i partecipanti?
- Quali sono le regole operative "runtime" hello che devono essere applicate per lo scambio di informazioni di identità digitali?

tooanswer costruire tutte queste domande, criteri personalizzati di Azure Active Directory B2C che utilizzano hello di utilizzare Framework esperienza identità hello Trust Framework (TF). Esaminiamo ora questo costrutto e il suo contributo in questo senso.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Comprendere foundation di gestione della federazione e attendibilità Framework hello

Hello Framework Trust è una specifica scritta di hello identità, sicurezza, privacy e dati criteri di protezione devono essere conforme toowhich i partecipanti a una community di interesse.

L'identità federata rappresenta la base per ottenere la verifica delle identità degli utenti finali a livello di Internet. Delega le parti toothird di gestione di identità, una singola identità digitali per un utente finale può essere riutilizzata con più relying party.  

Garanzia di identità è necessario che il provider di identità (IdPs) e il provider di attributo (AtPs) rispettino toospecific sicurezza, privacy e criteri operativi e procedure consigliate.  Se non possono eseguire controlli diretti, relying party (RPs) necessario sviluppare le relazioni di trust con hello IdPs e AtPs sceglieranno toowork con.  

Man mano che aumenta il numero di hello di consumer e provider di informazioni di identità digitali, è difficile toocontinue management pairwise queste relazioni di trust, o anche hello pairwise scambio di metadati di documentazione tecnica di hello che ha richiesto la connettività di rete .  Gli hub di federazione hanno risolto questi problemi solo in parte.

### <a name="what-a-trust-framework-specification-defines"></a>Contenuto definito in una specifica di framework di attendibilità
TFs sono linchpins hello hello aprire Identity Exchange (OIX) attendibile del modello di Framework, in cui ogni community di interesse è governata da una determinata specifica di TF. Questa specifica di framework attendibilità definisce:

- **Hello metriche di sicurezza e privacy per la community di hello di interesse con la definizione di hello di:**
    - livelli di Hello di garanzia (LOA) che vengono offerti/richiesto dai partecipanti; ad esempio, un set ordinato di classificazioni di confidenza autenticità hello delle informazioni di identità digitali.
    - livelli di Hello di protezione (LOP) che vengono offerti/richiesto dai partecipanti; ad esempio, un set ordinato di punteggi di confidenza per la protezione di hello delle informazioni di identità digitale che sono gestite dai partecipanti della community di hello di interesse.

- **descrizione di hello informazioni di identità digitali che ha offerto/richiesto dai partecipanti Hello**.

- **criteri tecnici Hello per produzione e l'utilizzo di informazioni di identità digitali e quindi per la misurazione LOA e LOP. Scritto in genere criteri tra hello seguenti categorie di criteri:**
    - Criteri di verifica dell'identità, ad esempio *con quale rigore vengono controllate le informazioni sull'identità di un utente?*
    - Criteri di sicurezza, ad esempio *con quale rigore vengono protette l'integrità e la riservatezza delle informazioni?*
    - Criteri di privacy, ad esempio *quale controllo ha un utente sulle informazioni di identificazione personale*?
    - Criteri di capacità di sopravvivenza, ad esempio *come vengono gestite la continuità e la protezione delle informazioni di identificazione personale se un provider cessa l'attività?*

- **profili di tecniche di Hello per produzione e l'utilizzo di informazioni di identità digitali. Questi profili includono:**
    - Interfacce di ambito per le quali sono disponibili le informazioni su identità digitali al livello di verifica specificato.
    - Requisiti tecnici per l'interoperabilità in transito.

- **salve le descrizioni di hello diversi ruoli che i partecipanti della community di hello possono eseguire e hello qualifiche che sono necessari toofulfill questi ruoli.**

In questo modo una specifica di TF determina la modalità di scambio di informazioni di identità tra i partecipanti di hello della community di hello di interesse: relying party, l'identità e i provider di attributo e strumenti di verifica di attributo.

Una specifica di TF è uno o più documenti che fungono da un riferimento per la governance hello della community di hello di interesse che regola l'asserzione hello e utilizzo delle informazioni di identità digitali all'interno della community di hello. È un set di criteri documentato e procedure progettate attendibilità tooestablish identità digitali hello che vengono utilizzati per le transazioni online tra i membri di una community di interesse.  

In altre parole, una specifica di TF definisce le regole di hello per la creazione di un ecosistema di identità federativa valida per una community.

È attualmente presente contratto generalizzata vantaggio hello di tale approccio. È senza dubbio che trust specifiche del framework semplificano lo sviluppo di hello degli ecosistemi identità digitali con verificabile caratteristiche di sicurezza, sicurezza e privacy, vale a dire che possono essere riutilizzati in più comunità di interesse.

Per questo motivo, criteri personalizzati di Azure Active Directory B2C che utilizzano hello identità esperienza Framework utilizza specifica di hello come base per hello di rappresentazione di dati per l'interoperabilità di toofacilitate un TF.  

Criteri di Azure Active Directory B2C personalizzato che sfruttano hello identità esperienza Framework rappresentano una specifica di TF come una combinazione di dati leggibili dal computer e risorse umane. Alcune sezioni di questo modello (in genere le sezioni più orientati verso governance) vengono rappresentati come fa riferimento a documentazione di criteri di sicurezza e privacy toopublished insieme hello procedure relative (se presente). Altre sezioni descrivono in dettaglio hello metadati e runtime le regole di configurazione che facilitano l'automazione operativa.

## <a name="understand-trust-framework-policies"></a>Criteri di framework attendibilità

In termini di implementazione, hello specifica TF è costituito da un set di criteri che consentono il controllo completo esperienze e i comportamenti di identità.  Criteri personalizzati di Azure Active Directory B2C che sfruttano hello identità esperienza Framework abilitare si tooauthor e creare la propria TF tramite tali criteri dichiarativi che è possibile definire e configurare:

- riferimento al documento Hello o riferimenti che definiscono l'ecosistema di identità federativa hello della community di hello che correla toohello TF. Documentazione di TF toohello collegamenti sono. Hello operational (predefinito) "runtime" regole o i percorsi utente hello automatizzano e/o controllano exchange hello e l'utilizzo di attestazioni di hello. Questi percorsi utente sono associati a un livello di verifica e a un livello di protezione. Un criterio può quindi avere percorsi utente con livelli di verifica e livelli di protezione differenti.

- provider di attestazioni di provider di identità e attributo Hello o hello, community hello dei profili di documentazione tecnici di interesse e hello supportano insieme il riconoscimento LOA/LOP hello (out-of-band) che si riferisce toothem.

- integrazione di Hello con strumenti di verifica di attributo o un provider di attestazioni.

- Hello relying party community hello (tramite inferenza).

- metadati Hello per stabilire comunicazioni di rete tra i partecipanti. Questi metadati, insieme ai profili tecniche hello, vengono utilizzati durante una transazione tooplumb "in transito hello" interoperabilità tra hello relying party e altri partecipanti della community.

- Hello conversione di protocollo, se presente (ad esempio, SAML, OAuth2, WS-Federation e OpenID Connect).

- requisiti di autenticazione Hello.

- Hello a più fattori dell'orchestrazione se presente.

- Uno schema condiviso per tutte le attestazioni hello disponibili e tooparticipants i mapping di una community di interesse.

- Hello tutte le attestazioni di trasformazioni, con riduzione al minimo i dati possibili hello in questo contesto, exchange hello toosustain e l'utilizzo di attestazioni di hello.

- associazione di Hello e la crittografia.

- archiviazione di attestazioni Hello.

### <a name="understand-claims"></a>Attestazioni

> [!NOTE]
> Facciamo riferimento collettivamente tooall hello possibili tipi di informazioni di identità che potrebbe essere scambiata come "attestazioni": le attestazioni relative credenziale di autenticazione dell'utente finale, si di identity, il dispositivo di comunicazione, posizione fisica, identificazione personale gli attributi e così via.  
>
> Utilizziamo hello termine "attestazioni", anziché "attributi", perché le transazioni in linea, questi elementi di dati non sono fatti che possono essere verificati direttamente da hello relying party. Si tratta piuttosto asserzioni o attestazioni, sui fatti per cui hello relying party necessario sviluppare transazione richiesta sufficiente confidenza toogrant hello dell'utente finale.  
>
> Utilizziamo inoltre il termine hello "attestazioni" poiché Azure AD B2C sono criteri personalizzati che utilizzano hello identità esperienza Framework progettato exchange hello toosimplify di tutti i tipi di informazioni di identità digitali in modo coerente indipendentemente dal fatto hello sottostante protocollo è definito per il recupero di attributo o l'autenticazione utente.  Analogamente, viene usato il termine di hello toocollectively "provider di attestazioni" fanno riferimento a provider tooidentity, i provider di attributo e strumenti di verifica di attributo quando non si desidera toodistinguish tra funzioni specifiche.   

Questi determinano la modalità di scambio delle informazioni di identità tra una relying party, i provider di identità e di attributi e i verificatori di attributi. Stabiliscono i provider di identità e di attributi necessari per l'autenticazione di una relying party. Devono essere considerati un linguaggio specifico di dominio, ovvero un linguaggio di programmazione specializzato per un determinato dominio dell'applicazione con ereditarietà, istruzioni *if* e polimorfismo.

Questi criteri costituiscono hello leggibile parte hello TF costruire nei criteri personalizzati di Azure Active Directory B2C sfruttando hello Framework esperienza di identità. Includono tutti i dettagli operativi di hello, inclusi i provider di attestazioni e i metadati e profili tecnici, definizioni dello schema di attestazioni, le funzioni di trasformazione di attestazioni, viaggi utente che vengono compilati nell'orchestrazione operational toofacilitate e automazione.  

Vengono considerati come toobe *documenti living* perché è probabile che il relativo contenuto cambia nel tempo relative partecipanti attivi di hello dichiarati nei criteri di hello. Non vi è rischio di hello hello e le condizioni per partecipanti potrebbero cambiare.  

Il programma di installazione di federazione e di manutenzione sono notevolmente semplificati dagli relying party da in corso operazioni di riconfigurazione di trust e la connettività di schermatura come provider di attestazioni diverse/strumenti di verifica aggiunta o rimozione (rappresentata dalla community di hello) hello set di criteri.

L'interoperabilità è un'altra sfida importante. Provider di attestazioni aggiuntive/strumenti di verifica deve essere integrati, poiché le relying party sono toosupport improbabile tutti hello protocolli necessari. Criteri personalizzati di Azure Active Directory B2C risolvere il problema grazie al supporto di protocolli standard del settore e applicando i percorsi utente specifico quando il provider di attributi e le relying party non supporta le richieste di tootranspose hello stesso protocollo.  

I percorsi utente includono i profili di protocollo e i metadati che vengono utilizzati tooplumb "in transito hello" interoperabilità tra hello relying party e altri partecipanti. Sono previste inoltre regole di runtime operativo che sono messaggi di richiesta/risposta exchange informazioni tooidentity applicata per l'applicazione della conformità con i criteri pubblicati come parte della specifica di TF hello. il concetto di Hello di viaggi utente è toohello chiave personalizzazione dell'esperienza del cliente hello. Inoltre chiarezza luce sul funzionamento del sistema hello a livello di protocollo hello.

Alla base, applicazioni relying party e portali possono, in base al relativo contesto, richiamare Azure AD B2C criteri personalizzati che sfruttano hello identità esperienza Framework passando hello nome di un criterio specifico e con precisione il comportamento di hello e informazioni Exchange che desiderano senza qualsiasi muss, confusione o dei rischi.
