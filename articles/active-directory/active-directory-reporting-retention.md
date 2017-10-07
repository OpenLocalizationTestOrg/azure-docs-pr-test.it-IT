---
title: criteri di conservazione dei report di Active Directory aaaAzure | Documenti Microsoft
description: Criteri di conservazione dei dati di report in Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Criteri di conservazione dei report di Azure Active Directory


In questo argomento fornisce le risposte alle domande più comuni di toohello in combinazione con la conservazione dei dati hello per i report di attività differenti hello in Azure Active Directory. 

**D: come è possibile ottenere la raccolta hello dei dati di attività avviati.**

**R:**

| Edizione di Azure AD | Avvio della raccolta |
| :--              | :--   |
| Azure AD P1 Premium <br /> Azure AD P2 Premium | Quando ci si iscrive a una sottoscrizione |
| Azure AD Free | Hello prima apertura di hello [Pannello di Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) o utilizzare hello [reporting API](https://aka.ms/aadreports)  |

---
**D: quando i dati di attività è disponibile nel portale di Azure hello?**

**R:**

- **Immediatamente** : se sta già utilizzando i report nel portale di Azure classico hello
- **Entro 2 ore** : se è stato attivato reporting in hello portale di Azure classico

---
**D: come è possibile ottenere la raccolta hello dei segnali di sicurezza avviata.**  

**R:** per i segnali di sicurezza, viene avviato il processo di raccolta hello quando acconsentire esplicitamente toouse hello Identity Protection Center. 


---
**D: per quanto tempo è hello archiviati i dati raccolti?**

**R:**

**Report attività**    

| Report                 | Azure AD Free | Azure AD P1 Premium | Azure AD P2 Premium |
| :--                    | :--           | :--                 | :--                 |
| Directory Audit (Controllo directory)        | 7 giorni        | 30 giorni             | 30 giorni             |
| Attività di accesso       | 7 giorni        | 30 giorni             | 30 giorni             |

**Segnali di sicurezza**

| Report         | Azure AD Free | Azure AD P1 Premium | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| Utenti a rischio.  | 7 giorni        | 30 giorni             | 90 giorni             |
| Accessi a rischio | 7 giorni        | 30 giorni             | 90 giorni             |

---