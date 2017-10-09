---
title: un'applicazione con endpoint v 2.0 hello Azure AD tramite il portale di hello aaaRegister | Documenti Microsoft
description: "La modalità di servizi utilizzando hello v 2.0 endpoint tooregister un'app con Microsoft per l'attivazione di accesso e l'accesso a Microsoft"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a>Come un'app con endpoint v 2.0 hello tooregister
un'applicazione che accetta sia MSA & Azure AD toobuild sign-in, è prima necessario tooregister un'app con Microsoft.  A questo punto, è non essere in grado di toouse qualsiasi App esistenti con Azure Active Directory o account del servizio gestito, è necessario toocreate una marca di uno nuovo.

> [!NOTE]
> Non tutte le caratteristiche e gli scenari di Azure Active Directory sono supportati dall'endpoint di hello v 2.0.  toodetermine se è necessario utilizzare endpoint v 2.0 hello, conoscenza [limitazioni v 2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a>Visitare il portale di registrazione app Microsoft hello
Innanzitutto, passa troppo[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Il nuovo portale di registrazione delle app consente di gestire le app Microsoft.

Accedere con un account Microsoft personale, aziendale o dell'istituto di istruzione.  Se non si dispone di alcun account, iscriversi per creare un nuovo account personale. La procedura richiederà pochi minuti.

Dopo aver completato l'operazione, è possibile esaminare l'elenco delle app Microsoft, che probabilmente sarà vuoto.  A tale scopo, seguire questa procedura.

Fare clic sul pulsante per **aggiungere un'app**e attribuirle un nome.  portale Hello assegnerà app Id univoco globale dell'applicazione che verrà utilizzato successivamente nel codice.  Se l'applicazione include un componente sul lato server che necessita di token di accesso per chiamare le API (pensare: Office, Azure o API web proprie), è opportuno toocreate un **segreto dell'applicazione** anche qui.

Successivamente, aggiungere hello piattaforme che verrà utilizzati dall'applicazione.

* Per le applicazioni basate sul Web, specificare un **URI di reindirizzamento** dove possono essere inviati messaggi di accesso.
* App per dispositivi mobili, copia verso il valore predefinito di hello reindirizzare l'uri creato automaticamente.

Facoltativamente, è possibile personalizzare hello aspetto della pagina di accesso nel profilo hello.  Verificare che tooclick **salvare** prima di proseguire.

> [!NOTE]
> Quando si crea un'applicazione utilizzando [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), un'applicazione hello verrà registrata nel tenant di home hello di hello che l'account utilizzato toosign portale hello.  Ciò significa che non è possibile registrare un'applicazione nel tenant di Azure AD usando un account Microsoft personale.  Se in modo esplicito desidera tooregister un'applicazione in un particolare tenant, accedere con un account creato in origine in tale tenant.
> 
> 

## <a name="build-a-quick-start-app"></a>Creare un'app di avvio rapido
Dopo aver creato un'app Microsoft, è possibile completare una delle esercitazioni rapide v2.0.  Di seguito sono elencati alcuni suggerimenti:

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

