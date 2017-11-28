---
title: Avviso di ritiro della famiglia di sistemi operativi guest 1 | Documentazione Microsoft
description: "Fornisce informazioni sulla data in cui è stato effettuato il ritiro della famiglia di sistemi operativi guest 1 e su come stabilire se si è interessati"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: 3178a09dab1cb972a3460d54dc9908fb95cce68b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="dce20-103">Avviso di ritiro della famiglia di sistemi operativi guest 1</span><span class="sxs-lookup"><span data-stu-id="dce20-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="dce20-104">Il ritiro della famiglia di sistemi operativi guest 1 è stato annunciato il 1° giugno 2013.</span><span class="sxs-lookup"><span data-stu-id="dce20-104">The retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="dce20-105">**2 settembre 2014**. La famiglia di sistemi operativi guest 1.x di Azure, basata su Windows Server 2008, è stata ufficialmente ritirata.</span><span class="sxs-lookup"><span data-stu-id="dce20-105">**Sept 2, 2014** The Azure Guest operating system (Guest OS) Family 1.x, which is based on the Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="dce20-106">Qualsiasi tentativo di distribuire nuovi servizi o aggiornamenti di servizi esistenti mediante la famiglia 1 avrà esito negativo e restituirà un messaggio di errore simile al seguente: "La famiglia di sistemi operativi guest 1 è stata ritirata."</span><span class="sxs-lookup"><span data-stu-id="dce20-106">All attempts to deploy new services or upgrade existing services using Family 1 will fail with an error message informing you that the Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="dce20-107">**3 novembre 2014**. Il supporto esteso per la famiglia di sistemi operativi guest 1 è terminato ed è stato completamente ritirato.</span><span class="sxs-lookup"><span data-stu-id="dce20-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="dce20-108">Saranno interessati tutti i servizi ancora attivi nella famiglia 1.</span><span class="sxs-lookup"><span data-stu-id="dce20-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="dce20-109">Questi servizi potranno essere interrotti in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="dce20-109">We may stop those services at any time.</span></span> <span data-ttu-id="dce20-110">Non è garantito che i servizi continuino a essere operativi, a meno che l'utente non esegua manualmente l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="dce20-110">There is no guarantee your services will continue to run unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="dce20-111">Per altre domande, visitare i [forum dei servizi cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [contattare il supporto di Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="dce20-111">If you have additional questions, visit the [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="dce20-112">Si è interessati?</span><span class="sxs-lookup"><span data-stu-id="dce20-112">Are you affected?</span></span>
<span data-ttu-id="dce20-113">I servizi cloud sono interessati se si verifica una delle seguenti condizioni:</span><span class="sxs-lookup"><span data-stu-id="dce20-113">Your Cloud Services are affected if any one of the following applies:</span></span>

1. <span data-ttu-id="dce20-114">Nel file ServiceConfiguration.cscfg del servizio cloud è specificato esplicitamente il valore "osFamily = "1".</span><span class="sxs-lookup"><span data-stu-id="dce20-114">You have a value of "osFamily = "1" explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="dce20-115">Nel file ServiceConfiguration.cscfg per il servizio cloud non è specificato esplicitamente alcun valore per osFamily.</span><span class="sxs-lookup"><span data-stu-id="dce20-115">You do not have a value for osFamily explicitly specified in the ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="dce20-116">Attualmente viene usato il valore predefinito "1" in questo caso.</span><span class="sxs-lookup"><span data-stu-id="dce20-116">Currently, the system uses the default value of "1" in this case.</span></span>
3. <span data-ttu-id="dce20-117">Il valore della famiglia di sistemi operativi guest indicato nel portale di Azure è "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="dce20-117">The Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="dce20-118">Per trovare la famiglia di sistemi operativi in esecuzione sui servizi cloud, è possibile eseguire lo script seguente in Azure PowerShell, anche se prima è necessario [configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dce20-118">To find which of your cloud services are running which OS Family, you can run the following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="dce20-119">Per altre informazioni sullo script, vedere [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Fine vita della famiglia di sistemi operativi guest di Azure 1 di giugno 2014).</span><span class="sxs-lookup"><span data-stu-id="dce20-119">For more information on the script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="dce20-120">I servizi cloud saranno interessati dal ritiro della famiglia di sistemi operativi 1 se la colonna osFamily dell'output dello script è vuota o contiene il valore "1".</span><span class="sxs-lookup"><span data-stu-id="dce20-120">Your cloud services will be impacted by OS Family 1 retirement if the osFamily column in the script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="dce20-121">Indicazioni se i servizi cloud sono interessati</span><span class="sxs-lookup"><span data-stu-id="dce20-121">Recommendations if you are affected</span></span>
<span data-ttu-id="dce20-122">Si consiglia di migrare i ruoli del servizio cloud a una delle famiglie di sistemi operativi guest supportate:</span><span class="sxs-lookup"><span data-stu-id="dce20-122">We recommend you migrate your Cloud Service roles to one of the supported Guest OS Families:</span></span>

<span data-ttu-id="dce20-123">**Famiglia di sistema operativi guest 4.x** : Windows Server 2012 R2 *(scelta consigliata)*</span><span class="sxs-lookup"><span data-stu-id="dce20-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="dce20-124">Assicurarsi che l'applicazione usi SDK 2.1 o versioni successive con .NET Framework 4.0, 4.5 o 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="dce20-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="dce20-125">Impostare l'attributo osFamily su "4" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dce20-125">Set the osFamily attribute to “4” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="dce20-126">**Famiglia di sistemi operativi guest 3.x** : Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="dce20-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="dce20-127">Assicurarsi che l'applicazione usi SDK 1.8 o versioni successive con .NET Framework 4.0 o 4.5.</span><span class="sxs-lookup"><span data-stu-id="dce20-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="dce20-128">Impostare l'attributo osFamily su "3" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dce20-128">Set the osFamily attribute to “3” in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="dce20-129">**Famiglia di sistemi operativi guest 2.x** : Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="dce20-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="dce20-130">Assicurarsi che l'applicazione usi SDK 1.3 o versioni successive con .NET Framework 3.5 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="dce20-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="dce20-131">Impostare l'attributo osFamily su "2" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="dce20-131">Set the osFamily attribute to "2" in the ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="dce20-132">Supporto esteso per la famiglia di sistemi operativi guest 1 terminato il 3 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="dce20-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="dce20-133">I servizi cloud per la famiglia di sistemi operativi guest 1 non sono più supportati.</span><span class="sxs-lookup"><span data-stu-id="dce20-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="dce20-134">Disattivare la migrazione della famiglia 1 appena possibile per evitare l'interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="dce20-134">Migrate off family 1 as soon as possible to avoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="dce20-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dce20-135">Next steps</span></span>
<span data-ttu-id="dce20-136">Esaminare le [versioni del sistema operativo guest](cloud-services-guestos-update-matrix.md)più recenti.</span><span class="sxs-lookup"><span data-stu-id="dce20-136">Review the latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
