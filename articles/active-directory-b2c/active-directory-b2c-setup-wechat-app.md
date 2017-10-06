---
title: 'Azure Active Directory B2C: configurazione di WeChat | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account WeChat nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure B2C di Directory Active: Fornire tooconsumers iscrizione e Accedi con account WeChat

> [!NOTE]
> Questa funzionalità è in anteprima.
> 

## <a name="create-a-wechat-application"></a>Creare un'applicazione WeChat

toouse WeChat come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione WeChat e fornirlo con i parametri corretti hello. È necessario un toodo account WeChat questo. Se non si dispone di un account, è possibile ottenerne uno eseguendo l'iscrizione tramite una delle App per dispositivi mobili o usano il numero QQ. Successivamente, ottenere l'account registrato con programma per sviluppatori di hello WeChat. Altre informazioni sono disponibili [qui](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>Registrare un'applicazione WeChat

1. Andare troppo[https://open.weixin.qq.com/](https://open.weixin.qq.com/) ed effettuare l'accesso.
2. Fare clic su **管理中心** (Centro di gestione).
3. Seguire hello necessarie tooregister una nuova applicazione.
4. Per **授权回调域** (URL di callback) immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Trovare e copiare hello **ID APP** e **chiave APP**. che verranno usati in seguito.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Configurare WeChat come provider di identità nel tenant,
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. ad esempio, immettere "WeChat".
5. Fare clic su **Tipo di provider di identità**, selezionare **WeChat** e fare clic su **OK**.
6. Fare clic su **Configura questo provider di identità**
7. Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.
8. Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.
9. Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione WeChat.

