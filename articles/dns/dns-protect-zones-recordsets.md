---
title: Protezione di record e zone DNS | Microsoft Docs
description: Come proteggere le zone e i set di record in DNS di Microsoft Azure.
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
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="4ad49-103">Come proteggere le zone e i record DNS</span><span class="sxs-lookup"><span data-stu-id="4ad49-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="4ad49-104">Le zone e i record DNS sono risorse critiche.</span><span class="sxs-lookup"><span data-stu-id="4ad49-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="4ad49-105">L'eliminazione di una zona DNS o persino di un singolo record DNS può comportare un'interruzione del servizio totale.</span><span class="sxs-lookup"><span data-stu-id="4ad49-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="4ad49-106">È importante proteggere le zone e i record DNS critici da modifiche non autorizzate o accidentali.</span><span class="sxs-lookup"><span data-stu-id="4ad49-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="4ad49-107">Questo articolo spiega come è possibile proteggere i record e le zone DNS da queste modifiche con DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="4ad49-108">Si usano due potenti funzionalità di sicurezza fornite da Azure Resource Manager: il [controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md) e i [blocchi risorse](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="4ad49-109">Controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="4ad49-109">Role-based access control</span></span>

<span data-ttu-id="4ad49-110">Il Controllo degli accessi in base al ruolo di Azure consente una gestione degli accessi specifica per gli utenti, i gruppi e le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="4ad49-111">Il Controllo degli accessi in base al ruolo permette di concedere agli utenti esattamente il livello di accesso necessario per eseguire i propri processi.</span><span class="sxs-lookup"><span data-stu-id="4ad49-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="4ad49-112">Per altre informazioni su come il Controllo degli accessi in base al ruolo facilita la gestione degli accessi, vedere l'articolo relativo al [Controllo degli accessi in base al ruolo](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="4ad49-113">Il ruolo di "collaboratore zona DNS"</span><span class="sxs-lookup"><span data-stu-id="4ad49-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="4ad49-114">Il ruolo di "collaboratore zona DNS" è un ruolo predefinito fornito da Azure per la gestione delle risorse DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="4ad49-115">L'assegnazione di autorizzazioni come collaboratore zona DNS a un utente o a un gruppo consente a questo gruppo di gestire le risorse DNS, ma non le risorse di altro tipo.</span><span class="sxs-lookup"><span data-stu-id="4ad49-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="4ad49-116">Si supponga, ad esempio, che il gruppo di risorse "zonepersonali" contenga cinque zone per Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4ad49-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="4ad49-117">La concessione di autorizzazioni come "collaboratore zona DNS" all'amministratore DNS per questo gruppo di risorse consente il controllo completo su queste zone DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="4ad49-118">Si evita anche di concedere autorizzazioni non necessarie, ad esempio l'amministratore DNS non può creare o arrestare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4ad49-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="4ad49-119">Il modo più semplice per assegnare le autorizzazioni del Controllo degli accessi in base al ruolo è [tramite il portale di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="4ad49-120">Aprire il pannello "Controllo di accesso (IAM)" per il gruppo di risorse, fare clic su "Aggiungi", quindi selezionare il ruolo di "collaboratore zona DNS" e selezionare gli utenti o i gruppi necessari per concedere le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4ad49-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Controllo degli accessi in base al ruolo a livello di gruppo di risorse tramite il portale di Azure](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="4ad49-122">Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4ad49-123">Il comando equivalente è [disponibile anche tramite l'interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="4ad49-124">Controllo degli accessi in base al ruolo a livello di zona</span><span class="sxs-lookup"><span data-stu-id="4ad49-124">Zone level RBAC</span></span>

<span data-ttu-id="4ad49-125">Le regole del Controllo degli accessi in base al ruolo di Azure possono essere applicate a una sottoscrizione, a un gruppo di risorse o a una singola risorsa.</span><span class="sxs-lookup"><span data-stu-id="4ad49-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="4ad49-126">Nel caso di DNS di Azure, questa risorsa può essere una singola zona DNS o persino un singolo set di record.</span><span class="sxs-lookup"><span data-stu-id="4ad49-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="4ad49-127">Si supponga, ad esempio, che il gruppo di risorse "zone personali" contenga la zona "contoso.com" e una sottozona "customers.contoso.com" in cui vengono creati i record CNAME per ciascun account cliente.</span><span class="sxs-lookup"><span data-stu-id="4ad49-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="4ad49-128">All'account usato per gestire i record CNAME devono essere assegnate le autorizzazioni per creare i record solo nella zona "customers.contoso.com", senza consentire l'accesso alle altre zone.</span><span class="sxs-lookup"><span data-stu-id="4ad49-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="4ad49-129">È possibile concedere le autorizzazioni del Controllo degli accessi in base al ruolo a livello di zona tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="4ad49-130">Aprire il pannello "Controllo di accesso (IAM)" per la zona, fare clic su "Aggiungi", quindi selezionare il ruolo di "collaboratore zona DNS" e selezionare gli utenti o i gruppi necessari per concedere le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="4ad49-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Controllo degli accessi in base al ruolo a livello di zona DNS tramite il portale di Azure](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="4ad49-132">Queste autorizzazioni possono essere concesse anche [tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="4ad49-133">Il comando equivalente è [disponibile anche tramite l'interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="4ad49-134">Controllo degli accessi in base al ruolo a livello di set di record</span><span class="sxs-lookup"><span data-stu-id="4ad49-134">Record set level RBAC</span></span>

<span data-ttu-id="4ad49-135">È possibile fare un ulteriore passo in avanti.</span><span class="sxs-lookup"><span data-stu-id="4ad49-135">We can go one step further.</span></span> <span data-ttu-id="4ad49-136">L'amministratore di posta elettronica per Contoso Corporation, ad esempio, necessita dell'accesso ai record MX e TXT al vertice della zona "contoso.com".</span><span class="sxs-lookup"><span data-stu-id="4ad49-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="4ad49-137">Non ha necessità di accedere agli altri record MX o TXT oppure ai record di altro tipo.</span><span class="sxs-lookup"><span data-stu-id="4ad49-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="4ad49-138">DNS di Azure consente di assegnare le autorizzazioni a livello di set di record con precisione per i record a cui l'amministratore di posta elettronica deve accedere.</span><span class="sxs-lookup"><span data-stu-id="4ad49-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="4ad49-139">All'amministratore di posta elettronica viene concesso esattamente il controllo di cui necessita, senza poter apportare altre modifiche.</span><span class="sxs-lookup"><span data-stu-id="4ad49-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="4ad49-140">Le autorizzazioni del Controllo degli accessi in base al ruolo a livello di set di record possono essere configurate tramite il portale di Azure, usando il pulsante "Utenti" nel pannello dei set di record:</span><span class="sxs-lookup"><span data-stu-id="4ad49-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Controllo degli accessi in base al ruolo a livello di set di record tramite il portale di Azure](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="4ad49-142">Le autorizzazioni del Controllo degli accessi in base al ruolo a livello di set di record possono anche essere [concesse tramite Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="4ad49-143">Il comando equivalente è [disponibile anche tramite l'interfaccia della riga di comando di Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="4ad49-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="4ad49-144">Ruoli personalizzati</span><span class="sxs-lookup"><span data-stu-id="4ad49-144">Custom roles</span></span>

<span data-ttu-id="4ad49-145">Il ruolo di "collaboratore zona DNS" predefinito consente il controllo completo su una risorsa DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="4ad49-146">È anche possibile creare ruoli di Azure di clienti, per fornire un controllo più capillare.</span><span class="sxs-lookup"><span data-stu-id="4ad49-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="4ad49-147">Si consideri di nuovo l'esempio in cui viene creato un record CNAME nella zona "customers.contoso.com" per ogni account cliente di Contoso Corporation.</span><span class="sxs-lookup"><span data-stu-id="4ad49-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="4ad49-148">All'account usato per gestire i record CNAME deve essere concessa l'autorizzazione per gestire solo i record CNAME.</span><span class="sxs-lookup"><span data-stu-id="4ad49-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="4ad49-149">Non è quindi possibile modificare i record di altri tipi, ad esempio i record MX, oppure eseguire operazioni a livello di zona, ad esempio l'eliminazione di una zona.</span><span class="sxs-lookup"><span data-stu-id="4ad49-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="4ad49-150">L'esempio seguente illustra la definizione di un ruolo personalizzato per gestire solo record CNAME:</span><span class="sxs-lookup"><span data-stu-id="4ad49-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="4ad49-151">La proprietà Actions definisce le autorizzazioni specifiche di DNS seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ad49-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="4ad49-152">`Microsoft.Network/dnsZones/CNAME/*` concede il controllo completo sui record CNAME</span><span class="sxs-lookup"><span data-stu-id="4ad49-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="4ad49-153">`Microsoft.Network/dnsZones/read` concede l'autorizzazione per leggere le zone DNS, ma non per modificarle, consentendo di visualizzare l'area in cui viene creato il record CNAME.</span><span class="sxs-lookup"><span data-stu-id="4ad49-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="4ad49-154">Le azioni rimanenti vengono copiate dal [ruolo di collaboratore zona DNS predefinito](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="4ad49-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="4ad49-155">Non è efficace usare un ruolo personalizzato del Controllo degli accessi in base al ruolo per impedire l'eliminazione di set di record, consentendo tuttavia il relativo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4ad49-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="4ad49-156">Impedisce l'eliminazione di set di record, ma non la relativa modifica.</span><span class="sxs-lookup"><span data-stu-id="4ad49-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="4ad49-157">Alcune modifiche consentite sono l'aggiunta e la rimozione di record dal set di record, inclusa la rimozione di tutti i record per ottenere un set di record "vuoto".</span><span class="sxs-lookup"><span data-stu-id="4ad49-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4ad49-158">Questo è lo stesso effetto ottenuto eliminando il set di record dal punto di vista della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4ad49-159">Attualmente non è possibile specificare definizioni di ruoli personalizzati tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="4ad49-160">È possibile creare un ruolo personalizzato basato su questa definizione di ruolo tramite Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4ad49-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="4ad49-161">Può anche essere creato tramite l'interfaccia della riga di comando di Azure:</span><span class="sxs-lookup"><span data-stu-id="4ad49-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="4ad49-162">Il ruolo può quindi essere assegnato come avviene per i ruoli predefiniti, come descritto in precedenza in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4ad49-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="4ad49-163">Per altre informazioni su come creare, gestire e assegnare ruoli personalizzati, vedere [Ruoli personalizzati nel Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="4ad49-164">Blocchi risorse</span><span class="sxs-lookup"><span data-stu-id="4ad49-164">Resource locks</span></span>

<span data-ttu-id="4ad49-165">Oltre al Controllo degli accessi in base al ruolo, Azure Resource Manager supporta un altro tipo di controllo di sicurezza, vale a dire la possibilità di "bloccare" le risorse.</span><span class="sxs-lookup"><span data-stu-id="4ad49-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="4ad49-166">Le regole del Controllo degli accessi in base al ruolo di Azure consentono di controllare le azioni di utenti e gruppi specifici,mentre i blocchi risorse vengono applicati alla risorsa e hanno effetto su tutti gli utenti e i ruoli.</span><span class="sxs-lookup"><span data-stu-id="4ad49-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="4ad49-167">Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="4ad49-168">Esistono due tipi di blocchi risorse: **DoNotDelete** e **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="4ad49-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="4ad49-169">Questi blocchi possono essere applicati a una zona DNS o a un singolo set di record.</span><span class="sxs-lookup"><span data-stu-id="4ad49-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="4ad49-170">Le sezioni seguenti descrivono diversi scenari comuni e come supportarli usando i blocchi risorse.</span><span class="sxs-lookup"><span data-stu-id="4ad49-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="4ad49-171">Protezione da tutte le modifiche</span><span class="sxs-lookup"><span data-stu-id="4ad49-171">Protecting against all changes</span></span>

<span data-ttu-id="4ad49-172">Per evitare che vengano apportate modifiche, applicare un blocco ReadOnly alla zona.</span><span class="sxs-lookup"><span data-stu-id="4ad49-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="4ad49-173">In questo modo non è possibile creare nuovi set di record oppure modificare o eliminare i set di record esistenti.</span><span class="sxs-lookup"><span data-stu-id="4ad49-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="4ad49-174">I blocchi risorse a livello di zona possono essere creati tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="4ad49-175">Nel pannello Zona DNS, fare clic su "Blocchi", quindi su "Aggiungi":</span><span class="sxs-lookup"><span data-stu-id="4ad49-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Blocchi risorse a livello di zona tramite il portale di Azure](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="4ad49-177">I blocchi risorse a livello di zona possono essere creati anche tramite Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4ad49-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="4ad49-178">La configurazione di blocchi risorse di Azure non è attualmente supportata tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="4ad49-179">Protezione di singoli record</span><span class="sxs-lookup"><span data-stu-id="4ad49-179">Protecting individual records</span></span>

<span data-ttu-id="4ad49-180">Per evitare che venga modificato un set di record DNS esistente, impostare il blocco ReadOnly al set di record.</span><span class="sxs-lookup"><span data-stu-id="4ad49-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad49-181">L'applicazione di un blocco DoNotDelete a un set di record non è un controllo efficace.</span><span class="sxs-lookup"><span data-stu-id="4ad49-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="4ad49-182">Impedisce l'eliminazione del set di record, ma non impedisce che venga modificato.</span><span class="sxs-lookup"><span data-stu-id="4ad49-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="4ad49-183">Alcune modifiche consentite sono l'aggiunta e la rimozione di record dal set di record, inclusa la rimozione di tutti i record per ottenere un set di record "vuoto".</span><span class="sxs-lookup"><span data-stu-id="4ad49-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="4ad49-184">Questo è lo stesso effetto ottenuto eliminando il set di record dal punto di vista della risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="4ad49-185">I blocchi risorse a livello di set di record possono attualmente essere configurati solo tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ad49-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="4ad49-186">Non sono supportati nel portale di Azure o nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ad49-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="4ad49-187">Protezione dall'eliminazione di zone</span><span class="sxs-lookup"><span data-stu-id="4ad49-187">Protecting against zone deletion</span></span>

<span data-ttu-id="4ad49-188">Quando viene eliminata una zona in DNS di Azure, vengono eliminati anche tutti i set di record in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="4ad49-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="4ad49-189">Questa operazione non può essere annullata.</span><span class="sxs-lookup"><span data-stu-id="4ad49-189">This operation cannot be undone.</span></span>  <span data-ttu-id="4ad49-190">L'eliminazione accidentale di una zona critica può avere un impatto notevole.</span><span class="sxs-lookup"><span data-stu-id="4ad49-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="4ad49-191">È quindi molto importante evitare l'eliminazione accidentale di una zona.</span><span class="sxs-lookup"><span data-stu-id="4ad49-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="4ad49-192">L'applicazione di un blocco DoNotDelete a una zona impedisce l'eliminazione della zona.</span><span class="sxs-lookup"><span data-stu-id="4ad49-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="4ad49-193">Tuttavia, poiché i blocchi vengono ereditati dalle risorse figlio, impedisce anche che vengano eliminati set di record nella zona, creando un effetto potenzialmente indesiderato.</span><span class="sxs-lookup"><span data-stu-id="4ad49-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="4ad49-194">Inoltre, come descritto in precedenza, questo controllo non è efficace poiché i record possono essere rimossi dai set di record esistenti.</span><span class="sxs-lookup"><span data-stu-id="4ad49-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="4ad49-195">In alternativa, è possibile applicare un blocco DoNotDelete a un set di record nella zona, ad esempio il set di record SOA.</span><span class="sxs-lookup"><span data-stu-id="4ad49-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="4ad49-196">Poiché la zona non può essere eliminata senza eliminare anche i set di record, è possibile evitare l'eliminazione della zona, consentendo comunque di modificare i set di record all'interno della zona.</span><span class="sxs-lookup"><span data-stu-id="4ad49-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="4ad49-197">Se viene eseguito un tentativo di eliminare la zona, Azure Resource Manager rileva che questa operazione potrebbe eliminare anche il set di record SOA e blocca la chiamata perché il record SOA è bloccato.</span><span class="sxs-lookup"><span data-stu-id="4ad49-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="4ad49-198">Nessun set di record viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="4ad49-198">No record sets are deleted.</span></span>

<span data-ttu-id="4ad49-199">Il comando PowerShell seguente crea un blocco DoNotDelete sul record SOA della zona specificata:</span><span class="sxs-lookup"><span data-stu-id="4ad49-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="4ad49-200">Un altro modo per impedire di eliminare accidentalmente la zona è usare un ruolo personalizzato per garantire che l'account operatore e l'account di servizio usati per gestire le zone non dispongano delle autorizzazioni per eliminare le zone.</span><span class="sxs-lookup"><span data-stu-id="4ad49-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="4ad49-201">Quando è necessario eliminare una zona, è possibile farlo in due passaggi, prima concedendo le autorizzazioni per eliminare la zona (nell'ambito della zona stessa, per impedire di eliminarne una sbagliata) e poi eliminandola.</span><span class="sxs-lookup"><span data-stu-id="4ad49-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="4ad49-202">Questo secondo approccio ha il vantaggio di essere adatto a tutte le zone accessibili da tali account, senza che sia necessario ricordarsi di creare i blocchi.</span><span class="sxs-lookup"><span data-stu-id="4ad49-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="4ad49-203">Lo svantaggio, invece, è che tutti gli account con autorizzazioni per eliminare le zone, ad esempio il proprietario della sottoscrizione, possono sempre eliminare una zona critica accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="4ad49-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="4ad49-204">Usare entrambi gli approcci contemporaneamente (blocchi di risorse e ruoli personalizzati) è un metodo di difesa avanzato per la protezione delle zone DNS.</span><span class="sxs-lookup"><span data-stu-id="4ad49-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ad49-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ad49-205">Next steps</span></span>

* <span data-ttu-id="4ad49-206">Per altre informazioni sull'uso del Controllo degli accessi in base al ruolo, vedere l'argomento di [introduzione alla gestione degli accessi nel portale di Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="4ad49-207">Per altre informazioni sull'uso dei blocchi risorse, vedere [Bloccare le risorse con Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="4ad49-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

