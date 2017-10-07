---
title: aaaSingle sign-on tooapps con Proxy dell'applicazione Azure AD | Documenti Microsoft
description: Attivare single sign-on per le applicazioni pubblicate on-premise con Proxy dell'applicazione AD Azure nel portale di Azure hello.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Insieme di credenziali delle password per l'accesso Single Sign-On con il proxy dell'applicazione

Il proxy dell'applicazione Azure Active Directory consente di migliorare la produttività pubblicando le applicazioni locali in modo che possano accedervi anche i dipendenti remoti. Nel portale di Azure hello, è possibile impostare single sign-on (SSO) toothese app. Gli utenti devono solo tooauthenticate con Azure AD, e possa accedere all'applicazione enterprise senza toosign in.

Il proxy dell'applicazione supporta numerose [modalità Single Sign-On](application-proxy-sso-overview.md). L'accesso basato su password è progettato per le applicazioni che usano una combinazione di nome utente/password per l'autenticazione. Quando si configura basato su password sign-on per l'applicazione, gli utenti devono toosign in toohello nell'applicazione locale una volta. Successivamente, Azure Active Directory archivia le informazioni di accesso hello e automaticamente fornisce toohello applicazione quando gli utenti accedono in modalità remota. 

Si presuppone che l'utente abbia già pubblicato e testato l'app con il proxy dell'applicazione. In caso contrario, seguire i passaggi di hello in [pubblicare applicazioni mediante il Proxy di applicazione AD Azure](application-proxy-publish-azure-portal.md) e tornare indietro di seguito. 

## <a name="set-up-password-vaulting-for-your-application"></a>Configurare l'insieme di credenziali delle password per l'applicazione

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni**.
3. Dall'elenco a hello, selezionare l'applicazione hello che si desidera tooset backup con SSO.  
4. Selezionare **Single Sign-On**.

   ![Selezionare Single Sign-On](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Per la modalità SSO hello, scegliere **basato su Password Sign-on**.
6. Per hello Sign-on URL, immettere hello pagina hello in cui gli utenti immettono toosign loro nome utente e password in app tooyour all'esterno delle rete aziendale hello. Può trattarsi di un URL esterno che è stato creato quando si pubblica l'applicazione hello mediante il Proxy applicazione hello. 

   ![Scegliere l'accesso basato su password e immettere l'URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Selezionare **Salva**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Test dell'app

Vai a URL tooexternal configurato per l'applicazione tooyour di accesso remoto. Accedere con le credenziali per l'app (o le credenziali di hello per un account di prova configurata con accesso). Dopo l'accesso, deve essere in grado di tooleave hello app e tornare senza dover immettere nuovamente le credenziali. 

## <a name="next-steps"></a>Passaggi successivi

- Informazioni su altri modi tooimplement [Single sign-on con Proxy dell'applicazione](application-proxy-sso-overview.md)
- Informazioni sulle [Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD](application-proxy-security-considerations.md)