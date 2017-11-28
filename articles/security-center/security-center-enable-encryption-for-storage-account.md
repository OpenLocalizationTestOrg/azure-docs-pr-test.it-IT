---
title: crittografia aaaEnable account di archiviazione nel Centro sicurezza di Azure | Documenti Microsoft
description: Questo documento viene illustrato come tooimplement hello indicazioni Centro sicurezza di Azure * * abilitare la crittografia per Azure Storage Account * *.
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
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="dd4fa-103">Abilitare la crittografia per l'account di archiviazione nel Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="dd4fa-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="dd4fa-104">Il Centro sicurezza di Azure consiglia all'utente di abilitare la crittografia del servizio di archiviazione di Azure per i dati inattivi.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="dd4fa-105">Crittografia del servizio di archiviazione (SSE) funziona la crittografia dei dati di hello quando viene scritta tooAzure archiviazione e la decrittografia dei dati di hello prima del recupero.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="dd4fa-106">SSE è attualmente disponibile solo per hello servizio Blob di Azure e può essere utilizzato per i BLOB in blocchi, BLOB di pagine e BLOB di aggiunta.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="dd4fa-107">vedere, più toolearn [la crittografia del servizio di archiviazione per i dati inattivi](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fa-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="dd4fa-108">Dopo avere attivato la crittografia, vengono crittografati solo i nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="dd4fa-109">Qualsiasi BLOB esistente nell'account di archiviazione non viene crittografato.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="dd4fa-110">tooencrypt BLOB esistenti, vedere hello [domande frequenti di crittografia del servizio di archiviazione](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="dd4fa-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="dd4fa-111">La crittografia del servizio di archiviazione è supportata solo negli account di archiviazione di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="dd4fa-112">Gli account di archiviazione classici non sono attualmente supportati.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="dd4fa-113">hello toounderstand classico e modelli di distribuzione di gestione delle risorse, vedere [modelli di distribuzione Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="dd4fa-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="dd4fa-114">Questo documento introduce servizio hello utilizzando un esempio di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="dd4fa-115">Questo argomento non costituisce una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="dd4fa-116">Implementare la raccomandazione hello</span><span class="sxs-lookup"><span data-stu-id="dd4fa-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="dd4fa-117">In hello **indicazioni** pannello seleziona **abilitare la crittografia per l'Account di archiviazione Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="dd4fa-118">![Abilita la crittografia per l'account di archiviazione][1]</span><span class="sxs-lookup"><span data-stu-id="dd4fa-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="dd4fa-119">Hello **abilitare la crittografia di archiviazione** apre blade.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="dd4fa-120">Questo pannello sono elencati gli account di archiviazione di Azure hello in cui la crittografia di archiviazione è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="dd4fa-121">In questo esempio selezioniamo **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="dd4fa-122">![Abilita la crittografia di archiviazione][2]</span><span class="sxs-lookup"><span data-stu-id="dd4fa-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="dd4fa-123">Hello **crittografia** pannello **storageacct1** apre.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="dd4fa-124">Selezionare **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-124">Select **Enabled**.</span></span>
   <span data-ttu-id="dd4fa-125">![Pannello di crittografia][3]</span><span class="sxs-lookup"><span data-stu-id="dd4fa-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="dd4fa-126">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-126">Select **Save**.</span></span>

<span data-ttu-id="dd4fa-127">A questo punto è stata abilitata la crittografia di archiviazione per **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="dd4fa-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="dd4fa-128">See also</span></span>
<span data-ttu-id="dd4fa-129">Questo documento ha illustrato come tooimplement hello Centro sicurezza PC indicazione "Abilita la crittografia per Account di archiviazione Azure."</span><span class="sxs-lookup"><span data-stu-id="dd4fa-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="dd4fa-130">toolearn ulteriori informazioni su Azure la crittografia del servizio di archiviazione, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="dd4fa-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="dd4fa-131">Crittografia del servizio di archiviazione di Azure per dati inattivi</span><span class="sxs-lookup"><span data-stu-id="dd4fa-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="dd4fa-132">toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="dd4fa-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="dd4fa-133">[L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) -informazioni su come tooconfigure i criteri di sicurezza per le sottoscrizioni di Azure e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="dd4fa-134">[Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) -informazioni su come toomonitor hello integrità delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="dd4fa-135">[La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) -informazioni su come avvisi toosecurity toomanage e rispondere.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="dd4fa-136">[Gestione delle raccomandazioni di sicurezza nel Centro sicurezza di Azure](security-center-recommendations.md) : informazioni sul modo in cui le raccomandazioni semplificano la protezione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="dd4fa-137">[Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) -domande frequenti sull'utilizzo di hello servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="dd4fa-138">[Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità di Azure.</span><span class="sxs-lookup"><span data-stu-id="dd4fa-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
