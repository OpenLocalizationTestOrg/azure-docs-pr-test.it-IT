---
title: aaaProtecting record e zone DNS | Documenti Microsoft
description: Il record e zone DNS tooprotect imposta DNS di Microsoft Azure.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a>Come tooprotect DNS zone e record

Le zone e i record DNS sono risorse critiche. L'eliminazione di una zona DNS o persino di un singolo record DNS può comportare un'interruzione del servizio totale.  È importante proteggere le zone e i record DNS critici da modifiche non autorizzate o accidentali.

Questo articolo spiega come DNS di Azure consente di tooprotect le zone DNS e i record in base a tali modifiche.  Si usano due potenti funzionalità di sicurezza fornite da Azure Resource Manager: il [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) e i [blocchi risorse](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Controllo degli accessi in base al ruolo

Il Controllo degli accessi in base al ruolo di Azure consente una gestione degli accessi specifica per gli utenti, i gruppi e le risorse di Azure. Usa tale controllo, è possibile concedere in modo preciso i quantità hello di accesso che gli utenti devono tooperform i processi. Per altre informazioni su come il Controllo degli accessi in base al ruolo facilita la gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>ruolo di 'collaboratore alla zona DNS ' Hello

Hello 'Collaboratore di zona DNS' è un ruolo predefinito fornito da Azure per la gestione delle risorse DNS.  L'assegnazione di utente tooa autorizzazioni di collaboratore di zona DNS o un gruppo consente di risorse DNS toomanage del gruppo, ma non le risorse di qualsiasi altro tipo.

Si supponga, ad esempio, gruppo di risorse hello 'myzones' contiene cinque aree per Contoso Corporation. Concessione hello 'Collaboratore di zona DNS' autorizzazioni toothat risorsa gruppo di amministratori DNS, consente il controllo completo su tali zone DNS. Inoltre, evita la concessione di autorizzazioni non necessarie, ad esempio amministratore di hello DNS non è possibile creare o arrestare le macchine virtuali.

autorizzazioni RBAC tooassign Hello più semplice modalità è [tramite il portale di Azure hello](../active-directory/role-based-access-control-configure.md).  Aprire il pannello hello 'controllo di accesso (IAM)' per il gruppo di risorse hello, quindi fare clic su 'Add', quindi selezionare il ruolo di 'collaboratore alla zona DNS ' hello e gli utenti di selezionare hello richiesto o gruppi toogrant le autorizzazioni.

![Livello di gruppo di risorse RBAC tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac1.png)

Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>Controllo degli accessi in base al ruolo a livello di zona

Le regole RBAC Azure possono essere applicati tooa sottoscrizione, un gruppo o tooan singola risorsa. Nel caso di hello di DNS di Azure, la risorsa può essere una zona DNS singoli, o anche un singolo set di record.

Si supponga, ad esempio, gruppo di risorse hello 'myzones' contiene hello zona 'contoso.com' e un sottozona 'customers.contoso.com' in cui vengono creati i record CNAME per ogni account del cliente.  Hello account utilizzato toomanage questi record CNAME devono essere assegnati record toocreate autorizzazioni solo zona 'customers.contoso.com' hello, non dovrebbe avere accesso toohello altre aree.

È possibile concedere le autorizzazioni RBAC a livello di zona tramite hello portale di Azure.  Aprire Pannello di hello 'Controllo di accesso (IAM)' per la zona hello, quindi fare clic su 'Add', quindi selezionare il ruolo di 'collaboratore alla zona DNS ' hello e gli utenti di selezionare hello richiesto o gruppi toogrant le autorizzazioni.

![RBAC livello di zona DNS tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac2.png)

Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>Controllo degli accessi in base al ruolo a livello di set di record

È possibile fare un ulteriore passo in avanti. Prendere in considerazione messaggio posta elettronica per l'amministratore di Contoso Corporation, che necessita di accesso toohello MX e il record TXT al vertice hello della zona 'contoso.com' hello.  Lei non è necessario accedere tooany altri record MX o TXT o tooany record di qualsiasi altro tipo.  DNS di Azure consente di autorizzazioni tooassign hello set di record, livello tooprecisely hello record hello amministratore di posta elettronica richiede l'accesso alla.  Hello posta privilegi di amministratore di controllare in modo accurato hello Lei necessita di ed è Impossibile toomake tutte le altre modifiche.

Autorizzazioni RBAC a livello di set di record possono essere configurate tramite hello portale Azure, usando il pulsante "hello"utenti nel Pannello di set di record hello:

![Set di record livello RBAC tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac3.png)

Le autorizzazioni del Controllo degli accessi in base al ruolo a livello di set di record possono anche essere [concesse tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Ruoli personalizzati

ruolo incorporato e 'Collaboratore di zona DNS' Hello consente il controllo completo su una risorsa DNS. Si è anche possibile toobuild ai propri clienti Azure i ruoli, tooprovide anche controllo più preciso.

Si consideri di nuovo esempio hello in cui viene creato un record CNAME nella zona hello 'customers.contoso.com' per ogni account cliente di Contoso Corporation.  Hello account utilizzato toomanage questi record CNAME devono essere concesse autorizzazioni toomanage CNAME solo i record.  È Impossibile toomodify record di altri tipi (ad esempio la modifica di record MX) o eseguire operazioni a livello di zona, ad esempio eliminazione zona.

Hello di esempio seguente viene illustrata una definizione di ruolo personalizzata per la gestione dei record CNAME:

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

proprietà Actions Hello definisce hello queste autorizzazioni specifiche DNS:

* `Microsoft.Network/dnsZones/CNAME/*` concede il controllo completo sui record CNAME
* `Microsoft.Network/dnsZones/read`concede le zone DNS tooread di autorizzazione, ma non toomodify li, abilitazione si toosee hello zona in cui hello CNAME viene creato.

le azioni rimanenti vengono copiate dal hello Hello [ruolo di collaboratore di zona DNS predefinita](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Utilizzando un tooprevent di ruolo RBAC personalizzato l'eliminazione di record imposta mentre ancora consentendo toobe aggiornato non è un controllo effettivo. Impedisce l'eliminazione di set di record, ma non la relativa modifica.  Consentite modifiche includono l'aggiunta e la rimozione dei record dal set di record di hello, inclusa la rimozione di tutti i record tooleave un set di record "vuoto". Questa operazione equivale all'eliminazione del record di hello impostato da un punto di vista la risoluzione DNS hello.

Attualmente non è possibile definire le definizioni di ruolo personalizzata tramite hello portale di Azure. È possibile creare un ruolo personalizzato basato su questa definizione di ruolo tramite Azure PowerShell:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Può anche essere creato tramite hello CLI di Azure:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello ruolo può quindi essere assegnato in hello stesso modo come ruoli predefiniti, come descritto in precedenza in questo articolo.

Per ulteriori informazioni su come toocreate, gestire e assegnare ruoli personalizzati, vedere [ruoli personalizzati in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Blocchi risorse

In aggiunta tooRBAC, Gestione risorse di Azure supporta un altro tipo di controllo di sicurezza, vale a dire hello possibilità too'lock' risorse. Dove RBAC regole consentono di azioni di hello toocontrol di utenti e gruppi specifici, blocchi di risorse sono risorse toohello applicato e hanno effetto su tutti gli utenti e ruoli. Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md).

Esistono due tipi di blocchi risorse: **DoNotDelete** e **ReadOnly**. Queste possono essere applicate zona DNS tooa o tooan singoli set di record.  Hello nelle sezioni seguenti vengono descritti diversi scenari comuni e come toosupport loro l'utilizzo dei blocchi di risorse.

### <a name="protecting-against-all-changes"></a>Protezione da tutte le modifiche

tooprevent eventuali modifiche apportate, si applicano a una zona toohello blocco di sola lettura.  In questo modo non è possibile creare nuovi set di record oppure modificare o eliminare i set di record esistenti.

Blocchi di risorse a livello di zona possono essere creati tramite hello portale di Azure.  Dal pannello della zona DNS hello, fare clic su 'Blocchi', quindi 'Aggiungi':

![Blocchi di risorse a livello di zona tramite hello portale di Azure](./media/dns-protect-zones-recordsets/locks1.png)

I blocchi risorse a livello di zona possono essere creati anche tramite Azure PowerShell:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Configurazione dei blocchi di risorse di Azure non è attualmente supportata tramite hello CLI di Azure.

### <a name="protecting-individual-records"></a>Protezione di singoli record

tooprevent un record DNS esistente, impostare per la modifica, applicare un set di record toohello di blocco di sola lettura.

> [!NOTE]
> L'applicazione un tooa blocco DoNotDelete set di record non è un controllo effettivo. Impedisce hello set di record da in corso l'eliminazione, ma non impedisce che venga modificato.  Consentite modifiche includono l'aggiunta e la rimozione dei record dal set di record di hello, inclusa la rimozione di tutti i record tooleave un set di record "vuoto". Questa operazione equivale all'eliminazione del record di hello impostato da un punto di vista la risoluzione DNS hello.

I blocchi risorse a livello di set di record possono attualmente essere configurati solo tramite Azure PowerShell.  Non sono supportate nelle hello portale di Azure o CLI di Azure.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Protezione dall'eliminazione di zone

Durante l'eliminazione di una zona DNS di Azure vengono eliminati anche tutti i set di record nella zona hello.  Questa operazione non può essere annullata.  Eliminazione accidentale di una zona critica hello potenziali toohave ha un impatto significativo.  È pertanto molto importante tooprotect l'eliminazione accidentale di zona.

L'applicazione di una zona di tooa DoNotDelete blocco impedisce l'eliminazione zona hello.  Tuttavia, poiché i blocchi vengono ereditati dalle risorse figlio, si impedisce inoltre a qualsiasi set di record nella zona hello venga eliminato, che potrebbero essere indesiderate.  Inoltre, come descritto nella nota hello precedente, è anche inefficace poiché è ancora possano rimuovere i record dal set di record esistenti hello.

In alternativa, prendere in considerazione l'applicazione di un record di tooa DoNotDelete blocco impostata nell'area di hello, ad esempio set di record SOA hello.  Zona hello non può essere eliminata senza inoltre eliminati tutti i set di record hello, ciò consente di proteggere l'eliminazione della zona, consentendo al set di record all'interno di hello zona toobe liberamente modificato. Se viene effettuato un tentativo di zona hello toodelete, Gestione risorse di Azure rileva questa verrebbe eliminerà anche i set di record SOA hello e blocchi hello chiamata perché è bloccato hello SOA.  Nessun set di record viene eliminato.

Hello comando PowerShell seguente crea un blocco di DoNotDelete record SOA hello di hello dato zona:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Autorizzazioni di eliminazione di un altro modo l'eliminazione accidentale di zona tooprevent usando un operatore di ruolo personalizzata tooensure hello e servizio gli account utilizzati toomanage le zone non dispone della zona. Quando è necessario toodelete una zona, è possibile applicare un'eliminazione in due passaggi, concedono autorizzazioni di eliminazione zona prima (nell'ambito di zona hello, l'eliminazione di un'area errata hello tooprevent) e il secondo toodelete hello fuso.

Secondo questo approccio presenta vantaggio di hello che funziona per tutte le zone accessibili da tali account, senza dovere tooremember toocreate eventuali blocchi. Presenta gli svantaggi di hello che tutti gli account con autorizzazioni di eliminazione zona, ad esempio proprietario della sottoscrizione hello, è possono eliminare ancora accidentalmente una zona critica.

È possibile toouse entrambi gli approcci, blocchi di risorse e ruoli personalizzati, in hello stesso tempo, come una protezione di zona tooDNS approccio di difesa in profondità.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sull'utilizzo di accessi, vedere [Introduzione alla gestione di accesso nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).
* Per altre informazioni sull'uso dei blocchi risorse, vedere [Bloccare le risorse con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

