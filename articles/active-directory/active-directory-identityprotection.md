---
title: "la protezione dell'identità di Active Directory aaaAzure | Documenti Microsoft"
description: "Informazioni su come Azure AD Identity Protection consenta il possibilità hello toolimit di un tooexploit malintenzionato un'identità compromessa o il dispositivo e toosecure un'identità o un dispositivo che in precedenza era noto o sospetta toobe compromesso."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestione applicazioni, sicurezza, rischio, livello di rischio, vulnerabilità, criteri di sicurezza"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

Azure Active Directory Identity Protection è una funzionalità dell'edizione di Azure AD Premium P2 hello che consente di:

- Rilevare le potenziali vulnerabilità per le identità dell'organizzazione

- Configurare le risposte automatiche toodetected sospette azioni sono le identità dell'organizzazione tooyour correlati  

- Esaminare gli eventi imprevisti sospetti e richiedere l'azione appropriata tooresolve li   


## <a name="getting-started"></a>introduttiva

Microsoft protegge le identità basate sul cloud per oltre un decennio. Protezione dell'identità di Azure Active Directory, nel proprio ambiente, è possibile utilizzare hello stessi sistemi di protezione Microsoft utilizza le identità toosecure.

Posizionare Hello gran parte richiedere violazioni della sicurezza degli utenti malintenzionati ad ambiente tooan accesso dal furto di identità dell'utente. Negli anni hello, gli utenti malintenzionati sono diventate sempre più efficaci per sfruttare violazioni della sicurezza di terze parti e l'utilizzo di attacchi di phishing sofisticate. Non appena un utente malintenzionato ottenga l'accesso degli account utente con privilegi limitati tooeven, è relativamente facile relativa toogain accedere tooimportant alle risorse aziendali tramite il movimento laterale.

Di conseguenza, è necessario:

- Proteggere tutte le identità indipendentemente dal livello di privilegi

- Impedire in modo proattivo l'uso improprio delle identità compromesse

Trovare le identità compromesse non è un compito facile. Azure Active Directory Usa algoritmi di apprendimento automatico adattivo e anomalie toodetect euristica e gli eventi imprevisti sospetti indicano potenzialmente compromessi identità. Con questi dati, la protezione dell'identità genera report e gli avvisi che consentono di tooevaluate hello ha rilevato dei problemi e richiedere di attenuazione appropriati o azioni correttive.

Azure Active Directory Identity Protection è ben più di un semplice strumento di monitoraggio e reporting. tooprotect identità dell'organizzazione, è possibile configurare criteri basati sui rischi di rispondere automaticamente toodetected problemi quando viene raggiunto un livello di rischio specificato. Questi criteri, inoltre tooother condizionale accedere ai controlli forniti da Azure Active Directory ed EMS, può bloccare automaticamente oppure avviare azioni di correzione adattivo inclusi la reimpostazione della password e l'applicazione multi-factor authentication.


#### <a name="identity-protection-capabilities"></a>Funzionalità di Identity Protection

**Rilevamento di vulnerabilità e di account rischiosi:**  

* Fornire consigli personalizzati tooimprove generali di sicurezza, evidenziando le vulnerabilità
* Calcolo dei livelli di rischio di accesso.
* Calcolo dei livelli di rischio utente.


**Analisi degli eventi di rischio:**

* Invio di notifiche per gli eventi di rischio.
* Analisi degli eventi di rischio con informazioni rilevanti e contestuali.
* Fornisce i flussi di lavoro di base indagini tootrack
* Fornendo un accesso semplice tooremediation azioni, ad esempio la reimpostazione della password

**Criteri di accesso condizionale basati sul rischio:**

* Criteri toomitigate rischiosi accessi da accessi di blocco o la richiesta di richieste di autenticazione a più fattori.
* Criteri tooblock o gli account utente di rischiosa sicura
* Criteri toorequire utenti tooregister multi-factor Authentication



## <a name="identity-protection-roles"></a>Ruoli di Identity Protection

tooload saldo hello Gestione attività per l'implementazione di Identity Protection, è possibile assegnare più ruoli. Azure AD Identity Protection supporta 3 ruoli di directory:

