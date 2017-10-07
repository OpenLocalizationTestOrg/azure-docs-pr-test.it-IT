---
title: un servizio cloud di Azure in Windows PowerShell aaaScale | Documenti Microsoft
description: (versione classica) Informazioni su come toouse PowerShell tooscale un ruolo web o un ruolo di lavoro in o out in Azure.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Come tooscale un cloud service in PowerShell

È possibile utilizzare Windows PowerShell tooscale un ruolo web o un ruolo di lavoro in o out aggiungendo o rimuovendo istanze.  

## <a name="log-in-tooazure"></a>Accedi tooAzure

Prima di poter eseguire qualsiasi operazione sulla sottoscrizione tramite PowerShell, è necessario eseguire l'accesso:

```powershell
Add-AzureAccount
```

Se si dispone di più sottoscrizioni associate all'account, potrebbe essere abbonamento hello toochange a seconda di dove si trova il servizio cloud. toocheck hello sottoscrizione corrente, eseguire:

```powershell
Get-AzureSubscription -Current
```

Se è necessario toochange sottoscrizione corrente di hello, eseguire:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Verifica numero di istanze per il ruolo corrente hello

stato corrente di hello toocheck del ruolo, eseguire:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

È necessario ottenere informazioni sul ruolo hello, incluso il relativo numero di versione e l'istanza del sistema operativo corrente. In questo caso, il ruolo di hello dispone di una singola istanza.

![Informazioni sul ruolo hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Scalabilità orizzontale aggiungendo altre istanze del ruolo hello

tooscale orizzontale il ruolo, passaggio hello numero desiderato di istanze come hello **conteggio** parametro toohello **Set-AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

blocchi di cmdlet Hello temporaneamente durante le nuove istanze hello vengono configurati e avviati. Durante questo periodo, se si apre una nuova finestra di PowerShell e chiamare **Get-AzureRole** come illustrato in precedenza, è possibile vedere conteggio delle istanze hello nuova destinazione. E, se si analizza lo stato di ruolo hello nel portale di hello, dovrebbe essere nuova istanza di hello avvio:

![Avvio dell'istanza VM in corso nel portale](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Una volta avviate le nuove istanze hello, hello cmdlet restituirà correttamente:

![Aumento delle istanze del ruolo riuscito](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Scala nel ruolo hello tramite la rimozione di istanze

È possibile scalare in un ruolo tramite la rimozione di istanze in hello allo stesso modo. Set hello **conteggio** parametro **Set-AzureRole** toohello numero di istanze desiderato toohave dopo scala hello nell'operazione è stata completata.

## <a name="next-steps"></a>Passaggi successivi

Non è possibile tooconfigure scalabilità automatica per i servizi cloud da PowerShell. toodo che, vedere [le modalità di scalabilità di un servizio cloud tooauto](cloud-services-how-to-scale-portal.md).
