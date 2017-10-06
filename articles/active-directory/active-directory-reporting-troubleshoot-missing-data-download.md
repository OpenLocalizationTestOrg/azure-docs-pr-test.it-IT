---
title: "Risoluzione dei problemi: I dati mancanti in hello scaricato log attività di Azure Active Directory | Documenti Microsoft"
description: "Fornisce dati toomissing una risoluzione log attività di Azure Active Directory scaricato."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Non è possibile trovare tutti i dati nel log attività di Azure Active Directory hello che ho scaricato


## <a name="symptoms"></a>Sintomi

Scaricato log attività di hello (controllo o accessi) e non è possibile visualizzare tutti i record di hello per volta hello che ho scelto. Perché? 

 ![Creazione di report](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Causa

Quando si scarica log di attività nel portale di Azure hello, limitiamo hello scala too120K record, ordinati in base più recente. 

## <a name="resolution"></a>Risoluzione

È possibile sfruttare [API di Reporting AD Azure](active-directory-reporting-api-getting-started.md) toofetch tooa milioni di record in un determinato momento. L'approccio consigliato è toorun uno script in base a una pianificazione che chiama hello reporting API toofetch registra in modo incrementale in un periodo di tempo (ad esempio, giornaliera o settimanale).

## <a name="next-steps"></a>Passaggi successivi
Vedere hello [reporting domande frequenti su Azure Active Directory](active-directory-reporting-faq.md).

