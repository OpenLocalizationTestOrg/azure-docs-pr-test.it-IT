---
title: Si noti 1 ritiro della famiglia del sistema operativo aaaGuest | Documenti Microsoft
description: "Vengono fornite informazioni su quando si è verificato il ritiro della famiglia di sistemi operativi Guest Azure 1 hello e come toodetermine se si è interessati"
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
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a><span data-ttu-id="45e71-103">Avviso di ritiro della famiglia di sistemi operativi guest 1</span><span class="sxs-lookup"><span data-stu-id="45e71-103">Guest OS Family 1 retirement notice</span></span>
<span data-ttu-id="45e71-104">ritiro di Hello della famiglia di sistemi operativi 1 è stato annunciato il 1 giugno 2013.</span><span class="sxs-lookup"><span data-stu-id="45e71-104">hello retirement of OS Family 1 was first announced on June 1, 2013.</span></span>

<span data-ttu-id="45e71-105">**2 settembre 2014** hello il sistema operativo Guest Azure (sistema operativo Guest) famiglia 1. x, basata sul sistema operativo Windows Server 2008 hello, è stata ufficialmente ritirata.</span><span class="sxs-lookup"><span data-stu-id="45e71-105">**Sept 2, 2014** hello Azure Guest operating system (Guest OS) Family 1.x, which is based on hello Windows Server 2008 operating system, was officially retired.</span></span> <span data-ttu-id="45e71-106">Tutti i tentativi toodeploy nuovi servizi o aggiornamento di servizi esistenti mediante la famiglia 1 avrà esito negativo con un messaggio di errore che informa che hello che famiglia di sistemi operativi Guest 1 è stata ritirata.</span><span class="sxs-lookup"><span data-stu-id="45e71-106">All attempts toodeploy new services or upgrade existing services using Family 1 will fail with an error message informing you that hello Guest OS Family 1 has been retired.</span></span>

<span data-ttu-id="45e71-107">**3 novembre 2014**. Il supporto esteso per la famiglia di sistemi operativi guest 1 è terminato ed è stato completamente ritirato.</span><span class="sxs-lookup"><span data-stu-id="45e71-107">**November 3, 2014** Extended support for Guest OS Family 1 ended and it is fully retired.</span></span> <span data-ttu-id="45e71-108">Saranno interessati tutti i servizi ancora attivi nella famiglia 1.</span><span class="sxs-lookup"><span data-stu-id="45e71-108">All services still on Family 1 will be impacted.</span></span> <span data-ttu-id="45e71-109">Questi servizi potranno essere interrotti in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="45e71-109">We may stop those services at any time.</span></span> <span data-ttu-id="45e71-110">Non c'è garanzia che i servizi continuino toorun a meno che non si manualmente l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="45e71-110">There is no guarantee your services will continue toorun unless you manually upgrade them yourself.</span></span>

