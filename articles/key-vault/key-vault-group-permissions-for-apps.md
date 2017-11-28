---
title: aaaGrant autorizzazione toomany applicazioni tooaccess un insieme di credenziali chiave di Azure | Documenti Microsoft
description: Informazioni su come toogrant autorizzazione toomany applicazioni tooaccess una chiave dell'insieme di credenziali
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
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="66696-103">Concedere l'autorizzazione toomany applicazioni tooaccess un insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="66696-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="66696-104">D: ho diversi (oltre 16) alle applicazioni che richiedono tooaccess un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="66696-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="66696-105">Poiché Key Vault consente solo 16 voci di controllo di accesso, come è possibile ottenere procedere?</span><span class="sxs-lookup"><span data-stu-id="66696-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="66696-106">I criteri di controllo di accesso a Key Vault supportano solo 16 voci.</span><span class="sxs-lookup"><span data-stu-id="66696-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="66696-107">È tuttavia possibile creare un gruppo di sicurezza di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66696-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="66696-108">Aggiungere tutti hello associata gruppo di sicurezza toothis entità servizio e quindi concesse l'accesso toothis sicurezza gruppo tooKey insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="66696-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="66696-109">Di seguito sono prerequisiti hello:</span><span class="sxs-lookup"><span data-stu-id="66696-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="66696-110">[Installare il modulo di Azure Active Directory V2 per PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="66696-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="66696-111">[Installare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66696-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="66696-112">i comandi seguenti di hello toorun, è necessario che le autorizzazioni toocreate o modifica gruppi nel tenant di Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="66696-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="66696-113">Se non si dispone delle autorizzazioni, potrebbe essere necessario toocontact l'amministratore di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66696-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="66696-114">A questo punto eseguire hello seguenti comandi di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66696-114">Now run hello following commands in PowerShell.</span></span>

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

<span data-ttu-id="66696-115">Se è necessario toogrant un set diverso di gruppo tooa autorizzazioni delle applicazioni, creare un gruppo di sicurezza di Azure Active Directory separato per tali applicazioni.</span><span class="sxs-lookup"><span data-stu-id="66696-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66696-116">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="66696-116">Next steps</span></span>

<span data-ttu-id="66696-117">Per ulteriori informazioni su troppo[proteggere credenziali delle chiavi](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="66696-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
