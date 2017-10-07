---
title: aaaManage Azure soluzioni con PowerShell | Documenti Microsoft
description: Usare le risorse di Azure PowerShell e toomanage Gestione risorse.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Gestire le risorse con Azure PowerShell e Resource Manager
> [!div class="op_single_selector"]
> * [Portale](resource-group-portal.md)
> * [Interfaccia della riga di comando di Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
>
>

In questo articolo viene illustrato come toomanage soluzioni con Azure PowerShell e Gestione risorse di Azure. Se non si ha familiarità con Resource Manager, vedere [Panoramica di Azure Resource Manager](resource-group-overview.md). Questo argomento è incentrato sulle attività di gestione. Si apprenderà come:

1. Creare un gruppo di risorse
2. Aggiungere un gruppo di risorse toohello
3. Aggiungere una risorsa toohello tag
4. Eseguire query sulle risorse in base ai nomi o ai valori dei tag
5. Applicare e rimuovere un blocco sulla risorsa hello
6. Eliminare un gruppo di risorse

In questo articolo non vengono visualizzati come una sottoscrizione di gestione risorse modello tooyour toodeploy. Per informazioni in merito, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>guida introduttiva ad Azure PowerShell

Se non è installato Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

Se è installato Azure PowerShell in hello precedente ma abbia non aggiornato di recente, è consigliabile installare la versione più recente di hello. È possibile aggiornare una versione di hello tramite hello stesso metodo usato tooinstall è. Ad esempio, se si utilizza l'installazione guidata piattaforma Web hello, avviarla di nuovo e cercare un aggiornamento.

Utilizzare la versione del modulo di risorse di Azure, hello toocheck hello seguenti cmdlet:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Questo argomento è stato aggiornato per la versione 3.3.0. Se si dispone di una versione precedente, l'esperienza potrebbe non corrispondere passaggi hello illustrati in questo argomento. Per la documentazione sui cmdlet di hello in questa versione, vedere [AzureRM.Resources modulo](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Accedi tooyour account Azure
Per eseguire la soluzione, è necessario accedere tooyour account.

toolog in tooyour account Azure, utilizzare hello **accesso AzureRmAccount** cmdlet.

```powershell
Login-AzureRmAccount
```

cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure. Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.

Hello cmdlet restituisce informazioni su toouse di sottoscrizione l'account e hello per le attività di hello.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Se si dispone di più di una sottoscrizione, è possibile passare tooa altra sottoscrizione. In primo luogo, esaminare tutte le sottoscrizioni di hello per l'account.

```powershell
Get-AzureRmSubscription
```

Vengono restituite le sottoscrizioni abilitate e disabilitate.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa altra sottoscrizione, fornire il nome di sottoscrizione hello hello **Set AzureRmContext** cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
Prima di distribuire qualsiasi sottoscrizione tooyour risorse, è necessario creare un gruppo di risorse contenenti risorse hello.

toocreate un gruppo di risorse, utilizzare hello **New AzureRmResourceGroup** cmdlet. comando Hello utilizza hello **nome** toospecify parametro un nome per il gruppo di risorse hello e hello **percorso** toospecify parametro relativo percorso.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

output di Hello è nel seguente formato hello:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Gruppo di risorse tooretrieve hello in un secondo momento, utilizzare hello seguente cmdlet:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget tutti hello gruppi di risorse nella sottoscrizione, non si specifica un nome:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Aggiungi gruppo di risorse tooa risorse
un gruppo di risorse toohello tooadd, è possibile utilizzare hello **New-AzureRmResource** cmdlet o un cmdlet che fa toohello specifico tipo di risorsa che si sta creando (ad esempio **New AzureRmStorageAccount**). Può risultare più semplice toouse un cmdlet che è il tipo di risorsa specifico tooa poiché include parametri per le proprietà di hello che sono necessari per le nuove risorse hello. toouse **New-AzureRmResource**, è necessario conoscere tutti hello proprietà tooset senza che venga richiesto per loro.

Tuttavia, l'aggiunta di una risorsa tramite i cmdlet potrebbe causare confusione future perché hello nuova risorsa non esiste in un modello di gestione risorse. Si consiglia di definizione dell'infrastruttura di hello per la soluzione di Azure in un modello di gestione risorse. I modelli consentono tooreliably e distribuire ripetutamente la soluzione. Per questo argomento viene creato un account di archiviazione con un cmdlet di PowerShell, ma successivamente viene generato un modello dal gruppo di risorse.

Hello seguente cmdlet crea un account di archiviazione. Anziché il nome di hello illustrato nell'esempio hello, specificare un nome univoco per l'account di archiviazione hello. nome Hello deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare solo numeri e lettere minuscole. Se si utilizza il nome di hello illustrato nell'esempio hello, viene visualizzato un errore perché tale nome è già in uso.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Se occorre tooretrieve questa risorsa in un secondo momento, utilizzare hello seguente cmdlet:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Aggiungere un tag

Tag consentono di tooorganize le risorse in base a proprietà toodifferent. Ad esempio, è possibile diverse risorse in gruppi di risorse diversi appartenenti toohello stesso reparto. È possibile applicare un toomark reparto tag e il valore toothose risorse come appartenenti toohello stessa categoria. oppure indicare se una risorsa viene usata in un ambiente di produzione o di testing. In questo argomento si applica a una risorsa di tag tooonly, ma nell'ambiente in uso è molto probabile senso tooapply tag tooall le risorse.

Hello seguente cmdlet applica due account di archiviazione tooyour tag:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

I tag vengono aggiornati come un singolo oggetto. tooadd una risorsa tooa tag che include già tag, recuperare innanzitutto i tag esistenti hello. Aggiungere hello nuovo tag toohello oggetto contenente i tag esistenti hello e riapplicare tutte le risorse toohello tag hello.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Cercare le risorse

Hello utilizzare **Find-AzureRmResource** cmdlet tooretrieve risorse per le condizioni di ricerca diverso.

* tooget una risorsa in base al nome, fornire hello **ResourceNameContains** parametro:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget tutte le risorse di hello in un gruppo di risorse, fornire hello **ResourceGroupNameContains** parametro:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget tutte le risorse di hello con un nome di tag e il valore fornire hello **TagName** e **TagValue** parametri:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* risorse di hello tooall con un determinato tipo di risorsa, forniscono hello **ResourceType** parametro:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Bloccare una risorsa

Quando è necessario che una risorsa critica viene accidentalmente eliminata o modificata toomake, applicare una risorsa di blocco toohello. È possibile specificare **CanNotDelete** o **ReadOnly**.

i blocchi di gestione toocreate o delete, è necessario avere accesso troppo`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` azioni. Ruoli predefiniti, hello solo proprietario e amministratore di accesso utente vengono concesse tali azioni.

tooapply un blocco, utilizzare hello seguente cmdlet:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Hello risorsa bloccata nel precedente esempio hello non è possibile eliminare il blocco di hello viene rimosso. tooremove un blocco, utilizzare:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Per altre informazioni sull'impostazione di blocchi, vedere l'articolo su come [bloccare le risorse con Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Rimuovere risorse o un gruppo di risorse
È possibile rimuovere una risorsa o un gruppo di risorse. Quando si rimuove un gruppo di risorse, è inoltre possibile rimuovere tutte le risorse di hello all'interno del gruppo di risorse.

* una risorsa dal gruppo di risorse hello, utilizzare hello toodelete **Remove-AzureRmResource** cmdlet. Questo cmdlet Elimina risorsa hello, ma non elimina il gruppo di risorse hello.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete un gruppo di risorse e tutte le relative risorse, utilizzare hello **Remove AzureRmResourceGroup** cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Per entrambi i cmdlet, viene chiesto tooconfirm che si desidera tooremove hello risorsa o il gruppo. Se operazione hello consente di eliminare correttamente la risorsa hello o un gruppo di risorse, restituisce **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Eseguire script di Resource Manager con Automazione di Azure

In questo argomento illustra come operazioni di base tooperform le risorse con Azure PowerShell. Per gli scenari di gestione più avanzati, in genere desiderato toocreate uno script e riutilizzare tale script in base alle esigenze o in una pianificazione. [Automazione di Azure](../automation/automation-intro.md) fornisce un modo per consentire script tooautomate utilizzati di frequente per la gestione di soluzioni di Azure.

Hello argomenti seguenti illustrano come PowerShell tooeffectively toouse automazione di Azure e Gestione risorse di eseguire attività di gestione:

- Per informazioni sulla creazione di un runbook, vedere [Il primo runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Per informazioni sull'uso di raccolte di script, vedere [Raccolte di runbook e moduli per Automazione di Azure](../automation/automation-runbook-gallery.md).
- Per i runbook che avviare e arrestare le macchine virtuali, vedere [uno scenario di automazione di Azure: toocreate tag in formato JSON con una pianificazione per la macchina virtuale di Azure avvio e arresto](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Per informazioni sui runbook per l'avvio e l'arresto di macchine virtuali durante gli orari di minore attività, vedere [Soluzione Avvio/Arresto di macchine virtuali durante gli orari di minore attività in Automazione di Azure](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla creazione di modelli di gestione delle risorse, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md).
* toolearn sulla distribuzione di modelli, vedere [distribuire un'applicazione con il modello di gestione risorse di Azure](resource-group-template-deploy.md).
* È possibile spostare le risorse tooa nuovo gruppo di risorse esistente. Per esempi, vedere [tooNew di spostare risorse gruppo di risorse o sottoscrizione](resource-group-move-resources.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

