---
title: Report utilizzo aaaUnlicensed | Documenti Microsoft
description: "salve le funzionalità di Azure AD a pagamento consente di che identificare gli utenti senza licenza che usano report di utilizzo senza licenza."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a>Report Utilizzo senza licenza
salve le funzionalità di Azure AD a pagamento consente di che identificare gli utenti senza licenza che usano report di utilizzo senza licenza. In questo modo toomake un migliore utilizzo delle licenze acquistate e tooidentify si conosce quando potrebbe essere necessario ottenere licenze aggiuntive. 

report di Hello Mostra utilizzo attivo di hello le funzionalità a pagamento in hello ultimi 30 giorni. 

## <a name="report-structure"></a>Struttura del report
| Nome colonna | Descrizione |
|:--- |:--- |
| Utente senza licenza |Nome dell'utente hello |
| Funzionalità |nome della funzionalità Hello. Ad esempio: accesso condizionale. |
| Applicazioni a cui è stato eseguito l'accesso |nome di Hello dell'applicazione hello cui si accede con funzionalità hello. Ad esempio: Office 365 SharePoint Online. |

> [!NOTE]
> Se è stato eliminato un account utente hello 'Senza licenza utente' colonna verrà popolata con un ID, ad esempio 1003000090D8B285
> 
> 

## <a name="conditional-access-feature"></a>Funzionalità di accesso condizionale
Gli utenti senza licenza verranno contrassegnati quando accedono a un servizio a cui sono applicati criteri di accesso, se non hanno una licenza di Azure AD Premium. 

Si applica tooMFA / criteri di posizione, nonché dispositivi criteri che utilizzano Intune.

## <a name="see-also"></a>Vedere anche
* [Protezione dell'accesso a Office 365 e ad altre app connesse ad Azure Active Directory](active-directory-conditional-access.md)
* [Guida introduttiva con accesso condizionale tooAzure AD](active-directory-conditional-access-azuread-connected-apps.md) 

