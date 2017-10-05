---
title: Abilitare la crittografia per l'account di archiviazione nel Centro sicurezza di Azure | Microsoft Docs
description: In questo documento viene illustrato come implementare le raccomandazioni del Centro sicurezza di Azure **Abilitare la crittografia per l'account di archiviazione nel Centro sicurezza di Azure**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="e8e80-103">Abilitare la crittografia per l'account di archiviazione nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="e8e80-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="e8e80-104">Il Centro sicurezza di Azure consiglia all'utente di abilitare la crittografia del servizio di archiviazione di Azure per i dati inattivi.</span><span class="sxs-lookup"><span data-stu-id="e8e80-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="e8e80-105">La Crittografia del servizio di archiviazione (SSE) applica la crittografia ai dati quando vengono scritti nell'archiviazione di Azure e li decrittografa prima del recupero.</span><span class="sxs-lookup"><span data-stu-id="e8e80-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="e8e80-106">SSE è attualmente disponibile solo per il servizio BLOB di Azure e può essere usata per BLOB in blocchi, BLOB di pagine e BLOB di aggiunta.</span><span class="sxs-lookup"><span data-stu-id="e8e80-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="e8e80-107">Per altre informazioni, vedere [Crittografia del servizio di archiviazione di Azure per dati inattivi](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="e8e80-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="e8e80-108">Dopo avere attivato la crittografia, vengono crittografati solo i nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="e8e80-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="e8e80-109">Qualsiasi BLOB esistente nell'account di archiviazione non viene crittografato.</span><span class="sxs-lookup"><span data-stu-id="e8e80-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="e8e80-110">Per crittografare un BLOB esistente, vedere [Domande frequenti su Crittografia del servizio di archiviazione per i dati inattivi](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="e8e80-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="e8e80-111">La crittografia del servizio di archiviazione è supportata solo negli account di archiviazione di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="e8e80-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="e8e80-112">Gli account di archiviazione classici non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="e8e80-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="e8e80-113">Per informazioni sui modelli di distribuzione classico e di Gestione risorse, vedere i [modelli di distribuzione di Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="e8e80-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e8e80-114">Il documento introduce il servizio usando una distribuzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="e8e80-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="e8e80-115">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e8e80-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e8e80-116">Implementare la raccomandazione</span><span class="sxs-lookup"><span data-stu-id="e8e80-116">Implement the recommendation</span></span>
1. <span data-ttu-id="e8e80-117">Nel pannello **Raccomandazioni** selezionare **Enable encryption for Azure Storage Account** (Abilita la crittografia per l'account di archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="e8e80-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="e8e80-118">![Enable encryption for storage account][1] (Abilita la crittografia per l'account di archiviazione)</span><span class="sxs-lookup"><span data-stu-id="e8e80-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="e8e80-119">Viene visualizzato il pannello **Enable storage encryption** (Abilita la crittografia di archiviazione).</span><span class="sxs-lookup"><span data-stu-id="e8e80-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="e8e80-120">In questo pannello sono elencati gli account di archiviazione di Azure in cui la crittografia di archiviazione è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="e8e80-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="e8e80-121">In questo esempio selezioniamo **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e8e80-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="e8e80-122">![Abilita la crittografia di archiviazione][2]</span><span class="sxs-lookup"><span data-stu-id="e8e80-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="e8e80-123">Si apre il pannello **Crittografia** per **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e8e80-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="e8e80-124">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="e8e80-124">Select **Enabled**.</span></span>
   <span data-ttu-id="e8e80-125">![Pannello di crittografia][3]</span><span class="sxs-lookup"><span data-stu-id="e8e80-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="e8e80-126">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e8e80-126">Select **Save**.</span></span>

<span data-ttu-id="e8e80-127">A questo punto è stata abilitata la crittografia di archiviazione per **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="e8e80-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="e8e80-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e8e80-128">See also</span></span>
<span data-ttu-id="e8e80-129">In questo documento viene illustrato come implementare la raccomandazione del Centro sicurezza di Azure "Abilitare la crittografia per l'account di archiviazione di Azure".</span><span class="sxs-lookup"><span data-stu-id="e8e80-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="e8e80-130">Per ulteriori informazioni sulla crittografia del servizio di archiviazione di Azure, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8e80-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="e8e80-131">Crittografia del servizio di archiviazione di Azure per dati inattivi</span><span class="sxs-lookup"><span data-stu-id="e8e80-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="e8e80-132">Per altre informazioni sul Centro sicurezza, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8e80-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e8e80-133">[Impostare i criteri di sicurezza nel Centro sicurezza di Azure](security-center-policies.md) : informazioni su come configurare i criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e80-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e8e80-134">[Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](security-center-monitoring.md) : informazioni su come monitorare l'integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e80-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e8e80-135">[Gestione e risposta agli avvisi di sicurezza nel Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) : informazioni su come gestire e rispondere agli avvisi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="e8e80-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e8e80-136">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e80-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e8e80-137">[Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'uso del servizio.</span><span class="sxs-lookup"><span data-stu-id="e8e80-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e8e80-138">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e80-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
