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
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="39c10-103">Toogrant autorizzazioni tooa personalizzato-sviluppo di applicazioni</span><span class="sxs-lookup"><span data-stu-id="39c10-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="39c10-104">Se si desidera toogrant consenso modalità preemptive nella tua app o sono in esecuzione in un errore che non è stato autorizzato tooan app, provare questi passaggi riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="39c10-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="39c10-105">Come tooperform consenso dell'amministratore dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="39c10-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="39c10-106">Ha effetto hello di concedere il consenso toohello applicazione per tutti gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="39c10-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="39c10-107">Passare toohello **registrazioni di App** pannello come un **amministratore globale**, quindi selezionare app hello.</span><span class="sxs-lookup"><span data-stu-id="39c10-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="39c10-108">Selezionare **autorizzazioni obbligatorie**e infine fare clic su hello **concedere autorizzazioni** pulsante nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="39c10-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="39c10-109">In alternativa, è possibile costruire una richiesta troppo*login.microsoftonline.com* con le configurazioni di app e Accodamento nel *& Chiedi conferma = admin\_consenso*.</span><span class="sxs-lookup"><span data-stu-id="39c10-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="39c10-110">Dopo aver effettuato l'accesso con le credenziali di amministratore, hello app è stato concesso il consenso per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="39c10-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="39c10-111">Come tooforce utente di consenso per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="39c10-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="39c10-112">Aggiungere in richieste di autenticazione *& Chiedi conferma = consenso* che richiede agli utenti finali tooconsent ogni volta che l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="39c10-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39c10-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="39c10-113">Next steps</span></span>

[<span data-ttu-id="39c10-114">L'integrazione di applicazioni e consenso tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="39c10-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

<span data-ttu-id="39c10-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes) (Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0)</span><span class="sxs-lookup"><span data-stu-id="39c10-115">[Consent and Permissioning for AzureAD v2.0 converged Apps](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)</span></span><br>

[<span data-ttu-id="39c10-116">Azure AD in Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="39c10-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
