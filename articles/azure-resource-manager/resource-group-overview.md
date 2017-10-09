---
title: Panoramica di gestione risorse aaaAzure | Documenti Microsoft
description: Viene descritto come toouse Gestione risorse di Azure per la distribuzione, gestione e controllo di accesso delle risorse in Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Panoramica di Gestione risorse di Microsoft Azure
infrastruttura di Hello per l'applicazione è in genere costituito da numerosi componenti, forse una macchina virtuale, account di archiviazione e rete virtuale, o un'app web, database, server di database e i servizi di terze parti 3rd. Questi componenti non appaiono come entità separate, ma come parti correlate e interdipendenti di una singola entità Si desidera toodeploy, gestire e monitorarli come gruppo. Gestione risorse di Azure consente toowork con risorse hello nella soluzione come gruppo. È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per la soluzione in un'operazione singola, coordinata. Per la distribuzione viene usato un modello; questo modello può essere usato per diversi ambienti, ad esempio di testing, staging e produzione. Gestione risorse offre sicurezza, il controllo e assegnazione di tag toohelp funzionalità Gestione delle risorse dopo la distribuzione. 

## <a name="terminology"></a>Terminologia
Se si tooAzure nuovo gestore delle risorse, esistono alcuni termini potrebbe non essere familiarità con.