<span data-ttu-id="45e71-111">Se si dispone di ulteriori domande, visitare hello [forum dei servizi Cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [contattare il supporto tecnico di Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="45e71-111">If you have additional questions, visit hello [Cloud Services Forums](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) or [contact Azure support](https://azure.microsoft.com/support/options/).</span></span>

## <a name="are-you-affected"></a><span data-ttu-id="45e71-112">Si è interessati?</span><span class="sxs-lookup"><span data-stu-id="45e71-112">Are you affected?</span></span>
<span data-ttu-id="45e71-113">I servizi Cloud sono interessati se si applica una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="45e71-113">Your Cloud Services are affected if any one of hello following applies:</span></span>

1. <span data-ttu-id="45e71-114">Si dispone di un valore di "osFamily ="1"specificato in modo esplicito nel file ServiceConfiguration. cscfg hello per il servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="45e71-114">You have a value of "osFamily = "1" explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span>
2. <span data-ttu-id="45e71-115">Non si dispone di un valore per osFamily specificato in modo esplicito nel file ServiceConfiguration. cscfg hello per il servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="45e71-115">You do not have a value for osFamily explicitly specified in hello ServiceConfiguration.cscfg file for your Cloud Service.</span></span> <span data-ttu-id="45e71-116">Attualmente, sistema di hello Usa valore predefinito hello "1" in questo caso.</span><span class="sxs-lookup"><span data-stu-id="45e71-116">Currently, hello system uses hello default value of "1" in this case.</span></span>
3. <span data-ttu-id="45e71-117">Hello portale di Azure, il valore della famiglia di sistemi operativi Guest sono elencati come "Windows Server 2008".</span><span class="sxs-lookup"><span data-stu-id="45e71-117">hello Azure portal lists your Guest Operating System family value as "Windows Server 2008".</span></span>

<span data-ttu-id="45e71-118">toofind che dei servizi cloud sono famiglia del sistema operativo in esecuzione, è possibile eseguire lo script in Azure PowerShell seguente hello anche se è necessario [configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) prima.</span><span class="sxs-lookup"><span data-stu-id="45e71-118">toofind which of your cloud services are running which OS Family, you can run hello following script in Azure PowerShell, though you must [set up Azure PowerShell](/powershell/azureps-cmdlets-docs) first.</span></span> <span data-ttu-id="45e71-119">Per ulteriori informazioni sullo script hello, vedere [Azure Guest del sistema operativo 1 fine vita della famiglia: giugno 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="45e71-119">For more information on hello script, see [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).</span></span>

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

<span data-ttu-id="45e71-120">I servizi cloud saranno interessati dal ritiro della famiglia di sistemi operativi 1 se la colonna osFamily hello nell'output di hello script è vuoto o contiene un "1".</span><span class="sxs-lookup"><span data-stu-id="45e71-120">Your cloud services will be impacted by OS Family 1 retirement if hello osFamily column in hello script output is empty or contains a "1".</span></span>

## <a name="recommendations-if-you-are-affected"></a><span data-ttu-id="45e71-121">Indicazioni se i servizi cloud sono interessati</span><span class="sxs-lookup"><span data-stu-id="45e71-121">Recommendations if you are affected</span></span>
<span data-ttu-id="45e71-122">Si consiglia di che migrare tooone di ruoli del servizio Cloud di famiglie di sistemi operativi Guest supportato hello:</span><span class="sxs-lookup"><span data-stu-id="45e71-122">We recommend you migrate your Cloud Service roles tooone of hello supported Guest OS Families:</span></span>

<span data-ttu-id="45e71-123">**Famiglia di sistema operativi guest 4.x** : Windows Server 2012 R2 *(scelta consigliata)*</span><span class="sxs-lookup"><span data-stu-id="45e71-123">**Guest OS family 4.x** - Windows Server 2012 R2 *(recommended)*</span></span>

1. <span data-ttu-id="45e71-124">Assicurarsi che l'applicazione usi SDK 2.1 o versioni successive con .NET Framework 4.0, 4.5 o 4.5.1.</span><span class="sxs-lookup"><span data-stu-id="45e71-124">Ensure that your application is using SDK 2.1 or later with .NET framework 4.0, 4.5 or 4.5.1.</span></span>
2. <span data-ttu-id="45e71-125">Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "4", quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="45e71-125">Set hello osFamily attribute too“4” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="45e71-126">**Famiglia di sistemi operativi guest 3.x** : Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="45e71-126">**Guest OS family 3.x** - Windows Server 2012</span></span>

1. <span data-ttu-id="45e71-127">Assicurarsi che l'applicazione usi SDK 1.8 o versioni successive con .NET Framework 4.0 o 4.5.</span><span class="sxs-lookup"><span data-stu-id="45e71-127">Ensure that your application is using SDK 1.8 or later with .NET framework 4.0 or 4.5.</span></span>
2. <span data-ttu-id="45e71-128">Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "3", quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="45e71-128">Set hello osFamily attribute too“3” in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

<span data-ttu-id="45e71-129">**Famiglia di sistemi operativi guest 2.x** : Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="45e71-129">**Guest OS family 2.x** - Windows Server 2008 R2</span></span>

1. <span data-ttu-id="45e71-130">Assicurarsi che l'applicazione usi SDK 1.3 o versioni successive con .NET Framework 3.5 o 4.0.</span><span class="sxs-lookup"><span data-stu-id="45e71-130">Ensure that your application is using SDK 1.3 and above with .NET framework 3.5 or 4.0.</span></span>
2. <span data-ttu-id="45e71-131">Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "2", quindi ridistribuire il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="45e71-131">Set hello osFamily attribute too"2" in hello ServiceConfiguration.cscfg file, and redeploy your cloud service.</span></span>

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a><span data-ttu-id="45e71-132">Supporto esteso per la famiglia di sistemi operativi guest 1 terminato il 3 novembre 2014</span><span class="sxs-lookup"><span data-stu-id="45e71-132">Extended Support for Guest OS Family 1 ended Nov 3, 2014</span></span>
<span data-ttu-id="45e71-133">I servizi cloud per la famiglia di sistemi operativi guest 1 non sono più supportati.</span><span class="sxs-lookup"><span data-stu-id="45e71-133">Cloud services on Guest OS family 1 are no longer supported.</span></span> <span data-ttu-id="45e71-134">Migrazione disattivata famiglia 1 appena tooavoid possibili interruzioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="45e71-134">Migrate off family 1 as soon as possible tooavoid service disruption.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="45e71-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45e71-135">Next steps</span></span>
<span data-ttu-id="45e71-136">Hello revisione più recente [versioni del sistema operativo Guest](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="45e71-136">Review hello latest [Guest OS releases](cloud-services-guestos-update-matrix.md).</span></span>
