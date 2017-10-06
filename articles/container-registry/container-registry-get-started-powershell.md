---
title: repository del Registro di sistema di contenitore aaaAzure | Documenti Microsoft
description: Il repository del Registro di sistema di Azure contenitore toouse per le immagini Docker
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Creare un registro di sistema contenitore Docker privata mediante hello Azure PowerShell
Usare i comandi in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate del Registro di sistema un contenitore e gestire le impostazioni dal computer Windows. È anche possibile creare e gestire i registri di contenitore usando hello [portale di Azure](container-registry-get-started-portal.md), hello [CLI di Azure](container-registry-get-started-azure-cli.md), o a livello di codice con hello contenitore del Registro di sistema [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Per lo sfondo e i concetti, vedere [hello Panoramica](container-registry-intro.md)
* Per un elenco completo dei cmdlet supportati, vedere [AzureRM.ContainerRegistry](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Prerequisiti
* **Azure PowerShell**: tooinstall e acquisire familiarità con Azure PowerShell, vedere hello [le istruzioni di installazione](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Accedi tooyour sottoscrizione di Azure eseguendo `Login-AzureRMAccount`. Per altre informazioni, vedere [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep) (Introduzione ad Azure PowerShell).
* **Gruppo di risorse**: creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md#resource-groups) prima di creare un registro di contenitori o usare un gruppo di risorse esistente. Verificare che il gruppo di risorse hello è in una posizione in cui è hello servizio Registro di sistema contenitore [disponibile](https://azure.microsoft.com/regions/services/). toocreate un gruppo di risorse con Azure PowerShell, vedere [hello PowerShell riferimento](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Account di archiviazione** (facoltativo): creare un Azure standard [account di archiviazione](../storage/common/storage-introduction.md) tooback hello contenitore nel Registro di sistema hello nello stesso percorso. Se non si specifica un account di archiviazione durante la creazione di un registro di sistema `New-AzureRMContainerRegistry`, comando hello viene creata una automaticamente. uno spazio di archiviazione toocreate account usando PowerShell, vedere [hello PowerShell riferimento](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Archiviazione Premium non è attualmente supportata.
* **Entità servizio** (facoltativo): quando si crea un registro con PowerShell, per impostazione predefinita il registro non è configurato per l'accesso. A seconda delle esigenze, è possibile assegnare un registro tooa principale di servizio Azure Active Directory esistente, creare e assegnare una nuova. In alternativa, è possibile abilitare l'account amministratore del Registro di sistema di hello. Vedere hello sezioni più avanti in questo articolo. Per ulteriori informazioni sull'accesso del Registro di sistema, vedere [autentica con del Registro di sistema di hello contenitore](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Creare un registro di contenitori
Eseguire hello `New-AzureRMContainerRegistry` toocreate comando del Registro di sistema un contenitore.

> [!TIP]
> Quando si crea un registro, specificare un nome di dominio univoco globale di primo livello, contenente solo lettere e numeri. nome del Registro di sistema Hello negli esempi di hello è `MyRegistry`, ma sostituire un nome univoco del proprio.
>
>

Hello comando utilizza hello del Registro di sistema di numero minimo di parametri toocreate contenitore seguente `MyRegistry` nel gruppo di risorse hello `MyResourceGroup` in hello centro-meridionali percorso:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` è facoltativo. Se non viene specificato, viene creato un account di archiviazione con un nome composto dal nome del Registro di sistema hello e un timestamp in hello specificato gruppo di risorse.

## <a name="assign-a-service-principal"></a>Assegnare un'entità servizio
Utilizzare i comandi di PowerShell tooassign di Azure Active Directory [dell'entità servizio](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa Registro di sistema. Hello dell'entità servizio in questi esempi viene assegnato il ruolo di proprietario hello, ma è possibile assegnare [altri ruoli](../active-directory/role-based-access-control-configure.md) se si desidera.

### <a name="create-a-service-principal"></a>Creare un’entità servizio
Nel comando seguente di hello, viene creata una nuova entità servizio. Specificare una password complessa con hello `-Password` parametro.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Assegnare un'entità servizio nuova o esistente
È possibile assegnare un nuovo oggetto o un registro di sistema di tooa dell'entità servizio esistente. tooassign è proprietario ruolo accesso toohello Registro di sistema, eseguire una toohello simile comando riportato di seguito:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Accedi al Registro di sistema toohello entità servizio hello
Dopo l'assegnazione del Registro di sistema di hello servizio toohello principale, è possibile accedere tramite hello comando seguente:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Gestire le credenziali di amministratore
Per ogni registro di contenitori viene creato automaticamente un account amministratore che è disabilitato per impostazione predefinita. Hello esempi seguenti mostrano i comandi di PowerShell le credenziali di amministratore hello toomanage per il Registro di sistema del contenitore.

### <a name="obtain-admin-user-credentials"></a>Ottenere le credenziali di utente amministratore
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Abilitare l'utente amministratore per un registro esistente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Disabilitare l'utente amministratore per un registro esistente
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Passaggi successivi
* [La prima immagine usando Docker CLI hello push](container-registry-get-started-docker-cli.md)