| Ruolo                         | Operazione consentita                          | Operazione non consentita
| :--                          | ---                                |  ---   |
| Amministratore globale         | Accesso completo tooIdentity, protezione, caricare Identity Protection| |
| Amministratore della sicurezza       | Accesso completo tooIdentity protezione | Implementazione di Identity Protection, reimpostazione delle password per un utente |
| Ruolo con autorizzazioni di lettura per la sicurezza              | Accesso in sola lettura tooIdentity protezione | Implementazione di Identity Protection, correzione degli utenti, configurazione dei criteri, reimpostazione delle password |




Per altri dettagli, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)



## <a name="detection"></a>Rilevamento

### <a name="vulnerabilities"></a>Vulnerabilità

Azure Active Directory Identity Protection analizza la configurazione e rileva le vulnerabilità che possono avere effetto sulle identità dell'utente. Per altri dettagli, vedere [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).

### <a name="risk-events"></a>Eventi di rischio

Azure Active Directory Usa adattivo di machine learning algoritmi euristica toodetect sospette azioni e che sono le identità dell'utente tooyour correlati. sistema di Hello crea un record per ogni azione sospetti rilevato. Questi record sono denominati anche eventi di rischio.  
Per altre informazioni, vedere [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md).


## <a name="investigation"></a>Analisi
Il trasporto tramite la protezione dell'identità in genere inizia con dashboard Identity Protection hello.

![Correzione](./media/active-directory-identityprotection/1000.png "Correzione")

dashboard Hello consente di accedere a:

* Report, ad esempio **Utenti contrassegnati per il rischio**, **Eventi di rischio** e **Vulnerabilità**
* Le impostazioni come configurazione hello del **criteri di sicurezza**, **notifiche** e **registrazione con l'autenticazione a più fattori**

In genere è il punto di partenza per l'analisi, ovvero il processo di hello di revisione hello attività, i registri e altre informazioni rilevanti tooa correlato rischio toodecide evento se sono necessarie operazioni di correzione o riduzione, e come è stato identità hello compromesso e comprendere come hello compromesso identità è stata utilizzata.

È possibile collegare il toohello le attività di analisi [notifiche](active-directory-identityprotection-notifications.md) protezione di Azure Active Directory invia per posta elettronica.

Hello nelle sezioni seguenti offrono altre informazioni e i passaggi di hello analisi tooan correlati.  


## <a name="risky-sign-ins"></a>Accessi a rischio

Azure Active Directory rileva i [tipi di eventi di rischio](active-directory-reporting-risk-events.md#risk-event-types) in tempo reale e offline. Ogni evento di rischio rilevati per un accesso di un utente contribuisce tooa concetto logico Accedi rischiosa. Un rischiosa Accedi sono un indicatore per un tentativo di accesso che è possibile che non siano eseguito dal legittimo proprietario di hello di un account utente.


### <a name="sign-in-risk-level"></a>Livello di rischio di un accesso

Un livello di rischio di accesso è un'indicazione (alta, Media o bassa) di probabilità hello che un tentativo di accesso non è stato eseguito dal legittimo proprietario di hello di un account utente.

### <a name="mitigating-sign-in-risk-events"></a>Mitigazione degli eventi di rischio di accesso

Una riduzione dei rischi è la capacità di hello toolimit azione di un utente malintenzionato tooexploit un'identità compromessa o un dispositivo senza ripristino hello identità o un dispositivo tooa sicuri dello stato. Una mitigazione non viene risolto precedente Accedi rischio gli eventi associati identità hello o un dispositivo.

accessi toomitigate, rischiosa automaticamente, è possibile configurare l'accesso rischio sicurezza policicies. Grazie a questi criteri, prendere in considerazione il livello di rischio hello dell'utente di hello o hello Accedi tooblock accessi rischiosi o richiedere hello utente tooperform multi-factor authentication. Queste azioni possono impedire a un utente malintenzionato di sfruttare un danno toocause furto di identità e possono generare un'identità di hello toosecure ora.

### <a name="sign-in-risk-security-policy"></a>Criteri di sicurezza per il rischio di accesso
Un criterio di accesso rischi è un criterio di accesso condizionale che valuta hello rischio tooa specifico Accedi e applica le misure di attenuazione in base alle regole e condizioni predefinite.

![Criteri di rischio di accesso](./media/active-directory-identityprotection/1014.png "Criteri di rischio di accesso")

Azure AD Identity Protection consente di gestire attenuazione hello di accessi rischiosi poiché consente di:

* Hello utenti e gruppi hello criterio di impostazione si applica a:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1015.png "Criteri di rischio di accesso")
* Impostare hello Accedi rischio soglia (low, medium o high) che attiva i criteri di hello:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1016.png "Criteri di rischio di accesso")
* Set hello controlli toobe applicato quando i criteri di hello attiva:  

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")
* Stato di hello commutatore dei criteri:

    ![Registrazione MFA](./media/active-directory-identityprotection/403.png "Registrazione MFA")
