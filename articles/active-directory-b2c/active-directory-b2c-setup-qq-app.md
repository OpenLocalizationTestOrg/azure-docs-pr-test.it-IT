---
title: 'Azure Active Directory B2C: configurazione di QQ | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account q nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active B2C di Directory: Fornire tooconsumers iscrizione e Accedi con account q

> [!NOTE]
> Questa funzionalità è in anteprima.
> 

## <a name="create-a-qq-application"></a>Creare un'applicazione QQ

toouse q come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione di q e fornirlo con i parametri corretti hello. Necessaria una toodo account q. Se non si ha un account, è possibile ottenerne uno nel sito [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Registrarsi al programma per sviluppatori di hello q

1. Passare toohello [portale per sviluppatori q](http://open.qq.com) e accedere con le credenziali dell'account q.
2. Dopo avere effettuato l'accesso, andare troppo[http://open.qq.com/reg](http://open.qq.com/reg) tooregister manualmente gli sviluppatori.
3. Selezionare menu hello**个人**(developer singoli).
4. Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**下一步**(passaggio successivo).
5. Completamento del processo di verifica tramite posta elettronica hello.

> [!NOTE]
> È necessario toowait alcuni toobe giorni approvato dopo la registrazione come uno sviluppatore. 

### <a name="register-a-qq-application"></a>Registrare un'applicazione QQ

1. Andare troppo[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Fare clic su **应用管理** (Gestione app).
3. Fare clic su **创建应用** (Crea app).
4. Immettere le informazioni necessarie app hello.
5. Fare clic su **创建应用** (Crea app).
6. Immettere le informazioni necessarie hello.
7. Per hello**授权回调域**(URL callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Fare clic su **创建应用** (Crea app).
9. Nella pagina di conferma hello, fare clic su**应用管理**pagina di gestione app toohello tooreturn (gestione delle app).
10. Fare clic su**查看**(visualizzazione) prossima toohello applicazione appena creato.
11. Fare clic su **修改** (Modifica).
12. Dall'alto hello della pagina hello, copiare hello **ID APP** e **chiave APP**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Configurare QQ come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. Ad esempio, immettere "QQ".
5. Fare clic su **Tipo di provider di identità**, selezionare **QQ** e fare clic su **OK**.
6. Fare clic su **Configura questo provider di identità**
7. Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.
8. Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.
9. Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione q.

