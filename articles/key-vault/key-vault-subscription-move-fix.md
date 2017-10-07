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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Modificare l'ID tenant per un insieme di credenziali delle chiavi dopo lo spostamento di una sottoscrizione
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>D: nel sottoscrizione è stata spostata dal tenant A tootenant B. Come modificare l'ID tenant di hello per l'insieme di credenziali chiave esistente e impostare gli ACL corretti per le entità nel tenant B?
Quando si crea un nuovo insieme di credenziali chiave in una sottoscrizione, è l'ID tenant di Azure Active Directory toohello automaticamente collegato predefinito per la sottoscrizione. Tutte le voci di criteri di accesso sono anche collegati toothis ID del tenant. Quando si sposta la sottoscrizione di Azure dal tenant B, la chiave esistente gli insiemi di credenziali non sono accessibili da un tootenant hello entità (utenti e applicazioni) in toofix tenant B. questo problema, è necessario:

* Modificare l'ID tenant hello associata a tutti gli archivi di chiavi esistenti in questo tootenant sottoscrizione B.
* Rimuovere tutte le voci dei criteri di accesso esistenti.
* Aggiungere nuove voci dei criteri di accesso associate al tenant B.

Ad esempio, se si dispone dell'insieme di credenziali chiave 'myvault' in una sottoscrizione che è stata spostata dal tenant A tootenant B, come hello toochange ID tenant per questo insieme di credenziali chiave e rimuovere i criteri di accesso precedente.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Poiché questo insieme di credenziali è stata nel tenant A prima di spostare hello, hello valore originale di **$vault. Properties.TenantId** è un tenant, mentre **(Get-AzureRmContext). Tenant.TenantId** è tenant B.

Ora che l'insieme di credenziali è associato con l'ID tenant corretto hello e vengono rimosse le voci di criteri di accesso precedenti, impostare l'accesso nuove voci di criteri con [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Passaggi successivi
In caso di domande sull'insieme di credenziali chiave di Azure, visitare hello [forum di insieme di credenziali chiave di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

