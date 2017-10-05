---
title: "Risoluzione dei problemi: dati mancanti nei log attività scaricati di Azure Active Directory | Microsoft Docs"
description: "Offre una soluzione per i dati mancanti nei log attività scaricati di Azure Active Directory."
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
ms.openlocfilehash: 3d56f89035da4d1a0074256b165663f81fc2b01e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-any-data-in-the-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="08ae9-103">Non è possibile trovare dati nei log attività di Azure Active Directory scaricati</span><span class="sxs-lookup"><span data-stu-id="08ae9-103">I can’t find any data in the Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="08ae9-104">Sintomi</span><span class="sxs-lookup"><span data-stu-id="08ae9-104">Symptoms</span></span>

<span data-ttu-id="08ae9-105">I log attività (controllo o accessi) sono stati scaricati ma non vengono visualizzati tutti i record per l'orario scelto.</span><span class="sxs-lookup"><span data-stu-id="08ae9-105">I downloaded the activity logs (audit or sign-ins) and I don’t see all the records for the time I chose.</span></span> <span data-ttu-id="08ae9-106">Perché?</span><span class="sxs-lookup"><span data-stu-id="08ae9-106">Why?</span></span> 

 ![Creazione di report](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="08ae9-108">Causa</span><span class="sxs-lookup"><span data-stu-id="08ae9-108">Cause</span></span>

<span data-ttu-id="08ae9-109">Quando si scaricano i log attività nel portale di Azure, viene applicata una limitazione a 120.000 record, ordinati a partire dal più recente.</span><span class="sxs-lookup"><span data-stu-id="08ae9-109">When you download activity logs in the Azure portal, we limit the scale to 120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="08ae9-110">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="08ae9-110">Resolution</span></span>

<span data-ttu-id="08ae9-111">È possibile sfruttare le [API di Creazione rapporti di Azure AD](active-directory-reporting-api-getting-started.md) per recuperare fino a un milione di record per un momento specifico.</span><span class="sxs-lookup"><span data-stu-id="08ae9-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) to fetch up to a million records at any given point.</span></span> <span data-ttu-id="08ae9-112">L'approccio consigliato consiste nell'eseguire uno script in base a una pianificazione per chiamare le API di Creazione rapporti per recuperare i record in modo incrementale in un periodo di tempo specifico, ad esempio ogni giorno oppure ogni settimana.</span><span class="sxs-lookup"><span data-stu-id="08ae9-112">Our recommended approach is to run a script on a scheduled basis that calls the reporting APIs to fetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ae9-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08ae9-113">Next steps</span></span>
<span data-ttu-id="08ae9-114">Vedere [Domande frequenti sulla creazione di report in Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="08ae9-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

