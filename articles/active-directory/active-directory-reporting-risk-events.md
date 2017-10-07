---
title: eventi di rischio di Active Directory aaaAzure | Documenti Microsoft
description: Questo argomento presenta una panoramica dettagliata degli eventi di rischio.
services: active-directory
keywords: "Azure Active Directory Identity Protection, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
author: MarkusVi
manager: femila
ms.assetid: fa2c8b51-d43d-4349-8308-97e87665400b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d771c1f43707744aac728c4f72000d855cbd6e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-risk-events"></a>Eventi di rischio di Azure Active Directory

Posizionare Hello gran parte richiedere violazioni della sicurezza degli utenti malintenzionati ad ambiente tooan accesso dal furto di identità dell'utente. Trovare le identità compromesse non è un compito facile. Azure Active Directory Usa adattivo di machine learning algoritmi euristica toodetect sospette azioni e che sono account utente tooyour correlati. Ogni azione sospetta rilevata viene archiviata in un record denominato *evento di rischio*.

Azure Active Directory rileva attualmente sei tipi di eventi di rischio:

- [Utenti con credenziali perse](#leaked-credentials) 
- [Accessi da indirizzi IP anonimi](#sign-ins-from-anonymous-ip-addresses) 
- [Comunicazione Impossibile tooatypical percorsi](#impossible-travel-to-atypical-locations) 
- [Accessi da posizioni non note](#sign-in-from-unfamiliar-locations)
- [Accessi da dispositivi infetti](#sign-ins-from-infected-devices) 
- [Accessi da indirizzi IP con attività sospette](#sign-ins-from-ip-addresses-with-suspicious-activity) 


![Evento di rischio](./media/active-directory-reporting-risk-events/91.png)

In questo argomento offre una panoramica dettagliata di quali eventi di rischio sono come è possibile usarli tooprotect le identità di Azure AD.


## <a name="risk-event-types"></a>Tipi di evento di rischio

proprietà tipo di evento rischio Hello è che un identificatore per l'azione sospette hello un record di eventi di rischio è stato creato per.  
Provocare investimenti nel processo di rilevamento hello Microsoft:

- Accuratezza di rilevamento toohello miglioramenti di eventi di rischio esistenti 
- Nuovi tipi di eventi di rischio che verranno aggiunto in futuro hello

### <a name="leaked-credentials"></a>Credenziali perse

Quando cybercriminali compromettono valida password degli utenti autorizzati, utenti malintenzionati hello spesso condivideranno tali credenziali. Ciò viene solitamente eseguita da pubblicandole pubblicamente su siti web o Incolla scuri hello o commerciali o le credenziali di hello sul mercato nero hello in vendita. Microsoft Hello comunicati credenziali servizio acquisisce il nome utente / password coppie mediante il monitoraggio di siti web pubblico e scuro e quando si lavora con:

- Ricercatori
- Forze dell'ordine
- Team di sicurezza di Microsoft
- Altre fonti attendibili 

Quando il servizio hello acquisisce il nome utente / coppie di password, vengono confrontate con credenziali valide corrente agli utenti AAD. Quando viene trovata una corrispondenza, significa che la password di un utente è stata compromessa e si crea un *evento di rischio di credenziali perse*.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Accessi da indirizzi IP anonimi

Questo tipo di evento di rischio identifica gli utenti che hanno eseguito l'accesso da un indirizzo IP riconosciuto come un indirizzo IP proxy anonimo. Questi proxy vengono utilizzati dagli utenti che desiderano toohide indirizzo IP del dispositivo in uso e possono essere utilizzate per fini dannosi.


### <a name="impossible-travel-tooatypical-locations"></a>Comunicazione Impossibile tooatypical percorsi

Questo tipo di evento di rischio identifica due accessi provenienti da posizioni geograficamente distanti, in cui almeno uno dei percorsi di hello potrebbe anche essere atipico per utente hello, dato il comportamento passato. Inoltre, il tempo di hello tra hello due accessi è più breve tempo hello avrebbe tenuto hello utente tootravel da hello primo percorso toohello secondo, che indica che un altro utente sta utilizzando hello stesso credenziali. 

Questo algoritmo di apprendimento automatico che ignora ovvio "*falsi positivi*" che hanno contribuito toohello trasferimento Impossibile condizione, ad esempio posizioni regolarmente utilizzati da altri utenti nell'organizzazione hello e VPN.  sistema Hello ha un periodo di apprendimento iniziale di 14 giorni durante i quali apprende comportamento del nuovo utente di accesso.

### <a name="sign-in-from-unfamiliar-locations"></a>Accessi da posizioni non note

Questo tipo di evento di rischio prende in considerazione oltre i percorsi di accesso (IP, latitudine / longitudine e ASN) toodetermine nuovo / familiarità percorsi. il sistema Hello archivia informazioni sui percorsi precedenti utilizzato da un utente e considera questi percorsi "familiari". eventi di rischio Hello viene attivato quando hello si verifica l'accesso da un percorso che non sia già nell'elenco di hello delle posizioni familiarità. sistema Hello ha un periodo di apprendimento iniziale di 30 giorni, durante il quale non segnala tutti i nuovi percorsi come posizioni non familiari. posizioni geograficamente chiudere posizione familiare tooa sistema Hello ignora inoltre accessi da dispositivi familiarità. 

### <a name="sign-ins-from-infected-devices"></a>Accessi da dispositivi infetti

Questo tipo di evento di rischio identifica accessi da dispositivi infettati da malware, che sono note tooactively di comunicare con un server bot. Ciò è determinato dal correlazione degli indirizzi IP del dispositivo dell'utente hello gli indirizzi IP in contatto con un server bot. 

### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Accessi da indirizzi IP con attività sospette
Questo tipo di evento di rischio identifica gli indirizzi IP da cui si è verificato un numero elevato di tentativi di accesso non riusciti, per più account utente e in un periodo di tempo breve. Ciò corrisponde a modelli di traffico degli indirizzi IP utilizzati da utenti malintenzionati e indica che gli account sono già o stanno toobe compromesso. Si tratta di un algoritmo di apprendimento automatico che ignora ovvio "*falsi positivi*", ad esempio gli indirizzi IP che vengono utilizzate regolarmente da altri utenti nell'organizzazione hello.  sistema Hello ha un periodo di apprendimento iniziale di 14 giorni in cui apprende hello Accedi comportamento di un nuovo utente e un nuovo tenant.


## <a name="detection-type"></a>Tipo di rilevamento

proprietà del tipo di rilevamento Hello è un indicatore (in tempo reale o Offline) per il periodo di tempo di hello rilevamento di un evento di rischio.  
Attualmente, la maggior parte degli eventi di rischio sono offline in un'operazione di post-elaborazione dopo che si è verificato un evento di rischio hello.

Hello nella tabella seguente sono elencate hello quantità di tempo per un tooshow tipo rilevamento in un report correlato:

| Tipo di rilevamento | Latenza creazione di report |
| --- | --- |
| Tempo reale | too10 5 minuti |
| Offline | too4 2 ore |


Per i tipi di evento rischio hello che Azure Active Directory rileva, i tipi di rilevamento hello sono:

| Tipo di evento di rischio | Tipo di rilevamento |
| :-- | --- | 
| [Utenti con credenziali perse](#leaked-credentials) | Offline |
| [Accessi da indirizzi IP anonimi](#sign-ins-from-anonymous-ip-addresses) | Tempo reale |
| [Comunicazione Impossibile tooatypical percorsi](#impossible-travel-to-atypical-locations) | Offline |
| [Accessi da posizioni non note](#sign-in-from-unfamiliar-locations) | Tempo reale |
| [Accessi da dispositivi infetti](#sign-ins-from-infected-devices) | Offline |
| [Accessi da indirizzi IP con attività sospette](#sign-ins-from-ip-addresses-with-suspicious-activity) | Offline|


## <a name="risk-level"></a>Livello di rischio

proprietà del livello di rischio Hello di un evento di rischio è un indicatore (alta, Media o bassa) per gravità hello e confidenza hello di un evento di rischio. Questa proprietà consente di azioni di hello tooprioritize che è necessario eseguire. 

gravità Hello dell'evento di rischio hello rappresenta forza hello del segnale di hello come un predittore di compromissione di identità.  
confidenza Hello è un indicatore per il possibilità hello di falsi positivi. 

Ad esempio, 

* **Alta**: evento di rischio con livello di gravità elevato e attendibilità elevata. Questi eventi sono indicatori sicuri che è stato compromesso l'identità dell'utente hello e tutti gli account utente interessati devono essere risolti immediatamente.

* **Media**: evento di rischio con livello di gravità elevato e minore attendibilità o viceversa. Questi eventi sono potenzialmente rischiosi e tutti gli account utente interessati devono essere corretti.

* **Bassa**: evento di rischio con livello di gravità basso e attendibilità bassa. Questo evento non richiedano un intervento immediato, ma in combinazione con altri eventi di rischio, può fornire un'indicazione sicura che hello identità è compromesso.

![Livello di rischio](./media/active-directory-reporting-risk-events/01.png)

### <a name="leaked-credentials"></a>Credenziali perse

Perdita di eventi di rischio sono classificati come credenziali di un **elevata**, in quanto forniscono una chiara indicazione che nome utente hello e la password sono disponibili tooan autore dell'attacco.

### <a name="sign-ins-from-anonymous-ip-addresses"></a>Accessi da indirizzi IP anonimi

livello di rischio Hello per questo tipo di evento di rischio è **Media** perché un indirizzo IP anonimo non è un'indicazione sicura di una violazione dell'account.  
È consigliabile contattare hello utente tooverify immediatamente se gli indirizzi IP anonimi erano in uso.


### <a name="impossible-travel-tooatypical-locations"></a>Comunicazione Impossibile tooatypical percorsi

Comunicazione Impossibile: è in genere un buon indicatore che un pirata informatico è stato in grado di toosuccessfully sign-in. Tuttavia, i falsi positivi possono verificarsi quando un utente verrà trasferiti utilizzando un nuovo dispositivo o una rete VPN che non viene in genere utilizzata da altri utenti nell'organizzazione hello. Un'altra origine di falsi positivi è applicazioni che in modo non corretto passato server gli indirizzi IP come indirizzi IP, che può dare l'impressione di hello client di accessi è ospitato in atto dal hello data center in cui l'applicazione di back-end (spesso si tratta di Data Center Microsoft, che può dare l'impressione di hello di accessi luogo da Microsoft proprietà indirizzi IP). In seguito a queste falsi positivi, è il livello di rischio hello per questo evento di rischio **Media**.

> [!TIP]
> È possibile ridurre quantità hello di false-positves segnalati per questo tipo di evento di rischio configurando [posizioni denominate](active-directory-named-locations.md). 

### <a name="sign-in-from-unfamiliar-locations"></a>Accessi da posizioni non note

Posizioni non familiari possono fornire un'indicazione sicura che un utente malintenzionato è in grado di toouse un'identità rubata. Possono verificarsi falsi positivi quando un utente è in viaggio, sta provando un nuovo dispositivo o usando una nuova VPN. In seguito a queste falsi positivi, il livello di rischio hello per questo tipo di evento è **Media**.

### <a name="sign-ins-from-infected-devices"></a>Accessi da dispositivi infetti

Questo evento di rischio identifica gli indirizzi IP, non i dispositivi degli utenti. Se più dispositivi si trovano dietro un singolo indirizzo IP e solo alcuni sono controllate da una rete bot, accessi da altri dispositivi il trigger questo evento inutilmente, che è il motivo di hello per classificare questo evento di rischio come **bassa**.  

Si consiglia di contattare l'utente hello e analizza i dispositivi dell'utente di hello tutti. È inoltre possibile che un dispositivo dell'utente personali è infetto o come indicato in precedenza, che un altro utente utilizzava un dispositivo infetto da hello stesso indirizzo IP come utente hello. Dispositivi infetti sono spesso infettati da malware che non sono ancora stati identificati dal software antivirus e può inoltre essere indicato come abitudini utente errati che potrebbero aver causato hello dispositivo toobecome infetti.

Per ulteriori informazioni su come tooaddress infezioni malware, vedere hello [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773&clcid=0x409).


### <a name="sign-ins-from-ip-addresses-with-suspicious-activity"></a>Accessi da indirizzi IP con attività sospette

Si consiglia di contattare hello utente tooverify se effettivamente firmato da un indirizzo IP che è stato contrassegnato come sospetto. livello di rischio Hello per questo tipo di evento è "**Media**" poiché alcuni dispositivi potrebbero trovarsi dietro hello stesso indirizzo IP, mentre solo alcune potrebbero essere responsabili di attività sospette hello. 


 
## <a name="next-steps"></a>Passaggi successivi

Gli eventi di rischio sono foundation hello per la protezione di identità di Azure AD. Azure AD attualmente è in grado di rilevare sei eventi di rischio: 


| Tipo di evento di rischio | Livello di rischio | Tipo di rilevamento |
| :-- | --- | --- |
| [Utenti con credenziali perse](#leaked-credentials) | Alto | Offline |
| [Accessi da indirizzi IP anonimi](#sign-ins-from-anonymous-ip-addresses) | Media | Tempo reale |
| [Comunicazione Impossibile tooatypical percorsi](#impossible-travel-to-atypical-locations) | Media | Offline |
| [Accessi da posizioni non note](#sign-in-from-unfamiliar-locations) | Media | Tempo reale |
| [Accessi da dispositivi infetti](#sign-ins-from-infected-devices) | Basso | Offline |
| [Accessi da indirizzi IP con attività sospette](#sign-ins-from-ip-addresses-with-suspicious-activity) | Media | Offline|

In cui è possibile determinare hello gli eventi di rischio che sono stati rilevati nell'ambiente in uso?
Esistono due posizioni in cui è possibile esaminare gli eventi di rischio segnalati:

 - **Creazione di report di AD Azure**: gli eventi di rischio fanno parte dei report sulla sicurezza di Azure AD. Per ulteriori informazioni, vedere hello [gli utenti dei report di sicurezza di rischio](active-directory-reporting-security-user-at-risk.md) hello e [rapporto sulla sicurezza accessi rischiosa](active-directory-reporting-security-risky-sign-ins.md).

 - **Azure AD Identity Protection:** gli eventi di rischio fanno parte anche delle capacità di segnalazione di [Azure AD Identity Protection](active-directory-identityprotection.md).
    

Mentre hello il rilevamento di eventi di rischio già rappresenta un aspetto importante della protezione delle identità, è inoltre hello opzione tooeither risolverli manualmente o anche implementare risposte automatiche tramite la configurazione di criteri di accesso condizionale. Per altre informazioni, consultare l'articolo su [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
 
