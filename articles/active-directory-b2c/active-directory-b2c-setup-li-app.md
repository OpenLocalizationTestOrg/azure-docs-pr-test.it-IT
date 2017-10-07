---
title: 'Azure Active Directory B2C: Configurazione di LinkedIn | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di LinkedIn nelle applicazioni che sono protetti da Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con gli account di LinkedIn
## <a name="create-a-linkedin-application"></a>Creare un'applicazione su LinkedIn
toouse LinkedIn come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di LinkedIn e fornirlo con i parametri corretti hello. Necessaria una toodo account LinkedIn. Se non si ha un account, è possibile crearlo nel sito [https://www.linkedin.com/](https://www.linkedin.com/).

1. Passare toohello [sito Web gli sviluppatori di LinkedIn](https://www.developer.linkedin.com/) e accedere con le credenziali dell'account LinkedIn.
2. Fare clic su **My Apps** in hello barra dei menu superiore e quindi fare clic su **Crea applicazione**.
   
    ![LinkedIn - Nuova app](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. In hello **creare una nuova applicazione** modulo, inserire le informazioni pertinenti hello (**nome società**, **nome**, **descrizione**, **URL del Logo dell'applicazione**, **l'utilizzo dell'applicazione**, **URL del sito Web**, **posta elettronica aziendali** e **telefono ufficio**).
4. Accettare toohello **condizioni di utilizzo dell'API di LinkedIn** e fare clic su **Invia**.
   
    ![LinkedIn - Registro app](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Copiare i valori hello di **ID Client** e **segreto Client**. che si trovano nella sezione **Authentication Keys** (Chiavi di autenticazione). Sarà necessario entrambi tooconfigure LinkedIn come provider di identità nel tenant.
   
   > [!NOTE]
   > **Client Segreto** è un'importante credenziale di sicurezza.
   > 
   > 
6. Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **autorizzato URL di reindirizzamento** campo (in **OAuth 2.0**). Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com. Fare clic su **Add** (Aggiungi) e quindi su **Update** (Aggiorna). Hello **{tenant}** valore è tra maiuscole e minuscole.
   
    ![LinkedIn - Installazione app](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Configurare LinkedIn come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "LI".
5. Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **LinkedIn** e fare clic su **OK**.
6. Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello LinkedIn applicazione creata in precedenza.
7. Fare clic su **OK** e quindi fare clic su **crea** toosave la configurazione di LinkedIn.

