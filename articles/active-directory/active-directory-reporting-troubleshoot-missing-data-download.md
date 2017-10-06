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
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="f3861-103">Non è possibile trovare tutti i dati nel log attività di Azure Active Directory hello che ho scaricato</span><span class="sxs-lookup"><span data-stu-id="f3861-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="f3861-104">Sintomi</span><span class="sxs-lookup"><span data-stu-id="f3861-104">Symptoms</span></span>

<span data-ttu-id="f3861-105">Scaricato log attività di hello (controllo o accessi) e non è possibile visualizzare tutti i record di hello per volta hello che ho scelto.</span><span class="sxs-lookup"><span data-stu-id="f3861-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="f3861-106">Perché?</span><span class="sxs-lookup"><span data-stu-id="f3861-106">Why?</span></span> 

 ![Creazione di report](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="f3861-108">Causa</span><span class="sxs-lookup"><span data-stu-id="f3861-108">Cause</span></span>

<span data-ttu-id="f3861-109">Quando si scarica log di attività nel portale di Azure hello, limitiamo hello scala too120K record, ordinati in base più recente.</span><span class="sxs-lookup"><span data-stu-id="f3861-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="f3861-110">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="f3861-110">Resolution</span></span>

<span data-ttu-id="f3861-111">È possibile sfruttare [API di Reporting AD Azure](active-directory-reporting-api-getting-started.md) toofetch tooa milioni di record in un determinato momento.</span><span class="sxs-lookup"><span data-stu-id="f3861-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="f3861-112">L'approccio consigliato è toorun uno script in base a una pianificazione che chiama hello reporting API toofetch registra in modo incrementale in un periodo di tempo (ad esempio, giornaliera o settimanale).</span><span class="sxs-lookup"><span data-stu-id="f3861-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3861-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3861-113">Next steps</span></span>
<span data-ttu-id="f3861-114">Vedere hello [reporting domande frequenti su Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="f3861-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

