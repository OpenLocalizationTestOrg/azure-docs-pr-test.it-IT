---
title: autenticazione di Azure Active Directory tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come tooconfigure l'autenticazione di Azure Active Directory per l'applicazione di servizi di App.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Come tooconfigure l'account di accesso Active Directory di Azure di toouse applicazione di servizio App
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

In questo argomento illustra come tooconfigure toouse di servizi di App di Azure Active Directory di Azure come provider di autenticazione.

## <a name="express"> </a>Configurare Azure Active Directory usando le impostazioni rapide
1. In hello [portale di Azure], passare tooyour applicazione. Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.
2. Se l'autenticazione di hello / non è abilitata la funzionalità di autorizzazione, l'opzione di hello troppo**su**.
3. Fare clic su **Azure Active Directory** e quindi su **Express** in **Modalità di gestione**.
4. Fare clic su **OK** tooregister un'applicazione hello in Azure Active Directory. Verrà creata una nuova registrazione. Se si desidera invece toochoose una registrazione esistente, fare clic su **selezionare un'app esistente** e quindi cercare il nome di hello della registrazione creata in precedenza all'interno del tenant.
   Fare clic su tooselect registrazione hello e fare clic su **OK**. Quindi fare clic su **OK** nel pannello impostazioni di hello Azure Active Directory.
   
   ![][0]
   
   Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
5. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Azure Active Directory, impostare **tootake azione quando la richiesta non è autenticata** troppo**Accedi con Azure Active Directory**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooAzure Active Directory per l'autenticazione.
6. Fare clic su **Salva**.

Si è ora pronto toouse Azure Active Directory per l'autenticazione nell'app.

## <a name="advanced"></a>(Metodo alternativo) Configurare manualmente Azure Active Directory con impostazioni avanzate
È inoltre possibile tooprovide le impostazioni di configurazione manualmente. Questa soluzione di hello preferito è, se si desidera toouse tenant AAD hello è diverso dal tenant hello con cui si accede a Azure. configurazione di hello toocomplete, è innanzitutto necessario creare una registrazione in Azure Active Directory e quindi è necessario fornire alcune hello registrazione dettagli tooApp servizio.

### <a name="register"></a>Registrare l'applicazione con Azure Active Directory
1. Accesso toohello [portale di Azure]e passare tooyour applicazione. Copiare l' **URL**. Si utilizzerà questo tooconfigure l'app di Azure Active Directory.
2. Accedi toohello [portale di Azure classico] e passare troppo**Active Directory**.
   
    ![][2]
3. Selezionare la directory e quindi selezionare hello **applicazioni** scheda nella parte superiore di hello. Fare clic su **aggiungere** in hello inferiore toocreate una nuova registrazione di app.
4. Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
5. In aggiunta guidata applicazione hello, immettere un **nome** per l'applicazione e fare clic su di hello **applicazione Web, e/o API Web** tipo. Fare clic su toocontinue.
6. In hello **URL accesso** incollare l'URL dell'applicazione hello copiato in precedenza. Immettere l'URL stesso in hello **URI ID App** casella. Fare clic su toocontinue.
7. Dopo aver aggiunto un'applicazione hello, fare clic su hello **configura** scheda. Modifica hello **URL di risposta** in **Single Sign-on** toobe hello URL dell'applicazione con il percorso di hello, */.auth/login/aad/callback*. ad esempio `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Assicurarsi che si sta utilizzando lo schema HTTPS hello.
   
    ![][3]
8. Fare clic su **Salva**. Quindi hello copia **ID Client** per app hello. Si configurerà l'applicazione toouse più avanti.
9. Nella barra dei comandi nella parte inferiore di hello, fare clic su **Visualizza endpoint**e quindi copia Ciao **documento metadati federazione** URL e il download del documento o passare tooit in un browser.
10. Nell'ambito radice hello **EntityDescriptor** elemento, dovrebbe esserci un **entityID** attributo del modulo hello `https://sts.windows.net/` seguito da un tenant specifico tooyour GUID (denominato "ID tenant"). Copiare questo valore, che verrà usato come **URL dell'autorità di certificazione**. Si configurerà l'applicazione toouse più avanti.

### <a name="secrets"></a>Applicazione tooyour aggiungere Azure Active Directory
1. In hello [portale di Azure], passare tooyour applicazione. Fare clic su **Impostazioni** e quindi su **Autenticazione/Autorizzazione**.
2. Se non è abilitata la funzionalità di autenticazione/autorizzazione hello, opzione hello troppo**su**.
3. Fare clic su **Azure Active Directory** e quindi su **Avanzata** in **Modalità di gestione**. Incolla in hello ID Client e l'URL dell'autorità di certificazione valore a cui si è ottenuto in precedenza. Fare quindi clic su **OK**.
   
   ![][1]
   
   Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
4. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati da Azure Active Directory, impostare **tootake azione quando la richiesta non è autenticata** troppo**Accedi con Azure Active Directory**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooAzure Active Directory per l'autenticazione.
5. Fare clic su **Salva**.

Si è ora pronto toouse Azure Active Directory per l'autenticazione nell'app.

## <a name="optional-configure-a-native-client-application"></a>(Facoltativo) Configurare un'applicazione client nativa
Azure Active Directory consente inoltre tooregister client nativi, che offre maggiore controllo delle autorizzazioni di mapping. Necessaria se si desidera tooperform account di accesso usando una libreria, ad esempio hello **Active Directory Authentication Library**.

1. Passare troppo**Active Directory** in hello [portale di Azure classico].
2. Selezionare la directory e quindi selezionare hello **applicazioni** scheda nella parte superiore di hello. Fare clic su **aggiungere** in hello inferiore toocreate una nuova registrazione di app.
3. Fare clic su **Aggiungi un'applicazione che l'organizzazione sta sviluppando**.
4. In aggiunta guidata applicazione hello, immettere un **nome** per l'applicazione e fare clic su di hello **applicazione Client nativa** tipo. Fare clic su toocontinue.
5. In hello **URI di reindirizzamento** , immettere il sito */.auth/login/done* endpoint, utilizzando lo schema HTTPS hello. Questo valore dovrebbe essere simile troppo*https://contoso.azurewebsites.net/.auth/login/done*. Se la creazione di un'applicazione Windows, utilizzare invece hello [SID del pacchetto](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) come hello URI.
6. Dopo aver aggiunto un'applicazione nativa hello, fare clic su hello **configura** scheda. Trovare hello **ID Client** e prendere nota di questo valore.
7. Pagina hello di scorrimento verso il basso toohello **autorizzazioni tooother applicazioni** sezione e fare clic su **aggiungere applicazione**.
8. Eseguire la ricerca di un'applicazione web hello registrato in precedenza e scegliere l'icona di addizione hello. Fare clic su finestra di dialogo hello tooclose controllo hello. Se un'applicazione hello web non può essere trovato, passare tooits registrazione e aggiungere un nuovo URL di risposta (ad esempio, hello versione HTTP dell'URL corrente), fare clic su Salva e quindi ripetere questi passaggi: un'applicazione hello deve visualizzati nell'elenco di hello.
9. In hello nuova voce appena aggiunto, aprire hello **autorizzazioni delegate** elenco a discesa e selezionare **accesso (appName)**. Fare quindi clic su **Salva**.

Ora è stata configurata un'applicazione client nativa che può accedere all'applicazione del servizio App.

## <a name="related-content"> </a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[portale di Azure]: https://portal.azure.com/
[portale di Azure classico]: https://manage.windowsazure.com/
[alternative method]:#advanced
