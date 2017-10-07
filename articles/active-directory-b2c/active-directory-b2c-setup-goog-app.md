---
title: 'Azure Active Directory B2C: configurazione di Google+ | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Google + account nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account di Google +
## <a name="create-a-google-application"></a>Creazione di un'applicazione Google+
toouse Google + come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Google + e fornirlo con i parametri corretti hello. È necessario questo toodo un account Google +. Se non è disponibile un account, è possibile crearlo nel sito [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Passare toohello [Google Developers Console](https://console.developers.google.com/) e accedere con le credenziali dell'account Google +.
2. Fare clic su **Crea progetto**, immettere un nome in **Nome progetto**e fare clic su **Crea**.
   
    ![Google+ - Introduzione](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google+ - Nuovo progetto](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Fare clic su **API Manager** e quindi fare clic su **credenziali** nel riquadro di spostamento sinistro hello.
4. Fare clic su hello **schermata consenso OAuth** scheda nella parte superiore di hello.
   
    ![Google+ - Credenziali](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Selezionare o specificare un **Indirizzo e-mail** valido, fornire un **Nome prodotto** e fare clic su **Salva**.
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Fare clic su **Nuove credenziali** e scegliere **ID client OAuth**.
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. In **Tipo di applicazione** selezionare **Applicazione Web**.
   
    ![Google+ - Schermata consenso OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Fornire un **nome** per l'applicazione, immettere `https://login.microsoftonline.com` in hello **autorizzato JavaScript origins** , campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URI**campo. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com. Hello **{tenant}** valore è tra maiuscole e minuscole. Fare clic su **Crea**.
   
    ![Google+ - Creare ID client](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Copiare i valori hello di **ID Client** e **segreto Client**. Sarà necessario entrambi tooconfigure Google + come provider di identità nel tenant. **Segreto client** è una credenziale di sicurezza importante.
   
    ![Google+ - Segreto client](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Configurare Google+ come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "G+".
5. Fare clic su **Tipo di provider di identità**, selezionare **Google** e fare clic su **OK**.
6. Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello applicazione Google + creato in precedenza.
7. Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione Google +.

