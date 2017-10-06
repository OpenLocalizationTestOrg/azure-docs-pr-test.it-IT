---
title: aaaHow toodelegate registrazione e il prodotto sottoscrizione utente
description: Informazioni su come utente toodelegate registrazione e il prodotto tooa sottoscrizione di terze parti in Gestione API di Azure.
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>La sottoscrizione di prodotto e la registrazione utente toodelegate
La delega consente toouse il sito Web esistente per la gestione tooproducts sign-in/iscrizione e sottoscrizione di sviluppatore come anziché funzionalità incorporate di hello toousing nel portale per sviluppatori hello. Questo modo i dati degli utenti del sito Web tooown hello ed eseguire la convalida di hello di questi passaggi in modo personalizzato.

## <a name="delegate-signin-up"></a>Delega dell'accesso e dell'iscrizione degli sviluppatori
toodelegate developer tooyour Accedi ed effettuare l'iscrizione sito Web esistente che è necessario un endpoint speciale delega toocreate del sito che funge da punto di ingresso per tale richiesta avviata dal portale per sviluppatori di gestione API hello hello.

flusso di lavoro finale Hello verrà modificato come segue:

1. Developer fare clic sul collegamento di iscrizione o di accesso di hello in hello portale per sviluppatori di gestione API
2. Browser viene reindirizzato toohello delega endpoint
3. Endpoint di delega in cambio utente viene reindirizzato tooor presenta dell'interfaccia utente in cui viene chiesto toosign aggiuntivo o per l'abbonamento
4. Se l'operazione riesce, hello è reindirizzato toohello indietro gestione API per sviluppatori pagina del portale da che sono avviate

toobegin, si prima tooroute gestione API di configurazione richieste con l'endpoint di delega. Nel portale di pubblicazione di gestione API hello, fare clic su **sicurezza** e quindi fare clic su hello **delega** scheda. Fare clic sulla casella di controllo di hello tooenable 'Delegate Accedi & iscrizione'.

![Pagina Delega][api-management-delegation-signin-up]

* Decidere quali hello URL dell'endpoint speciali delega verrà e immetterlo nel hello **URL dell'endpoint delega** campo. 
* All'interno di hello **chiave di autenticazione delega** immettere una chiave privata che verrà utilizzato toocompute tooyou una firma fornito per la verifica tooensure che hello richiesta proviene effettivamente da Gestione API di Azure. È possibile fare clic su hello **generare** toohave pulsante Gestione API in modo casuale, generare una chiave per l'utente.

È possibile procedere hello toocreate **endpoint delega**. Dispone di tooperform una serie di azioni:

1. Riceve una richiesta in hello seguente formato:
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*
   > 
   > 
   
    Parametri di query per il caso di accesso / iscrizione hello:
   
   * **operation**: identifica il tipo di richiesta di delega; in questo caso può essere solo di tipo **SignIn**
   * **returnUrl**: hello URL della pagina hello in cui hello utente ha fatto clic su un collegamento di iscrizione o di accesso
   * **salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza
   * **SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati
