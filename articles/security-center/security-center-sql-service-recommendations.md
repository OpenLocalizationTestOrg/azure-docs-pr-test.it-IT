---
title: SQL Azure aaaProtecting servizio e i dati in Centro sicurezza di Azure | Documenti Microsoft
description: "Questo documento illustra le raccomandazioni presenti nel Centro sicurezza di Azure che facilitano la protezione dei dati e del servizio SQL di Azure e garantiscano la conformità ai criteri di sicurezza."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="bfe2e-103">Protezione del servizio SQL di Azure e dei dati nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe2e-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="bfe2e-104">Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="bfe2e-105">Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene creato indicazioni che consentono di eseguire il processo di hello di configurazione dei controlli di hello necessita.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="bfe2e-106">Consigli si applicano a tipi di risorse tooAzure: macchine virtuali (VM), rete, SQL e i dati e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="bfe2e-107">Questo articolo illustra indicazioni che si applicano i dati e il servizio SQL tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="bfe2e-108">e relative all'abilitazione del controllo per i database SQL Azure e della crittografia per i database SQL e dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="bfe2e-109">Tabella di hello utilizzare riportata di seguito come un riferimento di toohelp comprendere hello disponibili SQL servizio e dati indicazioni e la funzione ognuno se lo si applica.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="bfe2e-110">Raccomandazioni disponibili per il servizio SQL e i dati</span><span class="sxs-lookup"><span data-stu-id="bfe2e-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="bfe2e-111">Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="bfe2e-111">Recommendation</span></span> | <span data-ttu-id="bfe2e-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bfe2e-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="bfe2e-113">Abilitare il controllo e il rilevamento delle minacce nei server SQL</span><span class="sxs-lookup"><span data-stu-id="bfe2e-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="bfe2e-114">Consiglia di attivare il controllo e il rilevamento delle minacce per i server di Azure SQL (solo il servizio Azure SQL, non è incluso SQL in esecuzione nelle macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="bfe2e-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="bfe2e-115">Abilitare il controllo e il rilevamento delle minacce nei database SQL</span><span class="sxs-lookup"><span data-stu-id="bfe2e-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="bfe2e-116">Consiglia di attivare il controllo e il rilevamento delle minacce per i database SQL di Azure (solo il servizio Azure SQL, non è incluso SQL in esecuzione nelle macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="bfe2e-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="bfe2e-117">Abilitare Transparent Data Encryption sui database SQL</span><span class="sxs-lookup"><span data-stu-id="bfe2e-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="bfe2e-118">Consiglia di abilitare la crittografia per i database SQL (solo il servizio di SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="bfe2e-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="bfe2e-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bfe2e-119">See also</span></span>
<span data-ttu-id="bfe2e-120">toolearn ulteriori informazioni sui suggerimenti che si applicano tooother tipi di risorse di Azure, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="bfe2e-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="bfe2e-121">Protezione delle macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe2e-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="bfe2e-122">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="bfe2e-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="bfe2e-123">Protezione della rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="bfe2e-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="bfe2e-124">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="bfe2e-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="bfe2e-125">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bfe2e-126">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="bfe2e-127">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="bfe2e-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
