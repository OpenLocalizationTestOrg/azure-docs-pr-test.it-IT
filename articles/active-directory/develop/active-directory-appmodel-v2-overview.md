---
title: endpoint v 2.0 di Active Directory aaaAzure | Documenti Microsoft
description: Un'app di toobuilding introduzione con sign-in sia Account Microsoft e Azure Active Directory.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Accesso per account Microsoft e utenti di Azure AD nella stessa app
In hello precedenti, uno sviluppatore di app che volevano toosupport entrambi gli account Microsoft personali e gli account di lavoro da Azure Active Directory è stato richiesto toointegrate con due sistemi separati.  Hello **endpoint v 2.0 di Azure AD** introduce una nuova versione di API di autenticazione che consente di toosign in entrambi i tipi di account con una facile integrazione.  Applicazioni che utilizzano endpoint v 2.0 hello possono usare anche le API REST da hello [Microsoft Graph](https://graph.microsoft.io) utilizzando dei tipi di account.

## <a name="getting-started"></a>Introduzione
Scegliere la piattaforma preferita dal seguente elenco toobuild hello un'app usando il nostro librerie open source e Framework.  In alternativa, è possibile utilizzare il protocollo documentazione toosend di OAuth 2.0 e OpenID Connect e ricevere messaggi di protocollo direttamente senza usare una libreria di autenticazione.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Novità
informazioni di Hello qui saranno utili per comprendere cosa è & ciò che è possibile con endpoint v 2.0 hello.

* Informazioni su hello [tipi di App, è possibile compilare con endpoint v 2.0 hello](active-directory-v2-flows.md).
* Comprendere hello [vincoli, restrizioni e limitazioni](active-directory-v2-limitations.md) con endpoint v 2.0 hello.
* Questa panoramica video per l'endpoint di hello v 2.0, consultare:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>riferimento
Questi collegamenti sono utili per l'esplorazione della piattaforma hello in modo approfondito:

* [Riferimento al protocollo v2.0](active-directory-v2-protocols.md)
* [Riferimento al token v2.0](active-directory-v2-tokens.md)
* [Informazioni di riferimento sulla libreria v2.0](active-directory-v2-libraries.md)
* [Gli ambiti e consenso nell'endpoint di hello v 2.0](active-directory-v2-scopes.md)
* [Hello Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Guida e supporto
Si tratta di hello migliore posizioni tooget assistenza per lo sviluppo di Azure Active Directory.

* [Tag `azure-active-directory` e `adal` di Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Commenti e suggerimenti su Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Se è necessario solo toosign gli account di lavoro e dell'istituto di istruzione da Azure Active Directory, è consigliabile iniziare con il nostro [Guida per gli sviluppatori di Azure AD](active-directory-developers-guide.md).  endpoint di Hello v 2.0 deve essere utilizzato dagli sviluppatori che necessitano di toosign negli account personale di Microsoft in modo esplicito.