2. Verificare che la richiesta hello proviene da Gestione API di Azure (facoltativo ma consigliato per la sicurezza)
   
   * Calcolare un hash di HMAC-SHA512 di una stringa in base a hello **returnUrl** e **salt** parametri di query ([codice di esempio riportate di seguito]):
     
     > HMAC(**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Confrontare hello hash calcolato in precedenza toohello valore hello **sig** parametro di query. Se hello due hash corrispondono, spostare nel passaggio successivo toohello, in caso contrario negare hello richiesta.
3. Verificare che si riceve una richiesta per l'accesso in/segno: hello **operazione** verrà impostato il parametro di query troppo "**SignIn**".
4. Utente hello presente con interfaccia utente toosign-in o iscrizione
5. Se l'utente di hello è iscrizione è toocreate un account corrispondente per tali in Gestione API. [Creare un utente] con hello API REST gestione API. In tal caso, assicurarsi di impostare toohello ID utente di hello stesso che si trovi nell'archivio utente o ID tooan che è possibile tenere traccia delle.
6. Quando hello viene correttamente autenticato:
   
   * [richiedere un token di single sign-on (SSO)] tramite hello API REST gestione API
   * aggiungere un toohello di parametro di query returnUrl URL SSO ricevuto dalla chiamata all'API hello precedente:
     
     > ad esempio, https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * hello utente toohello sopra prodotti URL di reindirizzamento

In aggiunta toohello **SignIn** operazione, è anche possibile eseguire la gestione degli account seguendo i passaggi precedenti hello e utilizzando uno di hello seguenti operazioni.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

È necessario passare hello seguenti parametri di query per le operazioni di gestione di account.

* **operation**: identifica il tipo di richiesta di delega (ChangePassword, ChangeProfile o CloseAccount)
* **userId**: id utente hello di hello account toomanage
* **salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza
* **SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati

## <a name="delegate-product-subscription"></a>Delega della sottoscrizione ai prodotti
La sottoscrizione al prodotto di delega funziona in modo analogo toodelegating utente Accedi/verticale. flusso di lavoro Hello finale sarà come segue:

1. Sviluppatore seleziona un prodotto nel portale per sviluppatori di gestione API hello e fa clic sul pulsante Sottoscrivi hello
2. Browser viene reindirizzato toohello delega endpoint
3. Endpoint di delega esegue operazioni di sottoscrizione di prodotto obbligatorio: si tratta di tooyou e può comportare reindirizzamento toorequest di pagina tooanother informazioni di fatturazione, porre altre domande, o semplicemente l'archiviazione delle informazioni di hello e che non richiedono un'azione dell'utente

funzionalità di hello tooenable, su hello **delega** pagina fare clic su **delegare sottoscrizione al prodotto**.

Assicurarsi quindi di endpoint di delega hello esegue hello seguenti azioni:

1. Riceve una richiesta in hello seguente formato:
   
   > *{operazione} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {toosubscribe prodotto per} & userId = {user richiesta} & salt = {stringa} & sig = {stringa}*
   > 
   > 
   
    Parametri di query per il caso di sottoscrizione hello prodotto:
   
   * **operation**: identifica il tipo di richiesta di delega. Per la sottoscrizione al prodotto richieste hello i valori validi sono:
     * "Sottoscrizione": fornito di un tooa di utente richiesta toosubscribe hello ha prodotto con ID (vedere sotto)
     * "Annullare la sottoscrizione": toounsubscribe una richiesta utente da un prodotto
     * "Rinnovare": un toorenew richiesta una sottoscrizione (ad esempio, che può scadere in)
   * **productId**: hello ID dell'utente di hello hello prodotto richiesto toosubscribe per
   * **userId**: hello ID dell'utente hello per il quale hello richiesta
   * **salt**: stringa salt speciale usata per il calcolo di un hash di sicurezza
   * **SIG**: hash calcolato un toobe hash sicurezza calcolata utilizzata per tooyour di confronto personalizzati
2. Verificare che la richiesta hello proviene da Gestione API di Azure (facoltativo ma consigliato per la sicurezza)
   
   * Calcolare un HMAC-SHA512 di una stringa in base a hello **productId**, **userId** e **salt** parametri di query:
     
     > HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Confrontare hello hash calcolato in precedenza toohello valore hello **sig** parametro di query. Se hello due hash corrispondono, spostare nel passaggio successivo toohello, in caso contrario negare hello richiesta.
3. Eseguire l'elaborazione della sottoscrizione qualsiasi prodotto in base al tipo di hello dell'operazione richiesta **operazione** -ad esempio fatturazione, ulteriori domande e così via.
4. Nella sottoscrizione correttamente hello utente toohello prodotto del lato, sottoscrizione prodotto di gestione API di hello utente toohello da [hello chiamata API REST per la sottoscrizione al prodotto].

## <a name="delegate-example-code"></a> Codice di esempio
Questi mostra esempi di codice come hello tootake *chiave di convalida di delega*, questo valore è impostato nella schermata di delega hello del portale di pubblicazione hello, toocreate un HMAC che viene quindi utilizzato firma hello toovalidate, dimostrando validità hello di hello returnUrl passato. Hello stesso codice funziona per productId hello e ID utente con una lieve modifica.

**Hash toogenerate codice c# di returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**NodeJS codice toogenerate hash returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla delega, vedere hello video seguenti.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[richiedere un token di single sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[hello chiamata API REST per la sottoscrizione al prodotto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[codice di esempio riportate di seguito]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
