---
title: aaaCreate ruoli personalizzati per Azure RBAC | Documenti Microsoft
description: "Informazioni su come ruoli personalizzati toodefine con il controllo di accesso di gestire più precisa gestione delle identità nella sottoscrizione di Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Creare ruoli personalizzati per il controllo degli accessi in base al ruolo di Azure
Creare un ruolo personalizzato nel controllo di accesso gestire (RBAC), se nessuno dei ruoli predefiniti hello soddisfano le esigenze di accesso specifico. È possibile creare ruoli personalizzati utilizzando [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md) (CLI), hello e [API REST](role-based-access-control-manage-access-rest.md). Proprio come i ruoli predefiniti, è possibile assegnare ruoli personalizzati toousers, gruppi e le applicazioni di sottoscrizione, gruppo di risorse e gli ambiti di risorsa. I ruoli personalizzati vengono archiviati in un tenant di Azure AD e possono essere condivisi tra le sottoscrizioni.

Ogni tenant può creare dei ruoli personalizzati too2000. 

Hello seguente illustra un ruolo personalizzato per il monitoraggio e il riavvio delle macchine virtuali:

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Azioni
Hello **azioni** proprietà di un ruolo personalizzato specifica hello Azure operazioni toowhich hello ruolo concede l'accesso. Si tratta di una raccolta di stringhe di operazione che identificano operazioni a protezione diretta dei provider di risorse di Azure. Stringhe di operazione seguono il formato di hello delle `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Le stringhe di operazione che contengono i caratteri jolly (\*) concedere l'accesso tooall operazioni che corrispondono a stringa hello dell'operazione. Ad esempio:

* `*/read`concede l'accesso tooread operazioni per tutti i tipi di risorse di tutti i provider di risorse di Azure.
* `Microsoft.Compute/*`concede l'accesso tooall operazioni per tutti i tipi di risorse di provider di risorse Microsoft. COMPUTE hello.
* `Microsoft.Network/*/read`concede l'accesso tooread operazioni per tutti i tipi di risorsa nel provider di risorse Microsoft. Network hello di Azure.
* `Microsoft.Compute/virtualMachines/*`concede l'accesso tooall operazioni delle macchine virtuali e i relativi tipi di risorsa figlio.
* `Microsoft.Web/sites/restart/Action`concede l'accesso di siti Web toorestart.

Utilizzare `Get-AzureRmProviderOperation` (in PowerShell) o `azure provider operations show` (in Azure CLI) operazioni toolist di provider di risorse di Azure. È anche possibile utilizzare questi comandi tooverify che una stringa di operazione è valida e tooexpand con caratteri jolly operazione stringhe.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Schermata PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Screenshot dell'interfaccia della riga di comando di Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Hello utilizzare **NotActions** proprietà se il set di hello di operazioni che si desidera tooallow è definito più facilmente escludendo operazioni con restrizioni. Hello accesso concesso da un ruolo personalizzato viene calcolato sottraendo hello **NotActions** operazioni hello **azioni** operazioni.

> [!NOTE]
> Se un utente è assegnato un ruolo che esclude in un'operazione **NotActions**e viene assegnato un secondo ruolo che concede l'accesso toohello utente hello stessa operazione è consentita tooperform tale operazione. **NotActions** non è un'istruzione deny regola: è semplicemente un modo pratico toocreate un set di operazioni consentite quando operazioni specifiche necessitano toobe esclusi.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Hello **AssignableScopes** proprietà del ruolo personalizzata hello specifica ambiti hello (sottoscrizioni, gruppi di risorse o di risorse) all'interno delle quali hello è disponibile per l'assegnazione ruolo personalizzato. È possibile rendere disponibili per l'assegnazione di ruolo personalizzata hello in solo le sottoscrizioni di hello o gruppi di risorse che richiedono e non gli utenti di confusione esperienza per rest hello di sottoscrizioni hello o gruppi di risorse.

Ecco alcuni esempi di ambiti assegnabili validi:

* "le sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e", "sottoscrizioni/e91d47c4-76f3-4271-a796-21b4ecfe3624" - rende disponibili per l'assegnazione ruolo hello in due sottoscrizioni.
* "le sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e" - rende disponibili per l'assegnazione ruolo hello in una singola sottoscrizione.
* "/ sottoscrizioni/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/di rete" - rende hello ruolo disponibile per l'assegnazione solo nel gruppo di risorse di rete hello.

> [!NOTE]
> È necessario usare almeno una sottoscrizione, un gruppo di risorse o un ID della risorsa.
>
>

## <a name="custom-roles-access-control"></a>Controllo di accesso ai ruoli personalizzati
Hello **AssignableScopes** proprietà del ruolo personalizzata hello controlla inoltre che può visualizzare, modificare ed eliminare il ruolo di hello.

* È necessario specificare gli utenti autorizzati a creare un ruolo personalizzato.
    I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono creare ruoli personalizzati da usare in questi ambiti.
    utente che Crea ruolo hello Hello deve tooperform in grado di toobe `Microsoft.Authorization/roleDefinition/write` operazione su tutti hello **AssignableScopes** del ruolo hello.
* È necessario specificare gli utenti autorizzati a modificare un ruolo personalizzato.
    I ruoli Proprietario e Amministratore Accessi utenti di sottoscrizioni, gruppi di risorse e risorse possono modificare i ruoli personalizzati in questi ambiti. Gli utenti devono hello in grado di tooperform toobe `Microsoft.Authorization/roleDefinition/write` operazione su tutti hello **AssignableScopes** di un ruolo personalizzato.
* Chi può visualizzare i ruoli personalizzati
    Tutti i ruoli predefiniti nel Controllo degli accessi in base al ruolo di Azure consentono la visualizzazione dei ruoli disponibili per l'assegnazione. Gli utenti possono eseguire hello `Microsoft.Authorization/roleDefinition/read` operazione in un ambito è possibile visualizzare i ruoli RBAC hello che sono disponibili per l'assegnazione in quell'ambito.

## <a name="see-also"></a>Vedere anche
* [Controllo di accesso basato su ruoli](role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.
* Informazioni su come accedere a toomanage con:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Interfaccia della riga di comando di Azure](role-based-access-control-manage-access-azure-cli.md)
  * [API REST](role-based-access-control-manage-access-rest.md)
* [Ruoli predefiniti](role-based-access-built-in-roles.md): ottenere informazioni sui ruoli hello forniti come standard in RBAC.
