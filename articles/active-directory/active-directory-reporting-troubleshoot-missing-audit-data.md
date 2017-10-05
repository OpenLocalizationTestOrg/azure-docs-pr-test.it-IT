---
title: "Risoluzione dei problemi: dati mancanti nel log attività di Azure Active Directory | Microsoft Docs"
description: Elenca i vari report disponibili per Azure Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="63ce7-103">Non è possibile trovare alcune azioni eseguite nel log attività di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63ce7-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="63ce7-104">Sintomi</span><span class="sxs-lookup"><span data-stu-id="63ce7-104">Symptoms</span></span>

<span data-ttu-id="63ce7-105">Sono state eseguite alcune azioni nel portale di Azure e si prevedeva la visualizzazione dei log di controllo per tali azioni nel pannello `Activity logs > Audit Logs`, ma non è possibile trovarli.</span><span class="sxs-lookup"><span data-stu-id="63ce7-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Creazione di report](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="63ce7-107">Causa</span><span class="sxs-lookup"><span data-stu-id="63ce7-107">Cause</span></span>

<span data-ttu-id="63ce7-108">Le azioni non vengono visualizzate immediatamente nel log di controllo delle attività.</span><span class="sxs-lookup"><span data-stu-id="63ce7-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="63ce7-109">La visualizzazione dei log di controllo nel portale può richiedere tra i 15 minuti e un'ora, a partire dal momento in cui viene eseguita l'azione.</span><span class="sxs-lookup"><span data-stu-id="63ce7-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="63ce7-110">Risoluzione</span><span class="sxs-lookup"><span data-stu-id="63ce7-110">Resolution</span></span>

<span data-ttu-id="63ce7-111">Attendere tra 15 minuti e un'ora e verificare se le azioni vengono visualizzate nel log.</span><span class="sxs-lookup"><span data-stu-id="63ce7-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="63ce7-112">Se non vengono ancora visualizzate, creare un ticket di supporto e il problema verrà esaminato.</span><span class="sxs-lookup"><span data-stu-id="63ce7-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="63ce7-113">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63ce7-113">Next steps</span></span>
<span data-ttu-id="63ce7-114">Vedere [Domande frequenti sulla creazione di report in Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="63ce7-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

