---
title: Abilitare Transparent Data Encryption nel Centro sicurezza di Azure | Documentazione Microsoft
description: "In questo documento è illustrato come implementare la raccomandazione **AbilitareTransparent Data Encryption** del Centro sicurezza di Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="09d0b-103">Abilitare Transparent Data Encryption nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="09d0b-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="09d0b-104">Il Centro sicurezza di Azure consiglia di abilitare Transparent Data Encryption (TDE) nel database SQL, se non è già abilitato.</span><span class="sxs-lookup"><span data-stu-id="09d0b-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="09d0b-105">TDE protegge i dati e consente di soddisfare i requisiti di conformità tramite la crittografia del database, backup associati e file di log delle transazioni inattive, senza richiedere modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="09d0b-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="09d0b-106">Per altre informazioni, vedere [Transparent Data Encryption con il database SQL di Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="09d0b-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="09d0b-107">Questa indicazione si applica esclusivamente al servizio SQL di Azure e non include SQL in esecuzione sulle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="09d0b-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="09d0b-108">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="09d0b-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="09d0b-109">Questa non è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="09d0b-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="09d0b-110">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="09d0b-110">Implement the recommendation</span></span>
1. <span data-ttu-id="09d0b-111">Nel pannello **Raccomandazioni** selezionare **Abilita Transparent Data Encryption**.</span><span class="sxs-lookup"><span data-stu-id="09d0b-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="09d0b-112">![Abilita Transparent Data Encryption][1]</span><span class="sxs-lookup"><span data-stu-id="09d0b-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="09d0b-113">Viene visualizzato il pannello **Abilita Transparent Data Encryption nei database SQL** .</span><span class="sxs-lookup"><span data-stu-id="09d0b-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="09d0b-114">Selezionare un database SQL su cui abilitare la crittografiaTDE.</span><span class="sxs-lookup"><span data-stu-id="09d0b-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="09d0b-115">![Selezionare database SQL per abilitare la crittografia TDE][2]</span><span class="sxs-lookup"><span data-stu-id="09d0b-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="09d0b-116">Nel pannello **Transparent Data Encryption** selezionare **ON** in Crittografia dati e selezionare **Salva** nella barra multifunzione situata nella parte superiore del pannello.</span><span class="sxs-lookup"><span data-stu-id="09d0b-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="09d0b-117">![Attivare la crittografia TDE][3]</span><span class="sxs-lookup"><span data-stu-id="09d0b-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="09d0b-118">Dopo aver abilitato TDE nel database SQL selezionato, lo **Stato crittografia** diventerà **Crittografato**.</span><span class="sxs-lookup"><span data-stu-id="09d0b-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![Stato della crittografia][4]

## <a name="see-also"></a><span data-ttu-id="09d0b-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="09d0b-120">See also</span></span>
<span data-ttu-id="09d0b-121">Questo documento illustra come implementare la raccomandazione "Abilitare Transparent Data Encryption" del Centro sicurezza.</span><span class="sxs-lookup"><span data-stu-id="09d0b-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="09d0b-122">Per altre informazioni su TDE di SQL, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="09d0b-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="09d0b-123">Transparent Data Encryption con il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="09d0b-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="09d0b-124">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="09d0b-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="09d0b-125">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="09d0b-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="09d0b-126">[Impostazione dei criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="09d0b-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="09d0b-127">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="09d0b-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="09d0b-128">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="09d0b-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="09d0b-129">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="09d0b-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="09d0b-130">[Monitoraggio delle soluzioni dei partner con il Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come monitorare lo stato integrità delle soluzioni dei partner.</span><span class="sxs-lookup"><span data-stu-id="09d0b-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="09d0b-131">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="09d0b-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="09d0b-132">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : informazioni e notizie aggiornate sulla sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="09d0b-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
