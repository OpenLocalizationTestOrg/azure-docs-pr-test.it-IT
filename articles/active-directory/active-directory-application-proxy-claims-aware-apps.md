---
title: applicazioni che supportano aaaClaims - Proxy App di Azure AD | Documenti Microsoft
description: Come toopublish locale le applicazioni ASP.NET che accetta le attestazioni ADFS per l'accesso remoto sicuro dagli utenti.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Uso di app in grado di riconoscere attestazioni nel proxy di applicazione
[Grado di riconoscere attestazioni app](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) eseguire toohello un reindirizzamento la servizio Token di sicurezza (STS). servizio token di sicurezza di Hello richiede le credenziali utente hello in cambio un token e quindi reindirizza un'applicazione hello utente toohello. Esistono alcuni modi tooenable Proxy dell'applicazione toowork con questi reindirizzamenti. Utilizzare la distribuzione di tooconfigure questo articolo per le applicazioni in grado di riconoscere attestazioni. 

## <a name="prerequisites"></a>Prerequisiti
Verificare che tale hello servizio token di sicurezza che hello app grado di riconoscere attestazioni reindirizza toois disponibile di fuori della rete locale. Si può rendere hello servizio token di sicurezza disponibili esporlo tramite un proxy o consentendo di fuori di connessioni. 

## <a name="publish-your-application"></a>Pubblicare l'applicazione

1. Pubblicare l'applicazione in base a istruzioni toohello [pubblicare applicazioni con Proxy dell'applicazione](application-proxy-publish-azure-portal.md).
2. Passare toohello pagina applicazione hello portale e seleziona **Single sign-on**.
3. Se si sceglie **Azure Active Directory** come **Metodo di autenticazione preliminare**, selezionare **Single Sign-On di Azure AD disabilitato** come **Metodo di autenticazione interna**. Se si sceglie **pass-through** come il **metodo di preautenticazione**, non è necessario toochange nulla.

## <a name="configure-adfs"></a>Configurare AD FS

È possibile configurare AD FS per le app in grado di riconoscere attestazioni in due modi diversi. Hello per primo è l'utilizzo dei domini personalizzati. in secondo luogo, Hello è con WS-Federation. 

### <a name="option-1-custom-domains"></a>Opzione 1: domini personalizzati

Se tutti hello URL interni per le applicazioni sono complete (FQDN) dei nomi di dominio, quindi è possibile configurare [domini personalizzati](active-directory-application-proxy-custom-domains.md) per le applicazioni. Utilizzare hello domini personalizzati toocreate URL esterni che sono hello stesso hello URL interno. Quando l'URL esterni corrispondono gli URL interni, reindirizzamenti STS hello funzionano se gli utenti siano in locale o remoto. 

### <a name="option-2-ws-federation"></a>Opzione 2: WS-Federation

1. Aprire la console di gestione di AD FS.
2. Andare troppo**Relying Party Trusts**, fare clic su hello app pubblicate con Proxy dell'applicazione e scegliere **proprietà**.  

   ![Schermata: clic con il pulsante destro del mouse sul nome dell'app in Attendibilità componente](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. In hello **endpoint** scheda **tipo di Endpoint**selezionare **WS-Federation**.
4. In **attendibili URL**, immettere l'URL hello immesso in hello Proxy dell'applicazione in **URL esterno** e fare clic su **OK**.  

   ![Schermata: aggiunta di un endpoint e impostazione del valore per URL attendibile](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Passaggi successivi
* [Abilitare Single Sign-On](application-proxy-sso-overview.md) per le applicazioni che non sono in grado di riconoscere attestazioni
* [Abilitare toointeract di App client nativa con applicazioni di proxy](active-directory-application-proxy-native-client.md)


