---
title: durata dei token aaaConfigurable in Azure Active Directory | Documenti Microsoft
description: Informazioni su come tooset durate per i token rilasciati da Azure AD.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: 0d4c8545981c5463cc7c95f669167bbc38230123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a>Durata dei token configurabili in Azure Active Directory (anteprima pubblica)
È possibile specificare una durata hello di un token emesso da Azure Active Directory (Azure AD). La durata dei token può essere impostata per tutte le app di un'organizzazione, per un'applicazione multi-tenant (più organizzazioni) o per un'entità servizio specifica in un'organizzazione.

> [!NOTE]
> Questa funzionalità è attualmente disponibile in anteprima pubblica. Essere preparati toorevert o rimuovere tutte le modifiche. funzionalità di Hello è disponibile in alcuna sottoscrizione di Azure Active Directory durante l'anteprima pubblica. Tuttavia, quando la funzionalità hello diventa disponibile in genere, alcuni aspetti della funzionalità hello potrebbero richiedere un [Azure Active Directory Premium](active-directory-get-started-premium.md) sottoscrizione.
>
>

In Azure AD, un oggetto criteri rappresenta un set di regole applicate a singole applicazioni o a tutte le applicazioni di un'organizzazione. Ciascun tipo di criterio ha una struttura univoca, con un set di proprietà che vengono applicati tooobjects toowhich che vengono assegnati.

È possibile designare un criterio come criterio di hello predefinito per l'organizzazione. criteri di Hello sono applicato tooany applicazione hello organizzazione, fino a quando non viene sottoposto a override da un criterio con una priorità più alta. È inoltre possibile assegnare un criterio toospecific applicazioni. ordine di priorità di Hello varia in base al tipo di criteri.


## <a name="token-types"></a>Tipi di token

È possibile impostare i criteri di durata dei token per i token di aggiornamento, i token di accesso, i token di sessione e i token ID.

### <a name="access-tokens"></a>Token di accesso
Usare l'accesso client token tooaccess una risorsa protetta. I token di accesso possono essere usati solo per una combinazione specifica di utente, client e risorsa. Non è possibile revocare i token di accesso, che rimangono validi fino alla scadenza. Un attore malintenzionato può usare un eventuale token di accesso ottenuto per la sua intera durata. Regolare la durata hello un accesso token è un compromesso tra le prestazioni del sistema e crescente hello periodo di tempo che hello client mantiene l'accesso dopo aver disabilitato hello account utente. Prestazioni del sistema migliorate avviene tramite la riduzione hello numero di volte in cui che un client deve tooacquire un token di accesso aggiornata.

### <a name="refresh-tokens"></a>Token di aggiornamento
Quando un client acquisisce un tooaccess token di accesso una risorsa protetta, il client di hello riceve un token di aggiornamento sia un token di accesso. token di aggiornamento Hello è tooobtain utilizzato nuovo aggiornamento di accesso token coppie quando scade il token di accesso corrente hello. Un token di aggiornamento è combinazione tooa associato dell'utente e client. Un token di aggiornamento può essere revocato, e la validità del token hello è selezionata, ogni volta che viene utilizzato il token hello.

