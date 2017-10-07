---
title: aaaHow toogrant autorizzazioni tooa applicazione personalizzata | Documenti Microsoft
description: Toogrant autorizzazioni tooyour applicazione sviluppata utilizzando hello come portale di Azure AD o un parametro URL
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>Toogrant autorizzazioni tooa personalizzato-sviluppo di applicazioni

Se si desidera toogrant consenso modalità preemptive nella tua app o sono in esecuzione in un errore che non è stato autorizzato tooan app, provare questi passaggi riportata di seguito.

## <a name="how-tooperform-admin-consent-for-your-application"></a>Come tooperform consenso dell'amministratore dell'applicazione

Ha effetto hello di concedere il consenso toohello applicazione per tutti gli utenti dell'organizzazione.

1. Passare toohello **registrazioni di App** pannello come un **amministratore globale**, quindi selezionare app hello.

2. Selezionare **autorizzazioni obbligatorie**e infine fare clic su hello **concedere autorizzazioni** pulsante nella parte superiore di hello del pannello hello.

In alternativa, è possibile costruire una richiesta troppo*login.microsoftonline.com* con le configurazioni di app e Accodamento nel *& Chiedi conferma = admin\_consenso*. Dopo aver effettuato l'accesso con le credenziali di amministratore, hello app è stato concesso il consenso per tutti gli utenti.

## <a name="how-tooforce-user-consent-for-your-application"></a>Come tooforce utente di consenso per l'applicazione

* Aggiungere in richieste di autenticazione *& Chiedi conferma = consenso* che richiede agli utenti finali tooconsent ogni volta che l'autenticazione.

## <a name="next-steps"></a>Passaggi successivi

[L'integrazione di applicazioni e consenso tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes) (Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0)<br>

[Azure AD in Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
