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
# <a name="guest-os-family-1-retirement-notice"></a>Avviso di ritiro della famiglia di sistemi operativi guest 1
ritiro di Hello della famiglia di sistemi operativi 1 è stato annunciato il 1 giugno 2013.

**2 settembre 2014** hello il sistema operativo Guest Azure (sistema operativo Guest) famiglia 1. x, basata sul sistema operativo Windows Server 2008 hello, è stata ufficialmente ritirata. Tutti i tentativi toodeploy nuovi servizi o aggiornamento di servizi esistenti mediante la famiglia 1 avrà esito negativo con un messaggio di errore che informa che hello che famiglia di sistemi operativi Guest 1 è stata ritirata.

**3 novembre 2014**. Il supporto esteso per la famiglia di sistemi operativi guest 1 è terminato ed è stato completamente ritirato. Saranno interessati tutti i servizi ancora attivi nella famiglia 1. Questi servizi potranno essere interrotti in qualsiasi momento. Non c'è garanzia che i servizi continuino toorun a meno che non si manualmente l'aggiornamento.

Se si dispone di ulteriori domande, visitare hello [forum dei servizi Cloud](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) o [contattare il supporto tecnico di Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Si è interessati?
I servizi Cloud sono interessati se si applica una delle seguenti hello:

1. Si dispone di un valore di "osFamily ="1"specificato in modo esplicito nel file ServiceConfiguration. cscfg hello per il servizio Cloud.
2. Non si dispone di un valore per osFamily specificato in modo esplicito nel file ServiceConfiguration. cscfg hello per il servizio Cloud. Attualmente, sistema di hello Usa valore predefinito hello "1" in questo caso.
3. Hello portale di Azure, il valore della famiglia di sistemi operativi Guest sono elencati come "Windows Server 2008".

toofind che dei servizi cloud sono famiglia del sistema operativo in esecuzione, è possibile eseguire lo script in Azure PowerShell seguente hello anche se è necessario [configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) prima. Per ulteriori informazioni sullo script hello, vedere [Azure Guest del sistema operativo 1 fine vita della famiglia: giugno 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

I servizi cloud saranno interessati dal ritiro della famiglia di sistemi operativi 1 se la colonna osFamily hello nell'output di hello script è vuoto o contiene un "1".

## <a name="recommendations-if-you-are-affected"></a>Indicazioni se i servizi cloud sono interessati
Si consiglia di che migrare tooone di ruoli del servizio Cloud di famiglie di sistemi operativi Guest supportato hello:

**Famiglia di sistema operativi guest 4.x** : Windows Server 2012 R2 *(scelta consigliata)*

1. Assicurarsi che l'applicazione usi SDK 2.1 o versioni successive con .NET Framework 4.0, 4.5 o 4.5.1.
2. Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "4", quindi ridistribuire il servizio cloud.

**Famiglia di sistemi operativi guest 3.x** : Windows Server 2012

1. Assicurarsi che l'applicazione usi SDK 1.8 o versioni successive con .NET Framework 4.0 o 4.5.
2. Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "3", quindi ridistribuire il servizio cloud.

**Famiglia di sistemi operativi guest 2.x** : Windows Server 2008 R2

1. Assicurarsi che l'applicazione usi SDK 1.3 o versioni successive con .NET Framework 3.5 o 4.0.
2. Impostare file ServiceConfiguration. cscfg di hello osFamily attributo hello in troppo "2", quindi ridistribuire il servizio cloud.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>Supporto esteso per la famiglia di sistemi operativi guest 1 terminato il 3 novembre 2014
I servizi cloud per la famiglia di sistemi operativi guest 1 non sono più supportati. Migrazione disattivata famiglia 1 appena tooavoid possibili interruzioni del servizio.  

## <a name="next-steps"></a>Passaggi successivi
Hello revisione più recente [versioni del sistema operativo Guest](cloud-services-guestos-update-matrix.md).
