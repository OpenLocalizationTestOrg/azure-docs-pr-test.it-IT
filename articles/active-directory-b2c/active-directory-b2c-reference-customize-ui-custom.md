---
title: 'Azure B2C di Directory Active: Fare riferimento: personalizzare l''interfaccia utente del proprio processo di un utente con i criteri personalizzati di hello | Documenti Microsoft'
description: Un argomento sui criteri personalizzati di Azure Active Directory B2C
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
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Personalizzare l'interfaccia utente del proprio processo di un utente con i criteri personalizzati di hello

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Questo articolo è una descrizione di come funziona la personalizzazione dell'interfaccia utente e come tooenable con i criteri personalizzati B2C, utilizzando hello identità esperienza Framework avanzata


Un'esperienza utente integrata è fondamentale per qualsiasi soluzione Business to Consumer. Per un'esperienza utente trasparente, si intende un'esperienza di, nel dispositivo o browser, in cui il passaggio di un utente tramite il servizio non è possibile distinguere da quello del servizio clienti hello in uso.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Comprendere il modo CORS hello per la personalizzazione dell'interfaccia utente

Azure Active Directory B2C consente si toocustomize hello-e-l'aspetto dell'utente esperienza hello varie pagine che possono essere potenzialmente servite e visualizzate da Azure AD B2C tramite i criteri personalizzati.

A tale scopo, Azure AD B2C esegue codice nel browser del consumer e utilizza l'approccio moderno e standard di hello [condivisione delle risorse Multiorigine (CORS)](http://www.w3.org/TR/cors/) contenuto personalizzato di tooload da un URL specifico che si specifica in un criterio personalizzato modelli di HTML5/CSS tooyour toopoint. CORS è un meccanismo che consente di risorse limitate, ad esempio tipi di carattere, in una pagina web di toobe richiesto da un altro dominio esterno al dominio hello da cui proviene la risorsa hello.

Confronto toohello tradizionali modalità precedente, in cui le pagine modello sono di proprietà di soluzione hello in cui è fornito limitato del testo e immagini, in cui un controllo limitato di layout e l'aspetto è stato offerto toomore iniziali di difficoltà tooachieve un'esperienza senza problemi, hello CORS modo supporta HTML5 e CSS e consentono di:

- Ospitare il contenuto di hello e soluzione hello inserisce i controlli usando uno script sul lato client.
- Avere il controllo completo di ogni pixel del layout e dell'aspetto.

È possibile inserire un numero illimitato di pagine contenuto creando file HTML5/CSS secondo le esigenze.

> [!NOTE]
> Per motivi di sicurezza, utilizzare hello di JavaScript è attualmente bloccato per la personalizzazione. è necessario toounblock JavaScript, l'utilizzo di un nome di dominio personalizzato per il tenant di Azure Active Directory B2C.

In ognuno dei modelli HTML5/CSS, fornisci un *ancoraggio* elemento che corrisponde a toohello necessario `<div id=”api”>` elemento hello pagina HTML o hello contenuta come illustrato di seguito. Azure AD B2C richiede che tutte le pagine contenuto abbiano questo specifico elemento div.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Contenuto correlato AD B2C Azure può essere usata liberamente per pagina hello verrà inserita in questo elemento div, mentre altri hello della pagina hello toocontrol. il codice JavaScript Hello Azure Active Directory B2C effettua il pull di contenuti e inserisce l'HTML in questo elemento div specifico. Azure Active Directory B2C inserisce i seguenti controlli esigenze hello: account controllo di selezione, controlli di accesso, i controlli di multi-factor (attualmente telefonica) e controlli di raccolta di attributi. Azure Active Directory B2C garantisce che tutti i controlli di hello HTML5 conformi e accessibile, tutti i controlli di hello possono essere formattati e che una versione del controllo verrà non tornare.

Hello contenuto sottoposto a merge è segnalato come consumer di tooyour hello documento dinamico.

tooensure di hello sopra funziona come previsto, è necessario:

- Assicurarsi che il contenuto sia conforme a HTML5 e accessibile
- Assicurarsi che il server di contenuti sia abilitato per CORS.
- Rendere disponibile il contenuto tramite HTTPS.
- Usare URL assoluti, ad esempio https://yourdomain/content per tutti i collegamenti e il contenuto CSS.

> [!TIP]
> tooverify che hello si ospita il contenuto nel sito è abilitato CORS e verificare richieste CORS, è possibile utilizzare http://test-cors.org/ sito hello. Sito toothis grazie, è possibile semplicemente inviare hello CORS tooa server remoto della richiesta (tootest se CORS è supportata), o inviare i server di prova tooa richiesta CORS hello (tooexplore determinate funzionalità di CORS).

> [!TIP]
> Hello sito http://enable-cors.org/ costituisce inoltre più risorse utili sull'argomento.

Grazie toothis approccio basato su CORS, gli utenti finali di hello avranno un'esperienza coerenza tra l'applicazione e pagine hello servite da Azure Active Directory B2C.

## <a name="create-a-storage-account"></a>Creare un account di archiviazione

