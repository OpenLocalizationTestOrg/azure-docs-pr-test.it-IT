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
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="4a63d-103">Come tooprotect DNS zone e record</span><span class="sxs-lookup"><span data-stu-id="4a63d-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="4a63d-104">Le zone e i record DNS sono risorse critiche.</span><span class="sxs-lookup"><span data-stu-id="4a63d-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="4a63d-105">L'eliminazione di una zona DNS o persino di un singolo record DNS può comportare un'interruzione del servizio totale.</span><span class="sxs-lookup"><span data-stu-id="4a63d-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="4a63d-106">È importante proteggere le zone e i record DNS critici da modifiche non autorizzate o accidentali.</span><span class="sxs-lookup"><span data-stu-id="4a63d-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="4a63d-107">Questo articolo spiega come DNS di Azure consente di tooprotect le zone DNS e i record in base a tali modifiche.</span><span class="sxs-lookup"><span data-stu-id="4a63d-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="4a63d-108">Si usano due potenti funzionalità di sicurezza fornite da Azure Resource Manager: il [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) e i [blocchi risorse](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="4a63d-109">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="4a63d-109">Role-based access control</span></span>

<span data-ttu-id="4a63d-110">Il Controllo degli accessi in base al ruolo di Azure consente una gestione degli accessi specifica per gli utenti, i gruppi e le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="4a63d-111">Usa tale controllo, è possibile concedere in modo preciso i quantità hello di accesso che gli utenti devono tooperform i processi.</span><span class="sxs-lookup"><span data-stu-id="4a63d-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="4a63d-112">Per altre informazioni su come il Controllo degli accessi in base al ruolo facilita la gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="4a63d-113">ruolo di 'collaboratore alla zona DNS ' Hello</span><span class="sxs-lookup"><span data-stu-id="4a63d-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="4a63d-114">Hello 'Collaboratore di zona DNS' è un ruolo predefinito fornito da Azure per la gestione delle risorse DNS.</span><span class="sxs-lookup"><span data-stu-id="4a63d-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="4a63d-115">L'assegnazione di utente tooa autorizzazioni di collaboratore di zona DNS o un gruppo consente di risorse DNS toomanage del gruppo, ma non le risorse di qualsiasi altro tipo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="4a63d-116">Si supponga, ad esempio, gruppo di risorse hello 'myzones' contiene cinque aree per Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4a63d-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="4a63d-117">Concessione hello 'Collaboratore di zona DNS' autorizzazioni toothat risorsa gruppo di amministratori DNS, consente il controllo completo su tali zone DNS.</span><span class="sxs-lookup"><span data-stu-id="4a63d-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="4a63d-118">Inoltre, evita la concessione di autorizzazioni non necessarie, ad esempio amministratore di hello DNS non è possibile creare o arrestare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4a63d-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="4a63d-119">autorizzazioni RBAC tooassign Hello più semplice modalità è [tramite il portale di Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="4a63d-120">Aprire il pannello hello 'controllo di accesso (IAM)' per il gruppo di risorse hello, quindi fare clic su 'Add', quindi selezionare il ruolo di 'collaboratore alla zona DNS ' hello e gli utenti di selezionare hello richiesto o gruppi toogrant le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4a63d-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Livello di gruppo di risorse RBAC tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="4a63d-122">Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4a63d-123">comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="4a63d-124">Controllo degli accessi in base al ruolo a livello di zona</span><span class="sxs-lookup"><span data-stu-id="4a63d-124">Zone level RBAC</span></span>

<span data-ttu-id="4a63d-125">Le regole RBAC Azure possono essere applicati tooa sottoscrizione, un gruppo o tooan singola risorsa.</span><span class="sxs-lookup"><span data-stu-id="4a63d-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="4a63d-126">Nel caso di hello di DNS di Azure, la risorsa può essere una zona DNS singoli, o anche un singolo set di record.</span><span class="sxs-lookup"><span data-stu-id="4a63d-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="4a63d-127">Si supponga, ad esempio, gruppo di risorse hello 'myzones' contiene hello zona 'contoso.com' e un sottozona 'customers.contoso.com' in cui vengono creati i record CNAME per ogni account del cliente.</span><span class="sxs-lookup"><span data-stu-id="4a63d-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="4a63d-128">Hello account utilizzato toomanage questi record CNAME devono essere assegnati record toocreate autorizzazioni solo zona 'customers.contoso.com' hello, non dovrebbe avere accesso toohello altre aree.</span><span class="sxs-lookup"><span data-stu-id="4a63d-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="4a63d-129">È possibile concedere le autorizzazioni RBAC a livello di zona tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="4a63d-130">Aprire Pannello di hello 'Controllo di accesso (IAM)' per la zona hello, quindi fare clic su 'Add', quindi selezionare il ruolo di 'collaboratore alla zona DNS ' hello e gli utenti di selezionare hello richiesto o gruppi toogrant le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4a63d-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![RBAC livello di zona DNS tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="4a63d-132">Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="4a63d-133">comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="4a63d-134">Controllo degli accessi in base al ruolo a livello di set di record</span><span class="sxs-lookup"><span data-stu-id="4a63d-134">Record set level RBAC</span></span>

<span data-ttu-id="4a63d-135">È possibile fare un ulteriore passo in avanti.</span><span class="sxs-lookup"><span data-stu-id="4a63d-135">We can go one step further.</span></span> <span data-ttu-id="4a63d-136">Prendere in considerazione messaggio posta elettronica per l'amministratore di Contoso Corporation, che necessita di accesso toohello MX e il record TXT al vertice hello della zona 'contoso.com' hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="4a63d-137">Lei non è necessario accedere tooany altri record MX o TXT o tooany record di qualsiasi altro tipo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="4a63d-138">DNS di Azure consente di autorizzazioni tooassign hello set di record, livello tooprecisely hello record hello amministratore di posta elettronica richiede l'accesso alla.</span><span class="sxs-lookup"><span data-stu-id="4a63d-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="4a63d-139">Hello posta privilegi di amministratore di controllare in modo accurato hello Lei necessita di ed è Impossibile toomake tutte le altre modifiche.</span><span class="sxs-lookup"><span data-stu-id="4a63d-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="4a63d-140">Autorizzazioni RBAC a livello di set di record possono essere configurate tramite hello portale Azure, usando il pulsante "hello"utenti nel Pannello di set di record hello:</span><span class="sxs-lookup"><span data-stu-id="4a63d-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Set di record livello RBAC tramite hello portale di Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="4a63d-142">Le autorizzazioni del Controllo degli accessi in base al ruolo a livello di set di record possono anche essere [concesse tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="4a63d-143">comando equivalente Hello è anche [disponibile tramite hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4a63d-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="4a63d-144">Ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="4a63d-144">Custom roles</span></span>

<span data-ttu-id="4a63d-145">ruolo incorporato e 'Collaboratore di zona DNS' Hello consente il controllo completo su una risorsa DNS.</span><span class="sxs-lookup"><span data-stu-id="4a63d-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="4a63d-146">Si è anche possibile toobuild ai propri clienti Azure i ruoli, tooprovide anche controllo più preciso.</span><span class="sxs-lookup"><span data-stu-id="4a63d-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="4a63d-147">Si consideri di nuovo esempio hello in cui viene creato un record CNAME nella zona hello 'customers.contoso.com' per ogni account cliente di Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4a63d-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="4a63d-148">Hello account utilizzato toomanage questi record CNAME devono essere concesse autorizzazioni toomanage CNAME solo i record.</span><span class="sxs-lookup"><span data-stu-id="4a63d-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="4a63d-149">È Impossibile toomodify record di altri tipi (ad esempio la modifica di record MX) o eseguire operazioni a livello di zona, ad esempio eliminazione zona.</span><span class="sxs-lookup"><span data-stu-id="4a63d-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="4a63d-150">Hello di esempio seguente viene illustrata una definizione di ruolo personalizzata per la gestione dei record CNAME:</span><span class="sxs-lookup"><span data-stu-id="4a63d-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="4a63d-151">proprietà Actions Hello definisce hello queste autorizzazioni specifiche DNS:</span><span class="sxs-lookup"><span data-stu-id="4a63d-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="4a63d-152">`Microsoft.Network/dnsZones/CNAME/*` concede il controllo completo sui record CNAME</span><span class="sxs-lookup"><span data-stu-id="4a63d-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="4a63d-153">`Microsoft.Network/dnsZones/read`concede le zone DNS tooread di autorizzazione, ma non toomodify li, abilitazione si toosee hello zona in cui hello CNAME viene creato.</span><span class="sxs-lookup"><span data-stu-id="4a63d-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="4a63d-154">le azioni rimanenti vengono copiate dal hello Hello [ruolo di collaboratore di zona DNS predefinita](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="4a63d-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="4a63d-155">Utilizzando un tooprevent di ruolo RBAC personalizzato l'eliminazione di record imposta mentre ancora consentendo toobe aggiornato non è un controllo effettivo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="4a63d-156">Impedisce l'eliminazione di set di record, ma non la relativa modifica.</span><span class="sxs-lookup"><span data-stu-id="4a63d-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="4a63d-157">Consentite modifiche includono l'aggiunta e la rimozione dei record dal set di record di hello, inclusa la rimozione di tutti i record tooleave un set di record "vuoto".</span><span class="sxs-lookup"><span data-stu-id="4a63d-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="4a63d-158">Questa operazione equivale all'eliminazione del record di hello impostato da un punto di vista la risoluzione DNS hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4a63d-159">Attualmente non è possibile definire le definizioni di ruolo personalizzata tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="4a63d-160">È possibile creare un ruolo personalizzato basato su questa definizione di ruolo tramite Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4a63d-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="4a63d-161">Può anche essere creato tramite hello CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="4a63d-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="4a63d-162">Hello ruolo può quindi essere assegnato in hello stesso modo come ruoli predefiniti, come descritto in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="4a63d-163">Per ulteriori informazioni su come toocreate, gestire e assegnare ruoli personalizzati, vedere [ruoli personalizzati in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="4a63d-164">Blocchi risorse</span><span class="sxs-lookup"><span data-stu-id="4a63d-164">Resource locks</span></span>

<span data-ttu-id="4a63d-165">In aggiunta tooRBAC, Gestione risorse di Azure supporta un altro tipo di controllo di sicurezza, vale a dire hello possibilità too'lock' risorse.</span><span class="sxs-lookup"><span data-stu-id="4a63d-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="4a63d-166">Dove RBAC regole consentono di azioni di hello toocontrol di utenti e gruppi specifici, blocchi di risorse sono risorse toohello applicato e hanno effetto su tutti gli utenti e ruoli.</span><span class="sxs-lookup"><span data-stu-id="4a63d-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="4a63d-167">Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="4a63d-168">Esistono due tipi di blocchi risorse: **DoNotDelete** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="4a63d-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="4a63d-169">Queste possono essere applicate zona DNS tooa o tooan singoli set di record.</span><span class="sxs-lookup"><span data-stu-id="4a63d-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="4a63d-170">Hello nelle sezioni seguenti vengono descritti diversi scenari comuni e come toosupport loro l'utilizzo dei blocchi di risorse.</span><span class="sxs-lookup"><span data-stu-id="4a63d-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="4a63d-171">Protezione da tutte le modifiche</span><span class="sxs-lookup"><span data-stu-id="4a63d-171">Protecting against all changes</span></span>

<span data-ttu-id="4a63d-172">tooprevent eventuali modifiche apportate, si applicano a una zona toohello blocco di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="4a63d-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="4a63d-173">In questo modo non è possibile creare nuovi set di record oppure modificare o eliminare i set di record esistenti.</span><span class="sxs-lookup"><span data-stu-id="4a63d-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="4a63d-174">Blocchi di risorse a livello di zona possono essere creati tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="4a63d-175">Dal pannello della zona DNS hello, fare clic su 'Blocchi', quindi 'Aggiungi':</span><span class="sxs-lookup"><span data-stu-id="4a63d-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Blocchi di risorse a livello di zona tramite hello portale di Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="4a63d-177">I blocchi risorse a livello di zona possono essere creati anche tramite Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4a63d-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="4a63d-178">Configurazione dei blocchi di risorse di Azure non è attualmente supportata tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="4a63d-179">Protezione di singoli record</span><span class="sxs-lookup"><span data-stu-id="4a63d-179">Protecting individual records</span></span>

<span data-ttu-id="4a63d-180">tooprevent un record DNS esistente, impostare per la modifica, applicare un set di record toohello di blocco di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="4a63d-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="4a63d-181">L'applicazione un tooa blocco DoNotDelete set di record non è un controllo effettivo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="4a63d-182">Impedisce hello set di record da in corso l'eliminazione, ma non impedisce che venga modificato.</span><span class="sxs-lookup"><span data-stu-id="4a63d-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="4a63d-183">Consentite modifiche includono l'aggiunta e la rimozione dei record dal set di record di hello, inclusa la rimozione di tutti i record tooleave un set di record "vuoto".</span><span class="sxs-lookup"><span data-stu-id="4a63d-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="4a63d-184">Questa operazione equivale all'eliminazione del record di hello impostato da un punto di vista la risoluzione DNS hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4a63d-185">I blocchi risorse a livello di set di record possono attualmente essere configurati solo tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a63d-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="4a63d-186">Non sono supportate nelle hello portale di Azure o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a63d-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="4a63d-187">Protezione dall'eliminazione di zone</span><span class="sxs-lookup"><span data-stu-id="4a63d-187">Protecting against zone deletion</span></span>

<span data-ttu-id="4a63d-188">Durante l'eliminazione di una zona DNS di Azure vengono eliminati anche tutti i set di record nella zona hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="4a63d-189">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="4a63d-189">This operation cannot be undone.</span></span>  <span data-ttu-id="4a63d-190">Eliminazione accidentale di una zona critica hello potenziali toohave ha un impatto significativo.</span><span class="sxs-lookup"><span data-stu-id="4a63d-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="4a63d-191">È pertanto molto importante tooprotect l'eliminazione accidentale di zona.</span><span class="sxs-lookup"><span data-stu-id="4a63d-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="4a63d-192">L'applicazione di una zona di tooa DoNotDelete blocco impedisce l'eliminazione zona hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="4a63d-193">Tuttavia, poiché i blocchi vengono ereditati dalle risorse figlio, si impedisce inoltre a qualsiasi set di record nella zona hello venga eliminato, che potrebbero essere indesiderate.</span><span class="sxs-lookup"><span data-stu-id="4a63d-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="4a63d-194">Inoltre, come descritto nella nota hello precedente, è anche inefficace poiché è ancora possano rimuovere i record dal set di record esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="4a63d-195">In alternativa, prendere in considerazione l'applicazione di un record di tooa DoNotDelete blocco impostata nell'area di hello, ad esempio set di record SOA hello.</span><span class="sxs-lookup"><span data-stu-id="4a63d-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="4a63d-196">Zona hello non può essere eliminata senza inoltre eliminati tutti i set di record hello, ciò consente di proteggere l'eliminazione della zona, consentendo al set di record all'interno di hello zona toobe liberamente modificato.</span><span class="sxs-lookup"><span data-stu-id="4a63d-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="4a63d-197">Se viene effettuato un tentativo di zona hello toodelete, Gestione risorse di Azure rileva questa verrebbe eliminerà anche i set di record SOA hello e blocchi hello chiamata perché è bloccato hello SOA.</span><span class="sxs-lookup"><span data-stu-id="4a63d-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="4a63d-198">Nessun set di record viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="4a63d-198">No record sets are deleted.</span></span>

<span data-ttu-id="4a63d-199">Hello comando PowerShell seguente crea un blocco di DoNotDelete record SOA hello di hello dato zona:</span><span class="sxs-lookup"><span data-stu-id="4a63d-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4a63d-200">Autorizzazioni di eliminazione di un altro modo l'eliminazione accidentale di zona tooprevent usando un operatore di ruolo personalizzata tooensure hello e servizio gli account utilizzati toomanage le zone non dispone della zona.</span><span class="sxs-lookup"><span data-stu-id="4a63d-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="4a63d-201">Quando è necessario toodelete una zona, è possibile applicare un'eliminazione in due passaggi, concedono autorizzazioni di eliminazione zona prima (nell'ambito di zona hello, l'eliminazione di un'area errata hello tooprevent) e il secondo toodelete hello fuso.</span><span class="sxs-lookup"><span data-stu-id="4a63d-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="4a63d-202">Secondo questo approccio presenta vantaggio di hello che funziona per tutte le zone accessibili da tali account, senza dovere tooremember toocreate eventuali blocchi.</span><span class="sxs-lookup"><span data-stu-id="4a63d-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="4a63d-203">Presenta gli svantaggi di hello che tutti gli account con autorizzazioni di eliminazione zona, ad esempio proprietario della sottoscrizione hello, è possono eliminare ancora accidentalmente una zona critica.</span><span class="sxs-lookup"><span data-stu-id="4a63d-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="4a63d-204">È possibile toouse entrambi gli approcci, blocchi di risorse e ruoli personalizzati, in hello stesso tempo, come una protezione di zona tooDNS approccio di difesa in profondità.</span><span class="sxs-lookup"><span data-stu-id="4a63d-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a63d-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a63d-205">Next steps</span></span>

* <span data-ttu-id="4a63d-206">Per ulteriori informazioni sull'utilizzo di accessi, vedere [Introduzione alla gestione di accesso nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="4a63d-207">Per altre informazioni sull'uso dei blocchi risorse, vedere [Bloccare le risorse con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4a63d-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

