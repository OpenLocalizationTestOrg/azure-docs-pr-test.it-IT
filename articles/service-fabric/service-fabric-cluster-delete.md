---
title: aaaDelete di Azure cluster e le relative risorse | Documenti Microsoft
description: Informazioni su come toocompletely Elimina un'infrastruttura di servizio cluster un gruppo di risorse hello eliminazione contenente cluster hello o eliminando in modo selettivo le risorse.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Eliminare un cluster di Service Fabric sulle risorse di Azure e hello che usa
Un cluster di Service Fabric è costituito da molte altre risorse di Azure inoltre toohello risorsa del cluster stesso. In modo toocompletely eliminare un cluster di Service Fabric è inoltre necessario toodelete che tutti hello è composto di risorse.
Sono disponibili due opzioni: è un gruppo di risorse hello delete hello cluster in (che elimina risorsa cluster hello e altre risorse nel gruppo di risorse hello) o eliminare in modo specifico la risorsa di cluster hello e sono associati alle risorse (ma non altri risorse nel gruppo di risorse hello).

> [!NOTE]
> L'eliminazione di risorse cluster hello **non** tutti hello altre risorse del cluster di Service Fabric è composta da eliminare.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Eliminare hello intero gruppo di risorse (RG) che hello cluster di Service Fabric
Si tratta di tooensure modo più semplice hello di eliminare tutte le risorse di hello associate al cluster, inclusi il gruppo di risorse hello. È possibile eliminare il gruppo di risorse hello tramite PowerShell o tramite hello portale di Azure. Se il gruppo di risorse include risorse che non sono correlati tooService cluster di infrastruttura, è possibile eliminare le risorse specifiche.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Eliminare il gruppo di risorse hello con Azure PowerShell
È anche possibile eliminare il gruppo di risorse hello eseguendo hello seguendo i cmdlet PowerShell di Azure. Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva. Se non è stata eseguita questa operazione prima di, seguire i passaggi di hello illustrati in [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)

Aprire una finestra di PowerShell ed eseguire hello cmdlet di Powershell seguente:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Si otterrà l'eliminazione dei messaggi di richiesta tooconfirm hello se non è stato utilizzato hello *-Force* opzione. In conferma hello RG e vengono eliminate tutte le risorse di hello che contiene.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Eliminare un gruppo di risorse in hello portale di Azure
1. Account di accesso toohello [portale di Azure](https://portal.azure.com).
2. Passare il cluster di Service Fabric toohello da toodelete.
3. Fare clic su hello Nome gruppo di risorse nella pagina di essentials hello del cluster.
4. Verrà visualizzata hello **risorse gruppo Essentials** pagina.
5. Fare clic su **Elimina**.
6. Seguire le istruzioni di hello l'eliminazione di hello toocomplete pagina hello del gruppo di risorse.

![Eliminazione di un gruppo di risorse][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Eliminare una risorsa cluster hello e risorse di hello che viene utilizzato, ma non ad altre risorse nel gruppo di risorse hello
Se il gruppo di risorse contiene solo le risorse cluster di Service Fabric toohello correlati si desidera toodelete, quindi è più facile toodelete hello intero gruppo di risorse. Se si desiderano risorse hello di eliminazione tooselectively uno alla volta nel gruppo di risorse, attenersi alla seguente procedura.

Se è stato distribuito il cluster usando il portale di hello o usando uno dei modelli di gestione risorse di infrastruttura servizio hello dalla raccolta di modelli di hello, tutte le risorse hello hello cluster utilizza sono contrassegnate con hello due tag seguenti. È possibile usarli toodecide le risorse che si desidera toodelete.

***Tag n. 1:*** chiave = NomeCluster, valore = 'nome del cluster hello'

***Tag#2:*** chiave = resourceName, valore = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Elimina le risorse specifiche in hello portale di Azure
1. Account di accesso toohello [portale di Azure](https://portal.azure.com).
2. Passare il cluster di Service Fabric toohello da toodelete.
3. Andare troppo**tutte le impostazioni** nel Pannello di essentials hello.
4. Fare clic su **tag** in **la gestione delle risorse** nel pannello impostazioni hello.
5. Fare clic su uno di hello **tag** in hello tag pannello tooget un elenco di tutte le risorse di hello con tale tag.
   
    ![Tag delle risorse][ResourceTags]
6. Dopo aver creato elenco hello delle risorse con tag, fare clic su ognuna delle risorse hello ed eliminarli.
   
    ![Risorse con tag][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Eliminare le risorse di hello con Azure PowerShell
È possibile eliminare le risorse hello uno alla volta eseguendo hello seguendo i cmdlet PowerShell di Azure. Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva. Se non è stata eseguita questa operazione prima di, seguire i passaggi di hello illustrati in [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)

Aprire una finestra di PowerShell ed eseguire hello cmdlet di Powershell seguente:

```powershell
Login-AzureRmAccount
```
Per ogni risorsa hello toodelete desiderata, eseguire hello seguente:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

risorsa di cluster di hello di toodelete, eseguire hello seguente:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Passaggi successivi
Hello lettura seguente tooalso informazioni sull'aggiornamento di un cluster e partizionamento servizi:

* [Informazioni sugli aggiornamenti dei cluster](service-fabric-cluster-upgrade.md)
* [Informazioni sul partizionamento dei servizi con stato per la massima scalabilità](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
