---
title: aaaChange hello insieme di credenziali chiave ID tenant dopo lo spostamento di una sottoscrizione | Documenti Microsoft
description: "Informazioni su come si spostano i tenant diversi tooa tooswitch hello tenant ID per un insieme di credenziali chiave dopo che è una sottoscrizione"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="151ae-103">Modificare l'ID tenant per un insieme di credenziali delle chiavi dopo lo spostamento di una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="151ae-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="151ae-104">D: nel sottoscrizione è stata spostata dal tenant A tootenant B. Come modificare l'ID tenant di hello per l'insieme di credenziali chiave esistente e impostare gli ACL corretti per le entità nel tenant B?</span><span class="sxs-lookup"><span data-stu-id="151ae-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="151ae-105">Quando si crea un nuovo insieme di credenziali chiave in una sottoscrizione, è l'ID tenant di Azure Active Directory toohello automaticamente collegato predefinito per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="151ae-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="151ae-106">Tutte le voci di criteri di accesso sono anche collegati toothis ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="151ae-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="151ae-107">Quando si sposta la sottoscrizione di Azure dal tenant B, la chiave esistente gli insiemi di credenziali non sono accessibili da un tootenant hello entità (utenti e applicazioni) in toofix tenant B. questo problema, è necessario:</span><span class="sxs-lookup"><span data-stu-id="151ae-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="151ae-108">Modificare l'ID tenant hello associata a tutti gli archivi di chiavi esistenti in questo tootenant sottoscrizione B.</span><span class="sxs-lookup"><span data-stu-id="151ae-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="151ae-109">Rimuovere tutte le voci dei criteri di accesso esistenti.</span><span class="sxs-lookup"><span data-stu-id="151ae-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="151ae-110">Aggiungere nuove voci dei criteri di accesso associate al tenant B.</span><span class="sxs-lookup"><span data-stu-id="151ae-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="151ae-111">Ad esempio, se si dispone dell'insieme di credenziali chiave 'myvault' in una sottoscrizione che è stata spostata dal tenant A tootenant B, come hello toochange ID tenant per questo insieme di credenziali chiave e rimuovere i criteri di accesso precedente.</span><span class="sxs-lookup"><span data-stu-id="151ae-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="151ae-112">Poiché questo insieme di credenziali è stata nel tenant A prima di spostare hello, hello valore originale di **$vault. Properties.TenantId** è un tenant, mentre **(Get-AzureRmContext). Tenant.TenantId** è tenant B.</span><span class="sxs-lookup"><span data-stu-id="151ae-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="151ae-113">Ora che l'insieme di credenziali è associato con l'ID tenant corretto hello e vengono rimosse le voci di criteri di accesso precedenti, impostare l'accesso nuove voci di criteri con [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="151ae-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="151ae-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="151ae-114">Next steps</span></span>
<span data-ttu-id="151ae-115">In caso di domande sull'insieme di credenziali chiave di Azure, visitare hello [forum di insieme di credenziali chiave di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="151ae-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

