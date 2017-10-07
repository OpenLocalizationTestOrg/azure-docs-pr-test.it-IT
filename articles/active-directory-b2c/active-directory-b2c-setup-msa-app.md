---
title: 'Azure Active Directory B2C: Configurazione dell''account Microsoft | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di Microsoft nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Microsoft
## <a name="create-a-microsoft-account-application"></a>Creare un'applicazione di account Microsoft
toouse Microsoft account come un provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di account Microsoft e fornirlo con i parametri corretti hello. Necessaria una toodo account Microsoft. Se non si ha un account, è possibile crearlo nel sito [https://www.live.com/](https://www.live.com/).

1. Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) e accedere con le credenziali dell'account Microsoft.
2. Fare clic su **Aggiungi un'app**.
   
    ![Account Microsoft - Aggiungere una nuova app](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Specificare un **Nome** per l'applicazione e fare clic su **Crea applicazione**.
   
    ![Account Microsoft - Nome applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Copiare il valore di hello di **Id applicazione**. Sarà necessario tooconfigure account Microsoft come provider di identità nel tenant.
   
    ![Account Microsoft - ID applicazione](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Fare clic su **Aggiungi piattaforma** e scegliere **Web**.
   
    ![Account Microsoft - Aggiungi piattaforma](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Account Microsoft - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** campo. Sostituire **{tenant}** con il nome del tenant, ad esempio contosob2c.onmicrosoft.com.
   
    ![Account Microsoft - URL di reindirizzamento](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Fare clic su **generare una nuova Password** in hello **applicazione segreti** sezione. Copia hello nuova password visualizzata sullo schermo. Sarà necessario tooconfigure account Microsoft come provider di identità nel tenant. La password è una credenziale di sicurezza importante.
   
    ![Account Microsoft - Genera nuova password](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Account Microsoft - Nuova password](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Casella di controllo hello indicante **il supporto di Live SDK** in hello **opzioni avanzate** sezione. Fare clic su **Salva**.
   
    ![Account Microsoft - Supporto Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Configurare un account Microsoft come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "MSA".
5. Fare clic su **Tipo di provider di identità**, selezionare **Account Microsoft** e fare clic su **OK**.
6. Fare clic su **impostare il provider di identità** e immettere l'Id applicazione hello e la password di hello applicazione Microsoft account creato in precedenza.
7. Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione dell'account di Microsoft.