È importante toomake una distinzione tra i client riservati e pubblico. Per altre informazioni sui diversi tipi di client, vedere la specifica [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a>Durata dei token con token di aggiornamento per client riservati
I client riservati sono applicazioni che possono archiviare in modo sicuro una password client, ovvero un segreto, Può dimostrare che le richieste provengano da un'applicazione client hello e non da un attore dannoso. Ad esempio, un'app web è un client riservato perché consente di archiviare un segreto client nel server web hello. e non viene esposto. Perché questi flussi sono più sicuri, hello durata predefinita dei token di aggiornamento viene emesso toothese flussi `until-revoked`, non può essere modificato tramite criteri e non sarà possibile revocare per la reimpostazione della password su base volontaria.

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a>Durata dei token con token di aggiornamento per client pubblici

I client pubblici non possono archiviare in modo sicuro una password client, ovvero un segreto. Ad esempio, un'app iOS/Android non è possibile offuscare un segreto dal proprietario della risorsa hello, pertanto viene considerato un client pubblico. È possibile impostare criteri risorse tooprevent i token di aggiornamento da pubblico client precedenti a un determinato periodo di ottenere una nuova coppia di token di aggiornamento di accesso. (toodo, hello utilizzare proprietà Token Max inattiva ora di aggiornamento.) È inoltre possibile utilizzare criteri tooset un periodo di oltre i token di aggiornamento hello non verranno più accettate. (toodo, hello utilizzare proprietà Aggiorna Token Max Age.) È possibile regolare la durata hello di un toocontrol token di aggiornamento quando e con quale frequenza hello utente è obbligatorio tooreenter credenziali, anziché viene automaticamente riautenticare, quando si utilizza un'applicazione client pubblico.

### <a name="id-tokens"></a>Token ID
Token ID vengono passati toowebsites e native client. e contengono informazioni relative al profilo di un utente. Un ID token è tooa associato combinazione specifica di client e utente. ed è considerato valido fino alla relativa scadenza. In genere, un'applicazione web corrisponde a un utente la durata della sessione hello applicazione toohello sua durata token ID hello emesso per utente hello. È possibile regolare la durata hello di un ID token toocontrol la frequenza con cui un'applicazione web hello scadenza della sessione dell'applicazione hello e la frequenza con cui richiede toobe utente hello riautenticare con Azure AD (invisibile all'utente o in modo interattivo).

### <a name="single-sign-on-session-tokens"></a>Token di sessione Single Sign-On
Quando un utente esegue l'autenticazione con Azure AD e seleziona hello **Mantieni l'accesso** casella di controllo, viene stabilita una singola sessione sign-on (SSO) con i browser dell'utente hello e Azure AD. token SSO Hello, sotto forma di hello di un cookie, rappresenta la sessione. Si noti che il token di sessione hello SSO non è associato tooa specifica risorsa/applicazione client. I token di sessione SSO possono essere revocati e la relativa validità viene verificata ogni volta che vengono usati.

Azure AD usa due tipi di token di sessione SSO, ovvero permanenti e non permanenti. Token di sessione persistente vengono archiviati come i cookie permanenti dal browser hello. I token di sessione non permanenti vengono archiviati come cookie di sessione (I cookie di sessione vengono eliminati quando hello browser viene chiuso).

I token di sessione non permanenti hanno una durata di 24 ore, mentre i token permanenti hanno una durata di 180 giorni. Ogni volta che viene utilizzato un token di sessione SSO rientra nel periodo di validità, il periodo di validità hello viene estesa altro 24 ore o 180 giorni, in base al tipo di token hello. Se un token di sessione SSO non viene usato entro il relativo periodo di validità, è considerato scaduto e non viene più accettato.

È possibile utilizzare un tempo di hello tooset criteri dopo che è stato rilasciato il token di sessione prima di hello oltre cui hello token di sessione non accettato. (toodo, hello utilizzare proprietà Max Age Token di sessione.) È possibile regolare la durata hello di un toocontrol token di sessione quando e la frequenza con cui un utente è obbligatorio tooreenter credenziali, anziché invisibile all'utente viene autenticato, quando si utilizza un'applicazione web.

### <a name="token-lifetime-policy-properties"></a>Proprietà dei criteri per la durata dei token
I criteri per la durata dei token rappresentano un tipo di oggetto criteri contenente le regole di durata dei token. Utilizzare le proprietà di hello di hello criteri toocontrol specificavano durata dei token. Se non è impostato alcun criterio, il sistema di hello Applica valore di durata predefinito hello.

