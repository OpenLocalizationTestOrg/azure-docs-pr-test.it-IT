---
title: Protezione del servizio SQL di Azure e dei dati nel Centro sicurezza di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="564ce-103">Protezione del servizio SQL di Azure e dei dati nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="564ce-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="564ce-104">Il Centro sicurezza di Azure analizza lo stato di sicurezza delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="564ce-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="564ce-105">Quando il Centro sicurezza identifica potenziali vulnerabilità della sicurezza, crea raccomandazioni utili per definire il processo di configurazione dei controlli necessari.</span><span class="sxs-lookup"><span data-stu-id="564ce-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="564ce-106">Le raccomandazioni sono applicabili a diversi tipi di risorse di Azure, ovvero macchine virtuali, risorse di rete, SQL, dati e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="564ce-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="564ce-107">Questo articolo illustra le raccomandazioni applicabili al servizio SQL di Azure e ai dati</span><span class="sxs-lookup"><span data-stu-id="564ce-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="564ce-108">e relative all'abilitazione del controllo per i database SQL Azure e della crittografia per i database SQL e dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="564ce-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="564ce-109">Usare la tabella seguente come riferimento per conoscere le raccomandazioni disponibili per il servizio SQL e per i dati e i relativi effetti se vengono applicate.</span><span class="sxs-lookup"><span data-stu-id="564ce-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="564ce-110">Raccomandazioni disponibili per il servizio SQL e i dati</span><span class="sxs-lookup"><span data-stu-id="564ce-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="564ce-111">Raccomandazione</span><span class="sxs-lookup"><span data-stu-id="564ce-111">Recommendation</span></span> | <span data-ttu-id="564ce-112">Descrizione</span><span class="sxs-lookup"><span data-stu-id="564ce-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="564ce-113">Abilitare il controllo e il rilevamento delle minacce nei server SQL</span><span class="sxs-lookup"><span data-stu-id="564ce-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="564ce-114">Consiglia di attivare il controllo e il rilevamento delle minacce per i server di Azure SQL (solo il servizio Azure SQL, non è incluso SQL in esecuzione nelle macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="564ce-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="564ce-115">Abilitare il controllo e il rilevamento delle minacce nei database SQL</span><span class="sxs-lookup"><span data-stu-id="564ce-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="564ce-116">Consiglia di attivare il controllo e il rilevamento delle minacce per i database SQL di Azure (solo il servizio Azure SQL, non è incluso SQL in esecuzione nelle macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="564ce-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="564ce-117">Abilitare Transparent Data Encryption sui database SQL</span><span class="sxs-lookup"><span data-stu-id="564ce-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="564ce-118">Consiglia di abilitare la crittografia per i database SQL (solo il servizio di SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="564ce-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="564ce-119">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="564ce-119">See also</span></span>
<span data-ttu-id="564ce-120">Per altre informazioni sulle raccomandazioni applicabili ad altri tipi di risorse di Azure, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="564ce-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="564ce-121">Protezione delle macchine virtuali nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="564ce-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="564ce-122">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="564ce-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="564ce-123">Protezione della rete nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="564ce-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="564ce-124">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="564ce-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="564ce-125">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="564ce-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="564ce-126">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="564ce-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="564ce-127">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="564ce-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
