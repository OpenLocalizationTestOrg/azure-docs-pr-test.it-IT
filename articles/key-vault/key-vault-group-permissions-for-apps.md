---
title: Concedere a molte applicazioni l'autorizzazione per accedere ad Azure Key Vault | Documentazione Microsoft
description: Informazioni su come concedere a molte applicazioni l'autorizzazione per accedere a Key Vault
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="682e4-103">Concedere a molte applicazioni l'autorizzazione per accedere a Key Vault</span><span class="sxs-lookup"><span data-stu-id="682e4-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="682e4-104">D: Sono presenti più applicazioni (oltre 16) che devono accedere a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="682e4-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="682e4-105">Poiché Key Vault consente solo 16 voci di controllo di accesso, come è possibile ottenere procedere?</span><span class="sxs-lookup"><span data-stu-id="682e4-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="682e4-106">I criteri di controllo di accesso a Key Vault supportano solo 16 voci.</span><span class="sxs-lookup"><span data-stu-id="682e4-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="682e4-107">È tuttavia possibile creare un gruppo di sicurezza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="682e4-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="682e4-108">Aggiungere tutte le entità servizio associate a questo gruppo di sicurezza e quindi concedere a tale gruppo di accedere a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="682e4-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="682e4-109">Di seguito vengono indicati i prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="682e4-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="682e4-110">[Installare il modulo di Azure Active Directory V2 per PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="682e4-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="682e4-111">[Installare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="682e4-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="682e4-112">Per eseguire questi comandi, sono necessarie le autorizzazioni per creare o modificare gruppi nel tenant di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="682e4-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="682e4-113">Se non si dispone delle autorizzazioni, può essere necessario contattare l'amministratore di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="682e4-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="682e4-114">Eseguire questi comandi in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="682e4-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="682e4-115">Se è necessario concedere un diverso set di autorizzazioni a un gruppo di applicazioni, creare un gruppo di sicurezza di Azure Active Directory separato per tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="682e4-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="682e4-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="682e4-116">Next steps</span></span>

<span data-ttu-id="682e4-117">Altre informazioni su come [proteggere Key Vault](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="682e4-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
