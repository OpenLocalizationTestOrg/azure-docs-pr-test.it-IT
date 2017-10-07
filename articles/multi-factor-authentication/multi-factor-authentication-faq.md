---
title: domande frequenti di multi-Factor Authentication aaaAzure | Documenti Microsoft
description: "Domande frequenti e risposte relative tooAzure multi-Factor Authentication. Multi-Factor Authentication è un metodo di verifica dell'identità dell'utente che richiede l'uso di più fattori, oltre a un nome utente e una password. Fornisce un ulteriore livello di sicurezza toouser Accedi e transazioni."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8305cf4c41bf8e9802df192fecdb7e463eff9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-multi-factor-authentication"></a>Domande frequenti su Azure Multi-Factor Authentication
Questo risposte alle domande frequenti su Azure multi-Factor Authentication e tramite servizio multi-Factor Authentication hello. Si è suddivisa nei domande sul servizio hello in generale, fatturazione esperienze utente, modelli e risoluzione dei problemi.

## <a name="general"></a>Generale
**D: In che modo il server Azure Multi-Factor Authentication gestisce i dati utente?**

Con il Server di multi-Factor Authentication, solo su server locali hello sono archiviati i dati utente. Nessun dato utente persistente viene archiviato nel cloud hello. Quando l'utente hello esegue una verifica in due passaggi, Server multi-Factor Authentication invia dati toohello servizio cloud di Azure multi-Factor Authentication per l'autenticazione. La comunicazione tra Server multi-Factor Authentication e hello servizio cloud multi-Factor Authentication utilizza Secure Sockets Layer (SSL) o Transport Layer Security (TLS) sulla porta 443 in uscita.

Quando le richieste di autenticazione vengono inviate servizio cloud toohello, i dati raccolti per l'autenticazione e l'utilizzo di report. Di seguito sono riportati i campi di dati inclusi nei log di verifica in due passaggi:

* **ID univoco:** nome utente o ID del server Multi-Factor Authentication locale
* **Nome e cognome:** facoltativo
* **Indirizzo di posta elettronica:** facoltativo
* **Numero di telefono:** quando si esegue una chiamata vocale o l'autenticazione tramite SMS
* **Token del dispositivo:** quando si esegue l'autenticazione con l'app per dispositivi mobili
* **Modalità di autenticazione**
* **Risultato dell'autenticazione**
* **Nome del server Multi-Factor Authentication**
* **IP del server Multi-Factor Authentication**
* **IP client:** se disponibile

i campi facoltativi Hello possono essere configurati nel Server multi-Factor Authentication.

Hello risultato verifica (accesso o il rifiuto) e hello motivo se è stato negato, viene archiviato con i dati di autenticazione hello. Questi dati sono disponibili nei report di autenticazione e uso.

