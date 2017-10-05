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
# <a name="guest-os-family-1-retirement-notice"></a>Avviso di ritiro della famiglia di sistemi operativi guest 1
Il ritiro della famiglia di sistemi operativi guest 1 è stato annunciato il 1° giugno 2013.

**2 settembre 2014**. La famiglia di sistemi operativi guest 1.x di Azure, basata su Windows Server 2008, è stata ufficialmente ritirata. Qualsiasi tentativo di distribuire nuovi servizi o aggiornamenti di servizi esistenti mediante la famiglia 1 avrà esito negativo e restituirà un messaggio di errore simile al seguente: "La famiglia di sistemi operativi guest 1 è stata ritirata."

**3 novembre 2014**. Il supporto esteso per la famiglia di sistemi operativi guest 1 è terminato ed è stato completamente ritirato. Saranno interessati tutti i servizi ancora attivi nella famiglia 1. Questi servizi potranno essere interrotti in qualsiasi momento. Non è garantito che i servizi continuino a essere operativi, a meno che l'utente non esegua manualmente l'aggiornamento.

Per altre domande, visitare i [forum dei servizi cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [contattare il supporto di Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Si è interessati?
I servizi cloud sono interessati se si verifica una delle seguenti condizioni:

1. Nel file ServiceConfiguration.cscfg del servizio cloud è specificato esplicitamente il valore "osFamily = "1".
2. Nel file ServiceConfiguration.cscfg per il servizio cloud non è specificato esplicitamente alcun valore per osFamily. Attualmente viene usato il valore predefinito "1" in questo caso.
3. Il valore della famiglia di sistemi operativi guest indicato nel portale di Azure è "Windows Server 2008".

Per trovare la famiglia di sistemi operativi in esecuzione sui servizi cloud, è possibile eseguire lo script seguente in Azure PowerShell, anche se prima è necessario [configurare Azure PowerShell](/powershell/azureps-cmdlets-docs). Per altre informazioni sullo script, vedere [Azure Guest OS Family 1 End of Life: June 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx) (Fine vita della famiglia di sistemi operativi guest di Azure 1 di giugno 2014).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

I servizi cloud saranno interessati dal ritiro della famiglia di sistemi operativi 1 se la colonna osFamily dell'output dello script è vuota o contiene il valore "1".

## <a name="recommendations-if-you-are-affected"></a>Indicazioni se i servizi cloud sono interessati
Si consiglia di migrare i ruoli del servizio cloud a una delle famiglie di sistemi operativi guest supportate:

**Famiglia di sistema operativi guest 4.x** : Windows Server 2012 R2 *(scelta consigliata)*

1. Assicurarsi che l'applicazione usi SDK 2.1 o versioni successive con .NET Framework 4.0, 4.5 o 4.5.1.
2. Impostare l'attributo osFamily su "4" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.

**Famiglia di sistemi operativi guest 3.x** : Windows Server 2012

1. Assicurarsi che l'applicazione usi SDK 1.8 o versioni successive con .NET Framework 4.0 o 4.5.
2. Impostare l'attributo osFamily su "3" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.

**Famiglia di sistemi operativi guest 2.x** : Windows Server 2008 R2

1. Assicurarsi che l'applicazione usi SDK 1.3 o versioni successive con .NET Framework 3.5 o 4.0.
2. Impostare l'attributo osFamily su "2" nel file ServiceConfiguration.cscfg, quindi ridistribuire il servizio cloud.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Supporto esteso per la famiglia di sistemi operativi guest 1 terminato il 3 novembre 2014
I servizi cloud per la famiglia di sistemi operativi guest 1 non sono più supportati. Disattivare la migrazione della famiglia 1 appena possibile per evitare l'interruzione del servizio.  

## <a name="next-steps"></a>Passaggi successivi
Esaminare le [versioni del sistema operativo guest](cloud-services-guestos-update-matrix.md)più recenti.
