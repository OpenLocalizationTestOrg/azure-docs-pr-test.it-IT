---
title: aaaHow toofind un'API specifica necessaria per un'applicazione sviluppata | Documenti Microsoft
description: "Autorizzazioni hello tooconfigure personalizzato non è presente un'API specifica tooaccess sviluppo di applicazioni Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a>Come toofind un'API specifica necessaria per un'applicazione personalizzata

Accesso tooAPIs richiedono la configurazione di ambiti di accesso e i ruoli. Se si desidera tooexpose tooclient applicazioni API web risorsa dell'applicazione, è necessario tooconfigure gli ambiti di accesso e i ruoli per hello API. Se si desidera un tooaccess applicazione client un'API web, è necessario tooconfigure autorizzazioni tooaccess hello API nella registrazione dell'app hello.

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a>Configurazione di una web tooexpose di risorse dell'applicazione API

Quando si espone l'API web, hello API da visualizzare in hello **selezionare un'API** elenco durante l'aggiunta di registrazione dell'app tooan di autorizzazioni. gli ambiti di accesso tooadd, seguire i passaggi di hello illustrati in [aggiunta dell'accesso definisce l'ambito di applicazione della risorsa tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).

## <a name="configuring-a-client-application-tooaccess-web-apis"></a>Configurazione dell'applicazione client tooaccess web API

Quando si aggiunge una registrazione dell'app tooyour autorizzazioni, è possibile **aggiungere l'accesso all'API** tooexposed web API. tooaccess le API web, seguire i passaggi descritti nella procedura hello [aggiungere tooaccess credenziali o le autorizzazioni web API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).

## <a name="next-steps"></a>Passaggi successivi

-   [Integrazione di applicazioni con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [Manifesto dell'applicazione di conoscenza hello Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