* **risorsa** : elemento gestibile disponibile tramite Azure. Alcune risorse comuni sono le macchine virtuali, gli account di archiviazione, le app Web, i database e le reti virtuali, ma ne esistono molte altre.
* **gruppo di risorse** : contenitore con risorse correlate per una soluzione Azure. gruppo di risorse Hello può includere tutte le risorse di hello per soluzione hello o solo le risorse che si desidera toomanage come gruppo. Si decide come risorse tooallocate tooresource gruppi basati su cosa hello più utile per l'organizzazione. Vedere [Gruppi di risorse](#resource-groups).
* **provider di risorse** -un servizio che fornisce risorse hello è possibile distribuire e gestire tramite Gestione risorse. Ogni provider di risorse offre operazioni per l'utilizzo di risorse hello che vengono distribuite. Alcuni provider di risorse comuni sono Microsoft. COMPUTE, che fornisce la risorsa di macchina virtuale hello, Microsoft.Storage, che fornisce risorse di account di archiviazione hello, e Microsoft, che fornisce risorse correlate tooweb app. Vedere [Provider di risorse](#resource-providers).
* **Modello di gestione risorse** -file A JavaScript Object Notation (JSON) che definisce uno o più risorse toodeploy tooa gruppo di risorse. Definisce inoltre le dipendenze di hello tra risorse hello distribuito. modello di Hello può essere utilizzato toodeploy hello risorse ripetutamente e in modo coerente. Vedere [Distribuzione del modello](#template-deployment).
* **la sintassi dichiarativa** -sintassi che consente di stato "Ecco cosa prevede toocreate" senza una sequenza di hello toowrite di programmazione toocreate comandi è. il modello di gestione risorse di Hello è riportato un esempio di sintassi dichiarativa. Nel file hello, definire le proprietà di hello per hello infrastruttura toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>vantaggi di Hello dell'utilizzo di gestione risorse
Gestione risorse offre numerosi vantaggi:

* È possibile distribuire, gestire e monitorare tutte le risorse di hello per la soluzione come un gruppo, anziché gestire singolarmente queste risorse.
* Più volte, è possibile distribuire la soluzione in tutto il ciclo di sviluppo hello e che le risorse vengono distribuite in uno stato coerente di fiducia.
* È possibile gestire l'infrastruttura con modelli dichiarativi, piuttosto che con script.
* È possibile definire le dipendenze di hello tra risorse e pertanto vengono distribuiti in ordine corretto hello.
* È possibile applicare tooall servizi di controllo di accesso nel gruppo di risorse perché il controllo di accesso basato sui ruoli (RBAC) in modo nativo viene integrato nella piattaforma di gestione di hello.
* È possibile applicare tag tooresources toologically organizzare tutte le risorse di hello nella sottoscrizione.
* Si può aiutare a chiarire la fatturazione dell'organizzazione visualizzando i costi per un gruppo di risorse di condivisione hello stesso tag.  

Gestione risorse fornisce un nuovo toodeploy modo e gestire le soluzioni. Se è stato utilizzato un modello di distribuzione precedente hello e si desidera toolearn sulle modifiche di hello, vedere [distribuzione classica e gestione di informazioni sulle risorse](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Livello di gestione coerente
Gestione risorse fornisce un livello di gestione coerente per le attività di hello eseguite tramite Azure PowerShell, CLI di Azure, il portale di Azure, API REST e gli strumenti di sviluppo. Tutti gli strumenti di hello utilizzano un insieme comune di operazioni. Utilizzare gli strumenti di hello che funzionano meglio per l'utente e utilizzano in modo intercambiabile senza confusione. 

Hello immagine seguente viene illustrato come interagiscono tutti gli strumenti di hello hello stessa API di gestione risorse di Azure. Hello API passa le richieste di servizio di gestione risorse toohello, che autentica e autorizza le richieste di hello. Gestione risorse instrada quindi i provider di risorse appropriato hello richieste toohello.

![Modello di richiesta di Resource Manager](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Indicazioni
Hello suggerimenti seguenti consentono di usufruire appieno di gestione risorse quando si lavora con le soluzioni.

1. Definire e distribuire l'infrastruttura tramite la sintassi dichiarativa hello nei modelli di gestione delle risorse, anziché tramite comandi imperativi.
2. Definire tutti i passaggi di distribuzione e la configurazione nel modello di hello. Per la configurazione della soluzione, è consigliabile evitare procedure manuali.
3. Eseguire i comandi imperativo toomanage le risorse, ad esempio toostart o arrestare un'app o un computer.
4. Organizzare le risorse con hello stesso ciclo di vita in un gruppo di risorse. Usare le categorie per tutte le altre attività di organizzazione delle risorse.

Per altri suggerimenti sui modelli, vedere [Procedure consigliate per la creazione di modelli di Azure Resource Manager](resource-manager-template-best-practices.md).

Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Gruppi di risorse
Esistono tooconsider alcuni fattori importanti quando si definisce il gruppo di risorse:

1. Tutte le risorse di hello del gruppo devono condividere hello stesso ciclo di vita. Le risorse vengono distribuite, aggiornate ed eliminate insieme. Se una risorsa, ad esempio un server di database, è necessario tooexist in un ciclo di distribuzione diversi deve essere in un altro gruppo di risorse.
2. Ogni risorsa può appartenere a un solo gruppo di risorse.
3. È possibile aggiungere o rimuovere un gruppo di risorse tooa in qualsiasi momento.
4. È possibile spostare una risorsa da un gruppo di tooanother gruppo di risorse. Per ulteriori informazioni, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](resource-group-move-resources.md).
5. Un gruppo di risorse può contenere le risorse che risiedono in aree diverse.
6. Un gruppo di risorse può essere utilizzato il controllo di accesso tooscope per le azioni amministrative.
7. Una risorsa può interagire con le risorse di altri gruppi di risorse. Questa interazione è comune quando le risorse di hello due sono correlate ma non condividono hello stesso ciclo di vita (ad esempio, App web connessione database tooa).

Quando si crea un gruppo di risorse, è necessario tooprovide un percorso per il gruppo di risorse. Perché un gruppo di risorse necessita di un percorso? E, se le risorse di hello possono avere posizioni diverse rispetto al gruppo di risorse hello, perché il percorso del gruppo risorse hello importante affatto?" gruppo di risorse Hello archivia i metadati sulle risorse hello. Pertanto, quando si specifica un percorso per il gruppo di risorse hello, si specifica la memorizzazione dei metadati. Per motivi di conformità, potrebbe essere necessario tooensure che i dati sono archiviati in una determinata area.

## <a name="resource-providers"></a>Provider di risorse
Ogni provider di risorse offre una serie di risorse e operazioni per l'uso di un servizio di Azure. Ad esempio, se si desidera toostore chiavi e segreti, si utilizzano hello **Microsoft.KeyVault** provider di risorse. Questo provider di risorse offre un tipo di risorsa denominato **gli insiemi di credenziali** per la creazione dell'insieme di credenziali chiave hello. 

nome Hello di un tipo di risorsa è in formato hello: **{resource-provider} / {resource-type}**. Ad esempio, il tipo di insieme di credenziali chiave hello è **Microsoft.KeyVault/vaults**.

Operazioni preliminari alla distribuzione delle risorse, è necessario comprendere quali hello disponibili di provider di risorse. Conoscere i nomi di hello della risorsa provider e le risorse consente definire le risorse desiderate toodeploy tooAzure. Inoltre, è necessario tooknow i percorsi validi hello e le versioni dell'API per ogni tipo di risorsa. Per altre informazioni, vedere [Provider e tipi di risorse](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Distribuzione del modello
Con Gestione risorse, è possibile creare un modello (in formato JSON) che definisce l'infrastruttura di hello e configurazione della soluzione Azure. Usando il modello è possibile distribuire ripetutamente la soluzione nel corso del ciclo di vita garantendo al contempo che le risorse vengano distribuite in uno stato coerente. Quando si crea una soluzione dal portale di hello, soluzione hello include automaticamente un modello di distribuzione. Non è toocreate il modello da zero perché non è possibile iniziare con il modello di hello per la soluzione e personalizzarlo toomeet alle specifiche esigenze. È possibile recuperare un modello per un gruppo di risorse esistente da esportazione hello dello stato corrente del gruppo di risorse hello o visualizzazione modello di hello utilizzato per una particolare distribuzione. Visualizzazione hello [modello esportato](resource-manager-export-template.md) è un modo utile di toolearn sulla sintassi del modello hello.

toolearn sul formato hello del modello di hello e come creare l'oggetto, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md). hello tooview sintassi JSON per i tipi di risorse, vedere [definire le risorse nei modelli di Azure Resource Manager](/azure/templates/).

Gestione risorse Elabora modello hello come qualsiasi altra richiesta (vedere l'immagine di hello per [livello gestione coerente](#consistent-management-layer)). Modello hello analizza e converte la sintassi in operazioni dell'API REST per i provider di risorse appropriato hello. Ad esempio, quando Gestione risorse riceve un modello con hello seguente definizione di risorsa:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Converte hello definizione toohello operazione API REST, che viene inviato il provider toohello delle risorse seguenti:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Come definire i modelli e i gruppi di risorse è completamente backup tooyou e come si desidera toomanage la soluzione. Ad esempio, è possibile distribuire l'applicazione a tre livelli tramite un singolo modello tooa singolo gruppo di risorse.

![modello a tre livelli](./media/resource-group-overview/3-tier-template.png)

Tuttavia, non è toodefine dell'intera infrastruttura in un unico modello. Risulta spesso utile toodivide i requisiti di distribuzione in un set di modelli di destinazione, scopo specifico. È anche possibile riusare i modelli per altre soluzioni. toodeploy una particolare soluzione, creare un modello master che collega tutti i modelli di hello necessario. Hello immagine seguente viene illustrato come toodeploy una soluzione a tre livelli tramite un modello padre che include tre nidificata modelli.

![modello a tre livelli annidati](./media/resource-group-overview/nested-tiers-template.png)

Se si prevedere i livelli con cicli di vita separata, è possibile distribuire i gruppi di risorse tooseparate tre livelli. Si noti hello risorse possono comunque essere tooresources collegato in altri gruppi di risorse.

![modello a livelli](./media/resource-group-overview/tier-templates.png)

Per altre informazioni sulla progettazione di modelli, vedere [Procedure consigliate per la progettazione di modelli di Azure Resource Manager](best-practices-resource-manager-design-templates.md). Per informazioni sui modelli annidati, vedere [Uso di modelli collegati con Azure Resource Manager](resource-group-linked-templates.md).

Gestione risorse di Azure consente di analizzare dipendenze tooensure risorse vengono create nell'ordine corretto hello. Se una risorsa si basa sul valore di un'altra risorsa, ad esempio una macchina virtuale che richiede un account di archiviazione per i dischi, impostare una dipendenza. Per altre informazioni, vedere [Definizione delle dipendenze nei modelli di Gestione risorse di Azure](resource-group-define-dependencies.md).

È inoltre possibile utilizzare il modello di hello per infrastruttura toohello degli aggiornamenti. Ad esempio, è possibile aggiungere una soluzione di tooyour risorsa e aggiungere le regole di configurazione per le risorse di hello che sono già state distribuite. Se il modello di hello specifica la creazione di una risorsa ma che esiste già una risorsa, Gestione risorse di Azure esegue un aggiornamento anziché creare un nuovo asset. Azure Resource Manager aggiornamenti hello esistente asset toohello stesso stato perché sarebbe come nuovo.  

Gestione risorse fornisce le estensioni per gli scenari, quando è necessario operazioni aggiuntive, ad esempio l'installazione di software specifico che non è incluso nel programma di installazione hello. Se si utilizza già un servizio di gestione configurazione, ad esempio DSC, Chef o Puppet, è possibile continuare a usare il servizio utilizzando le estensioni. Per informazioni sulle estensioni delle macchine virtuali, vedere [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Infine, il modello di hello diventa parte del codice sorgente hello per l'app. È possibile archiviarlo nel repository di codice sorgente tooyour e aggiornarlo con l'evolversi dell'app. È possibile modificare il modello di hello tramite Visual Studio.

Dopo aver definito il modello, si è pronti toodeploy hello risorse tooAzure. Per le risorse hello comandi toodeploy hello, vedere:

* [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md)
* [Distribuire le risorse con i modelli di Azure Resource Manager e l'interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md)
* [Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure](resource-group-template-deploy-portal.md)
* [Distribuire le risorse con i modelli e l'API REST di Resource Manager](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Tag
Gestione risorse fornisce una funzionalità di assegnazione di tag che consente di toocategorize risorse in base a requisiti tooyour per la gestione o di fatturazione. Usare i tag quando si dispone di una raccolta di gruppi di risorse e risorse complessa ed è necessario toovisualize tali risorse in modo hello più hello tooyou senso la maggior parte delle. Ad esempio possibile contrassegnare le risorse che svolgono un ruolo simile all'interno dell'organizzazione o appartengono toohello stesso reparto. Senza tag, gli utenti dell'organizzazione è possibile creare più risorse che possono essere toolater difficile identificano e gestire. Ad esempio, si consiglia toodelete tutte le risorse di hello per un particolare progetto. Se tali risorse non vengono contrassegnate per il progetto di hello, è necessario toomanually trovarli. Assegnazione di tag può essere un aspetto importante è tooreduce costi non necessari nella sottoscrizione. 

Le risorse non è necessario tooreside in hello stessa risorsa gruppo tooshare un tag. È possibile creare la propria tooensure tassonomia di tag in tutti gli utenti nell'organizzazione di utilizzano comuni tag anziché utenti inavvertitamente l'applicazione di tag leggermente diverso (ad esempio "dept" anziché "department").

Hello di esempio seguente mostra una macchina virtuale di tooa tag applicato.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

utilizzare tutte le risorse di hello con un valore di tag, tooretrieve hello cmdlet di PowerShell seguente:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

In alternativa, hello comando CLI di Azure 2.0 seguente:

```azurecli
az resource list --tag costCenter=Finance
```

È inoltre possibile visualizzare le risorse contrassegnate tramite hello portale di Azure.

Hello [report utilizzo](../billing/billing-understand-your-bill.md) per la sottoscrizione include nomi di tag e valori, che consente di toobreak i costi da tag. Per ulteriori informazioni sui tag, vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md).

## <a name="access-control"></a>Controllo di accesso
Gestione risorse consente toocontrol che dispone di accesso toospecific azioni per l'organizzazione. In modo nativo è integrato di controllo di accesso basato sui ruoli (RBAC) nella piattaforma di gestione di hello e si applica tale servizi tooall di controllo di accesso nel gruppo di risorse. 

Quando si utilizza il controllo di accesso basato sui ruoli, esistono due toounderstand i concetti principali:

* Le definizioni di ruolo: descrivono un insieme di autorizzazioni e possono essere usate in più assegnazioni.
* Le assegnazioni di ruolo: una definizione viene assegnata a un'identità (utente o gruppo) per un particolare ambito (sottoscrizione, gruppo di risorse o risorsa). assegnazione di Hello viene ereditata da ambiti di livello inferiore.

È possibile aggiungere una piattaforma definita toopre gli utenti e ruoli specifici di risorse. Ad esempio, è possibile sfruttare i vantaggi del ruolo predefinito di hello chiamato lettore che consente agli utenti tooview alle risorse ma non di modificarle. Aggiungere gli utenti dell'organizzazione che richiedono questo tipo di ruolo di lettore toohello di accesso e applicare hello ruolo toohello sottoscrizione, gruppo di risorse o la risorsa.

Azure offre i seguenti quattro ruoli piattaforma hello:

1. Proprietario: può gestire tutto, compresi gli accessi
2. Collaboratore: può gestire tutto ad eccezione degli accessi
3. Lettore: può visualizzare tutto, ma non apportare modifiche
4. Amministratore accesso utenti, è possibile gestire risorse tooAzure di accesso utente

Azure offre anche diversi ruoli specifici delle risorse. Alcuni ruoli comuni sono i seguenti:

1. Collaboratore alla macchina virtuale, è possibile gestire le macchine virtuali ma non concedere accesso toothem e non può gestire hello virtuale rete o archiviazione account toowhich sono connessi
2. Collaboratore di rete - possibile gestire tutte le risorse di rete, ma non concedere accesso toothem
3. Collaboratore di Account di archiviazione - possono gestire gli account di archiviazione, ma non concedere accesso toothem
4. Collaboratore SQL Server: può gestire server e database SQL, ma non i criteri di sicurezza correlati
5. Collaboratore di sito Web - possono gestire i siti Web, ma non hello web piani toowhich sono connessi

Per hello l'elenco completo dei ruoli e delle azioni consentite, vedere [RBAC: compilato nei ruoli](../active-directory/role-based-access-built-in-roles.md). Per altre informazioni sul controllo degli accessi in base al ruolo, vedere [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md). 

In alcuni casi, si desidera toorun codice o script che accede alle risorse, ma non si desidera toorun in credenziali di un utente. Invece si desidera toocreate un'identità chiamata un servizio principale per un'applicazione hello e assegnare il ruolo appropriato di hello per l'entità servizio hello. Gestione risorse consente toocreate le credenziali per un'applicazione hello e l'autenticazione a livello di codice di un'applicazione hello. toolearn sulla creazione di entità servizio, vedere uno degli argomenti seguenti:

* [Usare Azure PowerShell toocreate una risorse tooaccess dell'entità servizio](resource-group-authenticate-service-principal.md)
* [Utilizzare toocreate CLI di Azure un risorse tooaccess dell'entità servizio](resource-group-authenticate-service-principal-cli.md)
* [Utilizzare l'applicazione Azure Active Directory toocreate portale e l'entità servizio che possono accedere alle risorse](resource-group-create-service-principal-portal.md)

Anche in modo esplicito, è possibile bloccare risorse critiche tooprevent agli utenti l'eliminazione o modificarli. Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Log attività
Resource Manager registra tutte le operazioni che creano, modificano o eliminano una risorsa. È possibile utilizzare hello attività registri toofind un errore durante la risoluzione dei problemi o toomonitor come un utente nell'organizzazione di modifica una risorsa. Selezionare i log hello toosee, **log attività** in hello **impostazioni** pannello per un gruppo di risorse. È possibile filtrare i registri di hello da molti valori diversi, tra cui l'operazione di hello avviata dall'utente. Per informazioni sull'utilizzo dei log attività hello, vedere [Visualizza attività registra toomanage Azure risorse](resource-group-audit.md).

## <a name="customized-policies"></a>Criteri personalizzati
Gestione risorse consente criteri toocreate personalizzato per gestire le risorse. tipi di Hello di criteri creati possono includere diversi scenari. È possibile applicare una convenzione di denominazione alle risorse e limitare i tipi e le istanze di risorse che possono essere distribuiti o le aree che possono ospitare un tipo di risorsa. È possibile richiedere un valore di tag sulla fatturazione tooorganize risorse dai servizi. Si creano criteri toohelp ridurre i costi e mantenere la coerenza tra la sottoscrizione. 

Definire criteri con JSON e quindi applicarli nell'intera sottoscrizione o all'interno di un gruppo di risorse. I criteri sono diversi dalle controllo di accesso basato sui ruoli perché sono tipi tooresource applicato.

Hello di esempio seguente viene illustrato un criterio che assicura la coerenza di tag, specificando che tutte le risorse includono un tag costCenter.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

È possibile creare molti altri tipi di criteri. Per ulteriori informazioni, vedere [risorse toomanage criteri di utilizzo e controllare l'accesso](resource-manager-policy.md).

## <a name="sdks"></a>SDK
Azure SDK sono disponibili per più linguaggi e piattaforme. Ogni implementazione del linguaggio è disponibile tramite Gestione pacchetti del relativo ecosistema e in GitHub.

Di seguito sono riportati i repository SDK open source. Sono graditi commenti e suggerimenti, segnalazioni di problemi e richieste pull.

* [Azure SDK per .NET](https://github.com/Azure/azure-sdk-for-net)
* [Librerie di gestione di Azure per Java](https://github.com/Azure/azure-sdk-for-java)
* [Azure SDK per Node.js](https://github.com/Azure/azure-sdk-for-node)
* [Azure SDK per PHP](https://github.com/Azure/azure-sdk-for-php)
* [Azure SDK per Python](https://github.com/Azure/azure-sdk-for-python)
* [Azure SDK per Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Per informazioni sull'uso di questi linguaggi con le proprie risorse, vedere:

* [Azure for .NET developers](/dotnet/azure/?view=azure-dotnet) (Azure per sviluppatori .NET)
* [Azure for Java developers](/java/azure/) (Azure per sviluppatori Java)
* [Azure for Node.js developers](/nodejs/azure/) (Azure per sviluppatori Node.js)
* [Azure for Python developers](/python/azure/) (Azure per sviluppatori Python)

> [!NOTE]
> Se hello SDK non offre funzionalità di hello necessario, è inoltre possibile chiamare toohello [API REST di Azure](https://docs.microsoft.com/rest/api/resources/) direttamente.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Per una semplice introduzione tooworking con i modelli, vedere [esportare un modello di gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).
* Per istruzioni dettagliate sulla creazione di un modello, vedere [Creare il primo modello di Azure Resource Manager](resource-manager-create-first-template.md).
* le funzioni hello toounderstand è possibile utilizzare in un modello, vedere [funzioni di modello](resource-group-template-functions.md)
* Per informazioni sull'uso di Visual Studio con Resource Manager, vedere [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Ecco una dimostrazione video di questa panoramica:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
