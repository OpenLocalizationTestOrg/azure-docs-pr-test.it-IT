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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Creare set di record mediante .NET SDK hello e zone DNS

È possibile automatizzare operazioni toocreate, delete o update zone DNS, set di record e i record con DNS SDK con libreria di gestione DNS .NET. Un progetto completo di Visual Studio è disponibile [qui](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True).

## <a name="create-a-service-principal-account"></a>Creare un account dell'entità servizio

In genere, accedere a livello di codice alle risorse di tooAzure viene concessa tramite un account dedicato anziché le proprie credenziali utente. Questi account dedicati sono denominati 'account dell'entità servizio'. il progetto di esempio toouse hello Azure SDK DNS, innanzitutto necessario toocreate un account dell'entità servizio e assegnare le autorizzazioni corrette hello.

1. Seguire [queste istruzioni](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate un account dell'entità servizio (progetto di esempio hello DNS di Azure SDK si presuppone l'autenticazione basata su password).
2. Creare un gruppo di risorse seguendo [questa procedura](../azure-resource-manager/resource-group-template-deploy-portal.md).
3. Utilizzare Azure RBAC toogrant hello service account dell'entità 'Collaboratore di zona DNS' autorizzazioni toohello gruppo di risorse ([Ecco come](../active-directory/role-based-access-control-configure.md).)
4. Se si usa progetto di esempio hello DNS di Azure SDK, modificare file 'Program' hello come indicato di seguito:

   * Inserire i valori corretti di hello per tenantId hello, clientId (noto anche come ID di account), segreto (password di account dell'entità servizio) e ID di sottoscrizione utilizzato nel passaggio 1.
   * Immettere nome gruppo di risorse hello scelto nel passaggio 2.
   * Immettere un nome a scelta per la zona DNS.

## <a name="nuget-packages-and-namespace-declarations"></a>Pacchetti NuGet e dichiarazioni degli spazi dei nomi

toouse hello DNS di Azure .NET SDK, è necessario hello tooinstall **libreria di gestione di Azure DNS** Azure pacchetti è necessario che il pacchetto NuGet e altri.

1. In **Visual Studio**aprire un progetto o un nuovo progetto.
2. Andare troppo**strumenti**  **>**  **Gestione pacchetti NuGet**  **>**  **Gestisci pacchetti NuGet per Soluzione...** .
3. Fare clic su **Sfoglia**, abilitare hello **versione provvisoria di inclusione** casella di controllo e il tipo **Microsoft.Azure.Management.Dns** nella casella di ricerca hello.
4. Selezionare il pacchetto di hello e fare clic su **installare** tooadd il progetto di Visual Studio tooyour.
5. Ripetere il processo di hello sopra tooalso installazione hello seguenti pacchetti: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Aggiungere le dichiarazioni dello spazio dei nomi

Aggiungere hello dopo le dichiarazioni dello spazio dei nomi

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Inizializzare i client di gestione DNS hello

Hello *DnsManagementClient* contiene metodi di hello e le proprietà necessarie per la gestione delle zone DNS e Recordset.  Hello codice riportato di seguito effettua l'accesso dell'entità servizio toohello account e crea un oggetto DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Creare o aggiornare una zona DNS

toocreate una zona DNS, prima di tutto "Zona" viene creato un oggetto parametri di zona DNS hello toocontain. Poiché le zone DNS non sono area specifica tooa collegato, il percorso di hello viene impostato too'global'. In questo esempio, un [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) viene aggiunto anche toohello zona.

tooactually crea o aggiorna hello zona nel DNS di Azure, oggetto fuso hello contenente i parametri di zona hello viene passato toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* metodo.

> [!NOTE]
> DnsManagementClient supporta tre modalità di funzionamento: sincrono ('CreateOrUpdate'), asincrona ('CreateOrUpdateAsync'), o asincrona con la risposta HTTP toohello di accesso ('CreateOrUpdateWithHttpMessagesAsync').  È possibile scegliere una modalità qualsiasi a seconda delle esigenze dell'applicazione.

DNS di Azure supporta la concorrenza ottimistica, definita [Etags](dns-getstarted-create-dnszone.md). In questo esempio, specificando "*" per intestazione hello 'If-None-Match' indica toocreate Azure DNS una zona DNS se non ne esiste già.  chiamata di Hello non riesce se una zona con il nome di hello specificato esiste già nel gruppo di risorse hello.

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

## <a name="create-dns-record-sets-and-records"></a>Creare set di record e record DNS

I record DNS vengono gestiti come set di record. Un set di record è un set di record con hello stesso nome e registrare tipo all'interno di una zona.  nome del set di record Hello toohello relativo nome della zona, non hello nome DNS completo.

toocreate o aggiorna un set di record, un oggetto di parametri "RecordSet" viene creato e passato troppo*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Come con le zone DNS, sono disponibili tre modalità di funzionamento: sincrono ('CreateOrUpdate'), asincrona ('CreateOrUpdateAsync'), o asincrona con la risposta HTTP toohello di accesso ('CreateOrUpdateWithHttpMessagesAsync').

Come nel caso delle zone DNS, le operazioni sui set di record includono il supporto per la concorrenza ottimistica.  In questo esempio, poiché 'If-Match' né 'If-None-Match' sono specificati, set di record hello viene sempre creato.  Questa chiamata sovrascrive qualsiasi set hello stesso nome e una registrazione di record esistenti tipo in questa zona DNS.

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

## <a name="get-zones-and-record-sets"></a>Ottenere zone e set di record

Hello *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* metodi recuperano singole aree e set di record, rispettivamente. Recordset sono identificati da tipo, nome e gruppo di zone e risorse di hello in che esistano. Le zone sono identificate dal relativo gruppo di risorse nome e hello in che esistano.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Aggiornare un set di record esistente

prima di recuperare set di record hello, quindi Aggiorna hello record il contenuto del set, inviare modifiche hello tooupdate un record DNS esistente viene impostata.  In questo esempio si specifica hello 'Etag' da hello recuperato nel parametro 'If-Match' hello set di record. chiamata di Hello non riesce se un'operazione simultanea è modificato hello set di record in hello frattempo.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Elencare zone e set di record

le zone toolist, utilizzare hello *DnsManagementClient.Zones.List...*  metodi, che supportano l'elenco di tutte le zone in un gruppo di risorse specificata o tutte le zone in un set di record toolist specifica sottoscrizione di Azure (tra risorse gruppi.), utilizzano *DnsManagementClient.RecordSets.List...*  metodi, che supportano un elenco di tutti i set di record in una zona specificato o solo i set di record di un tipo specifico.

Quando si elencano le zone e i set di record, i risultati potrebbero essere impaginati.  Hello seguente esempio viene illustrato come tooiterate tramite pagine hello dei risultati. (Una dimensione di pagina artificialmente small '2' è utilizzato tooforce paging; in pratica questo parametro deve essere omessa e dimensioni di pagina predefinite utilizzate hello).

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

## <a name="next-steps"></a>Passaggi successivi

Scaricare hello [il progetto di esempio di DNS di Azure .NET SDK](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), che include altri esempi di come toouse hello Azure DNS .NET SDK, inclusi alcuni esempi per altri tipi di record DNS.
