---
title: Come concedere autorizzazioni a un'applicazione personalizzata | Microsoft Docs
description: Come concedere autorizzazioni all'applicazione personalizzata tramite il portale di Azure AD o un parametro URL
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
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="15cdd-103">Come concedere autorizzazioni a un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="15cdd-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="15cdd-104">Se si vuole concedere in modo preventivo il consenso per l'app in uso o si verifica un errore che indica che non è stato fornito il consenso a un'app, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="15cdd-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="15cdd-105">Come fornire il consenso dell'amministratore per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="15cdd-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="15cdd-106">Questa operazione consente di fornire all'applicazione il consenso per tutti gli utenti dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="15cdd-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="15cdd-107">Passare al pannello **Registrazioni per l'app** in qualità di **amministratore globale** e quindi selezionare l'app.</span><span class="sxs-lookup"><span data-stu-id="15cdd-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="15cdd-108">Selezionare **Autorizzazioni necessarie** e infine scegliere il pulsante **Concedi autorizzazioni** nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="15cdd-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="15cdd-109">È possibile, in alternativa, creare una richiesta in *login.microsoftonline.com* con le configurazioni dell'app e aggiungerla in *&prompt=admin\_consent*.</span><span class="sxs-lookup"><span data-stu-id="15cdd-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="15cdd-110">Dopo avere eseguito l'accesso con le credenziali di amministratore, all'app viene concesso il consenso per tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="15cdd-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="15cdd-111">Come forzare il consenso dell'utente per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="15cdd-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="15cdd-112">Eseguire l'aggiunta alle richieste di autenticazione *&prompt=consent* che richiedono il consenso degli utenti finali a ogni autenticazione.</span><span class="sxs-lookup"><span data-stu-id="15cdd-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15cdd-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15cdd-113">Next steps</span></span>

[<span data-ttu-id="15cdd-114">Consenso e integrazione di applicazioni con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15cdd-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="15cdd-115">Consenso e concessione delle autorizzazioni per le app con convergenza di Azure Active Directory v2.0</span><span class="sxs-lookup"><span data-stu-id="15cdd-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="15cdd-116">Azure AD in Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="15cdd-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
