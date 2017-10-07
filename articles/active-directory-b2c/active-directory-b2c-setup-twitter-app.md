---
title: 'Azure Active Directory B2C: configurazione di Twitter | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con Twitter account nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account Twitter

> [!NOTE]
> Questa funzionalità è in anteprima.
> 

## <a name="create-a-twitter-application"></a>Creare un'applicazione Twitter
toouse Twitter come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di Twitter e fornirlo con i parametri corretti hello. Necessaria una toodo account sviluppatore di Twitter. Se non si ha un account, è possibile crearlo sul sito [https://dev.twitter.com/](https://dev.twitter.com/).

1. Passare toohello [sito Web per gli sviluppatori di Twitter](https://dev.twitter.com/) e accedere con le credenziali.
2. Fare clic su **My apps** (App personali) in **Tools & Support** (Strumenti e supporto) e quindi fare clic su **Create New App** (Crea nuova app). 
3. Nel modulo hello, fornire un valore per hello **nome**, **descrizione**, e **sito Web**.
4. Per hello **URL Callback**, immettere `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Verificare che tooreplace **{tenant}** con il nome del tenant (ad esempio, contosob2c.onmicrosoft.com).
5. Controllare hello casella tooagree toohello **contratto per gli sviluppatori** e fare clic su **creare un'applicazione Twitter**.
6. Una volta creato l'applicazione hello, fare clic su **chiavi e i token di accesso**.
7. Copiare il valore di hello di **chiave Consumer** e **segreto del cliente**. Sarà necessario entrambi tooconfigure Twitter come provider di identità nel tenant.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Configurare Twitter come provider di identità nel tenant,
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. ad esempio, immettere "Twitter".
5. Fare clic su **Tipo di provider di identità**, selezionare **Twitter** e fare clic su **OK**.
6. Fare clic su **impostare il provider di identità** e immettere hello Twitter **chiave Consumer** per hello **id Client** e hello Twitter **segreto del cliente**per hello **segreto Client**.
7. Fare clic su **OK**, quindi fare clic su **crea** toosave la configurazione di Twitter.

