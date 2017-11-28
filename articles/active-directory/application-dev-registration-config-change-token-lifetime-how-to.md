---
title: durata del token aaaHow toochange hello predefinite per un'applicazione sviluppata | Documenti Microsoft
description: Come criteri di durata del Token tooupdate per l'applicazione che si sta sviluppando su Azure AD
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="71832-103">La durata del token hello toochange per impostazione predefinita per un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="71832-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="71832-104">Azure AD Premium consente agli sviluppatori di app e la durata di hello tooconfigure amministratori tenant di token emesso per i client non riservata.</span><span class="sxs-lookup"><span data-stu-id="71832-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="71832-105">Criteri di durata del token vengono impostati in base a livello di tenant o risorse di hello viene effettuato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="71832-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="71832-106">tooset un criterio di durata del token, è necessario hello toodownload [modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="71832-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="71832-107">Eseguire hello **Connetti AzureAD-confermare** comando.</span><span class="sxs-lookup"><span data-stu-id="71832-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="71832-108">Di seguito è riportato un esempio di criterio che imposta i token di aggiornamento di un fattore età max hello.</span><span class="sxs-lookup"><span data-stu-id="71832-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="71832-109">Creare criteri hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="71832-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="71832-110">Hello estrazione [durata del token configurazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento come toolearn toocreate altri personalizzato.</span><span class="sxs-lookup"><span data-stu-id="71832-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71832-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71832-111">Next steps</span></span>
[<span data-ttu-id="71832-112">Configurazione della durata del token</span><span class="sxs-lookup"><span data-stu-id="71832-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="71832-113">Riferimento al token Azure AD</span><span class="sxs-lookup"><span data-stu-id="71832-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