Come prerequisito, è necessario un account di archiviazione toocreate. È necessario un toocreate sottoscrizione di Azure, un account di archiviazione Blob di Azure. È possibile effettuare l'iscrizione a una versione di valutazione gratuita in hello [sito Web di Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Aprire una sessione di esplorazione e passare toohello [portale di Azure](https://portal.azure.com).
2. Accedere con le credenziali amministrative.
3. Fare clic su **Nuovo** > **Dati e archiviazione** > **Account di archiviazione**.  Viene aperto un pannello **Crea account di archiviazione**.
4. In **nome**, specificare un nome per l'account di archiviazione hello, ad esempio *contoso369b2c*. Questo valore verrà indicato in un secondo momento come troppo*storageAccountName*.
5. Selezionare le selezioni appropriate di hello per hello piano tariffario, gruppo di risorse hello e sottoscrizione hello. Assicurarsi di avere hello **tooStartboard Pin** opzione selezionata. Fare clic su **Crea**.
6. Tornare indietro toohello schermata iniziale e fare clic su account di archiviazione hello appena creato.
7. In hello **servizi** fare clic su **BLOB**. Viene aperto un pannello **Servizio BLOB**.
8. Fare clic su **+ Contenitore**.
9. In **nome**, specificare un nome per il contenitore di hello, ad esempio, *b2c*. Questo valore deve essere in un secondo momento cui tooas *containerName*.
9. Selezionare **Blob** come hello **tipo di accesso**. Fare clic su **Crea**.
10. contenitore Hello creata verrà visualizzata nell'elenco di hello in hello **pannello servizio Blob**.
11. Chiude hello **BLOB** blade.
12. In hello **blade di account di archiviazione**, fare clic su hello **chiave** icona. Viene aperto un pannello **Chiavi di accesso**.  
13. Annotare il valore di hello di **key1**. Questo valore più avanti verrà indicato come *key1*.

## <a name="downloading-hello-helper-tool"></a>Download dello strumento di supporto hello

