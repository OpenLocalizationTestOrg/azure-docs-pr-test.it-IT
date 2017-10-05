---
title: Come modificare le impostazioni predefinite per la durata del token per un'applicazione personalizzata | Microsoft Docs
description: Informazioni su come aggiornare i criteri di durata del token per l'applicazione che si sta sviluppando in Azure AD
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
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="6f3dc-103">Come modificare le impostazioni predefinite per la durata del token per un'applicazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="6f3dc-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="6f3dc-104">Azure AD Premium consente agli sviluppatori di app e agli amministratori di tenant di configurare la durata dei token emessi per i client non riservati.</span><span class="sxs-lookup"><span data-stu-id="6f3dc-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="6f3dc-105">I criteri di durata dei token vengono impostati a livello di tenant o per le risorse a cui si accede.</span><span class="sxs-lookup"><span data-stu-id="6f3dc-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="6f3dc-106">Per impostare i criteri di durata del token, è necessario scaricare il [modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="6f3dc-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="6f3dc-107">Eseguire il comando **Connect-AzureAD -Confirm**.</span><span class="sxs-lookup"><span data-stu-id="6f3dc-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="6f3dc-108">Un esempio di criteri che impostano il token di aggiornamento di un singolo fattore di età massima è riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6f3dc-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="6f3dc-109">Creare i criteri: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="6f3dc-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="6f3dc-110">Vedere il documento [Configurazione della durata del token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) per scoprire come crearne altri personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6f3dc-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f3dc-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6f3dc-111">Next steps</span></span>
[<span data-ttu-id="6f3dc-112">Configurazione della durata del token</span><span class="sxs-lookup"><span data-stu-id="6f3dc-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="6f3dc-113">Riferimento al token Azure AD</span><span class="sxs-lookup"><span data-stu-id="6f3dc-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

