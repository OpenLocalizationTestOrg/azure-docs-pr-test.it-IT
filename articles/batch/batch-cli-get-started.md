---
title: aaaGet introduttiva CLI di Azure per Batch | Documenti Microsoft
description: Ottenere una rapida introduzione toohello Batch i comandi CLI di Azure per la gestione delle risorse del servizio Azure Batch
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Gestire le risorse di Batch con l'interfaccia della riga di comando di Azure

Hello Azure CLI 2.0 è una nuova esperienza della riga di comando di Azure per la gestione delle risorse di Azure. Può essere usata in macOS, Linux e Windows. Azure 2.0 CLI è ottimizzato per gestire e amministrare le risorse di Azure dalla riga di comando hello. È possibile utilizzare hello Azure CLI toomanage il toomanage risorse, ad esempio pool di processi e attività e un account Azure Batch. Con hello CLI di Azure, è possibile generare script molti hello stesse attività svolgere con hello API Batch, il portale di Azure e i cmdlet PowerShell di Batch.

Questo articolo offre una panoramica dell'uso dell'[interfaccia della riga di comando di Azure versione 2.0](https://docs.microsoft.com/cli/azure/overview) con Batch. Vedere [Introduzione a Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) per una panoramica dell'utilizzo hello CLI con Azure.

Microsoft consiglia di utilizzare hello l'ultima versione di hello CLI di Azure, versione 2.0. Per altre informazioni sulla versione 2.0, vedere l'articolo relativo alla [disponibilità generale dell'interfaccia della riga di comando di Azure 2.0](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Impostare hello CLI di Azure

hello tooinstall CLI di Azure, seguire i passaggi di hello illustrati in [installazione hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> È consigliabile aggiornare l'installazione di Azure CLI spesso tootake vantaggio di servizio aggiornamenti e miglioramenti.
> 
> 

## <a name="command-help"></a>Guida per i comandi

È possibile visualizzare il testo della Guida per ogni comando in hello Azure CLI aggiungendo `-h` toohello comando. Omettere qualsiasi altra opzione. ad esempio:

* Guida di tooget per hello `az` comando, immettere:`az -h`
* tooget un elenco di tutti i comandi Batch hello CLI, utilizzare:`az batch -h`
* tooget Guida sulla creazione di un account di Batch, immettere:`az batch account create -h`

In caso di dubbi, utilizzare hello `-h` help tooget opzione della riga di comando in qualsiasi comando CLI di Azure.

> [!NOTE]
> Le versioni precedenti di hello CLI di Azure usato `azure` toopreface un comando CLI. Nella versione 2.0 tutti i comandi ora sono preceduti da `az`. Essere tooupdate che la sintassi nuova di hello toouse script con la versione 2.0.
>
>  

Inoltre, consultare la documentazione di riferimento di CLI di Azure toohello per informazioni dettagliate sulle [i comandi CLI di Azure per Batch](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Accesso e autenticazione

hello toouse CLI di Azure batch, è necessario toolog in e l'autenticazione. Esistono due toofollow semplici passaggi:

1. **Accedere ad Azure.** Azure offre l'accesso accedere ai comandi di gestione risorse tooAzure, tra cui [servizio di gestione dei Batch](batch-management-dotnet.md) comandi.  
2. **Accedere all'account Batch.** L'accesso consente di account del Batch accedere ai comandi di servizio tooBatch.   

### <a name="log-in-tooazure"></a>Accedi tooAzure

Esistono alcuni modi diversi toolog in Azure, descritto dettagliatamente in [Accedi con Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Accedere modo interattivo](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). L'accesso in modo interattivo quando si eseguono i comandi CLI di Azure manualmente dalla riga di comando hello.
2. [Accedere con un'entità servizio](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Accedere con un'entità servizio quando si eseguono comandi dell'interfaccia della riga di comando di Azure da uno script o un'applicazione.

Ai fini di hello di questo articolo, ecco come toolog in Azure in modo interattivo. Tipo [accesso az](https://docs.microsoft.com/cli/azure/#login) nella riga di comando hello:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Hello `az login` comando restituisce un token che è possibile utilizzare tooauthenticate, come illustrato di seguito. Seguire le istruzioni fornite di hello tooopen una pagina web e inviare tooAzure token hello:

![Accedi tooAzure](./media/batch-cli-get-started/az-login.png)

esempi di Hello elencati in hello [gli script della shell di esempio](#sample-shell-scripts) sezione anche Mostra come toostart la sessione CLI di Azure effettuando l'accesso in modo interattivo in Azure. Dopo aver eseguito l'accesso, è possibile chiamare comandi toowork con risorse di gestione dei Batch, inclusi gli account Batch, le chiavi, i pacchetti di applicazioni e le quote.  

### <a name="log-in-tooyour-batch-account"></a>Accedi tooyour account Batch

toouse hello Azure CLI toomanage Batch risorse, ad esempio, i pool di processi e le attività, è necessario toolog nell'account di Batch e l'autenticazione. toolog in toohello servizio Batch, utilizzare hello [accesso dell'account batch az](https://docs.microsoft.com/cli/azure/batch/account#login) comando. 

Per l'autenticazione con l'account Batch è possibile procedere in due modi:

- **Tramite l'autenticazione con Azure Active Directory (Azure AD).** 

    L'autenticazione con Azure AD è hello predefinita quando si utilizza hello CLI di Azure batch e consigliata per la maggior parte degli scenari. 
    
    Quando si accede in modo interattivo, come descritto nella sezione precedente hello in tooAzure, le credenziali vengono memorizzati nella cache, in modo hello CLI di Azure può eseguire l'accesso tooyour account Batch con le stesse credenziali. Se si accede a tooAzure usando un'entità servizio, tali credenziali sono utilizzati toolog in tooyour account Batch.

    Uno dei vantaggi di Azure AD è che offre il controllo degli accessi in base al ruolo. Con RBAC, l'accesso dell'utente dipende dal ruolo assegnato, piuttosto che dispongono di chiavi dell'account di hello. Anziché gestire le chiavi dell'account, è possibile gestire i ruoli del controllo degli accessi in base al ruolo e lasciare la gestione dell'accesso e dell'autenticazione ad Azure AD.  

    L'autenticazione con Azure AD viene richiesto se è stato creato l'account Azure Batch con la modalità di allocazione del pool set too'User sottoscrizione '. 

    toolog in tooyour Batch account usando Azure AD, chiamare hello [accesso dell'account batch az](https://docs.microsoft.com/cli/azure/batch/account#login) comando: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Tramite l'autenticazione con chiave condivisa.**

    [L'autenticazione chiave condivisa](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) utilizza l'account di accesso chiavi tooauthenticate i comandi CLI di Azure per hello Batch del servizio.

    Se si creano script CLI di Azure i comandi Batch chiamati tooautomate, è possibile utilizzare l'autenticazione chiave condivisa o un'entità servizio di Azure AD. In alcuni scenari potrebbe essere più semplice usare l'autenticazione con chiave condivisa anziché creare un'entità servizio.  

    toolog utilizzando l'autenticazione chiave condivisa, includere hello `--shared-key-auth` opzione della riga di comando hello:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

esempi di Hello elencati in hello [gli script della shell di esempio](#sample-shell-scripts) sezione mostra come toolog sull'account Batch con hello CLI di Azure utilizzando sia Azure AD e la chiave condivisa.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Usare il trasferimento di file e i modelli dell'interfaccia della riga di comando di Azure Batch (anteprima)

È possibile utilizzare hello Azure CLI toorun Batch processi end-to-end senza scrivere codice. I file di modello batch supportano la Creazione pool di processi e attività con hello CLI di Azure. È inoltre possibile utilizzare i file di input hello Azure CLI tooupload processo account Batch, account di archiviazione di Azure toohello associato hello e scaricare i file di output del processo da esso. Per altre informazioni, vedere [Usare il trasferimento di file e i modelli dell'interfaccia della riga di comando di Azure Batch (anteprima)](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Script della shell di esempio

script di esempio Hello elencati nella seguente tabella mostrano hello funzionamento dei comandi con il servizio di Batch hello e attività comuni di gestione dei Batch servizio tooaccomplish toouse CLI di Azure. Questi script di esempio illustrano molti dei comandi di hello disponibili in hello CLI di Azure per Batch. 

| Script | Note |
|---|---|
| [Creare un account Batch](./scripts/batch-cli-sample-create-account.md) | Crea un account Batch e lo associa a un account di archiviazione. |
| [Aggiungere un'applicazione](./scripts/batch-cli-sample-add-application.md) | Aggiunge un'applicazione e carica i file binari nel pacchetto.|
| [Gestire i pool di Batch](./scripts/batch-cli-sample-manage-pool.md) | Illustra la creazione, il ridimensionamento e la gestione dei pool. |
| [Eseguire un processo e le attività con Batch](./scripts/batch-cli-sample-run-job.md) | Illustra l'esecuzione di un processo e l'aggiunta di attività. |

## <a name="json-files-for-resource-creation"></a>File JSON per la creazione di risorse

Quando si creano risorse Batch come pool e i processi, è possibile specificare un file JSON che contiene la configurazione della risorsa di hello nuovo invece di passare i parametri come opzioni della riga di comando. ad esempio:

```azurecli
az batch pool create my_batch_pool.json
```

Sebbene sia possibile creare la maggior parte delle risorse di Batch utilizzando solo le opzioni della riga di comando, alcune funzionalità è necessario specificare un file in formato JSON che contiene i dettagli delle risorse hello. Ad esempio, è necessario utilizzare un file JSON, se si desidera toospecify i file di risorse per un'attività di avvio.

hello toosee sintassi JSON richiesto toocreate una risorsa, fare riferimento toohello [riferimento all'API REST di Batch] [ rest_api] documentazione. Ogni "Aggiungi *tipo di risorsa*" argomento di riferimento all'API REST hello contiene script JSON di esempio per la creazione di tale risorsa. È possibile utilizzare tali script JSON di esempio come modelli per toouse file JSON con hello CLI di Azure. Ad esempio hello toosee sintassi JSON per la creazione del pool, fare riferimento troppo[aggiungere un account del pool di tooan][rest_add_pool].

Per uno script di esempio che specifica un file JSON, vedere [Eseguire processi in Azure Batch con l'interfaccia della riga di comando di Azure](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Se si specifica un file JSON quando si crea una risorsa, vengono ignorati i parametri specificati nella riga di comando hello per tale risorsa.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Query efficienti per le risorse Batch

Ogni tipo di risorsa di Batch supporta un comando `list` che esegue query sull'account Batch ed elenca le risorse di tale tipo. Ad esempio, è possibile elencare pool hello attività hello e account in un processo:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Quando si esegue una query del servizio Batch hello con un `list` operazione, è possibile specificare un importo di hello OData clausola toolimit dei dati restituiti. Poiché tutti i filtri, si verifica sul lato server, richiesta solo dati di hello interseca transito hello. Utilizzo della larghezza di banda toosave queste clausole (e pertanto time) quando si eseguono operazioni di elenco.

Hello nella tabella seguente vengono descritte le clausole di OData hello supportate dal servizio Batch hello:

| Clausola | Descrizione |
|---|---|
| `--select-clause [select-clause]` | Restituisce un subset di proprietà per ogni entità. |
| `--filter-clause [filter-clause]` | Restituisce solo le entità corrispondenti hello specificato espressione OData. |
| `--expand-clause [expand-clause]` | Ottiene informazioni sulle entità hello in una singola chiamata REST sottostante. Hello espandere clausola attualmente supporta solo hello `stats` proprietà. |

Per un esempio di script che mostra come toouse una clausola di OData, vedere [eseguire un processo e le attività con Batch](./scripts/batch-cli-sample-run-job.md).

Per ulteriori informazioni sull'esecuzione di query di elenco efficiente con clausole OData, vedere [Query in modo efficiente il servizio di Azure Batch hello](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Suggerimenti per la risoluzione dei problemi

i suggerimenti seguenti Hello possono essere utili durante la risoluzione di problemi di CLI di Azure:

* Utilizzare `-h` tooget **il testo della Guida** per qualsiasi comando CLI
* Utilizzare `-v` e `-vv` toodisplay **verbose** comando output. Quando hello `-vv` flag è incluso, hello CLI di Azure viene visualizzato hello effettive richieste e risposte REST. Queste opzioni sono utili per visualizzare l'output completo degli errori.
* È possibile visualizzare **comando output in formato JSON** con hello `--json` opzione. Ad esempio, `az batch pool show pool001 --json` visualizza le proprietà di pool001 in formato JSON. È quindi possibile copiare e modificare questo toouse output in un `--json-file` (vedere [file JSON](#json-files) più indietro in questo articolo).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Hello [forum Batch] [ batch_forum] viene monitorato dai membri del team Batch. Se si riscontrano problemi o si vuole assistenza per un'operazione specifica, è possibile pubblicare le proprie domande nel forum.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni su hello CLI di Azure, vedere hello [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).
* Per altre informazioni sulle risorse Batch, vedere la [panoramica di Azure Batch per gli sviluppatori](batch-api-basics.md).
* Per ulteriori informazioni sull'utilizzo di pool toocreate modelli, processi e attività Batch senza scrivere codice, vedere [usare Azure Batch CLI modelli e trasferimento di File (anteprima)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