1.  Scaricare lo strumento di supporto hello da [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Salvare hello *B2C-AzureBlobStorage-Client-master.zip* file nel computer locale.
3.  Estrarre il contenuto di hello del file hello B2C-AzureBlobStorage-Client-master.zip sul disco locale, ad esempio in hello **Pack di personalizzazione dell'interfaccia utente** cartella. Verrà creata una cartella *B2C-AzureBlobStorage-Client-master*.
4.  Apri la cartella ed Estrai contenuto hello del file di archivio hello *B2CAzureStorageClient.zip* all'interno di esso.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Caricare i file di esempio di hello-Pack di personalizzazione dell'interfaccia utente

1.  Utilizzando Esplora risorse, passare cartella toohello *B2C-AzureBlobStorage-Client-master* sotto hello *Pack di personalizzazione dell'interfaccia utente* cartella creata nella sezione precedente hello.
2.  Eseguire hello *B2CAzureStorageClient.exe* file. Questo programma verrà semplicemente caricare tutti i file nella directory hello specificare tooyour account di archiviazione e abilitare l'accesso a CORS per i file hello.
3.  Quando richiesto, specificare: a.  nome dell'account di archiviazione, di Hello *storageAccountName*, ad esempio *contoso369b2c*.
    b.  chiave di accesso primaria Hello dello spazio di archiviazione blob di azure, *key1*, ad esempio *contoso369b2c*.
    c.  nome Hello del contenitore di archiviazione blob di archiviazione, *containerName*, ad esempio *b2c*.
    d.  percorso di Hello di hello *Starter Pack* esempio file, ad esempio *... \B2CTemplates\wingtiptoys*.

Dopo avere eseguito i passaggi di hello precedenti, hello file HTML5 e CSS di hello *Pack di personalizzazione dell'interfaccia utente* per la società fittizia hello **wingtiptoys** verrà ora puntare tooyour account di archiviazione.  È possibile verificare che il contenuto di hello è stato caricato correttamente aprendo il pannello di contenitori correlati hello hello portale di Azure. In alternativa, è possibile verificare che il contenuto di hello è stato caricato correttamente accedendo alla pagina hello da un browser. Per ulteriori informazioni, vedere [Azure Active Directory B2C: uno strumento di supporto utilizzato toodemonstrate hello pagina funzionalità dell'interfaccia utente (UI) personalizzazione](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Assicurarsi di hello account di archiviazione è abilitata CORS

CORS (Cross-Origin Resource Sharing) deve essere abilitata per l'endpoint per tooload Premium di Azure Active Directory B2C il contenuto. Questo avviene perché il contenuto si trova in un dominio diverso rispetto a dominio hello Premium di Azure Active Directory B2C interagiranno con pagina hello.

tooverify si ospita il contenuto in archiviazione di hello con CORS è abilitata, procedere con hello alla procedura seguente:

1. Aprire una sessione di esplorazione e passare pagina toohello *unified.html* utilizzando hello URL completo della posizione nell'account di archiviazione, `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Ad esempio, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Passare toohttp://test-cors.org. Questo sito consente di tooverify che hello pagina che si utilizza è CORS abilitato.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. In **URL remoto**, immettere l'URL completo hello per il contenuto di unified.html e fare clic su **Invia richiesta**.
4. Verificare che l'output di hello hello **risultati** sezione *stato XHR: 200*. Questa impostazione indica che CORS è abilitato.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
account di archiviazione Hello dovrebbe contenere un contenitore blob denominato *b2c* nel nostro figura contenente hello seguenti modelli wingtiptoys dagli hello *Starter Pack*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Hello nella tabella seguente descrive hello scopo di hello sopra pagine HTML5.

| Modello HTML5 | Descrizione |
|----------------|-------------|
| *phonefactor.html* | Questa pagina può essere usata come modello per una pagina di autenticazione a più fattori. |
| *resetpassword.html* | Questa pagina può essere usata come modello per una pagina Password dimenticata. |
| *selfasserted.html* | Questa pagina può essere usata come modello per una pagina di iscrizione all'account di social networking, una pagina di iscrizione dell'account locale o una pagina di accesso dell'account locale. |
| *unified.html* | Questa pagina può essere usata come modello per una pagina unificata per l'iscrizione o l'accesso. |
| *updateprofile.html* | Questa pagina può essere usata come modello per una pagina di aggiornamento del profilo. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Aggiungere un passaggio di utente tooyour collegamento tooyour HTML5/CSS modelli

È possibile aggiungere un passaggio di utente collegamento tooyour HTML5/CSS modelli tooyour modificando direttamente un criterio personalizzato.

Hello personalizzato HTML5/CSS modelli toouse in viaggio l'utente dispone toobe specificato in un elenco di definizioni di contenuto che può essere usato in questi percorsi utente. A tale scopo, facoltativo  *<ContentDefinitions>*  elemento XML deve essere dichiarato in hello  *<BuildingBlocks>*  sezione del file XML di criteri personalizzati.

Hello nella tabella seguente descrive hello set di ID di definizione del contenuto riconosciuto dal motore di analisi di hello Azure Active Directory B2C identità e il tipo di hello di pagine che si riferisce toothem.

| ID definizione del contenuto | Descrizione |
|-----------------------|-------------|
| *api.error* | **Pagina di errore**. Questa pagina viene visualizzata quando viene rilevata un'eccezione o un errore. |
| *api.idpselections* | **Pagina di selezione del provider di identità**. Questa pagina contiene un elenco di identità, i provider che hello utente sono disponibili durante l'accesso. Sono presenti provider di identità aziendali, provider di identità basati su social network, ad esempio Facebook e Google+, o account locali (basati su indirizzo di posta elettronica o nome utente). |
| *api.idpselections.signup* | **Selezione del provider di identità per l'iscrizione**. Questa pagina contiene un elenco di provider che hello utente sono disponibili durante l'iscrizione di identità. Sono presenti provider di identità aziendali, provider di identità basati su social network, ad esempio Facebook e Google+, o account locali (basati su indirizzo di posta elettronica o nome utente). |
| *api.localaccountpasswordreset* | **Pagina Password dimenticata**. Questa pagina contiene un form dispone di tale utente hello tooinitiate toofill Reimposta la password.  |
| *api.localaccountsignin* | **Pagina di accesso dell'account locale**. Questa pagina contiene un modulo di accesso utente hello è toofill in quando si accede a un account locale che è basato su un indirizzo di posta elettronica o un nome utente. modulo Hello può contenere una casella di input di testo e una casella di immissione di password. |
| *api.localaccountsignup* | **Pagina di iscrizione dell'account locale**. Questa pagina contiene un modulo di iscrizione utente hello ha toofill nella quando eseguire l'iscrizione per un account locale che è basato su un indirizzo di posta elettronica o un nome utente. modulo Hello può contenere diversi controlli di input, ad esempio una casella di input di testo, casella di immissione di password, pulsante di opzione, caselle di riepilogo a selezione singola e selezionare più caselle di controllo. |
| *api.phonefactor* | **Pagina dell'autenticazione a più fattori**. In questa pagina gli utenti possono verificare il proprio numero di telefono (tramite SMS o chiamata vocale) durante la procedura di iscrizione o di accesso. |
| *api.selfasserted* | **Pagina di iscrizione dell'account locale**. Questa pagina contiene un modulo di iscrizione utente hello è toofill in quando iscrizione usando un account da un provider di identità di social networking, ad esempio Facebook o Google +. Questa pagina è simile toohello sopra una pagina di iscrizione social account con l'eccezione hello di campi di immissione di password hello. |
| *api.selfasserted.profileupdate* | **Pagina di aggiornamento del profilo**. Questa pagina contiene un form utente hello consente tooupdate proprio profilo. Questa pagina è simile toohello sopra una pagina di iscrizione social account con l'eccezione hello di campi di immissione di password hello. |
| *api.signuporsignin* | **Pagina unificata per l'iscrizione o l'accesso**.  Questa pagina consente di gestire sia l'iscrizione che l'accesso degli utenti, che possono usare provider di identità aziendali, provider di identità basati su social network come Facebook o Google+ o account locali.

## <a name="next-steps"></a>Passaggi successivi
[Guida di riferimento: Comprendere i criteri personalizzati come funzionano con hello Identity Framework esperienza in B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
