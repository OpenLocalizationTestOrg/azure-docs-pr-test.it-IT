---
title: le latenze reporting di Active Directory aaaAzure | Documenti Microsoft
description: "Informazioni sulle quantità hello di tempo impiegato per la segnalazione di eventi tooshow backup nel portale di Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a>Latenze dei report di Azure Active Directory

Con [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, si ottengono tutte le informazioni di hello è necessario toodetermine, svolgimento dell'ambiente. quantità di Hello di tempo impiegato per la segnalazione dei dati tooshow backup nel portale di Azure hello è noto anche come latenza. 

Questo argomento elenca le informazioni sulla latenza hello per hello tutte le categorie di report nel portale di Azure hello. 


## <a name="activity-reports"></a>Report sull’attività

Esistono due aree di reporting sulle attività:

- **Le attività di accesso** – informazioni sull'utilizzo di hello di applicazioni gestite e le attività di accesso dell'utente
- **Log di controllo** : informazioni relative alle attività di sistema sulla gestione di utenti e gruppi, sulle applicazioni gestite e sulle attività di directory

Hello nella tabella seguente elenca le informazioni sulla latenza hello per i report di attività.

| Report | Minima | Media | Massima |
| :-- | --- | --- | --- |
| Log di controllo             | 30 minuti  | 45 minuti | 1 ora     |
| Accessi               | 15 minuti  | 15 minuti | 2 ore*   |

>[!NOTE]
> Per alcuni dati di attività accessi provenienti da applicazioni di office legacy, può richiedere ore too8 hello reporting dati tooshow backup. 


## <a name="security-reports"></a>Report sulla sicurezza

Esistono due aree di reporting sulla sicurezza:

- **Accessi rischiosi** -un rischiosa l'accesso è un indicatore per un tentativo di accesso che siano stato eseguito da un utente che non è proprietario di legittimo hello di un account utente. 
- **Utenti contrassegnati per il rischio**. Un utente rischioso è indicativo di un account utente che potrebbe essere stato compromesso. 

Hello nella tabella seguente elenca le informazioni sulla latenza hello per i report di sicurezza.

| Report | Minima | Media | Massima |
| :-- | --- | --- | --- |
| Utenti a rischio.          | 5 minuti   | 15 minuti  | 2 ore  |
| Accessi a rischio         | 5 minuti   | 15 minuti  | 2 ore  |

## <a name="risk-events"></a>Eventi di rischio

Azure Active Directory Usa adattivo di machine learning algoritmi euristica toodetect sospette azioni e che sono account utente tooyour correlati. Ogni azione sospetta rilevata viene archiviata in un record denominato evento di rischio.

Hello nella tabella seguente elenca le informazioni di latenza hello per gli eventi di rischio.

| Report | Minima | Media | Massima |
| :-- | --- | --- | --- |
| Accessi da indirizzi IP anonimi |5 minuti |15 minuti |2 ore |
| Accessi da posizioni non note |5 minuti |15 minuti |2 ore |
| Utenti con credenziali perse |2 ore |4 ore |8 ore |
| Comunicazione Impossibile tooatypical percorsi |5 minuti |1 ora |8 ore  |
| Accessi da dispositivi infetti |2 ore |4 ore |8 ore  |
| Accessi da indirizzi IP con attività sospette |2 ore |4 ore |8 ore  |



## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooknow ulteriori informazioni sui report di attività hello in hello portale di Azure, vedere:

- [Report attività di accesso nel portale di Azure Active Directory hello](active-directory-reporting-activity-sign-ins.md)
- [Report attività nel portale di Azure Active Directory hello di controllo](active-directory-reporting-activity-audit-logs.md)

Se si desidera tooknow ulteriori informazioni sui report di sicurezza hello in hello portale di Azure, vedere:

- [Utenti dei report di rischio per la sicurezza nel portale di Azure Active Directory hello](active-directory-reporting-security-user-at-risk.md)
- [Report accessi rischiosa nel portale di Azure Active Directory hello](active-directory-reporting-security-risky-sign-ins.md)

Se si desidera tooknow ulteriori sugli eventi di rischio, vedere [gli eventi di rischio di Azure Active Directory](active-directory-reporting-risk-events.md).
