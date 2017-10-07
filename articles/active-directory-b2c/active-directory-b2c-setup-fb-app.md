---
title: 'Azure Active Directory B2C: configurazione di Facebook | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Facebook account nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Facebook
## <a name="create-a-facebook-application"></a>Creare un'applicazione Facebook
toouse Facebook come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Facebook e fornirlo con i parametri corretti hello. Necessaria una toodo account Facebook. Se non si ha un account, è possibile crearlo nel sito [https://www.facebook.com/](https://www.facebook.com/).

1. Passare toohello [Facebook per gli sviluppatori](https://developers.facebook.com/) sito Web e accedere con il Facebook delle credenziali dell'account.
2. Se non è già stato fatto, è necessario tooregister gli sviluppatori Facebook. toodo, fare clic su **registrare** (su hello angolo superiore destro della pagina hello), accettare i criteri di Facebook e completare i passaggi di registrazione hello.
3. Fare clic su **My Apps** (App personali) e quindi su **Add a new App** (Aggiungi una nuova app). 
4. Nel modulo hello, fornire un **nome visualizzato** e valido **Contact Email**.
5. Fare clic su **Crea ID app**. Questo potrebbe richiede i criteri della piattaforma Facebook tooaccept e completare una verifica di protezione in linea.
6. Nella colonna sinistra hello, fare clic su **impostazioni** e quindi selezionare **base** se non è già selezionata.
7. Selezionare una **categoria**. 
8. Fare clic su **+Add Platform** (+Aggiungi piattaforma) e selezionare **Website** (Sito Web).
   
    ![Facebook - Impostazioni](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - Impostazioni - sito Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Immettere `https://login.microsoftonline.com/` in hello **URL del sito** campo e quindi fare clic su **Salva modifiche** nella parte inferiore di hello della pagina hello.
   
    ![Facebook - URL del sito](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Copiare il valore di hello di **ID App**. Fare clic su **Mostra** e copiare il valore di hello di **segreto dell'applicazione**. Sarà necessario entrambi tooconfigure Facebook come provider di identità nel tenant. **App Segreta** è una credenziale di sicurezza importante.
   
    ![Facebook - ID app e segreto app](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Fare clic su **+ Aggiungi prodotto** hello spostamento a sinistra e quindi hello **Set Up** pulsante **account Facebook**.
   
    ![Facebook - Accesso a Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Fare clic su **impostazioni** in esplorazione hello in **account Facebook**

    ![Facebook - Impostazioni Account di accesso di Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **URI di reindirizzamento di OAuth valido** campo hello **impostazioni OAuth Client** sezione. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com. Fare clic su **Salva modifiche** nella parte inferiore di hello della pagina hello.
    
    ![Facebook - URI di reindirizzamento OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake applicazione Facebook utilizzabile da Azure Active Directory B2C, è necessario toomake pubblicamente disponibile. È possibile farlo facendo **revisione di App** nel riquadro di spostamento sinistro hello e attivazione hello passare nella parte superiore di hello della pagina hello troppo**Sì** e facendo clic su **conferma**.
    
    ![Facebook - App pubblica](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Configurare Facebook come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "Facebook".
5. Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Facebook** e scegliere **OK**.
6. Fare clic su **impostare il provider di identità** e immettere hello ID e app segreto dell'applicazione (di hello applicazione Facebook creato in precedenza) in hello **ID Client** e **segreto Client**campi rispettivamente.
7. Fare clic su **OK**, quindi fare clic su **crea** toosave la configurazione di Facebook.

> [!NOTE]
> Aggiunta di un **provider di identità** tooyour tenant non modifica i criteri esistenti. Tenere presente tooupdate i criteri includendo i provider di identità hello che appena creato.
>