* Rivedere e valutare l'impatto di hello di una modifica prima di attivarlo:

    ![Criteri di rischio di accesso](./media/active-directory-identityprotection/1018.png "Criteri di rischio di accesso")

#### <a name="what-you-need-tooknow"></a>È necessario tooknow
È possibile configurare l'autenticazione a più fattori toorequire un rischio di accesso sicurezza criteri:

![Criteri di rischio di accesso](./media/active-directory-identityprotection/1017.png "Criteri di rischio di accesso")

Tuttavia, per motivi di sicurezza, questa impostazione funziona soltanto per gli utenti che sono già stati registrati per l'autenticazione a più fattori. Se l'autenticazione a più fattori toorequire hello condizione è soddisfatta per gli utenti che non sono ancora registrato per l'autenticazione a più fattori, l'utente hello è bloccato.

Come procedura consigliata, se si desidera toorequire multi-factor authentication per accessi rischiosi, è necessario:

1. Abilitare hello [criteri di autenticazione a più fattori registrazione](#multi-factor-authentication-registration-policy) per hello utenti interessati.
2. Richiedi hello interessati toologin gli utenti in una sessione non rischioso di tooperform una registrazione di autenticazione a più fattori

L'esecuzione di questa procedura assicura che, in caso di accesso rischioso, venga richiesta l'autenticazione a più fattori.

#### <a name="best-practices"></a>Procedure consigliate
Scelta di un **elevata** soglia riduce il numero di hello di volte in cui un criterio viene attivato e riduce al minimo toousers impatto hello.  

Tuttavia, esclude **bassa** e **Media** accessi contrassegno i rischi dai criteri di hello, che non potrebbero bloccare un utente malintenzionato di sfruttare un'identità compromessa.

Quando impostazione hello criteri,

* Escludere gli utenti non hanno o non possono avere l'autenticazione a più fattori
* Escludere gli utenti con impostazioni locali in cui l'abilitazione di hello criterio non è pratico (ad esempio toohelpdesk alcun accesso)
* Escludere gli utenti che sono probabilmente toogenerate numerosi falsi positivi (sviluppatori, agli analisti della sicurezza)
* Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.
* Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza. La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.

impostazione predefinita consigliata per la maggior parte delle organizzazioni è tooconfigure una regola per Hello un **Media** soglia toostrike un equilibrio tra usabilità e sicurezza.

i criteri di accesso rischio Hello sono:

* Il traffico del browser tooall applicato e accesso tramite l'autenticazione moderna.
* Non applicato tooapplications utilizzando protocolli di sicurezza meno recenti, disabilitare endpoint WS-Trust hello IDP hello federato, ad esempio ADFS.

Hello **eventi di rischio** pagina hello Identity Protection console Elenca tutti gli eventi:

* Visualizzare a quali eventi sono stati applicati i criteri
* È possibile esaminare l'attività hello e determinare se l'azione hello era appropriato o non

Per una panoramica di hello correlate esperienza utente, vedere:

* [Ripristino di un accesso rischioso](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [Accesso rischioso bloccato](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md)  

**finestra di dialogo di configurazione correlato hello tooopen**:

- In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **Sign-in Criteri di rischio**.

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1014.png "Criteri di rischio utente")



## <a name="users-flagged-for-risk"></a>Utenti contrassegnati per il rischio

Tutte attive [gli eventi di rischio](active-directory-identity-protection-risk-events.md) che sono stati rilevati da Azure Active Directory per un utente contribuiscono tooa concetto logico chiamato rischio utente. Un utente contrassegnato per il rischio è indicativo di un account utente che potrebbe essere stato compromesso.

![Utenti contrassegnati per il rischio](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a>Livello di rischio utente

Livello di rischio un utente è un'indicazione (alta, Media o bassa) di probabilità hello che l'identità dell'utente hello sia stato compromesso. Viene calcolato in base sugli eventi di rischio utente hello associati con l'identità dell'utente.

Hello stato di un evento di rischio può essere **Active** o **chiuso**. Solo gli eventi di rischio **Active** contribuiscono calcolo livello di toohello utente dei rischi.

livello di rischio utente Hello viene calcolato mediante hello seguenti input:

* Eventi di rischio attivo conseguenze utente hello
* Livello di rischio di tali eventi.
* Eventuali azioni di correzione intraprese o meno.

![Rischi utente](./media/active-directory-identityprotection/1031.png "Rischi utente")

È possibile utilizzare hello utente dei rischi livelli toocreate criteri di accesso condizionale che bloccano l'accesso degli utenti rischiosi o forzarne toosecurely cambiare la password.

### <a name="closing-risk-events-manually"></a>Chiusura manuale degli eventi di rischio

Nella maggior parte dei casi, si avrà azioni correttive, ad esempio gli eventi di rischio Chiudi tooautomatically la reimpostazione della password sicura. Tuttavia, questo potrebbe non essere sempre possibile.  
Ciò accade, ad esempio, hello, quando:

* Un utente con eventi di rischio attivi è stato eliminato
* Un'analisi rivela che è stato eseguire un evento di rischio segnalati da utente legittimo hello

Poiché gli eventi di rischio che sono **Active** collaborazione calcolo del rischio di toohello utente, è possibile toomanually abbassare il livello di rischio chiudendo gli eventi di rischio manualmente.  
Corso hello dell'analisi, è possibile scegliere tootake uno stato di hello toochange queste azioni di un evento di rischio:

![Azioni](./media/active-directory-identityprotection/34.png "Azioni")

* **Risolvere** : se dopo aver esaminato un evento di rischio, è stata eseguita un'azione di correzione appropriata all'esterno di protezione dell'identità, e si ritiene che l'evento rischio hello deve essere considerato chiuso, evento hello contrassegna come risolto. Eventi risolti imposterà tooClosed lo stato dell'evento di rischio hello ed evento rischio hello non contribuirà toouser rischio.
* **Contrassegna come falso positivo** : in alcuni casi è possibile analizzare un evento di rischio e scoprire che è stato erroneamente contrassegnato come rischioso. È possibile ridurre il numero di hello di tali occorrenze contrassegnando l'evento di rischio hello come falsi positivi. Ciò consentirà di classificazione di hello tooimprove algoritmi di eventi simili in futuro hello di apprendimento automatico hello. stato Hello di eventi di falsi positivi è troppo**chiuso** e non contribuiscono non è più toouser rischio.
* **Ignora** : se non si è diventate qualsiasi azione di correzione, ma si desidera hello rischio evento toobe rimosso dall'elenco attivo hello, è possibile contrassegnare un evento di rischio Ignora e lo stato dell'evento hello verrà chiuso. Eventi ignorati non contribuiscono toouser rischio. Questa opzione deve essere usata solo in circostanze particolari.
* **Riattivare** -eventi che sono stati chiusi manualmente dei rischi (scegliendo **risolvere**, **falso positivo**, o **ignora**) possono essere riattivati, impostazione hello lo stato di evento nuovo troppo**Active**. Eventi di rischio riattivati contribuiscono calcolo livello di toohello utente dei rischi. Gli eventi di rischio chiusi tramite correzione, ad esempio la reimpostazione della password di protezione, non possono essere riattivati.

**finestra di dialogo di configurazione correlato hello tooopen**:

1. In hello **Azure AD Identity Protection** pannello, in **indagare**, fare clic su **gli eventi di rischio**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1002.png "Reimpostazione manuale della password")
2. In hello **gli eventi di rischio** elenco, fare clic su un rischio.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1003.png "Reimpostazione manuale della password")
3. Nel Pannello di rischio hello, fare doppio clic su un utente.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1004.png "Reimpostazione manuale della password")