## <a name="billing"></a>Fatturazione
La maggior parte delle domande sulla fatturazione possono ottenere risposta riferendosi hello tooeither [dettagli prezzi di multi-Factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/) o hello documentazione sulle [come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**D: è la mia organizzazione addebito per l'invio di telefonate hello e messaggi di testo che vengono utilizzati per l'autenticazione?**

No, non vengono addebitati i singole chiamate telefoniche effettuate o messaggi di testo inviato toousers mediante Azure multi-Factor Authentication. Se si utilizza un provider di autenticazione a più fattori per autenticazione, verrà addebitato per ciascuna autenticazione ma non per il metodo hello utilizzato.

Gli utenti potrebbe essere addebitati hello telefonate o SMS che ricevono, servizio di numero di telefono personale tootheir secondo.

**D: modello di fatturazione per ogni utente hello mi importo per gli utenti abilitati tutti o solo hello quelle effettuate verifica in due passaggi?**

Fatturazione si basa sul numero di hello di utenti configurati toouse multi-Factor Authentication, indipendentemente dal fatto che ha eseguito la verifica di tale mese.

**D: Come funziona la fatturazione per Multi-Factor Authentication?**

Quando si crea un provider di MFA per utente o per autenticazione, la sottoscrizione di Azure dell'organizzazione viene fatturata mensilmente in base all'utilizzo. Questo modello di fatturazione è simile toohow Azure addebita per l'utilizzo delle macchine virtuali e siti Web.

Quando si acquista una sottoscrizione per Azure multi-Factor Authentication, l'organizzazione paga solo annuali licenza hello per ogni utente. La fatturazione avviene in questo modo per le licenze MFA e per i bundle Office 365, Azure AD Premium o Enterprise Mobility + Security. 

Altre informazioni sulle opzioni in [come tooget Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md).

**D: È disponibile una versione gratuita di Azure Multi-Factor Authentication?**

In alcuni casi, sì.

Multi-Factor Authentication per amministratori di Azure offre un sottoinsieme di funzionalità di autenticazione a più fattori di Azure senza costi aggiuntivi per l'accesso tooMicrosoft online services, inclusi i portali di amministratore di Azure e Office 365 hello. Questa offerta si applica solo agli amministratori di tooglobal nelle istanze di Azure Active Directory che non hanno una versione completa di Azure MFA hello tramite un provider in base al consumo autonomo, un bundle o una licenza di autenticazione a più fattori. Se gli amministratori di utilizzare la versione gratuita di hello e quindi si acquista una versione completa di Azure MFA, tutti gli amministratori globali sono toohello con privilegi elevato a pagamento di versione automaticamente.

Multi-Factor Authentication per gli utenti di Office 365 offre un sottoinsieme di funzionalità di autenticazione a più fattori di Azure senza costi aggiuntivi per l'accesso tooOffice 365 services, inclusi Exchange Online e SharePoint Online. Questa offerta si applica toousers che dispongono di una licenza di Office 365 assegnata, quando hello corrispondente istanza di Azure Active Directory non è una versione completa di Azure MFA hello tramite un provider in base al consumo autonomo, un bundle o una licenza di autenticazione a più fattori.

**D: L'organizzazione può passare dai modelli di fatturazione in base all'utilizzo per utente a quelli per autenticazione in qualsiasi momento?**

Se l'organizzazione acquista MFA come servizio autonomo con fatturazione in base al consumo, il modello di fatturazione viene scelto quando si crea un provider di MFA. È possibile modificare modello di fatturazione hello dopo la creazione di un provider di autenticazione a più fattori. Tuttavia, è possibile eliminare il provider di autenticazione a più fattori hello e quindi crearne uno con un altro modello di fatturazione.

Quando viene creato un provider di autenticazione a più fattori, può essere collegato tooan Azure Active Directory (noto anche come "tenant di Azure AD"). Se hello corrente i Provider di autenticazione a più fattori è tenant tooan collegato AD Azure, è possibile eliminare il provider di autenticazione a più fattori hello e creare un tenant toohello collegato stesso Azure Active Directory. In alternativa, se è stato acquistato sufficiente MFA, Azure AD Premium o Enterprise Mobility + Security (EMS) licenze toocover tutti gli utenti che sono abilitati per l'autenticazione a più fattori, è possibile eliminare il provider di autenticazione a più fattori hello completamente.

Se il provider di autenticazione a più fattori è *non* tenant tooan collegato AD Azure, oppure collegare tenant hello nuova autenticazione a più fattori provider tooa di Azure AD, le impostazioni utente e le opzioni di configurazione non vengono trasferite. Inoltre, Azure MFA server necessario riattivati con le credenziali di attivazione generate tramite toobe hello nuovo Provider di autenticazione a più fattori. Riattivazione di hello server MFA toolink li toohello nuovo Provider di autenticazione a più fattori non influisce sulla chiamata telefonica e autenticazione dei messaggi di testo, ma le notifiche verranno smettere di funzionare per tutti gli utenti fino a quando la riattivazione di app per dispositivi mobili hello app per dispositivi mobili.

Per altre informazioni sui provider di MFA, vedere [Introduzione all'uso di un provider di Azure Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md).

**D: L'organizzazione può passare dal modello di fatturazione in base al consumo e la sottoscrizione (modello basato su licenza) in qualsiasi momento?**

In alcuni casi, sì.

Se la directory include un provider di Azure Multi-Factor Authentication *per utente*, è possibile aggiungere licenze MFA. Non vengono conteggiati gli utenti con licenze di fatturazione in base al consumo per utente di hello. Gli utenti senza licenza possono essere ancora abilitati per l'autenticazione a più fattori tramite il provider di autenticazione a più fattori hello. Se si acquistano e assegnare licenze per tutti gli utenti configurati toouse multi-Factor Authentication, è possibile eliminare il provider di Azure multi-Factor Authentication hello. È sempre possibile creare un altro provider di autenticazione a più fattori per utente se sono presenti più utenti rispetto a licenze hello future.

Se la directory include un *per autenticazione* provider Azure multi-Factor Authentication, sempre vengono fatturati per ciascuna autenticazione, come provider di autenticazione a più fattori hello è collegato tooyour sottoscrizione. È possibile assegnare toousers licenze autenticazione a più fattori, ma comunque verrà addebitato per ogni richiesta di verifica in due passaggi, che derivino da un utente con una licenza di autenticazione a più fattori assegnata oppure No.

**D: la mia organizzazione hanno toouse e sincronizzare le identità toouse Azure multi-Factor Authentication?**

Se l'organizzazione usa un modello di fatturazione in base al consumo, è possibile usare Azure Active Directory ma non è obbligatorio. Se il provider di autenticazione a più fattori non è collegato tooan tenant di Azure AD, è possibile distribuire solo il Server Azure multi-Factor Authentication o Azure multi-Factor Authentication SDK hello in locale.

Azure Active Directory è necessario per il modello di licenza hello perché quando si acquistano e assegnare loro toousers nella directory hello licenze vengono aggiunti toohello tenant di Azure AD.

## <a name="manage-and-support-user-accounts"></a>Gestire e supportare gli account utente

**D: cosa dire my toodo utenti se non riceve una risposta sul telefono oppure non è il proprio telefono con essi?**

È auspicabile che tutti gli utenti abbiano configurato più metodi di verifica. Segnalando tootry eseguire nuovamente l'accesso, ma si seleziona un altro metodo di verifica nella pagina di accesso hello.

È possibile puntare il toohello utenti [Guida alla risoluzione dei problemi di utenti finali](./end-user/multi-factor-authentication-end-user-troubleshoot.md).


**D: cosa fare se uno degli utenti non è possibile ottenere tootheir account?**

È possibile reimpostare l'account dell'utente hello rendendoli toogo attraverso il processo di registrazione hello nuovamente. Altre informazioni, vedere [la gestione delle impostazioni utente e dispositivo con Azure multi-Factor Authentication nel cloud hello](multi-factor-authentication-manage-users-and-devices.md).

**D: Cosa fare se uno degli utenti perde un telefono che usa le password di app?**

tooprevent accessi non autorizzati, Elimina le password di app dell'utente di hello tutti. Dopo che l'utente di hello dispone di un dispositivo sostitutivo, sono in grado di ricreare le password hello. Altre informazioni, vedere [la gestione delle impostazioni utente e dispositivo con Azure multi-Factor Authentication nel cloud hello](multi-factor-authentication-manage-users-and-devices.md).

**D: cosa accade se un utente non può accedere App toonon basate su browser?**

Se l'organizzazione Usa ancora i client legacy e si [consentito hello utilizzo di password di app](multi-factor-authentication-whats-next.md#app-passwords), quindi gli utenti non possono accedere i client legacy toothese con nome utente e password. In alternativa, è necessario troppo[impostare le password di app](./end-user/multi-factor-authentication-end-user-app-passwords.md). Gli utenti devono cancellare (delete) le informazioni di accesso, riavviare l'applicazione hello e quindi accedere con il proprio nome utente e *password di app* anziché le password normali.

Se l'organizzazione non dispone di client legacy, non è consigliabile consentire agli utenti le password di app toocreate.

> [!NOTE]
> Autenticazione moderna per i client di Office 2013
>
> Le password di app sono necessarie solo per le app che non supportano l'autenticazione moderna. Client di Office 2013 supporta i protocolli di autenticazione moderna, ma è necessario toobe configurato. I client Office più recenti supportano automaticamente i protocolli dell'autenticazione moderna. Per ulteriori informazioni, vedere hello [annuncio anteprima pubblica l'autenticazione moderna di Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).

**D: negli utenti sostengono che talvolta non ricevono il messaggio di testo hello, o in risposta a messaggi di testo bidirezionale tootwo ma timeout della verifica hello.**

Non è garantito il recapito dei messaggi di testo e la ricezione di risposte SMS bidirezionale perché non controllabile fattori che possono influire sull'affidabilità di hello del servizio hello. Tali fattori includono hello destinazione paese, il gestore di telefonia mobile hello e la potenza del segnale hello.

Se gli utenti hanno spesso problemi in modo affidabile la ricezione di messaggi di testo, indicare loro toouse mobile app o telefonata metodo hello invece. app per dispositivi mobili Hello può ricevere notifiche sia su rete cellulare e connessioni Wi-Fi. Inoltre, i codici di verifica hello app per dispositivi mobili possono essere generati anche quando il dispositivo di hello non rileva alcun segnale affatto. è disponibile per app di Microsoft Authenticator Hello [Android](http://go.microsoft.com/fwlink/?Linkid=825072), [IOS](http://go.microsoft.com/fwlink/?Linkid=825073), e [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071).

Se è necessario usare gli SMS, è consigliabile usare SMS unidirezionali anziché bidirezionali, SMS unidirezionali è più affidabile e impedisce agli utenti di incorrere in addebiti per SMS globali da parte delle relying tooa SMS inviati da un altro paese.

**D: è possibile modificare il tempo di hello in cui che gli utenti dispongono di codice di verifica hello tooenter da un messaggio di testo prima del timeout del sistema hello?**

In alcuni casi sì. 

Per SMS unidirezionali con versione di Azure MFA Server 7.0 o versione successiva, è possibile configurare il timeout di hello impostazione impostando una chiave del Registro di sistema. Dopo che il servizio cloud MFA hello Invia messaggio di testo hello, codice di verifica hello (o il passcode monouso) viene restituito toohello Server MFA. Server MFA Hello archivia il codice hello in memoria per 300 secondi per impostazione predefinita. Se l'utente hello non immesse codice hello prima hello 300 secondi trascorsi, l'autenticazione è negata. Utilizzare questi timeout predefinito di passaggi toochange hello impostazione:

1. Passare tooHKLM\Software\Wow6432Node\Positive Networks\PhoneFactor.
2. Creare una chiave del Registro di sistema DWORD denominata **pfsvc_pendingSmsTimeoutSeconds** e impostare l'ora di hello in secondi che si desidera hello Azure MFA Server toostore monouso passcode.

>[!TIP] 
>Se si dispone di più server di autenticazione a più fattori, solo hello una richiesta di autenticazione originale hello elaborati SA codice di verifica hello toohello utente è stato inviato. Quando l'utente hello entra codice hello, hello toovalidate richiesta di autenticazione deve essere inviato toohello nello stesso server. Se la convalida del codice hello viene inviato tooa diversi server, viene negata l'autenticazione di hello. 

Per SMS bidirezionale con il Server di autenticazione a più fattori di Azure, è possibile configurare l'impostazione di timeout hello in hello portale di gestione di autenticazione a più fattori. Se gli utenti non rispondono toohello SMS entro il periodo di timeout definito di hello, viene negata l'autenticazione. 

Per SMS unidirezionali con Azure MFA nel cloud hello (inclusi hello estensione di Server dei criteri di rete di adapter o hello AD FS), è possibile configurare l'impostazione di timeout hello. Azure AD archivia il codice di verifica hello per 180 secondi. 

**D: È possibile usare i token hardware con il server Azure multi-Factor Authentication?**

Se si usa il server Azure Multi-Factor Authentication, è possibile importare token OATH TOPT di terze parti e quindi usarli per la verifica in due passaggi.

È possibile utilizzare token ActiveIdentity di token OATH TOTP se si inserisce la chiave privata di hello in un file CSV e Importa tooAzure Server multi-Factor Authentication. È possibile utilizzare i token OATH con Active Directory Federation Services (ADFS), l'autenticazione basata su form di Internet Information Server (IIS) e RADIUS Remote Authentication Dial-In utente Service () come sistema di hello client può accettare l'input dell'utente hello.

È possibile importare token OATH TOTP di terze parti con hello seguenti formati:  

- Portable Symmetric Key Container (PSKC)  
- CSV hello contiene un numero di serie, una chiave segreta in formato Base 32 e un intervallo di tempo  

**D: è possibile usare il Server Azure multi-Factor Authentication toosecure Terminal Services?**

Sì, ma se si usa Windows Server 2012 R2 o versione successiva è possibile proteggere i Servizi Terminal solo usando Gateway Desktop remoto.

Modifiche della sicurezza in Windows Server 2012 R2, modificare la modalità di connessione toohello pacchetto di sicurezza di autorità di sicurezza locale (LSA) in Windows Server 2012 e versioni precedenti del Server Azure multi-Factor Authentication. Per le versioni di Servizi terminal in Windows Server 2012 o versioni precedenti è possibile [proteggere un'applicazione con l'autenticazione di Windows](multi-factor-authentication-get-started-server-windows.md#to-secure-an-application-with-windows-authentication-use-the-following-procedure). Se si usa Windows Server 2012 R2, è necessario un Gateway Desktop remoto.

**D: È stato configurato l'ID chiamante in MFA Server ma gli utenti continuano a ricevere le chiamate di Multi-Factor Authentication da un chiamante anonimo.**

Quando vengono effettuate le chiamate di multi-Factor Authentication tramite rete telefonica pubblica hello, a volte vengono indirizzate tramite un vettore che non supporta l'ID del chiamante. Per questo motivo, ID chiamante non è garantito, anche se hello sistema multi-Factor Authentication invia sempre.

**D: perché gli utenti vengono richieste tooregister le relative informazioni di sicurezza?**
Esistono diversi motivi che gli utenti potrebbe essere richiesta tooregister le relative informazioni di sicurezza:

- utente Hello è stata abilitata per l'autenticazione a più fattori dall'amministratore in Azure AD, ma non dispone di informazioni di sicurezza per l'account ancora registrate.
- utente Hello è stata abilitata per la modalità self-service la reimpostazione della password in Azure AD. informazioni di sicurezza Hello li aiuteranno a reimpostare la password in futuro hello qualora si dovesse dimenticare.
- utente Hello accede a un'applicazione che ha un toorequire di criteri di accesso condizionale autenticazione a più fattori e non è registrato in precedenza per l'autenticazione a più fattori.
- utente che Hello registra un dispositivo con Azure AD (ad esempio aggiunta ad Azure AD) e l'organizzazione richiede l'autenticazione a più fattori per la registrazione del dispositivo, ma utente hello non è registrato in precedenza per l'autenticazione a più fattori.
- utente Hello genera Windows Hello for Business in Windows 10 (che richiede l'autenticazione a più fattori) e non è registrato in precedenza per l'autenticazione a più fattori.
- organizzazione di Hello è creato e abilitato un criterio di registrazione di autenticazione a più fattori che è stato applicato toohello utente.
- utente Hello precedentemente registrato per l'autenticazione a più fattori, ma sceglie un metodo di verifica che un amministratore ha disabilitato poiché. Hello utente deve pertanto disporre dell'accesso tramite la registrazione di autenticazione a più fattori nuovamente tooselect un nuovo metodo di verifica predefinita.


## <a name="errors"></a>Errors
**D: Cosa fare quando viene visualizzato l'errore "Authentication request is not for an activated account" (La richiesta di autenticazione non si riferisce a un account attivato) quando si usano le notifiche delle app per dispositivi mobili?**

Segnalando toofollow tooremove questa procedura l'account dal hello app per dispositivi mobili, quindi aggiungerlo di nuovo:

1. Andare troppo[profilo portale Azure](https://account.activedirectory.windowsazure.com/profile/) e accedere con l'account dell'organizzazione.
2. Selezionare **Verifica aggiuntiva di sicurezza**.
3. Rimuovere account esistente di hello hello app per dispositivi mobili.
4. Fare clic su **configura**, quindi seguire hello istruzioni tooreconfigure hello mobile app.

**D: azioni da intraprendere se viene visualizzato un messaggio di errore 0x800434D4L durante l'accesso dell'applicazione non basata su browser tooa?**

Errore 0x800434D4L Hello si verifica quando si tenta di toosign in applicazioni non basate su browser tooa, installato in un computer locale, compatibile con gli account che richiedono la verifica in due passaggi.

Una soluzione alternativa per questo errore è l'account utente separato di toohave per correlati admin e operazioni amministrative. In un secondo momento, è possibile collegare le cassette postali tra l'account amministrativo e l'account non amministrativo in modo che sia possibile Accedi tooOutlook utilizzando l'account non amministrativo. Per ulteriori informazioni su questa soluzione, informazioni su come troppo[assegnare un hello amministratore possibilità tooopen e visualizzazione hello contenuto postale una cassetta](http://help.outlook.com/141/gg709759.aspx?sl=1).

## <a name="next-steps"></a>Passaggi successivi
Se qui non rispondere alla domanda, lasciarla nei commenti hello nella parte inferiore di hello della pagina hello. In alternativa, di seguito vengono elencate alcune opzioni aggiuntive per ottenere assistenza:

* Hello ricerca [Microsoft Support Knowledge Base](https://www.microsoft.com/en-us/Search/result.aspx?form=mssupport&q=phonefactor&form=mssupport) per problemi tecnici di soluzioni toocommon.
* Cercare e individuare domande e risposte dalla community di hello tecniche o porre una domanda in hello [forum di Azure Active Directory](https://social.msdn.microsoft.com/Forums/azure/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).
* Se si è un cliente PhoneFactor legacy e si hanno domande o assistenza, reimpostare la password, utilizzare hello [di reimpostazione della password](mailto:phonefactorsupport@microsoft.com) collegamento tooopen un caso di supporto.
* Contattare un tecnico del supporto tramite [Azure Multi-Factor Authentication - PhoneFactor](https://support.microsoft.com/oas/default.aspx?prid=14947). Quando si contatta Microsoft, è utile includere il maggior numero possibile di informazioni relative al problema. È possibile fornire le informazioni includono pagina hello in cui si è visto errore hello, codice di errore specifico hello, ID di sessione specifico hello e hello ID dell'utente hello che ha visualizzato l'errore hello.
