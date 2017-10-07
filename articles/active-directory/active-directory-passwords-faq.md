---
title: 'Domande frequenti: reimpostazione della password self-service di Azure AD | Microsoft Docs'
description: Domande frequenti su sulla reimpostazione della password self-service di Azure AD
services: active-directory
keywords: gestione delle password in Active Directory, gestione delle password, reimpostazione della password self-service di Azure AD
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Domande frequenti sulla gestione delle password

Hello seguente è riportate alcune domande frequenti per tutti gli elementi correlati toopassword reimpostare.

Se si dispone di una domanda generale sulle AD Azure password self-service e ripristino, che non viene risposta qui, è possibile richiedere community hello assistenza sul hello [forum di Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). I membri della community di hello includere tecnici, responsabili di prodotto, MVP e fellow ai professionisti IT.

Questa sezione è suddivisa in hello le sezioni seguenti:

* [**Domande sulla registrazione per la reimpostazione della password**](#password-reset-registration)
* [**Domande sulla reimpostazione della password**](#password-reset)
* [**Domande sulla modifica della password**](#password-change)
* [**Domande relative ai report di gestione delle password**](#password-management-reports)
* [**Domande sul writeback delle password**](#password-writeback)

## <a name="password-reset-registration"></a>Registrazione per la reimpostazione della password
* **D: Gli utenti possono registrare i propri dati per la reimpostazione della password?**

  > **R:** Sì, purché la reimpostazione della password è abilitata e sono concessi in licenza, possono passare toohello portale di registrazione della reimpostazione della Password in http://aka.ms/ssprsetup tooregister le informazioni di autenticazione. Gli utenti possono anche registrarsi tramite Pannello di accesso toohello passare a http://myapps.microsoft.com, facendo clic sulla scheda profilo hello e facendo clic su hello registro per l'opzione di reimpostazione della Password.
  >
  >
* **D: è possibile definire i dati di reimpostazione della password per conto degli utenti?**

  > **R:** Sì, è possibile farlo con Azure AD Connect, PowerShell, hello [portale di Azure](https://portal.azure.com), o il portale di amministrazione di Office hello. Per ulteriori informazioni, vedere l'articolo hello [dati utilizzati da Azure AD Self-Service di reimpostazione della Password](active-directory-passwords-data.md).
  >
  >
* **D: È possibile sincronizzare i dati per le domande di sicurezza dall'ambiente locale?**

  > **R:** Attualmente non è possibile.
  >
  >
* **D: Gli utenti possono registrare i dati in modo che non siano visibili ad altri utenti?**

  > **R:** Sì, quando gli utenti registrano dati tramite hello registrazione del portale di reimpostazione Password viene salvata in campi privati di autenticazione visibili solo gli amministratori globali e hello utente.
    >
    > [!NOTE]
    > Se un **account amministratore Azure** registra il numero di telefono di autenticazione viene inoltre popolato nel campo del telefono cellulare hello e visibile.
    >
  >
  >
* **D: gli utenti hanno toobe registrati prima di poter usare la reimpostazione della password?**

  > **R:** No, se si definiscono informazioni di autenticazione sufficienti per loro conto, gli utenti non sono tooregister. Funzionamento della reimpostazione password, purché siano formattati correttamente i dati archiviati nei campi appropriati di hello nella directory hello.
  >
  >
* **D: è possibile sincronizzare o impostare i campi di hello telefono per l'autenticazione, posta elettronica di autenticazione o telefono alternativo per l'autenticazione per conto degli utenti?**

  > **R:** Attualmente non è possibile.
  >
  >
* **D: come portale di registrazione hello sapere quali tooshow opzioni gli utenti?**

  > **R:** portale di registrazione di reimpostazione della password di hello solo Mostra hello opzioni che è stata abilitata per gli utenti. Queste opzioni sono disponibili nella sezione criteri di reimpostazione Password utente della scheda Configura della directory hello. Ad esempio, ciò significa che se non si abilita domande di sicurezza, quindi gli utenti non sono in grado di tooregister per tale opzione.
  >
  >
* **D: Quando un utente viene considerato registrato?**

  > **R:** un utente è considerato registrato per SSPR quando essi sono registrati almeno hello **numero di metodi obbligatorio tooreset** che sono stati impostati nel hello [portale di Azure](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Reimpostazione delle password
* **D: come tempo è consigliabile attendere tooreceive un messaggio di posta elettronica, SMS o chiamata telefonica di reimpostazione della password?**

  > **R:** posta elettronica, i messaggi SMS e telefonate dovrebbero arrivare in un minuto, in hello normale entro 5-20 secondi.
    >Se non si riceve notifica hello in questo periodo di tempo:
        > * Controllare la cartella della posta indesiderata.
        > * Verificare il numero hello o posta elettronica contattato è hello previsto.
        > * Controllare i dati di autenticazione hello nella directory hello sono formattati correttamente.
                >     * Esempio: "+1 4255551234" o "user@contoso.com"
  >
  >
* **D: Quali lingue sono supportate per la reimpostazione della password?**

  > **R:** hello la reimpostazione della password dell'interfaccia utente, i messaggi SMS e vocale chiamate sono localizzate in hello stesse lingue supportate in Office 365.
  >
  >
* **Q: quali parti dell'esperienza di reimpostazione della password hello personalizzate quando si imposta aziendale di branding nella directory di configurazione della scheda?**

  > **R:** hello portale di reimpostazione della password viene mostrato il logo aziendale e consente tooconfigure hello, contattare l'amministratore collegamento toopoint tooa personalizzato tramite posta elettronica o URL. Qualsiasi messaggio di posta elettronica viene inviato per la reimpostazione della password include il logo dell'organizzazione, colori, il nome nel corpo di hello del messaggio di posta elettronica hello e personalizzate dal nome.
  >
  >
* **D: come è possibile indicare agli utenti dove toogo tooreset le proprie password?**

  > **R:** è possibile inviare direttamente i toohttps://passwordreset.microsoftonline.com utenti oppure è possibile indicare loro hello tooclick **non può accedere il collegamento di account** trovato in qualsiasi pagina accesso aziendale o dell'istituto di istruzione. È anche possibile pubblicare questi collegamenti in un utenti tooyour facilmente accessibili sul posto.
  >
  >
* **D: Questa pagina può essere usata da un dispositivo mobile?**

  > **R:** Sì, la pagina funziona anche sui dispositivi mobili.
  >
  >
* **D: È supportato lo sblocco di account Active Directory locali quando gli utenti reimpostano le password?**

  > **R:** Sì, quando un utente reimposta la password e il writeback delle password viene distribuito mediante Azure AD Connect, tale account utente viene sbloccato automaticamente quando si reimposta la password.
  >
  >
* **D: Come è possibile integrare la reimpostazione della password direttamente nell'esperienza di accesso desktop degli utenti?**

  > **R:** nel caso di un cliente di Azure AD Premium, è possibile installare Microsoft Identity Manager senza alcun costo aggiuntivo e distribuire hello locale password reset soluzione toomeet questo requisito.
  >
  >
* **D: È possibile impostare domande di sicurezza diverse per impostazioni locali diverse?**

  > **R:** Attualmente non è possibile.
  >
  >
* **D: quante domande è possibile configurare per l'opzione di autenticazione domande di sicurezza hello?**

  > **R:** è possibile configurare le domande di sicurezza personalizzato too20 in hello [portale di Azure](https://portal.azure.com).
  >
  >
* **D: Qual è la lunghezza delle domande di sicurezza?**

  > **R:** Le domande di sicurezza possono avere una lunghezza compresa tra 3 e 200 caratteri.
  >
  >
* **D: come long risposte toosecurity domande sia?**

  > **R:** le risposte possono contenere 3 too40 caratteri.
  >
  >
* **D: sono rifiutate le risposte duplicate toosecurity domande?**

  > **R:** Sì, vengono rifiutate le risposte duplicate toosecurity domande.
  >
  >
* **Q: maggio un registro utente hello stessa domanda di sicurezza più volte?**

  > **R:** No. Dopo che l'utente ha registrato una determinata domanda, non potrà registrarsi per quella domanda una seconda volta.
  >
  >
* **D: è possibile tooset un limite minimo di domande di sicurezza per la registrazione e la reimpostazione?**

  > **R:** Sì, è possibile impostare un limite per la registrazione e un altro per la reimpostazione. Possono essere richieste da 3 a 5 domande di sicurezza per la registrazione e da 3 a 5 domande di sicurezza per la reimpostazione.
  >
  >
* **D: se un utente ha registrato più di numero massimo di hello di domande necessarie tooreset, come le domande di sicurezza selezionate durante la reimpostazione?**

  > **R:** sicurezza N domande vengono selezionate casualmente rispetto totale hello di domande che un utente è registrato, dove N è hello **numero di domande necessarie tooreset**. Ad esempio, se un utente ha registrato 5 domande di sicurezza, ma solo 3 sono necessari tooreset, sono selezionati in modo casuale 3 di 5 hello e sono presentati alla reimpostazione. Se l'utente hello Ottiene le risposte hello domande toohello errato, si ripete il processo di selezione hello tooprevent domanda hammering.
  >
  >
* **D: Viene impedito agli utenti di provare a reimpostare la password più volte in un breve periodo di tempo?**

  > **R:** Sì, sono disponibili funzionalità di sicurezza incorporate in tooprotect di reimpostazione della password da utilizzi impropri. Gli utenti possono effettuare solo 5 tentativi di reimpostazione della password nell'arco di un'ora, prima di essere bloccati per 24 ore. Gli utenti possono provare solo toovalidate un numero di telefono 5 volte entro un'ora prima di essere bloccati per 24 ore. Gli utenti possono provare solo 5 volte un singolo metodo di autenticazione nell'arco di un'ora, prima di essere bloccati per 24 ore.
  >
  >
* **D: per quanto tempo è posta elettronica hello e passcode monouso SMS valido?**

  > **R:** hello durata della sessione per la reimpostazione della password è di 105 minuti. Da inizio hello di hello operazione di reimpostazione della password, utente hello ha 105 minuti tooreset la propria password. Hello posta elettronica e il passcode monouso SMS non sono validi dopo questo periodo di tempo.
  >
  >

## <a name="password-change"></a>Modifica della password
* **D: dove gli utenti diverranno toochange le proprie password?**

  > **R:** gli utenti possono modificare le password in qualsiasi punto visualizzano le immagine del profilo o l'icona (come in hello angolo superiore destro della loro [Office 365](https://portal.office.com) o [Pannello di accesso](https://myapps.microsoft.com) esperienze. Gli utenti possono modificare le password da hello [pagina del profilo di Pannello di accesso](https://account.activedirectory.windowsazure.com/r#/profile). Gli utenti possono inoltre essere richiesto toochange le proprie password automaticamente nella schermata di accesso hello Azure AD, se la password è scaduta. Infine, gli utenti possono spostarsi toohello [portale di modifica Password di Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) direttamente se desiderano toochange le proprie password.
  >
  >
* **D: è possibile agli utenti una notifica nel portale di Office hello quando scade la password in locale?**

  > **R:** attualmente è possibile se si utilizza ADFS seguendo le istruzioni di hello qui: [l'invio di attestazioni di criteri Password con ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Se si usa la sincronizzazione dell'hash della password, al momento non è possibile. Infatti, non è la sincronizzazione criteri password locale, pertanto non è possibile che ci toopost scadenza notifiche toocloud esperienze. In entrambi i casi, è anche possibile troppo[notificare agli utenti le cui password stanno tooexpire tramite PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Report di gestione delle password
* **D: come tempo occorre per dati tooshow backup nei report di gestione di password hello?**

  > **R:** dati devono essere visualizzati nei report di gestione di hello password entro 5-10 minuti. Alcune istanze potrebbe richiedere fino a tooan ora tooappear.
  >
  >
* **D: come è possibile filtrare i report di gestione di password hello?**

  > **R:** è possibile filtrare i report di gestione di password hello facendo hello piccola lente di ingrandimento toohello estremità destra delle etichette di colonna hello, parte superiore di hello del report hello. Se si desidera toodo di filtro più completa, è possibile scaricare tooexcel report hello e creare una tabella pivot.
  >
  >
* **D: qual è il numero massimo di hello degli eventi vengono archiviati nel report di gestione di password hello?**

  > **R:** backup too75, 000 password Reimposta o password registrazione eventi di reimpostazione vengono archiviati nel report di gestione password hello, spanning too30 giorni di backup.  Stiamo lavorando tooexpand questo numero tooinclude più eventi.
  >
  >
* **Q: fino passare hello report di gestione delle password?**

  > **R:** la gestione delle password hello report mostra le operazioni che si verificano all'interno di hello ultimi 30 giorni. Per il momento, se è necessario tooarchive questi dati, si scaricare periodicamente report di hello e salvarli in una posizione separata.
  >
  >
* **D: è presente un numero massimo di righe che possono essere visualizzati nei report di gestione di password hello?**

  > **R:** Sì, in uno dei report di gestione delle password di hello, può essere visualizzato un massimo di 75.000 righe se vengono visualizzati nella hello dell'interfaccia utente o in corso il download.
  >
  >
* **D: è un'API tooaccess hello password Reimposta o registrazione dati dei report?**

  > **R:** Sì, vedere hello seguenti toolearn documentazione come accedere a password hello reimpostare reporting flusso di dati.  [Informazioni su come tooaccess di reimpostazione della password eventi di reporting a livello di codice](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Writeback delle password
* **D: come funziona il writeback delle password in background hello?**

  > **R:** vedere [funzionamento di writeback delle password](active-directory-passwords-writeback.md) per una spiegazione di ciò che accade quando si abilita il writeback delle password e il flusso dei dati tramite il sistema hello nuovamente nell'ambiente locale.
  >
  >
* **D: come writeback delle password tempo toowork?  Esiste un ritardo di sincronizzazione come per la sincronizzazione di hash della password?**

  > **R:** Il writeback delle password è immediato. Si tratta di una pipeline sincrona che funziona fondamentalmente in modo diverso rispetto alla sincronizzazione di hash della password. Writeback delle password consente agli utenti tooget feedback in tempo reale sulla riuscita hello del loro password reimpostare o modificare l'operazione. tempo medio di Hello per un writeback della password riuscito è inferiore a 500 ms.
  >
  >
* **D: Se l'account locale è disabilitato, cosa succede all'accesso o all'account cloud?**

  > **R:** se l'ID locale è disabilitato, il cloud verranno disabilitata anche ID o l'accesso all'intervallo di sincronizzazione successivo di hello mediante AAD Connect byt predefinito tratta ogni 30 minuti.
  >
  >
* **D: se l'account locale è vincolato da un criterio di password di Active Directory locale, SSPR rispetta questo criterio quando si modifica la password di hello?**

  > **R:** Sì, SSPR si basa su e ha aderito all'accordo hello locale criteri password di Active Directory, inclusi i criteri password di dominio Active Directory tipico, nonché eventuali criteri password granulari definiti tooa dato utente di destinazione.
  >
  >
* **D: Per quali tipi di account funziona il writeback delle password?**

  > **R:** Funziona per gli utenti federati e con sincronizzazione di hash della password.
  >
  >
* **D: Il writeback delle password applica i criteri di password del dominio?**

  > **R:** Sì, applica validità, cronologia, complessità, filtri e qualsiasi altra restrizione eventualmente applicata alle password nel dominio locale.
  >
  >
* **D: Il writeback delle password è sicuro?  Come si può essere certi di non essere oggetto di un attacco?**

  > **R:** Sì, il writeback delle password è sicuro. tooread ulteriori informazioni sui livelli di hello quattro di sicurezza implementata dal servizio di writeback della password hello, estrarre hello [modello di sicurezza di writeback della Password](active-directory-passwords-writeback.md#password-writeback-security-model) sezione nel funzionamento di writeback delle password.
  >
  >

## <a name="next-steps"></a>Passaggi successivi

Hello seguenti collegamenti fornisce ulteriori informazioni sull'uso di Azure AD di reimpostazione della password

* [**Guida introduttiva**](active-directory-passwords-getting-started.md) - Iniziare a usare la gestione self-service delle password di Azure AD 
* [**Licenze**](active-directory-passwords-licensing.md) - configurare le licenze di Azure AD
* [**Dati** ](active-directory-passwords-data.md) : comprendere hello i dati necessari e come utilizzarlo per la gestione delle password
* [**Implementazione** ](active-directory-passwords-best-practices.md) -pianificare e distribuire agli utenti di tooyour SSPR utilizzando istruzioni hello disponibili qui
* [**Personalizzare** ](active-directory-passwords-customize.md) -personalizzare hello aspetto di hello SSPR esperienza per l'azienda.
* [**Creazione di report**](active-directory-passwords-reporting.md) - verificare se, quando e dove gli utenti accedono alla reimpostazione password self-service
* [**Criteri**](active-directory-passwords-policy.md): comprendere e impostare i criteri password di Azure AD
* [**Writeback delle password**](active-directory-passwords-writeback.md): funzionamento del writeback delle password con la directory locale
* [**Approfondimento tecnico** ](active-directory-passwords-how-it-works.md) -Vai dietro hello pannelli toounderstand come funziona
* [**Risoluzione dei problemi** ](active-directory-passwords-troubleshoot.md) -informazioni su come tooresolve comuni problemi che vedremo con SSPR
