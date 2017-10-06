---
title: 'Azure Active Directory B2C: configurazione di Amazon | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con l'account di Amazon nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account di Amazon
## <a name="create-an-amazon-application"></a>Creare un'applicazione Amazon
toouse Amazon come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di Amazon e fornirlo con i parametri corretti hello. È necessario un toodo account Amazon questo. Se non si ha un account, è possibile crearlo nel sito [http://www.amazon.com/](http://www.amazon.com/).

1. Passare toohello [Centro per sviluppatori Amazon](https://login.amazon.com/) e accedere con le credenziali dell'account Amazon.
2. Se non è già stato fatto, fare clic su **iscrizione**, attenersi alla procedura di registrazione per sviluppatori hello e accettano criteri hello.
3. Fare clic su **Registra nuova applicazione**.
   
    ![Registrazione di una nuova applicazione nel sito Web di Amazon hello](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Fornire informazioni sull'applicazione, come **Name** (Nome), **Description** (Descrizione) e **Privacy Notice URL** (URL informativa sulla privacy) e fare clic su **Save** (Salva).
   
    ![Inserimento delle informazioni sull'applicazione per la registrazione di una nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. In hello **impostazioni Web** sezione valori hello copia di **ID Client** e **segreto Client**. (È necessario hello tooclick **Mostra segreto** pulsante questo toosee.) È necessario che entrambi gli elementi tooconfigure Amazon come provider di identità nel tenant. Fare clic su **modifica** nella parte inferiore di hello della sezione hello. **Client Segreto** è un'importante credenziale di sicurezza.
   
    ![Inserimento dell'ID Client e del Segreto client per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Immettere `https://login.microsoftonline.com` in hello **consentito JavaScript Origins** campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **consentito URL restituiti** campo. Sostituire **{tenant}** con il nome del tenant, ad esempio contoso.onmicrosoft.com. Fare clic su **Salva**. Hello **{tenant}** valore è tra maiuscole e minuscole.
   
    ![Inserimento delle origini JavaScript e degli URL restituiti per la nuova applicazione in Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Configurare Amazon come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "Amzn".
5. Fare clic su **Identity provider type** (Tipo di provider di identità), selezionare **Amazon** e fare clic su **OK**.
6. Fare clic su **impostare il provider di identità** e immettere privata hello client ID e il client di hello applicazione Amazon creato in precedenza.
7. Fare clic su **OK** e quindi fare clic su **crea** toosave la configurazione di Amazon.

