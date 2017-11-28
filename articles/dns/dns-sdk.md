---
title: zone DNS aaaCreate e set di record DNS di Azure utilizzando hello .NET SDK | Documenti Microsoft
description: Il record e zone DNS toocreate impostato nel DNS di Azure tramite hello .NET SDK.
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="524f7-103">Creare set di record mediante .NET SDK hello e zone DNS</span><span class="sxs-lookup"><span data-stu-id="524f7-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="524f7-104">È possibile automatizzare operazioni toocreate, delete o update zone DNS, set di record e i record con DNS SDK con libreria di gestione DNS .NET.</span><span class="sxs-lookup"><span data-stu-id="524f7-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="524f7-105">Un progetto completo di Visual Studio è disponibile [qui](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).</span><span class="sxs-lookup"><span data-stu-id="524f7-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="524f7-106">Creare un account dell'entità servizio</span><span class="sxs-lookup"><span data-stu-id="524f7-106">Create a service principal account</span></span>

<span data-ttu-id="524f7-107">In genere, accedere a livello di codice alle risorse di tooAzure viene concessa tramite un account dedicato anziché le proprie credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="524f7-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="524f7-108">Questi account dedicati sono denominati 'account dell'entità servizio'.</span><span class="sxs-lookup"><span data-stu-id="524f7-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="524f7-109">il progetto di esempio toouse hello Azure SDK DNS, innanzitutto necessario toocreate un account dell'entità servizio e assegnare le autorizzazioni corrette hello.</span><span class="sxs-lookup"><span data-stu-id="524f7-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="524f7-110">Seguire [queste istruzioni](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate un account dell'entità servizio (progetto di esempio hello DNS di Azure SDK si presuppone l'autenticazione basata su password).</span><span class="sxs-lookup"><span data-stu-id="524f7-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="524f7-111">Creare un gruppo di risorse seguendo [questa procedura](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="524f7-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="524f7-112">Utilizzare Azure RBAC toogrant hello service account dell'entità 'Collaboratore di zona DNS' autorizzazioni toohello gruppo di risorse ([Ecco come](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="524f7-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="524f7-113">Se si usa progetto di esempio hello DNS di Azure SDK, modificare file 'Program' hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="524f7-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="524f7-114">Inserire i valori corretti di hello per tenantId hello, clientId (noto anche come ID di account), segreto (password di account dell'entità servizio) e ID di sottoscrizione utilizzato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="524f7-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="524f7-115">Immettere nome gruppo di risorse hello scelto nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="524f7-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="524f7-116">Immettere un nome a scelta per la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="524f7-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="524f7-117">Pacchetti NuGet e dichiarazioni degli spazi dei nomi</span><span class="sxs-lookup"><span data-stu-id="524f7-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="524f7-118">toouse hello DNS di Azure .NET SDK, è necessario hello tooinstall **libreria di gestione di Azure DNS** Azure pacchetti è necessario che il pacchetto NuGet e altri.</span><span class="sxs-lookup"><span data-stu-id="524f7-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="524f7-119">In **Visual Studio**aprire un progetto o un nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="524f7-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="524f7-120">Andare troppo**strumenti**  **>**  **Gestione pacchetti NuGet**  **>**  **Gestisci pacchetti NuGet per Soluzione...** .</span><span class="sxs-lookup"><span data-stu-id="524f7-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="524f7-121">Fare clic su **Sfoglia**, abilitare hello **versione provvisoria di inclusione** casella di controllo e il tipo **Microsoft.Azure.Management.Dns** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="524f7-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="524f7-122">Selezionare il pacchetto di hello e fare clic su **installare** tooadd il progetto di Visual Studio tooyour.</span><span class="sxs-lookup"><span data-stu-id="524f7-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="524f7-123">Ripetere il processo di hello sopra tooalso installazione hello seguenti pacchetti: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="524f7-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="524f7-124">Aggiungere le dichiarazioni dello spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="524f7-124">Add namespace declarations</span></span>

<span data-ttu-id="524f7-125">Aggiungere hello dopo le dichiarazioni dello spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="524f7-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="524f7-126">Inizializzare i client di gestione DNS hello</span><span class="sxs-lookup"><span data-stu-id="524f7-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="524f7-127">Hello *DnsManagementClient* contiene metodi di hello e le proprietà necessarie per la gestione delle zone DNS e Recordset.</span><span class="sxs-lookup"><span data-stu-id="524f7-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="524f7-128">Hello codice riportato di seguito effettua l'accesso dell'entità servizio toohello account e crea un oggetto DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="524f7-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="524f7-129">Creare o aggiornare una zona DNS</span><span class="sxs-lookup"><span data-stu-id="524f7-129">Create or update a DNS zone</span></span>

<span data-ttu-id="524f7-130">toocreate una zona DNS, prima di tutto "Zona" viene creato un oggetto parametri di zona DNS hello toocontain.</span><span class="sxs-lookup"><span data-stu-id="524f7-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="524f7-131">Poiché le zone DNS non sono area specifica tooa collegato, il percorso di hello viene impostato too'global'.</span><span class="sxs-lookup"><span data-stu-id="524f7-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="524f7-132">In questo esempio, un [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) viene aggiunto anche toohello zona.</span><span class="sxs-lookup"><span data-stu-id="524f7-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="524f7-133">tooactually crea o aggiorna hello zona nel DNS di Azure, oggetto fuso hello contenente i parametri di zona hello viene passato toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* metodo.</span><span class="sxs-lookup"><span data-stu-id="524f7-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="524f7-134">DnsManagementClient supporta tre modalità di funzionamento: sincrono ('CreateOrUpdate'), asincrona ('CreateOrUpdateAsync'), o asincrona con la risposta HTTP toohello di accesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="524f7-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="524f7-135">È possibile scegliere una modalità qualsiasi a seconda delle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="524f7-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="524f7-136">DNS di Azure supporta la concorrenza ottimistica, definita [Etags](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="524f7-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="524f7-137">In questo esempio, specificando "*" per intestazione hello 'If-None-Match' indica toocreate Azure DNS una zona DNS se non ne esiste già.</span><span class="sxs-lookup"><span data-stu-id="524f7-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="524f7-138">chiamata di Hello non riesce se una zona con il nome di hello specificato esiste già nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="524f7-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="524f7-139">Creare set di record e record DNS</span><span class="sxs-lookup"><span data-stu-id="524f7-139">Create DNS record sets and records</span></span>

<span data-ttu-id="524f7-140">I record DNS vengono gestiti come set di record.</span><span class="sxs-lookup"><span data-stu-id="524f7-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="524f7-141">Un set di record è un set di record con hello stesso nome e registrare tipo all'interno di una zona.</span><span class="sxs-lookup"><span data-stu-id="524f7-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="524f7-142">nome del set di record Hello toohello relativo nome della zona, non hello nome DNS completo.</span><span class="sxs-lookup"><span data-stu-id="524f7-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="524f7-143">toocreate o aggiorna un set di record, un oggetto di parametri "RecordSet" viene creato e passato troppo*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="524f7-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="524f7-144">Come con le zone DNS, sono disponibili tre modalità di funzionamento: sincrono ('CreateOrUpdate'), asincrona ('CreateOrUpdateAsync'), o asincrona con la risposta HTTP toohello di accesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="524f7-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="524f7-145">Come nel caso delle zone DNS, le operazioni sui set di record includono il supporto per la concorrenza ottimistica.</span><span class="sxs-lookup"><span data-stu-id="524f7-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="524f7-146">In questo esempio, poiché 'If-Match' né 'If-None-Match' sono specificati, set di record hello viene sempre creato.</span><span class="sxs-lookup"><span data-stu-id="524f7-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="524f7-147">Questa chiamata sovrascrive qualsiasi set hello stesso nome e una registrazione di record esistenti tipo in questa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="524f7-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="524f7-148">Ottenere zone e set di record</span><span class="sxs-lookup"><span data-stu-id="524f7-148">Get zones and record sets</span></span>

<span data-ttu-id="524f7-149">Hello *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* metodi recuperano singole aree e set di record, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="524f7-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="524f7-150">Recordset sono identificati da tipo, nome e gruppo di zone e risorse di hello in che esistano.</span><span class="sxs-lookup"><span data-stu-id="524f7-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="524f7-151">Le zone sono identificate dal relativo gruppo di risorse nome e hello in che esistano.</span><span class="sxs-lookup"><span data-stu-id="524f7-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="524f7-152">Aggiornare un set di record esistente</span><span class="sxs-lookup"><span data-stu-id="524f7-152">Update an existing record set</span></span>

<span data-ttu-id="524f7-153">prima di recuperare set di record hello, quindi Aggiorna hello record il contenuto del set, inviare modifiche hello tooupdate un record DNS esistente viene impostata.</span><span class="sxs-lookup"><span data-stu-id="524f7-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="524f7-154">In questo esempio si specifica hello 'Etag' da hello recuperato nel parametro 'If-Match' hello set di record.</span><span class="sxs-lookup"><span data-stu-id="524f7-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="524f7-155">chiamata di Hello non riesce se un'operazione simultanea è modificato hello set di record in hello frattempo.</span><span class="sxs-lookup"><span data-stu-id="524f7-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="524f7-156">Elencare zone e set di record</span><span class="sxs-lookup"><span data-stu-id="524f7-156">List zones and record sets</span></span>

<span data-ttu-id="524f7-157">le zone toolist, utilizzare hello *DnsManagementClient.Zones.List...*  metodi, che supportano l'elenco di tutte le zone in un gruppo di risorse specificata o tutte le zone in un set di record toolist specifica sottoscrizione di Azure (tra risorse gruppi.), utilizzano *DnsManagementClient.RecordSets.List...*  metodi, che supportano un elenco di tutti i set di record in una zona specificato o solo i set di record di un tipo specifico.</span><span class="sxs-lookup"><span data-stu-id="524f7-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="524f7-158">Quando si elencano le zone e i set di record, i risultati potrebbero essere impaginati.</span><span class="sxs-lookup"><span data-stu-id="524f7-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="524f7-159">Hello seguente esempio viene illustrato come tooiterate tramite pagine hello dei risultati.</span><span class="sxs-lookup"><span data-stu-id="524f7-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="524f7-160">(Una dimensione di pagina artificialmente small '2' è utilizzato tooforce paging; in pratica questo parametro deve essere omessa e dimensioni di pagina predefinite utilizzate hello).</span><span class="sxs-lookup"><span data-stu-id="524f7-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="524f7-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="524f7-161">Next steps</span></span>

<span data-ttu-id="524f7-162">Scaricare hello [il progetto di esempio di DNS di Azure .NET SDK](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), che include altri esempi di come toouse hello Azure DNS .NET SDK, inclusi alcuni esempi per altri tipi di record DNS.</span><span class="sxs-lookup"><span data-stu-id="524f7-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