### <a name="configurable-token-lifetime-properties"></a>Proprietà configurabili per la durata dei token
| Proprietà | Stringa proprietà criteri | Impatto | Default | Minima | Massima |
| --- | --- | --- | --- | --- | --- |
| Durata dei token di accesso |AccessTokenLifetime |Token di accesso, token ID, token SAML2 |1 ora |10 minuti |1 giorno |
| Tempo inattività massimo token di aggiornamento |MaxInactiveTime |Token di aggiornamento |14 giorni |10 minuti |90 giorni |
| Validità massima token di aggiornamento a fattore singolo |MaxAgeSingleFactor |Token di aggiornamento (per tutti gli utenti) |Fino a revoca |10 minuti |Fino alla revoca<sup>1</sup> |
| Validità massima token di aggiornamento a più fattori |MaxAgeMultiFactor |Token di aggiornamento (per tutti gli utenti) |Fino a revoca |10 minuti |Fino alla revoca<sup>1</sup> |
| Validità massima token di sessione a fattore singolo |MaxAgeSessionSingleFactor<sup>2</sup> |Token di sessione (permanenti e non permanenti) |Fino a revoca |10 minuti |Fino alla revoca<sup>1</sup> |
| Validità massima token di sessione a più fattori |MaxAgeSessionMultiFactor<sup>3</sup> |Token di sessione (permanenti e non permanenti) |Fino a revoca |10 minuti |Fino alla revoca<sup>1</sup> |

* <sup>1</sup>365 giorni è hello esplicita lunghezza massima che è possibile impostare per questi attributi.
* <sup>2</sup>se **MaxAgeSessionSingleFactor** non è impostata, questo valore ha hello **MaxAgeSingleFactor** valore. Se è impostato nessuno dei parametri, proprietà di hello accetta il valore di predefinito hello (fino a quando revocati).
* <sup>3</sup>se **MaxAgeSessionMultiFactor** non è impostata, questo valore ha hello **MaxAgeMultiFactor** valore. Se è impostato nessuno dei parametri, proprietà di hello accetta il valore di predefinito hello (fino a quando revocati).

### <a name="exceptions"></a>Eccezioni
| Proprietà | Impatto | Default |
| --- | --- | --- |
| Validità massima dei token di aggiornamento (rilasciati a utenti federati con informazioni sulla revoca insufficienti<sup>1</sup>) |Token di aggiornamento (rilasciati a utenti federati con informazioni sulla revoca insufficienti<sup>1</sup>) |12 ore |
| Tempo inattività massimo token di aggiornamento (rilasciata a client riservati) |Token di aggiornamento (rilasciati a client riservati) |90 giorni |
| Validità massima token di aggiornamento (rilasciata a client riservati) |Token di aggiornamento (rilasciati a client riservati) |Fino a revoca |

