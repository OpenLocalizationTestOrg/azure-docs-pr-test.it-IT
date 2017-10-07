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
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>La durata del token hello toochange per impostazione predefinita per un'applicazione personalizzata

Azure AD Premium consente agli sviluppatori di app e la durata di hello tooconfigure amministratori tenant di token emesso per i client non riservata. Criteri di durata del token vengono impostati in base a livello di tenant o risorse di hello viene effettuato l'accesso.

 * tooset un criterio di durata del token, è necessario hello toodownload [modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).

 * Eseguire hello **Connetti AzureAD-confermare** comando.

 * Di seguito è riportato un esempio di criterio che imposta i token di aggiornamento di un fattore età max hello. Creare criteri hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Hello estrazione [durata del token configurazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento come toolearn toocreate altri personalizzato.

## <a name="next-steps"></a>Passaggi successivi
[Configurazione della durata del token](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Riferimento al token Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

