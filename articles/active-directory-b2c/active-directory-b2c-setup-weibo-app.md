---
title: 'Azure Active Directory B2C: configurazione di Weibo | Documentazione Microsoft'
description: Fornire tooconsumers iscrizione e Accedi con account Weibo nelle applicazioni che sono protetti da Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure B2C di Directory Active: Fornire tooconsumers iscrizione e Accedi con account Weibo

> [!NOTE]
> Questa funzionalità è in anteprima. Non usare questo provider di identità nell'ambiente di produzione.
> 

## <a name="create-a-weibo-application"></a>Creare un'applicazione Weibo

toouse Weibo come provider di identità in Azure Active Directory (Azure AD) B2C, è necessario toocreate un'applicazione Weibo e fornirlo con i parametri corretti hello. È necessario un toodo account Weibo questo. Se non si ha un account, è possibile ottenerne uno nel sito [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Registrarsi al programma per sviluppatori di hello Weibo

1. Passare toohello [portale per sviluppatori Weibo](http://open.weibo.com/) e accedere con le credenziali dell'account Weibo.
2. Dopo aver effettuato l'accesso, fare clic sul nome visualizzato nell'angolo superiore destro di hello.
3. Nell'elenco a discesa hello, selezionare**编辑开发者信息**(informazioni per gli sviluppatori di modifica).
4. Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**提交**(Invia).
5. Completamento del processo di verifica tramite posta elettronica hello.
6. Passare toohello [pagina Verifica identità](http://open.weibo.com/developers/identity/edit).
7. Immettere le informazioni necessarie hello nel modulo di hello e fare clic su**提交**(Invia).

### <a name="register-a-weibo-application"></a>Registrare un'applicazione Weibo

1. Passare toohello [nuova pagina di registrazione app Weibo](http://open.weibo.com/apps/new).
2. Immettere le informazioni necessarie applicazione hello.
3. Fare clic su **创建** (Crea).
4. Copiare i valori hello di **chiave App** e **segreto dell'applicazione**. che sarà necessario più avanti.
5. Caricare le foto hello necessarie e immettere le informazioni necessarie hello.
6. Fare clic su **保存以上信息** (Salva).
7. Fare clic su **高级信息** (Informazioni avanzate).
8. Fare clic su**编辑**campo successivo toohello (modifica) per OAuth 2.0**授权设置**(URL di reindirizzamento).
9. Immettere `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` per OAuth 2.0**授权设置** (URL di reindirizzamento). Ad esempio, se il `tenant_name` è contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Fare clic su **提交** (Invia).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Configurare Weibo come provider di identità nel tenant
1. Seguire questi passaggi troppo[passare pannello funzionalità toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) su hello portale di Azure.
2. Nel Pannello di hello B2C funzionalità, fare clic su **provider di identità**.
3. Fare clic su **+ Aggiungi** nella parte superiore di hello del pannello hello.
4. Fornire un nome **nome** per la configurazione del provider di identità hello. ad esempio, immettere "Weibo".
5. Fare clic su **Tipo di provider di identità**, selezionare **Weibo** e fare clic su **OK**.
6. Fare clic su **Configura questo provider di identità**
7. Immettere hello **chiave App** copiato in precedenza come hello **ID Client**.
8. Immettere hello **segreto dell'App** copiato in precedenza come hello **segreto Client**.
9. Fare clic su **OK** e quindi fare clic su **crea** toosave configurazione Weibo.

