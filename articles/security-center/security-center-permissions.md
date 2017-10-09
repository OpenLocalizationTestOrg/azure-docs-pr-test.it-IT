---
title: aaaPermissions nel Centro protezione di Azure | Documenti Microsoft
description: In questo articolo illustra come Centro sicurezza di Azure viene usato toousers autorizzazioni tooassign controllo di accesso basato sui ruoli e identifica le azioni per ogni ruolo consentita hello.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Autorizzazioni nel Centro sicurezza di Azure

Centro sicurezza di Azure Usa [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md), che fornisce [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) che può essere assegnato toousers, gruppi e i servizi in Azure.

Centro sicurezza PC valuta configurazione hello di problemi di sicurezza di risorse tooidentify e vulnerabilità. Centro sicurezza PC, visualizzare solo le informazioni correlate tooa risorse quando l'utente viene assegnato hello ruolo di proprietario, collaboratore o lettore per il gruppo hello sottoscrizione o la risorsa a cui appartiene una risorsa.

Nei ruoli toothese aggiunta, sono disponibili due ruoli specifici del Centro sicurezza:

* **Lettore di sicurezza**: un utente appartenente al ruolo toothis dispone di diritti tooSecurity centro di visualizzazione. utente Hello può visualizzare consigli, avvisi, un criterio di sicurezza e gli stati di sicurezza, ma non è possibile apportare modifiche.
* **Amministratore della sicurezza**: un utente appartenente al ruolo toothis hello stessi diritti come lettore sicurezza hello e può anche aggiornare criteri di sicurezza hello e chiudere gli avvisi e i consigli.

> [!NOTE]
> ruoli di sicurezza Hello, lettore di sicurezza e l'amministratore della sicurezza, hanno accesso solo in Centro sicurezza PC. ruoli di sicurezza Hello non dispone di accesso tooother servizio aree di Azure, ad esempio l'archiviazione, Web e dispositivi mobili o Internet delle cose.
>
>

## <a name="roles-and-allowed-actions"></a>Ruoli e azioni consentite

Hello nella tabella seguente vengono visualizzati i ruoli e le azioni consentite in Centro sicurezza PC. Una X indica che l'azione hello è consentita per tale ruolo.

| Ruolo | Modificare i criteri di sicurezza | Applicare i suggerimenti per la sicurezza per una risorsa | Ignorare gli avvisi e le raccomandazioni | Visualizzare gli avvisi e le raccomandazioni |
|:--- |:---:|:---:|:---:|:---:|
| Proprietario della sottoscrizione | X | X | X | X |
| Collaboratore alla sottoscrizione | X | X | X | X |
| Proprietario del gruppo di risorse | -- | X | -- | X |
| Collaboratore del gruppo di risorse | -- | X | -- | X |
| Lettore | -- | -- | -- | X |
| Amministratore della sicurezza | X | -- | X | X |
| Ruolo con autorizzazioni di lettura per la sicurezza | -- | -- | -- | X |

> [!NOTE]
> È consigliabile assegnare hello restrittivo ruolo necessari per utenti toocomplete le proprie attività. Ad esempio, assegnare hello lettore ruolo toousers che sufficiente tooview informazioni sullo stato di sicurezza hello di una risorsa ma non eseguire l'azione, ad esempio l'applicazione delle indicazioni o la modifica di criteri.
>
>

## <a name="next-steps"></a>Passaggi successivi
Questo articolo è illustrato l'utilizzo di Centro sicurezza PC RBAC tooassign autorizzazioni toousers e identificato hello azioni per ogni ruolo è consentito. Ora che si ha familiarità con le assegnazioni di ruolo hello necessari toomonitor hello lo stato di sicurezza della sottoscrizione, modificare i criteri di sicurezza e applica indicazioni, informazioni su come:

- [Impostare criteri di sicurezza in Centro sicurezza](security-center-policies.md)
- [Gestire i suggerimenti per la sicurezza in Centro sicurezza](security-center-recommendations.md)
- [Monitorare l'integrità della protezione hello delle risorse di Azure](security-center-monitoring.md)
- [Gestire e rispondere toosecurity avvisi del Centro sicurezza PC](security-center-managing-and-responding-alerts.md)
- [Monitorare le soluzioni di sicurezza dei partner](security-center-partner-solutions.md)