### <a name="closing-all-risk-events-for-a-user-manually"></a>Chiusura manuale di tutti gli eventi di rischio per un utente
Invece di chiuderla manualmente gli eventi di rischio per un utente singolarmente, la protezione dell'identità Azure Active Directory offre più tooclose un metodo tutti gli eventi per un utente con un solo clic.

![Azioni](./media/active-directory-identityprotection/2222.png "Azioni")

Quando fa clic su **chiudere tutti gli eventi**, vengono chiusi tutti gli eventi e hello interessata utente non è più a rischio.

### <a name="remediating-user-risk-events"></a>Correzione di eventi di rischio utente

Un monitoraggio e aggiornamento è un'azione toosecure un'identità o un dispositivo che è stato in precedenza o sospettato toobe compromesso. Un'azione correttiva Ripristina hello identità o un dispositivo tooa sicuro lo stato e risolve i precedenti eventi di rischio associati all'identità hello o un dispositivo.

eventi di rischio tooremediate utente, è possibile:

* Eseguire manualmente gli eventi di rischio una password sicura reimpostazione tooremediate utente
* Configurare un toomitigate di criteri utente rischio per la sicurezza o correggere automaticamente gli eventi di rischio dell'utente
* Ricreare l'immagine dispositivo hello infettato  

