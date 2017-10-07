---
title: 'Approfondimenti: reimpostazione della password self-service di Azure AD | Microsoft Docs'
description: Approfondimenti sulla reimpostazione della password self-service di Azure AD
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Approfondimenti sulla reimpostazione della password self-service in Azure AD

Come funziona la reimpostazione della password self-service? Che cosa significa che l'opzione nell'interfaccia hello? Continuare la lettura toofind ulteriori informazioni sulle password self-service di Azure AD reimpostare.

## <a name="how-does-hello-password-reset-portal-work"></a>In che modo password hello reimpostare lavoro portale

Quando un utente si sposta il portale di reimpostazione password toohello, un flusso di lavoro viene avviata toodetermine:

   * Come deve essere localizzata pagina hello?
   * È l'account utente di hello?
   * L'organizzazione appartenenza al utente hello?
   * In cui viene gestita la password dell'utente hello?
   * È hello utente con licenza toouse hello funzionalità?


Lettura passaggi hello sotto toolearn sulla logica di hello dietro hello pagina di reimpostazione della password.

1. Utente fa clic su hello non può accedere il collegamento di account o passa direttamente troppo[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Basato su hello delle impostazioni locali di hello browser viene eseguito il rendering esperienza nel linguaggio appropriato hello. Hello esperienza di reimpostazione della password è localizzato in hello stesse lingue, come Office 365 supporta.
3. L'utente immette un ID utente e un captcha.
4. Azure AD verifica se l'utente hello è in grado di toouse questa funzionalità eseguendo hello seguenti:
   * Verifica che l'utente hello è assegnata una licenza Azure AD e abilitare questa funzionalità.
     * Se l'utente hello non dispone di una licenza o abilitare questa funzionalità, l'utente di hello sia richiesto toocontact loro tooreset amministratore la password.
   * Verifica che l'utente hello disponga di dati della richiesta destra hello definiti nel proprio account in base ai criteri dell'amministratore.
     * Se i criteri prevedono un solo test, viene verificato che l'utente hello è hello definiti dati appropriati per almeno una delle sfide hello abilitate dai criteri amministratore hello.
       * Se non è configurato utente hello, hello utente è consigliato toocontact loro tooreset amministratore la password.
     * Se i criteri di hello prevedono due test, viene verificato che l'utente hello è hello definiti dati appropriati per almeno due delle sfide hello abilitate dai criteri amministratore hello.
       * Se l'utente hello non è configurato, quindi è hello utente è consigliato toocontact loro tooreset amministratore la password.
   * Controlla se la password dell'utente hello è gestita in locale (federati o con hash password sincronizzati).
     * Se viene distribuito il writeback e la password dell'utente hello viene gestita in locale, utente hello è consentito tooproceed tooauthenticate e reimposta la password.
     * Se non viene distribuito il writeback password dell'utente hello è gestita in locale, quindi hello utente è richiesto toocontact loro tooreset amministratore la password.
5. Se è stato stabilito che l'utente hello è in grado di toosuccessfully reimpostare la password, quindi hello viene avviata tramite il processo di reimpostazione hello.

## <a name="authentication-methods"></a>Metodi di autenticazione

Se la reimpostazione di Password Self-Service (SSPR) è abilitato, è necessario selezionare almeno una delle seguenti opzioni per i metodi di autenticazione hello. Si consiglia di scegliere almeno due metodi di autenticazione in modo che gli utenti dispongano di una maggiore flessibilità.

* Email
* Cellulare
* Telefono ufficio
* Domande di sicurezza

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>I campi che vengono utilizzati nella directory hello per dati di autenticazione

* Telefono ufficio corrisponde tooOffice telefono
    * Gli utenti sono tooset non è possibile in questo campo se stessi devono essere definito da un amministratore
* Cellulare corrisponde tooeither telefono per l'autenticazione (non visibile pubblicamente) o il telefono cellulare (visibile pubblicamente)
    * servizio Hello cerca innanzitutto telefono per l'autenticazione, quindi esegue il fallback tooMobile Phone se non è presente
* Indirizzo di posta elettronica alternativo corrisponde tooeither posta elettronica di autenticazione (non visibile pubblicamente) o posta elettronica alternativo
    * servizio Hello cerca innanzitutto posta elettronica di autenticazione, quindi ha esito negativo tooAlternate indietro posta elettronica

Per impostazione predefinita, solo attributi cloud hello telefono dell'ufficio e cellulare vengono sincronizzati directory cloud tooyour dalla directory locale per i dati di autenticazione.

Gli utenti possono solo la reimpostazione della password dispongono di dati nei metodi di autenticazione hello tale messaggio per l'amministratore ha abilitato e richiede.

Se gli utenti non si desidera che i relativi toobe numero di telefono cellulare visibile nella directory hello ma comunque come toouse per la reimpostazione della password, gli amministratori devono non viene popolato in directory hello e utente hello deve popolare i **telefono per l'autenticazione**  attributo mediante hello [portale di registrazione di reimpostazione della password](http://aka.ms/ssprsetup). Gli amministratori possono visualizzare queste informazioni nel profilo dell'utente hello ma non è pubblicata in un' posizione. Se un account amministratore di Azure si registra il numero di telefono di autenticazione, viene popolato nel campo del telefono cellulare hello ed è visibile.

### <a name="number-of-authentication-methods-required"></a>Numero di metodi di autenticazione necessari

Questa opzione determina numero minimo di hello hello disponibili dei metodi di autenticazione un utente deve passare attraverso tooreset o le password di sblocco e possono essere impostate tooeither 1 o 2.

Gli utenti possono scegliere toosupply ulteriori metodi di autenticazione se sono abilitati dall'amministratore di hello.

Se un utente non dispone di metodi hello minimo richiesto registrati, viene visualizzato una pagina di errore vengono indirizzati toorequest tooreset un amministratore la password.

### <a name="how-secure-are-my-security-questions"></a>Sicurezza delle domande di sicurezza

Se si usa domande di sicurezza, è consigliabile li in uso con un altro metodo che possano essere meno sicura rispetto ad altri metodi poiché alcuni utenti potrebbero conoscere le risposte hello tooanother domande di utenti.

> [!NOTE] 
> Domande di sicurezza vengono archiviate in locale e in modo sicuro in un oggetto utente nella directory hello e possono solo essere ottenere una risposta da parte degli utenti durante la registrazione. Non è possibile per un amministratore di tooread o modificare un utente domande e risposte.
>

### <a name="security-question-localization"></a>Localizzazione della domanda di sicurezza

Tutte le domande predefinite che seguono sono localizzate in set completo di hello delle lingue di Office 365 in base alle impostazioni locali del browser dell'utente hello.

* In quale città hai incontrato tuo marito o il tuo partner?
* In quale città si sono incontrati i tuoi genitori?
* In quale città vive tuo fratello/sorella più vicino/a?
* In quale città è nato tuo padre?
* In quale città hai avuto il tuo primo lavoro?
* In quale città è nata tua madre?
* In quale città hai trascorso il Capodanno del 2000?
* Che cos'è hello cognome dell'insegnante preferito in alta * dell'istituto di istruzione?
* Qual è il nome di hello del può citare un'università è applicato non hanno partecipato toobut?
* Qual è il nome di hello del hello luogo in cui il primo matrimonio?
* Qual è il secondo nome di tuo padre?
* Qual è il tuo piatto preferito?
* Qual è il nome e il cognome della nonna materna?
* Qual è il secondo nome di tua madre?
* Qual è l'anno e il mese di nascita di tuo/a fratello/sorella maggiore? Ad esempio, novembre 1985
* Qual è il secondo nome di tuo/a fratello/sorella maggiore?
* Qual è il nome e il cognome del nonno paterno?
* Qual è il secondo nome di tuo/a fratello/sorella minore?
* Quale scuola hai frequentato in prima media?
* Che cos'è hello innanzitutto nome e cognome della migliore amica dell'infanzia
* Cosa è stato hello innanzitutto nome e cognome del primo altri significative
* Qual era il cognome di hello dell'insegnante elementare preferito?
* Qual era hello marca e modello della prima auto o moto?
* Qual era il nome di hello della prima scuola frequentata hello?
* Qual era il nome di hello dell'ospedale hello in cui si è nati?
* Qual era il nome di hello di via hello della prima casa dell'infanzia?
* Qual era il nome di hello del supereroe preferito dell'infanzia?
* Qual era il nome di hello di pelouche preferito?
* Qual era il nome di hello del primo animale?
* Qual era il tuo soprannome da bambino?
* Qual è il tuo sport preferito alle scuole superiori?
* Qual è stato il tuo primo lavoro?
* Quali sono stati hello ultime quattro cifre del numero di telefono dell'infanzia?
* Professione, desiderata toobe quando sta crescendo?
* Chi è mai incontrata la persona più famosa hello?

### <a name="custom-security-questions"></a>Domande di sicurezza personalizzate

Le domande di sicurezza personalizzate non sono localizzate per le diverse impostazioni locali. Tutte le domande personalizzate vengono visualizzate in hello stessa lingua vengono immessi nell'interfaccia utente con privilegi amministrativi hello anche se impostazioni locali del browser dell'utente hello sono diversa. Se è necessario domande localizzate, utilizzare domande hello predefinito.

lunghezza massima di Hello di una domanda di sicurezza personalizzato è 200 caratteri.

### <a name="security-question-requirements"></a>Requisiti della domanda di sicurezza

* Il limite minimo di caratteri della risposta è 3 caratteri
* Il limite massimo di caratteri della risposta è 40 caratteri
* Gli utenti non possono rispondere hello stessa domanda di più di una volta
* Gli utenti potrebbero non fornire hello stesso rispondere toomore rispetto a una domanda
* Può essere qualsiasi set di caratteri utilizzato toodefine domande e risposte compresi i caratteri Unicode
* numero di Hello di domande definite deve essere maggiore di o uguale a toohello numero di domande necessarie tooregister

## <a name="registration"></a>Registrazione

### <a name="require-users-tooregister-when-signing-in"></a>Richiedi tooregister gli utenti durante l'accesso

Se si abilita questa opzione richiede un utente è abilitato per la password reimpostata registrazione per la reimpostazione password toocomplete hello se all'accesso tooapplications utilizzando Azure AD toosign in analoghe a quelle che seguono:

* Office 365
* Portale di Azure
* Pannello di accesso
* Applicazioni federate
* Applicazioni personalizzate che usano Azure AD

Disattivare questa funzionalità sarà comunque register toomanually agli utenti informazioni sul contatto, visita la pagina [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) o facendo clic su hello **registrare per la reimpostazione della password** collegamento hello scheda profilo nel Pannello di accesso hello.

> [!NOTE]
> Gli utenti possono chiudere un portale di registrazione reimpostazione password hello facendo clic su Annulla o chiudere la finestra hello ma richiesto ogni volta che all'accesso fino al completamento di registrazione.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Numero di giorni prima che gli utenti frequenti tooreconfirm le informazioni di autenticazione

Questa opzione determina hello periodo di tempo tra l'impostazione e riconfermare i dati del informazioni di autenticazione e disponibile solo se si abilita hello **richiedono tooregister gli utenti durante l'accesso** opzione.

I valori validi sono 0 e 730 giorni con 0, vale a dire mai chiedere agli utenti tooreconfirm le informazioni di autenticazione

## <a name="notifications"></a>Notifiche

### <a name="notify-users-on-password-resets"></a>Inviare notifiche agli utenti al momento della reimpostazione della password

Se questa opzione è impostata tooyes, gli utenti hello sta reimpostando la propria password riceve un messaggio che informa che la password è stata modificata tramite hello SSPR portale tootheir primario e indirizzi di posta elettronica alternativo nel file di Azure AD. La notifica per questo evento di reimpostazione non viene inviata ad altre persone.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Inviare una notifica a tutti gli amministratori quando altri amministratori reimpostano le proprie password

Se questa opzione è impostata, tooyes quindi **tutti gli amministratori** riceveranno un indirizzo di posta elettronica primario tootheir di posta elettronica nel file in Azure AD che informa che un altro amministratore ha modificato la password utilizzando SSPR.

Esempio: nell'ambiente sono presenti quattro amministratori. L'amministratore "A" reimposta la password tramite il servizio di reimpostazione della password self-service. Gli amministratori B, C e D ricevono un messaggio di posta elettronica che li avvisa di quanto sta accadendo.

## <a name="on-premises-integration"></a>Integrazione locale

Se Azure AD Connect è stato installato, configurato e attivato, sono presenti opzioni aggiuntive per le integrazioni locali.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Write-back directory locale tooyour di password

Controlla se il writeback delle password è abilitata per questa directory e, se il writeback è attivata, indica lo stato di hello del servizio di writeback locale hello. Ciò è utile se si desidera hello tootemporarily disabilita il writeback della password senza nuovamente la configurazione di Azure AD Connect.

* Se passa hello è tooyes set, il writeback verrà abilitato e federato e utenti sincronizzati hash password saranno in grado di tooreset le proprie password.
* Se passa hello è toono set, il writeback verrà disabilitato e federato e gli utenti sincronizzati hash di password non saranno in grado di tooreset le proprie password.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Consentire agli utenti toounlock account senza reimpostare la password

Indica se gli utenti che visitano il portale di reimpostazione password hello devono essere determinato hello opzione toounlock loro Active Directory locale degli account senza reimpostare la password. Per impostazione predefinita, Azure AD verrà sempre sbloccare gli account quando si esegue una reimpostazione della password, questa impostazione consente tooseparate queste due operazioni. 

* Se impostato troppo "yes", quindi gli utenti verranno tooreset opzione hello specificato la password e sbloccare l'account hello o toounlock senza reimpostare la password di hello.
* Se impostato troppo "no", solo gli utenti sono in grado di tooperform un account e la reimpostazione della password combinata operazione di sblocco.

## <a name="network-requirements"></a>Requisiti di rete

### <a name="firewall-rules"></a>Regole del firewall

[Elenco di indirizzi IP e di URL di Microsoft Office](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Per Azure AD Connect versione 1.1.443.0 e versioni successive, è necessario seguenti di toohello accesso HTTPS in uscita
* passwordreset.microsoftonline.com
* servicebus.windows.net

Per un accesso più granulare, è possibile trovare l'elenco di hello aggiornata di Microsoft Azure Datacenter intervalli IP che viene aggiornato ogni mercoledì e inseriti in seguito hello effetto lunedì [qui](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Timeout di connessione inattiva

strumento di Hello Azure AD Connect invia ping periodico pacchetti keep alive tooServiceBus endpoint tooensure che le connessioni hello restino attive. Strumento hello deve rilevare che un numero eccessivo di connessioni sono viene terminate, verrà automaticamente aumentata frequenza hello dell'endpoint toohello ping. Hello più basso 'ping intervalli' Elimina toois 1 ping ogni 60 secondi, tuttavia, è consigliabile che proxy/firewall consentano toopersist le connessioni inattive per almeno 2-3 minuti. *Per le versioni precedenti, è consigliata una persistenza di 4 minuti o più.

## <a name="active-directory-permissions"></a>Autorizzazioni di Active Directory

Hello account specificato nell'utilità di hello Azure AD Connect è necessario reimpostare la Password, modificare la Password, autorizzazioni di scrittura per lockoutTime e autorizzazioni di scrittura per pwdLastSet, esteso di diritti per l'oggetto radice hello di **ogni dominio** in tale foresta **o** utente hello unità organizzative desiderato nell'ambito per SSPR toobe.

Se non si è certi hello quali account precedente fa riferimento, aprire Configurazione di Azure Active Directory Connect hello dell'interfaccia utente e scegliere l'opzione di configurazione di hello visualizzazione corrente. account Hello che è necessario tooadd autorizzazione toois sotto "Sincronizzazione delle directory"

L'impostazione di queste autorizzazioni consente l'account del servizio MA hello per le password toomanage ogni foresta per conto degli account utente all'interno di tale foresta. **Se non si esegue tooassign queste autorizzazioni, quindi, anche se il writeback sembra toobe configurato correttamente, gli utenti riscontrano errori durante il tentativo di toomanage le password locali dal cloud hello.**

> [!NOTE]
> Potrebbero richiedere più di tooan ora per questi oggetti tooall tooreplicate di autorizzazioni nella directory.
>

tooset le autorizzazioni appropriate hello toooccur di writeback delle password

1. Aprire Active Directory Users and Computers con un account che dispone delle autorizzazioni di amministrazione di dominio appropriato hello
2. Dal menu Visualizza di hello, assicurarsi che sia acceso funzionalità avanzate
3. Nel riquadro sinistro hello oggetto hello che rappresenta la radice hello del dominio hello destro, quindi scegliere Proprietà
    * Fare clic sulla scheda sicurezza hello
    * Fare clic su Opzioni avanzate.
4. Dalla scheda autorizzazioni hello, fare clic su Aggiungi
5. Selezionare account hello che devono essere applicate autorizzazioni troppo (dal programma di installazione di Azure AD Connect)
6. In hello si applica toodrop casella a discesa selezionare gli oggetti utente discendenti
7. In autorizzazioni selezionare caselle di hello per seguenti hello
    * Password senza scadenza
    * Reimpostare la password
    * Modifica della password
    * Scrittura di lockoutTime
    * Scrittura di pwdLastSet
8. Fare clic su Aplicar o aceptar tramite tooapply e chiudere eventuali finestre di dialogo Apri.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Come funziona la reimpostazione della password per gli utenti B2B?
La modifica e la reimpostazione della password sono completamente supportate con tutte le configurazioni B2B.  Continuare a leggere per hello tre esplicita B2B casi supportato per la reimpostazione della password.

1. **Gli utenti da un'organizzazione partner con un tenant di Azure AD esistente** : se l'organizzazione di hello sono la collaborazione con dispone di un tenant di Azure AD esistente, è **rispettare qualsiasi criteri di reimpostazione della password sono attivati nel tenant**. Per password ripristinati toowork, hello partner dell'organizzazione deve semplicemente toomake che sia abilitato SSPR AD Azure, ovvero senza costi aggiuntivi per i clienti di Office 365, e può essere abilitata seguendo i passaggi da hello in nostro [Introduzione a Password Management ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) Guida.
2. **Gli utenti che ha sottoscritto con [iscrizione Self-Service](active-directory-self-service-signup.md)**  : se l'organizzazione hello sono la collaborazione con utilizzato hello [iscrizione Self-Service](active-directory-self-service-signup.md) tooget funzionalità in un tenant, è consentire di reimpostazione posta elettronica Hello che siano registrati.
3. **Gli utenti B2B** -B2B nuovi utenti creati utilizzando la nuova hello [funzionalità Azure AD B2B](active-directory-b2b-what-is-azure-ad-b2b.md) saranno anche in grado di tooreset le password con messaggio di posta elettronica hello siano registrati durante il processo di invito hello.

tootest, andare toohttp://passwordreset.microsoftonline.com con uno di questi utenti partner. Se l'utente ha un indirizzo di posta elettronica alternativo o un indirizzo di posta elettronica per l'autenticazione, la reimpostazione della password funziona come previsto.

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Domande frequenti**](active-directory-passwords-faq.md): come? Perché? Cosa? Dove? Chi? Quando? -Risposte tooquestions si desiderava sempre tooask
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR

