---
title: aaaConfigure al servizio Gestione API tramite Git - Azure | Documenti Microsoft
description: Informazioni su come toosave e configurare la configurazione del servizio Gestione API tramite Git.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Come toosave e configurare la configurazione del servizio Gestione API tramite Git
> 
> 

Ogni istanza del servizio Gestione API gestisce un database di configurazione che contiene informazioni sulla configurazione di hello e i metadati per l'istanza del servizio hello. Possibile modificare l'istanza del servizio toohello modificando un'impostazione nel portale di pubblicazione hello, usando un cmdlet di PowerShell o effettua una chiamata API REST. Inoltre metodi toothese, è inoltre possibile gestire la configurazione di istanza del servizio tramite Git, l'abilitazione di scenari di gestione del servizio, ad esempio:

* Controllo delle versioni della configurazione: downolad e archiviazione di versioni diverse della configurazione del servizio
* BULK modifiche di configurazione: l'apportare modifiche toomultiple parti della configurazione del servizio nel repository locale e l'integrazione di server di toohello indietro di hello modifiche con una singola operazione
* Toolchain Git e flusso di lavoro - utilizzare gli strumenti Git hello e flussi di lavoro che si ha già familiarità con

Hello seguente diagramma mostra una panoramica di hello modi tooconfigure all'istanza del servizio Gestione API.

![Configurare Git][api-management-git-configure]

Quando si apportano modifiche tooyour servizio tramite il portale di pubblicazione hello, i cmdlet di PowerShell o hello API REST, si sta gestendo il database di configurazione del servizio usando hello `https://{name}.management.azure-api.net` endpoint, come mostrato sul lato destro hello del diagramma hello. bordo sinistro del diagramma hello Hello viene illustrato come è possibile gestire la configurazione del servizio tramite Git e repository Git per il servizio disponibile all'indirizzo `https://{name}.scm.azure-api.net`.

Hello alla procedura seguente viene fornita una panoramica di gestione all'istanza del servizio Gestione API tramite Git.

1. Accedere alla configurazione Git nel servizio
2. Salvare il repository Git di tooyour database di configurazione di servizio
3. Clona macchina locale tooyour di hello repository Git
4. Pull repository più recente di hello verso il basso tooyour di computer locale e il commit e push repository tooyour indietro delle modifiche
5. Distribuire le modifiche di hello dal repository di in un database di configurazione del servizio

Questo articolo viene descritto come tooenable e utilizzare Git toomanage la configurazione del servizio e fornisce un riferimento per hello file e cartelle nel repository Git hello.

## <a name="access-git-configuration-in-your-service"></a>Accedere alla configurazione Git nel servizio
È possibile visualizzare rapidamente lo stato di hello della configurazione di Git visualizzando icona Git hello nell'angolo superiore destro di hello del portale di pubblicazione hello. In questo esempio, il messaggio di stato hello indica che non vi siano repository toohello le modifiche non salvate. Questo avviene perché il database di configurazione del servizio Gestione API hello non è ancora stato salvato toohello repository.

![Stato Git][api-management-git-icon-enable]

tooview e configurare le impostazioni di configurazione di Git, è possibile fare clic sull'icona Git hello o fare clic su hello **sicurezza** menu e passare toohello **repository di configurazioni** scheda.

![Abilitare GIT][api-management-enable-git]

> [!IMPORTANT]
> Le informazioni riservate che non sono definiti come proprietà verranno archiviate nel repository di hello e rimarranno nella cronologia di finché non si disabilitare e riabilitare l'accesso di Git. Proprietà forniscono toomanage un luogo sicuro i valori di stringa costante, inclusi i segreti, in tutte le API criteri di configurazione e, pertanto non è toostore loro direttamente nelle istruzioni dei criteri. Per ulteriori informazioni, vedere [come proprietà toouse nei criteri di gestione API di Azure](api-management-howto-properties.md).
> 
> 

Per informazioni sull'attivazione e disabilitazione dell'accesso Git utilizzando hello API REST, vedere [abilitare o disabilitare l'accesso di Git utilizzando l'API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>repository Git di toosave hello servizio configurazione toohello
innanzitutto Hello prima della clonazione del repository hello è stato corrente di hello toosave del repository di toohello hello servizio configurazione. Fare clic su **Salva configurazione toorepository**.

![Salvare la configurazione][api-management-save-configuration]

Apportare le modifiche desiderate nella schermata di conferma hello e fare clic su **Ok** toosave.

![Salvare la configurazione][api-management-save-configuration-confirm]

Dopo alcuni istanti configurazione hello viene salvato e viene visualizzato lo stato configurazione hello repository hello, tra cui hello data e ora dell'ultima modifica della configurazione hello e l'ultima sincronizzazione di hello tra la configurazione del servizio hello e hello repository.

![Stato della configurazione][api-management-configuration-status]

Dopo aver salvata la configurazione hello toohello repository, possono essere clonato.

Per informazioni su come eseguire questa operazione utilizzando hello API REST, vedere [configurazione Commit snapshot utilizzando l'API REST hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>computer locale tooyour tooclone hello repository
tooclone un repository, è necessario repository tooyour di hello URL, un nome utente e una password. Hello nome utente e l'URL vengono visualizzati parte superiore di hello di hello **repository di configurazioni** scheda.

![Clonare in Git][api-management-configuration-git-clone]

password Hello viene generata nella parte inferiore di hello di hello **repository di configurazioni** scheda.

![Generare password][api-management-generate-password]

toogenerate una password, verificare innanzitutto che hello **scadenza** toohello desiderato data di scadenza e l'ora di impostare e quindi fare clic su **genera Token**.

![Password][api-management-password]

> [!IMPORTANT]
> Prendere nota della password. Dopo avere chiuso la password di hello pagina non essere visualizzata nuovamente.
> 
> 

strumento Hello seguono esempi di utilizzo hello Git Bash da [Git per Windows](http://www.git-scm.com/downloads) ma è possibile utilizzare qualsiasi strumento Git che si ha familiarità con.

Aprire lo strumento di Git nella cartella desiderata hello ed eseguire hello successivo comando tooclone hello git repository tooyour locale, utilizzando il comando hello fornito dal portale di server di pubblicazione hello.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Fornire nome utente hello e una password quando richiesto.

Se si ricevono errori, provare a modificare il `git clone` comando tooinclude hello utente nome e una password, come illustrato nell'esempio seguente hello.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Se si fornisce un errore, provare a parte password hello del comando hello di codifica degli URL. Un modo rapido toodo tratta tooopen Visual Studio e il comando seguente di hello di problema in hello **finestra controllo immediato**. hello tooopen **finestra controllo immediato**, aprire qualsiasi soluzione o progetto in Visual Studio oppure creare una nuova applicazione console vuota, scegliere **Windows**, **immediato** da Hello **Debug** menu.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Utilizzare password hello codificato con il nome e del repository percorso tooconstruct hello git comando utente.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Una volta è clonazione del repository hello è possibile visualizzare e utilizzarlo nel file system locale. Per altre informazioni, vedere [Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate il repository locale con una configurazione dell'istanza del servizio più recente hello
Se l'istanza del servizio Gestione API tooyour le modifiche apportate nel portale di pubblicazione hello oppure utilizzando hello API REST, è necessario salvare questi repository toohello modifiche prima di aggiornare il repository locale con le modifiche più recenti di hello. toodo, fare clic su **Salva configurazione toorepository** su hello **repository di configurazioni** scheda nel portale di pubblicazione hello e quindi rilasciare hello seguente comando nel repository locale.

```
git pull
```

Prima di eseguire `git pull` assicurarsi che sia nella cartella hello per il repository locale. Se è stato completato hello `git clone` comando, è necessario modificare i repository di hello directory tooyour eseguendo un comando simile hello seguente.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>modifiche toopush dal repository di server toohello di repository locale
toopush cambia dall'archivio locale del repository toohello server, è necessario eseguire il commit delle modifiche e quindi inviarli toohello repository del server. toocommit le modifiche, aprire lo strumento di comando Git, switch toohello directory del repository locale e hello problema i comandi seguenti.

```
git add --all
git commit -m "Description of your changes"
```

toopush tutti hello viene eseguito il commit toohello server, eseguire hello il seguente comando.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy qualsiasi istanza del servizio Gestione API servizio configurazione modifiche toohello
Dopo aver eseguito il commit e push toohello repository del server le modifiche locali, è possibile distribuirli tooyour istanza del servizio Gestione API.

![Distribuire][api-management-configuration-deploy]

Per informazioni su come eseguire questa operazione utilizzando hello API REST, vedere [distribuire Git Cambia database tooconfiguration utilizzando l'API REST di hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Informazioni di riferimento sulla struttura di file e cartelle del repository Git locale
Hello file e cartelle nel repository git locale hello contengono informazioni di configurazione hello sull'istanza del servizio hello.

| Elemento | Descrizione |
| --- | --- |
| Cartella api-management radice |Contiene una configurazione di livello principale per l'istanza del servizio hello |
| Cartella apis |Contiene la configurazione hello hello API nell'istanza di servizio hello |
| Cartella groups |Contiene la configurazione hello gruppi hello nell'istanza di servizio hello |
| Cartella policies |Contiene i criteri di hello nell'istanza di servizio hello |
| Cartella portalStyles |Contiene configurazione hello per le personalizzazioni del portale per sviluppatori di hello nell'istanza di servizio hello |
| Cartella products |Contiene la configurazione hello prodotti hello nell'istanza di servizio hello |
| Cartella templates |Contiene configurazione hello per i modelli di messaggio di posta elettronica hello nell'istanza di servizio hello |

Ogni cartella può contenere uno o più file e in alcuni casi una o più cartelle, ad esempio una cartella per ogni API, prodotto o gruppo. file Hello all'interno di ogni cartella sono specifici per il tipo di entità hello descritto dal nome della cartella hello.

| Tipo file | Scopo |
| --- | --- |
| json |Informazioni di configurazione di entità corrispondente di hello |
| html |Descrizioni relative entità hello, spesso visualizzato nel portale per sviluppatori hello |
| xml |Policy statements |
| css |Fogli di stile per la personalizzazione del portale per sviluppatori |

Questi file possono essere creati, eliminati, modificati e gestiti nel file system locale e modifiche hello distribuiti toohello indietro all'istanza del servizio Gestione API.

> [!NOTE]
> Hello entità seguenti non sono contenute nel repository Git hello e non può essere configurata tramite Git.
> 
> * Utenti
> * Sottoscrizioni
> * Proprietà
> * Entità del portale per sviluppatori diverse dagli stili
> 
> 

### <a name="root-api-management-folder"></a>Cartella api-management radice
radice Hello `api-management` cartella contiene un `configuration.json` file che contiene informazioni sull'istanza del servizio hello in hello seguente formato di livello principale.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

Hello primi quattro impostazioni (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, e `UserRegistrationTermsConsentRequired`) eseguire il mapping toohello seguendo le impostazioni di hello **identità** scheda hello **sicurezza** sezione.

| Impostazione | Esegue il mapping troppo|
| --- | --- |
| RegistrationEnabled |**Reindirizzare gli utenti anonimi toosign-pagina** casella di controllo |
| UserRegistrationTerms |**Terms of use on user signup**  |
| UserRegistrationTermsEnabled |**Show terms of use on signup page** |
| UserRegistrationTermsConsentRequired |**Richiedi consenso**  |

![Impostazioni di identità][api-management-identity-settings]

Hello quattro impostazioni (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, e `DelegationValidationKey`) eseguire il mapping toohello seguendo le impostazioni di hello **delega** scheda hello **sicurezza** sezione.

| Impostazione | Esegue il mapping troppo|
| --- | --- |
| DelegationEnabled |Casella di controllo **Delegate sign-in & sign-up** (Delega accesso e iscrizione) |
| DelegationUrl |**Delegation endpoint URL** |
| DelegatedSubscriptionEnabled |**Delegate product subscription** |
| DelegationValidationKey |**Delegate Validation Key** |

![Impostazioni di delega][api-management-delegation-settings]

impostazione finale, Hello `$ref-policy`, esegue il mapping di file di istruzioni toohello criteri globali per l'istanza del servizio hello.

### <a name="apis-folder"></a>Cartella apis
Hello `apis` cartella contiene una cartella per ciascuna API nell'istanza di servizio hello che contiene i seguenti elementi hello.

* `apis\<api name>\configuration.json`-Questa configurazione hello per hello API e contiene informazioni sull'URL del servizio back-end hello e operazioni hello. Si tratta di hello stesse informazioni che verrebbero restituite se fosse toocall [ottenere un'API specifica](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) con `export=true` in `application/json` formato.
* `apis\<api name>\api.description.html`-si tratta di descrizione hello di hello API e corrispondono toohello `description` proprietà di hello [entità API](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Questa cartella contiene `<operation name>.description.html` file toohello operazioni mappa in hello API. Ogni file contiene la descrizione hello di una singola operazione di hello API che consente di associare toohello `description` proprietà di hello [entità operation](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello API REST.

### <a name="groups-folder"></a>Cartella groups
Hello `groups` cartella contiene una cartella per ogni gruppo definito nell'istanza di servizio hello.

* `groups\<group name>\configuration.json`-si tratta di hello configurazione per il gruppo di hello. Si tratta di hello stesse informazioni che verrebbero restituite se fosse hello toocall [ottenere un gruppo specifico](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operazione.
* `groups\<group name>\description.html`-si tratta di descrizione hello del gruppo di hello e corrispondono toohello `description` proprietà di hello [gruppo entità](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>Cartella policies
Hello `policies` cartella contiene le istruzioni dei criteri di hello per l'istanza del servizio.

* `policies\global.xml` : contiene i criteri definiti in ambito globale per l'istanza del servizio.
* `policies\apis\<api name>\`: se sono presenti criteri definiti nell'ambito delle API, tali criteri sono contenuti in questa cartella.
* `policies\apis\<api name>\<operation name>\`cartella - se si dispone di tutti i criteri definiti nell'ambito di operazione, sono contenuti in questa cartella `<operation name>.xml` file che eseguono il mapping toohello istruzioni dei criteri per ogni operazione.
* `policies\products\`-Se si dispone di tutti i criteri definiti nell'ambito del prodotto, sono contenuti in questa cartella contiene `<product name>.xml` file che eseguono il mapping toohello istruzioni dei criteri per ogni prodotto.

### <a name="portalstyles-folder"></a>Cartella portalStyles
Hello `portalStyles` cartella contiene i fogli di stile e di configurazione per le personalizzazioni del portale per sviluppatori per l'istanza del servizio hello.

* `portalStyles\configuration.json`-contiene i nomi di hello hello dei fogli di stile utilizzati dal portale per sviluppatori hello
* `portalStyles\<style name>.css`-ogni `<style name>.css` file contiene gli stili per il portale per sviluppatori di hello (`Preview.css` e `Production.css` per impostazione predefinita).

### <a name="products-folder"></a>Cartella products
Hello `products` cartella contiene una cartella per ogni prodotto definito nell'istanza di servizio hello.

* `products\<product name>\configuration.json`-si tratta di configurazione hello hello prodotto. Si tratta di hello stesse informazioni che verrebbero restituite se fosse hello toocall [ottenere un prodotto specifico](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operazione.
* `products\<product name>\product.description.html`-si tratta di descrizione hello del prodotto di hello e corrispondono toohello `description` proprietà di hello [entità product](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello API REST.

### <a name="templates"></a>Modelli
Hello `templates` cartella contiene la configurazione hello [modelli di posta elettronica](api-management-howto-configure-notifications.md) hello di istanze del servizio.

* `<template name>\configuration.json`-si tratta di hello configurazione per il modello di posta elettronica hello.
* `<template name>\body.html`-si tratta corpo hello del modello di posta elettronica hello.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni su altri modi di toomanage all'istanza del servizio, vedere:

* Gestire l'istanza di servizio utilizzando i cmdlet di PowerShell seguente hello
  * [Informazioni di riferimento sui cmdlet di PowerShell per la distribuzione dei servizi](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Informazioni di riferimento sui cmdlet di PowerShell per la gestione dei servizi](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Gestire l'istanza di servizio nel portale di pubblicazione hello
  * [Gestire la prima API in Gestione API di Azure](api-management-get-started.md)
* Gestire l'istanza di servizio utilizzando l'API REST hello
  * [Informazioni di riferimento sull'API REST di Gestione API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Guardare un video introduttivo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