#### <a name="manual-secure-password-reset"></a>Reimpostazione manuale della password di protezione
Per reimpostare la password sicura è un monitoraggio efficace per molti eventi di rischio e, quando eseguita, automaticamente chiude questi eventi di rischio e ricalcola a livello di rischio utente hello. È possibile utilizzare hello Identity Protection dashboard tooinitiate una reimpostazione della password per un utente rischioso.

finestra di dialogo correlate Hello fornisce due metodi diversi tooreset una password:

**Reimpostazione della password** : selezionare questa opzione **richiedono hello utente tooreset la propria password** tooallow hello utente tooself-ripristina se hello utente ha registrato per l'autenticazione a più fattori. Durante l'hello utente successivo accesso, utente hello sarà necessario toosolve richiesta di autenticazione a più fattori completata e la password di hello toochange forzato, quindi. Questa opzione non è disponibile se l'account utente di hello non è già registrato multi-factor authentication.

**Password temporanea** : selezionare questa opzione **generare una password temporanea** tooimmediately invalidare la password esistente hello e creare una nuova password temporanea per l'utente hello. Inviare hello nuova password temporanea tooan indirizzo e-mail alternativo per utente hello o un responsabile dell'utente toohello. Poiché la password di hello è temporanea, utente hello sarà password hello toochange richiesto al momento dell'accesso.

![Criteri](./media/active-directory-identityprotection/1005.png "Criteri")

**finestra di dialogo di configurazione correlato hello tooopen**:

1. In hello **Azure AD Identity Protection** pannello, fare clic su **utenti contrassegno i rischi**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1006.png "Reimpostazione manuale della password")
2. Hello l'elenco di utenti, selezionare un utente con gli eventi di almeno un rischio.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1007.png "Reimpostazione manuale della password")
3. Nel Pannello di hello utente, fare clic su **reimpostazione password**.

    ![Reimpostazione manuale della password](./media/active-directory-identityprotection/1008.png "Reimpostazione manuale della password")

### <a name="user-risk-security-policy"></a>Criteri di sicurezza per il rischio utente
Un criterio di sicurezza utente dei rischi è un criterio di accesso condizionale che valuta utente specifico di hello rischio tooa livello e applica le azioni di attenuazione e monitoraggio e aggiornamento in base alle regole e condizioni predefinite.

![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")

Azure AD Identity Protection consente di gestire attenuazione hello e monitoraggio e aggiornamento di utenti contrassegnati i rischi grazie alla possibilità di:

* Hello utenti e gruppi hello criterio di impostazione si applica a:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1010.png "Criteri di rischio utente")
* Impostare hello utente dei rischi soglia (low, medium o high) che attiva i criteri di hello:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1011.png "Criteri di rischio utente")
* Set hello controlli toobe applicato quando i criteri di hello attiva:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1012.png "Criteri di rischio utente")
* Stato di hello commutatore dei criteri:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/403.png "Registrazione MFA")
* Rivedere e valutare l'impatto di hello di una modifica prima di attivarlo:

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1013.png "Criteri di rischio utente")

Scelta di un **elevata** soglia riduce il numero di hello di volte in cui un criterio viene attivato e riduce al minimo toousers impatto hello.
Tuttavia, esclude **bassa** e **Media** utenti contrassegnati per rischi da criteri di hello, che potrebbero non sicuro identità o i dispositivi che sono state in precedenza o sospettati toobe compromesso.

Quando impostazione hello criteri,

* Escludere gli utenti che sono probabilmente toogenerate numerosi falsi positivi (sviluppatori, agli analisti della sicurezza)
* Escludere gli utenti con impostazioni locali in cui l'abilitazione di hello criterio non è pratico (ad esempio toohelpdesk alcun accesso)
* Usare una soglia **alta** durante il rollout iniziale dei criteri o se è necessario ridurre al minimo gli avvisi visualizzati dagli utenti finali.
* Usare una soglia **bassa** se l'organizzazione richiede una maggiore sicurezza. La scelta di una soglia **bassa** introduce richieste di accesso aggiuntive per l'utente, ma garantisce una maggiore sicurezza.