* <sup>1</sup>gli utenti federati con informazioni di revoca insufficiente comprende tutti gli utenti che non dispongono di hello "LastPasswordChangeTimestamp" attributo sincronizzato. Questi utenti sono specificati per questa breve Max Age perché AAD è tooverify non è possibile quando i token toorevoke che sono associate tooan vecchia credenziali (ad esempio una password che è stata modificata) e dovrà verificare nuovamente più frequentemente tooensure utente hello e associati i token sono ancora in regola. tooimprove questa esperienza, tenant admins deve garantire che essi sono sincronizzazione hello attributo "LastPasswordChangeTimestamp" (può essere impostata sull'oggetto utente hello tramite Powershell o mediante AADSync).

### <a name="policy-evaluation-and-prioritization"></a>Definizione della priorità e valutazione dei criteri
È possibile creare e quindi assegnare un'applicazione specifica di criteri tooa durata del token, l'organizzazione tooyour e tooservice entità. Più criteri, potrebbero applicarsi tooa specifica applicazione. criteri di durata del token Hello che diventa effettiva segue queste regole:

* Se un criterio viene assegnato in modo esplicito un'entità servizio toohello, viene applicato.
* Se nessun criterio dell'entità servizio toohello assegnate in modo esplicito, viene applicato un criterio assegnato in modo esplicito l'organizzazione principale toohello dell'entità servizio hello.
* Se l'entità servizio toohello o toohello organizzazione, in modo esplicito è assegnato alcun criterio, vengono applicati i criteri di hello toohello applicazione assegnato.
* Viene applicato se nessun criterio è stato assegnato toohello servizio principale, organizzazione hello o un oggetto applicazione hello, hello valori predefiniti. (Vedere la tabella hello in [le proprietà di durata dei token configurabile](#configurable-token-lifetime-properties).)

Per ulteriori informazioni sulla relazione hello tra gli oggetti dell'applicazione e oggetti entità servizio, vedere [applicazione e oggetti entità servizio in Azure Active Directory](active-directory-application-objects.md).

La validità del token viene valutata in fase di hello hello token viene usato. criteri di Hello con priorità più alta di hello in un'applicazione hello che si accede ha effetto.

> [!NOTE]
> Di seguito è riportato uno scenario di esempio.
>
> Un utente desideri tooaccess due applicazioni: applicazione Web A e B. applicazione Web
> 
> Fattori:
> * Entrambe le applicazioni web sono in hello stesso padre di organizzazione.
> * Token 1 di criteri di durata con sessione Token Max Age otto ore è impostato come predefinito dell'organizzazione di hello padre.
> * Applicazione Web è un'applicazione web di uso normale e non è collegato tooany criteri.
> * L'applicazione Web B viene usata per processi riservati. Il servizio dell'entità è collegato tooToken 2 di criteri di durata, che dispone di una sessione Token Max Age di 30 minuti.
>
> 12:00 PM, hello utente inizia a una nuova sessione del browser e prova tooaccess A. applicazione Web hello utente viene reindirizzato tooAzure AD e viene chiesto toosign in. Questo crea un cookie che presenta un token di sessione hello. utente Hello è reindirizzato tooWeb indietro applicazione con un ID di token che consente a un'applicazione hello tooaccess utente hello.
>
> 12:15 PM, utente hello tenta tooaccess B. applicazione Web hello browser reindirizzamenti tooAzure AD, che rileva i cookie di sessione hello. Entità di servizio Web dell'applicazione B è collegato tooToken 2 di criteri di durata, ma fa anche parte dell'organizzazione padre hello, con il valore predefinito 1 di criteri di durata Token. Token 2 di criteri di durata eseguita perché l'entità collegata tooservice criteri hanno la priorità rispetto a criteri predefiniti dell'organizzazione. token di sessione Hello sia stato rilasciato originariamente all'interno di hello ultimi 30 minuti, affinché sia considerato valido. utente Hello è reindirizzato tooWeb indietro applicazione B con un ID di token che concede l'accesso.
>
> 1:00 PM, hello tentativi tooaccess A. applicazione Web hello utente è reindirizzato tooAzure AD. Applicazione Web non è collegato tooany criteri, ma poiché è in un'organizzazione con il valore predefinito 1 di criteri di durata Token, tale criterio viene applicato. cookie di sessione Hello che sia stato rilasciato originariamente all'interno di hello ultime otto ore è stata rilevata. utente Hello viene automaticamente reindirizzato tooWeb indietro applicazione con un nuovo token ID. utente Hello non è necessario tooauthenticate.
>
> Immediatamente in seguito, utente hello tenta tooaccess B. applicazione Web hello è reindirizzato tooAzure Active Directory. Come prima, vengono applicati i criteri per la durata dei token 2. Perché il token hello è stato rilasciato più di 30 minuti, l'utente di hello è tooreenter richieste le credenziali di accesso. Vengono rilasciati un nuovo token di sessione e un nuovo token ID. utente Hello può quindi accedere a B. applicazione Web
>
>

## <a name="configurable-policy-property-details"></a>Dettagli sulla proprietà dei criteri configurabili
### <a name="access-token-lifetime"></a>Durata dei token di accesso
**Stringa:** AccessTokenLifetime

**Impatto:** token di accesso, token ID

**Riepilogo:** questo tipo di criteri controlla per quanto tempo i token di accesso e ID della risorsa sono considerati validi. La riduzione delle proprietà di durata del Token accesso hello riduce il rischio di hello di un token di accesso o un ID token utilizzato da un attore dannoso per un lungo periodo di tempo. (Questi token non è possibile revocare). compromesso di Hello è che le prestazioni vengano compromesse, perché i token di hello hanno toobe sostituito più spesso.

### <a name="refresh-token-max-inactive-time"></a>Tempo inattività massimo token di aggiornamento
**Stringa:** MaxInactiveTime

**Impatto:** token di aggiornamento

**Riepilogo:** questo criterio controlla la modalità precedente può essere un token di aggiornamento prima che un client può non utilizzarlo tooretrieve una nuova coppia di token di aggiornamento di accesso durante il tentativo di tooaccess questa risorsa. Poiché in genere, un nuovo token di aggiornamento viene restituito quando viene utilizzato un token di aggiornamento, questo criterio impedisce l'accesso se il client di hello tenta tooaccess qualsiasi risorsa utilizzando il token di aggiornamento corrente hello hello durante il periodo di tempo specificato.

Questo criterio impone che gli utenti che non sono stati attivi nel loro tooretrieve tooreauthenticate client un nuovo token di aggiornamento.

Hello proprietà Token Max inattiva ora di aggiornamento deve essere impostato tooa valore inferiore a fattore singolo Token Max Age hello e le proprietà di multi-Factor Aggiorna Token Max Age hello.

### <a name="single-factor-refresh-token-max-age"></a>Validità massima token di aggiornamento a fattore singolo
**String:** MaxAgeSingleFactor

**Impatto:** token di aggiornamento

**Riepilogo:** questo controlli dei criteri come prolungata a un utente può utilizzare un aggiornamento di token tooget un nuovo accesso aggiornamento coppia di token dopo che ultima autenticati correttamente utilizzando solo un singolo fattore. Dopo che un utente esegue l'autenticazione e riceve un nuovo token di aggiornamento, utente hello è possibile utilizzare il flusso di token aggiornamento hello per hello specificato periodo di tempo. (Questo è true, purché non sia stato revocato il token di aggiornamento corrente hello e che non rimanga inattiva per più di tempo inattivo hello). A questo punto, l'utente hello è forzato tooreauthenticate tooreceive un nuovo token di aggiornamento.

Riducendo l'età massima hello forza tooauthenticate gli utenti più spesso. Poiché l'autenticazione a fattore singolo è meno sicura rispetto all'autenticazione a più fattori, è consigliabile impostare il valore della proprietà tooa ovvero uguale tooor minore hello proprietà Age multi-Factor Aggiorna Token Max.

### <a name="multi-factor-refresh-token-max-age"></a>Validità massima token di aggiornamento a più fattori
**Strings:** MaxAgeMultiFactor

**Impatto:** token di aggiornamento

**Riepilogo:** questo controlli dei criteri come prolungata a un utente può utilizzare un aggiornamento di token tooget un nuovo accesso aggiornamento coppia di token dopo che ultima autenticati correttamente tramite più fattori. Dopo che un utente esegue l'autenticazione e riceve un nuovo token di aggiornamento, utente hello è possibile utilizzare il flusso di token aggiornamento hello per hello specificato periodo di tempo. (Questo è true, purché non sia stato revocato il token di aggiornamento corrente hello e non è inattiva per più di tempo inattivo hello). A questo punto, gli utenti sono obbligati tooreauthenticate tooreceive un nuovo token di aggiornamento.

Riducendo l'età massima hello forza tooauthenticate gli utenti più spesso. Poiché l'autenticazione a fattore singolo è meno sicura rispetto all'autenticazione a più fattori, è consigliabile impostare questo valore tooa della proprietà che è uguale tooor maggiore di proprietà a fattore singolo aggiornamento Token Max Age hello.

### <a name="single-factor-session-token-max-age"></a>Validità massima token di sessione a fattore singolo
**Stringa** MaxAgeSessionSingleFactor

**Impatto:** token di sessione (permanenti e non permanenti)

**Riepilogo:** questa criterio consente quanto tempo un utente può usare un tooget token di sessione un nuovo ID e la stessa sessione del token dopo che ultima autenticati correttamente utilizzando solo un singolo fattore. Dopo che un utente esegue l'autenticazione e riceve un token nuova sessione, utente hello è possibile utilizzare flusso token di sessione hello per hello specificato periodo di tempo. (Questo è true, purché il token della sessione corrente hello non sia stato revocato e non sia scaduto). Dopo il periodo di tempo specificato di hello, hello è forzato tooreauthenticate tooreceive un token di sessione di nuovo.

Riducendo l'età massima hello forza tooauthenticate gli utenti più spesso. Poiché l'autenticazione a fattore singolo è meno sicura rispetto all'autenticazione a più fattori, è consigliabile impostare questo valore di proprietà di multi-Factor sessione Token Max Age uguale tooor minore di hello tooa proprietà.

### <a name="multi-factor-session-token-max-age"></a>Validità massima token di sessione a più fattori
**Stringa:** MaxAgeSessionMultiFactor

**Impatto:** token di sessione (permanenti e non permanenti)

**Riepilogo:** questa criterio consente quanto tempo un utente può usare un tooget token di sessione un nuovo ID e la stessa sessione del token dopo hello ultima volta che autenticati correttamente tramite più fattori. Dopo che un utente esegue l'autenticazione e riceve un token nuova sessione, utente hello è possibile utilizzare flusso token di sessione hello per hello specificato periodo di tempo. (Questo è true, purché il token della sessione corrente hello non sia stato revocato e non sia scaduto). Dopo il periodo di tempo specificato di hello, hello è forzato tooreauthenticate tooreceive un token di sessione di nuovo.

Riducendo l'età massima hello forza tooauthenticate gli utenti più spesso. Poiché l'autenticazione a fattore singolo è meno sicura rispetto all'autenticazione a più fattori, è consigliabile impostare questo valore tooa della proprietà che è uguale tooor maggiore di proprietà a fattore singolo sessione Token Max Age hello.

## <a name="example-token-lifetime-policies"></a>Criteri per la durata dei token di esempio
In Azure AD sono disponibili diversi scenari che permettono di creare e gestire la durata dei token per le app, le entità servizio e l'intera organizzazione. Questa sezione illustra alcuni scenari comuni relativi ai criteri che consentono di definire nuove regole per:

* Durata del token
* Tempo di inattività massimo del token
* Validità massima del token

Negli esempi di hello, utili come:

* Gestire i criteri predefiniti di un'organizzazione
* Creare criteri per l'accesso Web
* Creare criteri per un'app nativa che chiama un'API Web
* Gestire criteri avanzati

### <a name="prerequisites"></a>Prerequisiti
In hello seguono esempi, creare, aggiornare, collegare ed eliminare i criteri per le app, le entità servizio e l'organizzazione complessiva. Nel caso di nuova tooAzure Active Directory, è consigliabile conoscere [come tooget un Azure AD tenant](active-directory-howto-tenant.md) prima di procedere con questi esempi.  

hello tooget avviato, alla procedura seguente:

1. Download più recenti hello [versione di Azure AD PowerShell modulo anteprima pubblica](https://www.powershellgallery.com/packages/AzureADPreview).
2. Eseguire hello `Connect` comando toosign in tooyour account amministratore di Azure AD. Eseguire questo comando ogni volta che si avvia una nuova sessione.

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. toosee tutti i criteri che sono stati creati all'interno dell'organizzazione, hello esecuzione dopo il comando. Eseguire questo comando dopo la maggior parte delle operazioni seguenti scenari hello. Comando hello inoltre consente ottenere hello * * * * dei criteri di.

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a>Esempio: gestire i criteri predefiniti di un'organizzazione
In questo esempio vengono creati criteri che permettono agli utenti di eseguire l'accesso con una frequenza minore nell'intera organizzazione. toodo, creare un criterio di durata del token per i token di aggiornamento a fattore singolo, che viene applicata all'interno dell'organizzazione. criteri Hello sono applicato tooevery applicazione nell'organizzazione e dell'entità servizio tooeach che non dispone già di un criterio impostato.

1. Creare i criteri per la durata dei token.

    1.  Set hello a fattore singolo Token di aggiornamento troppo "finché non revocati." token Hello non scade fino a quando non viene revocato l'accesso. Creare hello definizione dei criteri seguenti:

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  criteri di hello toocreate, Esegui hello comando seguente:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  toosee il nuovo criterio e criteri di tooget hello **ObjectId**eseguire hello il seguente comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Aggiornare i criteri di hello.

    È possibile decidere che i criteri prima di hello che è impostato in questo esempio non sono rigorose di quanto richiesto dal servizio. eseguire il Token di aggiornamento a fattore singolo tooexpire nei due giorni, tooset hello il seguente comando:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a>Esempio: creare criteri per l'accesso Web

In questo esempio, si crea un criterio che richiede agli utenti tooauthenticate più frequentemente nelle applicazioni web. Questo criterio Imposta durata hello del token di accesso o ID hello e la validità massima di hello di un'entità servizio toohello token di sessione a più fattori dell'app web.

1. Creare i criteri per la durata dei token.

    Questo criterio, per web Accedi, imposta durata token di accesso o ID hello e hello max sessione a fattore singolo token age tootwo ore.

    1.  criteri di hello toocreate, eseguiti questo comando:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee i nuovi criteri e i criteri di hello tooget **ObjectId**eseguire hello il seguente comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  Assegnare l'entità di servizio tooyour criteri hello. È inoltre necessario hello tooget **ObjectId** dell'entità servizio. 

    1.  toosee le entità servizio tutti dell'organizzazione, è possibile eseguire query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). O, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), accedi tooyour account Azure AD.

    2.  Quando si dispone di hello **ObjectId** dell'entità del servizio, eseguire hello comando seguente:

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a>Esempio: creare criteri per un'app nativa che chiama un'API Web
In questo esempio, si crea un criterio che richiede agli utenti tooauthenticate frequentemente. criteri di Hello ne aumentano anche il tempo di hello in cui che un utente può rimanere inattivo prima è necessario ripetere l'autenticazione utente hello. criteri di Hello sono applicato toohello web API. Quando app nativa hello richiede hello web API come una risorsa, viene applicato il criterio.

1. Creare i criteri per la durata dei token.

    1.  toocreate un criterio strict per un'API web, eseguire hello comando seguente:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  toosee i nuovi criteri e i criteri di hello tooget **ObjectId**eseguire hello il seguente comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Assegnare hello criteri tooyour web API. È inoltre necessario hello tooget **ObjectId** dell'applicazione. Hello toofind modo migliore l'app **ObjectId** è hello toouse [portale di Azure](https://portal.azure.com/).

   Quando si dispone di hello **ObjectId** dell'app, eseguire hello comando seguente:

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of hello Application> -RefObjectId <ObjectId of hello Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a>Esempio: gestire criteri avanzati
In questo esempio è creare alcuni criteri, toolearn funzionamento del sistema di priorità hello. È possibile inoltre come toomanage più criteri che sono oggetti tooseveral applicato.

1. Creare i criteri per la durata dei token.

    1.  toocreate un criterio predefinito di organizzazione che imposta i giorni hello too30 durata a fattore singolo Token di aggiornamento, eseguire hello comando seguente:

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  toosee il nuovo criterio e criteri di tooget hello **ObjectId**eseguire hello il seguente comando:

        ```PowerShell
        Get-AzureADPolicy
        ```

2. Assegnare l'entità di servizio tooa criteri hello.

    A questo punto, si dispone di un criterio che si applica toohello intera organizzazione. È possibile vuole toopreserve il criterio di 30 giorni per un'entità servizio specifico, ma modificare hello organizzazione predefinito criteri toohello limite massimo di "finché non revocati."

    1.  toosee le entità servizio tutti dell'organizzazione, è possibile eseguire query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity). In alternativa, eseguire l'accesso con l'account Azure AD dallo strumento [Graph Explorer di Azure AD](https://graphexplorer.cloudapp.net/).

    2.  Quando si dispone di hello **ObjectId** dell'entità del servizio, eseguire hello comando seguente:

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of hello ServicePrincipal> -RefObjectId <ObjectId of hello Policy>
            ```
        
3. Set hello `IsOrganizationDefault` flag toofalse:

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. Creare nuovi criteri predefiniti dell'organizzazione.

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    È ora entità servizio collegato tooyour hello originale criteri che il nuovo criterio di hello è impostato come il criterio predefinito di organizzazione. È importante tooremember che i criteri applicati tooservice entità hanno la priorità sui criteri predefiniti dell'organizzazione.

## <a name="cmdlet-reference"></a>Informazioni di riferimento sui cmdlet

### <a name="manage-policies"></a>Gestire i criteri

È possibile utilizzare i seguenti cmdlet toomanage criteri hello.

#### <a name="new-azureadpolicy"></a>New-AzureADPolicy

Crea nuovi criteri.

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| Parametri | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Definition</code> |Matrice di stringified JSON che contiene le regole dei criteri di hello tutti. | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |Stringa del nome dei criteri hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |Se true, imposta i criteri di hello come criteri predefiniti dell'organizzazione hello. Se false, non esegue alcuna operazione. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |Tipo di criteri. Per la durata dei token usare sempre "TokenLifetimePolicy". | `-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[Facoltativo] |Imposta un ID alternativo per i criteri di hello. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a>Get-AzureADPolicy
Ottiene tutti i criteri di Azure AD o i criteri specificati.

```PowerShell
Get-AzureADPolicy
```

| Parametri | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code>[Facoltativo] |**ID oggetto (Id)** del criterio hello desiderato. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a>Get-AzureADPolicyAppliedObject
Ottiene tutte le applicazioni e delle entità servizio che sono collegati tooa criteri.

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** del criterio hello desiderato. |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a>Set-AzureADPolicy
Aggiorna i criteri esistenti.

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| Parametri | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** del criterio hello desiderato. |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |Stringa del nome dei criteri hello. |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;Definition</code>[Facoltativo] |Matrice di stringified JSON che contiene le regole dei criteri di hello tutti. |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;IsOrganizationDefault</code>[Facoltativo] |Se true, imposta i criteri di hello come criteri predefiniti dell'organizzazione hello. Se false, non esegue alcuna operazione. |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code>[Facoltativo] |Tipo di criteri. Per la durata dei token usare sempre "TokenLifetimePolicy". |`-Type "TokenLifetimePolicy"` |
| <code>&#8209;AlternativeIdentifier</code>[Facoltativo] |Imposta un ID alternativo per i criteri di hello. |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a>Remove-AzureADPolicy
Eliminazioni hello specificato criteri.

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** del criterio hello desiderato. | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a>Criteri dell'applicazione
È possibile utilizzare i seguenti cmdlet per i criteri di applicazione hello.</br></br>

#### <a name="add-azureadapplicationpolicy"></a>Add-AzureADApplicationPolicy
Hello collegamenti specificato tooan applicazione dei criteri.

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** dei criteri di hello. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a>Get-AzureADApplicationPolicy
Ottiene i criteri di hello assegnato tooan applicazione.

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a>Remove-AzureADApplicationPolicy
Rimuove i criteri da un'applicazione.

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| Parametri | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** dei criteri di hello. | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a>Criteri dell'entità servizio
È possibile utilizzare i seguenti cmdlet per i criteri dell'entità servizio hello.

#### <a name="add-azureadserviceprincipalpolicy"></a>Add-AzureADServicePrincipalPolicy
Collegamenti hello dell'entità servizio tooa di criteri specificata.

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |**ObjectId** dei criteri di hello. | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a>Get-AzureADServicePrincipalPolicy
Ottiene qualsiasi entità di servizio specificato criteri toohello collegato.

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a>Remove-AzureADServicePrincipalPolicy
Rimuove i criteri di hello dall'entità servizio specificata hello.

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| parameters | Descrizione | Esempio |
| --- | --- | --- |
| <code>&#8209;Id</code> |**ID oggetto (Id)** di un'applicazione hello. | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |**ObjectId** dei criteri di hello. | `-PolicyId <ObjectId of Policy>` |
