---
title: aaaManage Role-Based Access Control (RBAC) with CLI di Azure | Documenti Microsoft
description: Informazioni su come interfaccia toomanage Role-Based Access Control (RBAC) with hello Azure della riga di comando dall'elenco di ruoli e ruolo azioni e assegnando ruoli toohello gli ambiti di sottoscrizione e dell'applicazione.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Controllare l'accesso basato sui ruoli con hello Azure interfaccia della riga di comando
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API REST](role-based-access-control-manage-access-rest.md)


Controllo di accesso basato sui ruoli (RBAC) è possibile utilizzare nel portale di Azure hello e API di gestione risorse di Azure toomanage accesso tooyour sottoscrizione e le risorse a un livello con granularità fine. Con questa funzionalità, è possibile concedere l'accesso per utenti, gruppi o entità servizio Active Directory assegnando toothem alcuni ruoli a un particolare ambito.

Prima di poter utilizzare hello Azure interfaccia della riga di comando (CLI) toomanage RBAC, è necessario disporre di hello seguenti prerequisiti:

* Usare la versione 0.8.8 o successiva dell'interfaccia della riga di comando di Azure. versione più recente di tooinstall hello e associare con la sottoscrizione di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager nell'interfaccia della riga di comando di Azure. Andare troppo[Using hello CLI di Azure con Gestione risorse di hello](../xplat-cli-azure-resource-manager.md) per altri dettagli.

## <a name="list-roles"></a>Elenco dei ruoli
### <a name="list-all-available-roles"></a>Elencare tutti i ruoli disponibili
toolist tutti i ruoli disponibili, utilizzare:

        azure role list

esempio Hello Mostra elenco hello di *tutti i ruoli disponibili*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Elencare le azioni di un ruolo
azioni di hello toolist di un ruolo, utilizzare:

    azure role show "<role name>"

Hello riportato di seguito azioni hello di hello *collaboratore* e *collaboratore alla macchina virtuale* ruoli.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Visualizzazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Elencare l'accesso
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Elencare le assegnazioni di ruoli valide per un gruppo di risorse
assegnazioni di ruolo hello toolist presenti in un gruppo di risorse, utilizzare:

    azure role assignment list --resource-group <resource group name>

Hello esempio seguente illustra le assegnazioni di ruolo hello in hello *registrazione al pharma-vendite-projecforcast* gruppo.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli di Azure per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Elencare i ruoli assegnati a un utente
le assegnazioni di ruolo hello toolist per un utente specifico e le assegnazioni di hello assegnati a gruppi dell'utente tooa, utilizzare:

    azure role assignment list --signInName <user email>

È inoltre possibile visualizzare le assegnazioni di ruolo vengono ereditate da gruppi modificando comando hello:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Hello riportato di seguito le assegnazioni di ruolo hello concesse toohello  *sameert@aaddemo.com*  utente. Sono inclusi i ruoli assegnati direttamente toohello utente e vengono ereditati dai gruppi.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di assegnazione di ruoli per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Concedere l'accesso
accesso toogrant dopo aver identificato il ruolo di hello che si desidera tooassign, utilizzare:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Assegnare un ruolo toogroup nell'ambito di sottoscrizione hello
tooassign un gruppo di ruoli tooa nell'ambito di sottoscrizione hello, utilizzare:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

esempio Hello assegna hello *lettore* ruolo troppo*Team di Christine Koch* in hello *sottoscrizione* ambito.

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Assegnare un'applicazione tooan ruolo nell'ambito di sottoscrizione hello
tooassign un'applicazione tooan ruolo nell'ambito di sottoscrizione hello, utilizzare:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

esempio Hello concede hello *collaboratore* ruolo tooan *AD Azure* applicazione hello selezionato una sottoscrizione.

 ![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli creata per applicazione](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Assegnare un utente tooa ruolo nell'ambito del gruppo di risorse hello
tooassign utente tooa ruolo nell'ambito di gruppo di risorse hello, utilizzare:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

esempio Hello concede hello *collaboratore alla macchina virtuale* ruolo troppo *samert@aaddemo.com*  utente hello *registrazione al Pharma-vendite-ProjectForcast* ambito del gruppo di risorse.

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per utente - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Assegnare un gruppo di tooa ruolo nell'ambito di risorsa hello
tooassign un gruppo di ruoli tooa nell'ambito di risorsa hello, utilizzare:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

esempio Hello concede hello *collaboratore alla macchina virtuale* ruolo tooan *AD Azure* gruppo un *subnet*.

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Assegnazione di ruoli di Azure creata per gruppo - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Rimuovere un accesso
tooremove un'assegnazione di ruolo, utilizzare:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

esempio Hello rimuove hello *collaboratore alla macchina virtuale* assegnazione di ruolo da hello  *sammert@aaddemo.com*  utente hello *registrazione al Pharma-vendite-ProjectForcast* gruppo di risorse.
esempio Hello rimuove quindi l'assegnazione di ruolo hello da un gruppo sottoscrizione hello.

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dell'assegnazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Creare un ruolo personalizzato
toocreate un ruolo personalizzato, utilizzare:

    azure role create --inputfile <file path>

esempio Hello crea un ruolo personalizzato chiamato *operatore macchina virtuale*. Concede l'accesso tooall leggere le operazioni di questo ruolo personalizzato *Microsoft. COMPUTE*, *Microsoft.Storage*, e *Network* provider e concede l'accesso alla risorsa toostart, riavviare e monitorare le macchine virtuali. Questo ruolo personalizzato può essere usato in due sottoscrizioni. In questo esempio viene usato un file JSON come input.

![JSON - Definizione di ruolo personalizzato - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Creazione di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Modificare un ruolo personalizzato
toomodify un ruolo personalizzato, utilizzare innanzitutto hello `azure role show` la definizione di ruolo tooretrieve del comando. In secondo luogo, verificare i file di definizione ruolo toohello hello modifiche desiderate. Infine, utilizzare `azure role set` toosave hello Modifica definizione di ruolo.

    azure role set --inputfile <file path>

esempio Hello aggiunge hello *Microsoft.Insights/diagnosticSettings/* operazione toohello **azioni**, toohello una sottoscrizione di Azure e **AssignableScopes**di ruolo personalizzata di hello operatore macchina virtuale.

![JSON - Modifica della definizione di ruolo personalizzata - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Impostazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Eliminare un ruolo personalizzato
toodelete un ruolo personalizzato, utilizzare innanzitutto hello `azure role show` comando toodetermine hello **ID** del ruolo hello. Utilizzare quindi hello `azure role delete` ruolo hello toodelete di comando specificando hello **ID**.

esempio Hello rimuove hello *operatore macchina virtuale* ruolo personalizzato.

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Eliminazione dei ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Elencare ruoli personalizzati
i ruoli di hello toolist che sono disponibili per l'assegnazione a un ambito, usano hello `azure role list` comando.

Hello comando seguente elenca tutti i ruoli che sono disponibili per l'assegnazione nella sottoscrizione hello selezionato.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco di ruoli di Azure - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

Nell'esempio seguente di hello, hello *operatore macchina virtuale* ruolo personalizzato non è disponibile in hello *Production4* sottoscrizione perché tale sottoscrizione non è in hello  **AssignableScopes** del ruolo hello.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Riga di comando di Controllo degli accessi in base al ruolo di Azure - Elenco dei ruoli di Azure per i ruoli personalizzati - Schermata](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

