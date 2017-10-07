---
title: autenticazione dell'Account Microsoft tooconfigure aaaHow per l'applicazione di servizi App
description: Informazioni su come tooconfigure autenticazione dell'Account Microsoft per l'applicazione di servizi di App.
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Come tooconfigure l'account di accesso Account Microsoft di toouse applicazione di servizio App
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

In questo argomento illustra come tooconfigure Azure App Service toouse Account Microsoft come un provider di autenticazione. 

## <a name="register-microsoft-account"></a>Registrare l'app con l'account Microsoft
1. Accesso toohello [portale di Azure]e passare tooyour applicazione. Copia il **URL**, che in seguito utilizzare tooconfigure app con Account Microsoft.
2. Passare toohello [applicazioni personali] pagina hello Microsoft Account Developer Center e accedere con l'account Microsoft, se necessario.
3. Fare clic su **Aggiungi un'app**, digitare un nome di applicazione e quindi fare clic su **Crea applicazione**.
4. Prendere nota di hello **ID applicazione**, perché sarà necessaria in un secondo momento. 
5. In "Piattaforme" fare clic su **Aggiungi piattaforma** e quindi selezionare "Web".
6. In "Redirect URIs" alimentatore hello endpoint per l'applicazione, quindi fare clic su **salvare**. 
   
   > [!NOTE]
   > L'URI di reindirizzamento URL hello dell'applicazione con il percorso di hello, */.auth/login/microsoftaccount/callback*. ad esempio `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Assicurarsi che si sta utilizzando lo schema HTTPS hello.
   
7. In "Segreti applicazione" fare clic su **Genera nuova password**. Prendere nota del valore di hello che viene visualizzato. Quando si esce hello pagina, non essere visualizzato nuovamente.

    > [!IMPORTANT]
    > password di Hello è un'importante credenziale di sicurezza. Non condividere password hello con nessuno o distribuirlo in un'applicazione client.

## <a name="secrets"></a>Aggiungere Account a Microsoft informazioni tooyour applicazione di servizio App
1. In hello [portale di Azure]passare tooyour applicazione, fare clic su **impostazioni** > **autenticazione / autorizzazione**.
2. Se hello autenticazione / autorizzazione funzionalità non è abilitata, attivarla **su**.
3. Fare clic su **Account Microsoft**. Incollare i valori ID applicazione e la Password hello cui ottenuto in precedenza e facoltativamente abilitare tutti gli ambiti che richiede l'applicazione. Fare quindi clic su **OK**.
   
    ![][1]
   
    Per impostazione predefinita, App servizio fornisce l'autenticazione, ma non limita l'accesso autorizzato tooyour contenuto del sito e le API. È necessario autorizzare gli utenti nel codice dell'app.
4. (Facoltativo) toorestrict tooyour sito tooonly gli utenti di accesso autenticati dall'account Microsoft, impostare **tootake azione quando la richiesta non è autenticata** troppo**Account Microsoft**. Questa operazione richiede che tutte le richieste di essere autenticato e tutte le richieste non autenticate vengono reindirizzate tooMicrosoft account per l'autenticazione.
5. Fare clic su **Salva**.

Si è ora pronto toouse Account Microsoft per l'autenticazione nell'app.

## <a name="related-content"></a>Contenuti correlati
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[applicazioni personali]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portale di Azure]: https://portal.azure.com/