impostazione predefinita consigliata per la maggior parte delle organizzazioni è tooconfigure una regola per Hello un **Media** soglia toostrike un equilibrio tra usabilità e sicurezza.

Per una panoramica di hello correlate esperienza utente, vedere:

* [Flusso di ripristino di account compromessi](active-directory-identityprotection-flows.md#compromised-account-recovery).  
* [Flusso di account compromessi bloccati](active-directory-identityprotection-flows.md#compromised-account-blocked).  

**finestra di dialogo di configurazione correlato hello tooopen**:

- In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **rischio utente**.

    ![Criteri di rischio utente](./media/active-directory-identityprotection/1009.png "Criteri di rischio utente")

### <a name="mitigating-user-risk-events"></a>Mitigazione di eventi di rischio utente
Gli amministratori possono impostare un utente dei rischi sicurezza criteri tooblock utenti al momento dell'accesso in base al livello di rischio hello.

Il blocco dell'accesso:

* Impedisce la generazione di hello del nuovo utente di eventi di rischio per l'utente interessato hello
* Consente agli amministratori toomanually risolvere gli eventi di rischio hello influire sull'identità dell'utente hello e ripristinarlo stato protetto tooa



## <a name="multi-factor-authentication-registration-policy"></a>Criteri di registrazione per l'autenticazione a più fattori
Azure multi-factor authentication è un metodo di verifica dell'identità dell'utente che richiede l'uso di hello di molto più di un nome utente e una password. Fornisce un secondo livello di sicurezza toouser accessi e le transazioni.  
È consigliabile richiedere l'autenticazione a più fattori per l'accesso degli utenti perché:

* Offre un'autenticazione avanzata con una gamma di opzioni di verifica semplici
* Svolge un ruolo chiave nella preparazione tooprotect l'organizzazione e il ripristino da compromette account

![Criteri di rischio utente](./media/active-directory-identityprotection/1019.png "Criteri di rischio utente")

Per altre informazioni, vedere la pagina relativa ad [Informazioni su Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)

Azure AD Identity Protection consente di gestire hello roll-out della registrazione di autenticazione a più fattori tramite la configurazione di un criterio che consente di:

* Hello utenti e gruppi hello criterio di impostazione si applica a:

    ![Criteri MFA](./media/active-directory-identityprotection/1020.png "Criteri MFA")
* Set hello controlli toobe applicato quando i criteri di hello attiva:  

    ![Criteri MFA](./media/active-directory-identityprotection/1021.png "Criteri MFA")
* Stato di hello commutatore dei criteri:

    ![Criteri MFA](./media/active-directory-identityprotection/403.png "Criteri MFA")
* Visualizzare lo stato della registrazione corrente hello:

    ![Criteri MFA](./media/active-directory-identityprotection/1022.png "Criteri MFA")

Per una panoramica di hello correlate esperienza utente, vedere:

* [Flusso di registrazione per l'autenticazione a più fattori](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).  
* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md).  

**finestra di dialogo di configurazione correlato hello tooopen**:

- In hello **Azure AD Identity Protection** pannello in hello **configura** fare clic su **registrazione a multi-factor authentication**.

    ![Criteri MFA](./media/active-directory-identityprotection/1019.png "Criteri MFA")

## <a name="next-steps"></a>Passaggi successivi
* [Channel 9: Azure AD and Identity Show: Identity Protection Preview](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [Abilitazione di Azure Active Directory Identity Protection](active-directory-identityprotection-enable.md)

* [Vulnerabilità rilevate da Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md)

* [Eventi di rischio di Azure Active Directory](active-directory-identity-protection-risk-events.md)

* [Notifiche di Azure Active Directory Identity Protection](active-directory-identityprotection-notifications.md)

* [Studio di Azure Active Directory Identity Protection](active-directory-identityprotection-playbook.md)

* [Glossario di Azure Active Directory Identity Protection](active-directory-identityprotection-glossary.md)

* [Esperienze di accesso con Azure AD Identity Protection](active-directory-identityprotection-flows.md)

* [Azure Active Directory la protezione dell'identità, come gli utenti toounblock](active-directory-identityprotection-unblock-howto.md)

* [Introduzione ad Azure Active Directory Identity Protection e a Microsoft Graph](active-directory-identityprotection-graph-getting-started.md)
