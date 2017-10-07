---
title: modifiche di tooprevent aaaLock risorse di Azure | Documenti Microsoft
description: Impedire agli utenti di aggiornare o eliminare le risorse critiche di Azure applicando un blocco per tutti gli utenti e i ruoli.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Bloccare le risorse tooprevent modifiche impreviste 
Come amministratore, potrebbe essere necessario toolock una sottoscrizione, gruppo di risorse o tooprevent risorse ad altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche. È possibile impostare il livello di blocco hello troppo**CanNotDelete** o **ReadOnly**. 

* **CanNotDelete** significa che gli utenti autorizzati possano comunque leggere e modificare una risorsa, ma non eliminare la risorsa hello. 
* **ReadOnly** significa che gli utenti autorizzati possono leggere una risorsa, ma non possono eliminare o aggiornare la risorsa hello. L'applicazione di questo blocco è simile toorestricting tutti autorizzato agli utenti toohello le autorizzazioni concesse da hello **lettore** ruolo. 

## <a name="how-locks-are-applied"></a>Come vengono applicati i blocchi

Quando si applica un blocco a un ambito padre, tutte le risorse in tale ambito ereditano hello stesso blocco. Anche le risorse in seguito si aggiungono ereditano blocco hello dall'elemento padre di hello. blocco di più restrittivo Hello nell'ereditarietà hello ha la precedenza.

A differenza di controllo di accesso basato sui ruoli, si utilizza Gestione blocchi tooapply una restrizione in tutti gli utenti e ruoli. toolearn sull'impostazione delle autorizzazioni per utenti e ruoli, vedere [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).

Blocchi di gestione risorse di si applicano solo toooperations che si verificano nel piano di gestione di hello, che include le operazioni inviate troppo`https://management.azure.com`. blocchi di Hello non limitano come risorse di eseguono le proprie funzioni. Vengono limitate le modifiche alle risorse, ma non le operazioni delle risorse. Ad esempio, un blocco di sola lettura su un Database SQL impedisce l'eliminazione o Modifica database hello, ma non impedisce la creazione, aggiornamento o eliminazione di dati nel database di hello. Le transazioni di dati sono consentite perché queste operazioni non vengono inviate troppo`https://management.azure.com`.

L'applicazione **ReadOnly** può generare risultati toounexpected perché alcune operazioni che sembrano leggere operazioni effettivamente richiedono ulteriori azioni. Ad esempio, inserire un **ReadOnly** blocco su un account di archiviazione impedisce l'elenco di chiavi hello tutti gli utenti. elenco di Hello operazione delle chiavi viene gestita tramite una richiesta POST hello ha restituito le chiavi sono disponibili per le operazioni di scrittura. Per un altro esempio, inserire un **ReadOnly** blocco su una risorsa di servizio App che impedisce la visualizzazione di file per la risorsa hello perché tale interazione richiede l'accesso in scrittura di Esplora Server Visual Studio.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Chi può creare o eliminare i blocchi nell'organizzazione
i blocchi di gestione toocreate o delete, è necessario avere accesso troppo`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` azioni. Di hello ruoli predefiniti, solo **proprietario** e **amministratore di accesso utente** vengono concesse tali azioni.

## <a name="portal"></a>di Microsoft Azure
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Modello
Hello esempio seguente viene illustrato un modello che crea un blocco su un account di archiviazione. account di archiviazione Hello su quali tooapply blocco hello viene fornito come parametro. Hello nome del blocco hello viene creato concatenando il nome di risorsa hello con **/Microsoft.Authorization/** e hello nome del blocco di hello, in questo caso **myLock**.

tipo di Hello fornito è il tipo di risorsa specifico toohello. Per l'archiviazione, impostare too"Microsoft.Storage/storageaccounts/providers/locks tipo hello".

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Blocco è distribuita risorse con Azure PowerShell con hello [New AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.

toolock una risorsa, specificare il nome di hello della risorsa hello, il tipo di risorsa e il nome del gruppo di risorse.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock un gruppo di risorse, fornire il nome di hello hello del gruppo di risorse.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

un blocco, l'utilizzo di informazioni tooget [Get AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget tutti i blocchi di hello nella sottoscrizione, utilizzare:

```powershell
Get-AzureRmResourceLock
```

tooget tutti i blocchi per una risorsa, utilizzare:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget tutti i blocchi per un gruppo di risorse, utilizzare:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

Azure PowerShell fornisce altri comandi per i blocchi di lavoro, ad esempio [Set AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un blocco, e [Remove AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un blocco.

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Si blocca distribuiti risorse con CLI di Azure tramite hello [blocco az creare](/cli/azure/lock#create) comando.

toolock una risorsa, specificare il nome di hello della risorsa hello, il tipo di risorsa e il nome del gruppo di risorse.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock un gruppo di risorse, fornire il nome di hello hello del gruppo di risorse.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

un blocco, l'utilizzo di informazioni tooget [elenco blocchi az](/cli/azure/lock#list). tooget tutti i blocchi di hello nella sottoscrizione, utilizzare:

```azurecli
az lock list
```

tooget tutti i blocchi per una risorsa, utilizzare:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget tutti i blocchi per un gruppo di risorse, utilizzare:

```azurecli
az lock list --resource-group exampleresourcegroup
```

CLI di Azure fornisce altri comandi per i blocchi di lavoro, ad esempio [aggiornamento blocco az](/cli/azure/lock#update) tooupdate un blocco, e [blocco az eliminare](/cli/azure/lock#delete) toodelete un blocco.

## <a name="rest-api"></a>API REST
È possibile bloccare le risorse distribuite con hello [API REST per blocchi di gestione](https://docs.microsoft.com/rest/api/resources/managementlocks). API REST Hello consente toocreate Elimina i blocchi e recuperare informazioni sui blocchi esistenti.

toocreate un blocco, eseguire:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

Hello ambito può essere una sottoscrizione, un gruppo di risorse o una risorsa. Hello-nome del blocco è qualsiasi blocco hello toocall. Per api-version, usare **2015-01-01**.

Nella richiesta di hello, includere un oggetto JSON che specifica le proprietà di hello blocco hello.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sull'uso dei blocchi di risorse, vedere [Blocco delle risorse di Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn sull'organizzazione in modo logico le risorse, vedere [tramite tag tooorganize le risorse](resource-group-using-tags.md)
* vedere toochange quale gruppo di risorse una risorsa in cui risiede [spostamento risorse toonew risorse del gruppo](resource-group-move-resources.md)
* È possibile applicare restrizioni e convenzioni all’interno della sottoscrizione con criteri personalizzati. Per ulteriori informazioni, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](resource-manager-policy.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

