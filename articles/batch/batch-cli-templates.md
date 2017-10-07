---
title: Azure Batch aaaRun processi end-to-end senza scrivere codice (anteprima) | Documenti Microsoft
description: "Creare il file di modello per hello Azure CLI toocreate Batch pool, processi e attività."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Usare il trasferimento di file e i modelli dell'interfaccia della riga di comando di Azure Batch (anteprima)

Utilizzando hello CLI di Azure, è possibile toorun i processi Batch senza scrivere codice.

File di modello possono essere creati e usati con hello CLI di Azure che consentono di pool di Batch, i processi e attività toobe creato. File di input del processo possono essere caricati facilmente all'account di archiviazione hello associato hello Batch account e processo di output file scaricati.

## <a name="overview"></a>Panoramica

Consente a un toohello estensione CLI di Azure Batch toobe utilizzato end-to-end dagli utenti che non sono sviluppatori. È possibile creare un pool, caricato i dati di input, processi e attività associate creata, e hello risultante output dati scaricati: nessun codice necessario, hello CLI viene utilizzato direttamente o viene integrato negli script.

Compilazione di modelli di batch in hello [le funzionalità di supporto Batch hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) file JSON che consente i valori delle proprietà toospecify per la creazione di hello di pool di processi, attività e altri elementi. Con i modelli di Batch, hello seguenti funzionalità sono state aggiunte su ciò che è possibile con i file JSON hello:

-   È possibile definire parametri. Quando si utilizza il modello di hello, solo i valori di parametro hello sono elemento hello toocreate specificato, con altri valori di proprietà di elemento specificato nel corpo del modello hello. Gli utenti in grado di riconoscere che batch e il toobe applicazioni eseguiti dal Batch è possono creare modelli, specificare i pool di processi e i valori delle proprietà di attività. Un utente minori che hanno familiarità con le applicazioni e/o di Batch deve solo i valori hello toospecify per i parametri di hello definito.

-   Factory delle attività processo creare uno o più attività associata a un processo, evitando hello necessario per molti toobe le definizioni di attività creata e allo scopo di semplificare notevolmente l'invio di processi.


File di dati di input devono toobe forniti per i processi e i file di dati di output vengono spesso generati. È associato un account di archiviazione, per impostazione predefinita, con ogni Batch account e i file possono essere trasferiti facilmente tooand da questo account di archiviazione usando l'interfaccia CLI, senza scrivere codice e credenziali di archiviazione non necessaria.

Ad esempio, [ffmpeg](http://ffmpeg.org/) è una diffusa applicazione che elabora i file audio e video. Hello CLI di Azure Batch può essere utilizzato tooinvoke ffmpeg tootranscode origine file video toodifferent risoluzioni.

-   Viene creato un modello di pool. utente Hello creazione modello hello sa come toocall hello ffmpeg applicazione e i relativi requisiti; specifichino hello OS appropriato, VM dimensioni, come ffmpeg sia installato (da un pacchetto di applicazione o tramite Gestione pacchetti, ad esempio) e altri valori di proprietà del pool. I parametri vengono creati quando si utilizza il modello di hello, solo l'id del pool hello e numero di macchine virtuali necessario toobe specificato.

-   Viene creato un modello di processo. modello di Hello utente Creazione hello sa come ffmpeg esigenze toobe richiamato una risoluzione diversa tootranscode origine video tooa e specifica riga di comando attività hello; Inoltre, che sappiano che vi sia una cartella contenente file video di origine hello, con un'attività necessaria per ogni file di input.

-   Un utente finale con un set di file video tootranscode crea innanzitutto un pool usando il modello di pool di hello, specificare solo l'id del pool hello e numero di macchine virtuali necessarie. È quindi possibile caricare tootranscode i file di origine hello. Un processo potrà quindi essere inviato utilizzando il modello di processo hello, specificare solo l'id del pool hello e percorso dei file di origine hello caricato. processo Batch Hello viene creato con un'attività per ciascun file di input in corso la generazione. Infine, i file di output di hello transcodificato possono essere il download.

## <a name="installation"></a>Installazione

funzionalità di trasferimento di modello e un file Hello richiedono toobe un'estensione installata.

Per istruzioni su come tooinstall hello CLI di Azure vedere [installare Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

Una volta hello che CLI di Azure è stato installato, hello Batch estensione può essere installata usando il comando CLI seguente:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Per ulteriori informazioni su hello estensione Batch, vedere [Microsoft Azure Batch CLI Extensions per Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Modelli

Hello CLI di Azure Batch consente di elementi, ad esempio pool di processi e attività toobe creato specificando un file JSON che contengono valori e nomi di proprietà. ad esempio:

```azurecli
az batch pool create –-json-file AppPool.json
```

Modelli di Azure Batch sono modelli di gestione risorse tooAzure simile, funzionalità e di sintassi. File JSON che contengono valori e nomi di proprietà di elementi, ma aggiungere hello seguendo i concetti principali sono:

-   **Parametri**

    -   Consenti toobe di valori di proprietà specificato in una sezione del corpo, con la necessità di toobe fornito quando si utilizza il modello di hello solo valori di parametro. Ad esempio, è stato possibile collocare definizione completa di hello per un pool nel corpo di hello e un solo parametro definito per l'id del pool. solo una stringa id pool deve pertanto toocreate toobe fornito un pool.
        
    -   corpo del modello Hello può essere creato da un utente con le informazioni di Batch e hello applicazioni toobe eseguito dal Batch. Quando si utilizza il modello di hello, è necessario specificare solo i valori per parametri definiti dall'autore hello. Un utente senza hello Batch approfondite e/o informazioni sulle applicazioni è pertanto possono utilizzare i modelli.

-   **Variabili**

    -   Consenti toobe valori di parametro semplici o complesse specificato in un'unica posizione e utilizzata in uno o più posizioni nel corpo del modello hello. Le variabili possono semplificare e ridurre le dimensioni di hello del modello di hello, così come renderla più gestibile con una proprietà toochange percorso il cui valore può essere modificato.

-   **Costrutti di livello superiore**

    -   Alcuni costrutti di livello superiore sono disponibili nel modello di hello che non sono ancora disponibili in hello API Batch. Ad esempio, una factory delle attività può essere definita in un modello di processo che crea più attività per il processo di hello utilizzando una definizione di attività comuni. Questi costrutti evitare hello necessario toocode per dinamicamente creare più file JSON, ad esempio un file per ogni attività, nonché per creare script applicazioni tooinstall file tramite Gestione pacchetti, ad esempio.

    -   In alcuni punti, dove applicabile, che questi costrutti possono essere aggiunto toothe Batch al servizio e disponibile in hello API Batch, le interfacce utente e così via.

### <a name="pool-templates"></a>Modelli di pool

Il modello di pool di hello sono inoltre supportate le funzionalità di modelli standard toohello di parametri e variabili, hello seguenti costrutti di livello superiore:

-   **Riferimenti ai pacchetti**

    -   Consente facoltativamente nodi toopool di software toobe copiati tramite pacchetti di gestori. gestione di pacchetti Hello e id del pacchetto vengono specificati. Viene toodeclare in grado di uno o più pacchetti evita hello necessità toocreate uno script che recupera i pacchetti hello necessario, installare script hello ed eseguire script hello in ogni nodo del pool.

Hello di seguito è riportato un esempio di un modello che crea un pool di macchine virtuali Linux con ffmpeg installato e solo richiede un pool id stringa e hello numero di macchine virtuali toobe fornito toouse:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Se è stato denominato file del modello di hello _pool ffmpeg.json_, quindi il modello di hello viene richiamato come indicato di seguito:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Modelli di processo

Funzionalità di modelli standard toohello di parametri e variabili, hello seguenti costrutti di livello superiore sono inoltre supportate dal modello di processo hello:

-   **Factory di attività**

    -   Vengono create più attività per un processo da una definizione di attività. Sono supportati tre tipi di factory di attività: processo parametrico di organizzazione, attività per file e raccolta di attività.

Hello Ecco un esempio di un modello che crea un processo che utilizza ffmpeg per eseguire la transcodifica MP4 file video tooone di due risoluzioni inferiori, con un'attività creata per ogni file video di origine:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Se è stato denominato file del modello di hello _processo ffmpeg.json_, quindi il modello di hello viene richiamato come indicato di seguito:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Gruppi e trasferimenti di file

La maggior parte dei processi e delle attività richiede file di input e produce file di output. Entrambi i file di input e i file di output è in genere necessario toobe trasferiti, dal nodo di toohello hello client o dal client di toohello nodo hello. Hello estensione CLI di Azure Batch estrae il trasferimento di file di stoccaggio e utilizza l'account di archiviazione hello viene creato per impostazione predefinita per ogni account Batch.

Un gruppo di file equivale contenitore tooa creati in hello account di archiviazione di Azure. gruppo di file Hello abbia le sottocartelle.

Hello estensione CLI Batch sono disponibili comandi per il caricamento di file dal gruppo di file specificato tooa client e il download dei file dal client tooa gruppo di file specificato hello.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Modelli di processo e di pool consentono i file archiviati nel file gruppi toobe specificata per la copia sui nodi pool o off pool nodi, eseguire il gruppo di file tooa. Ad esempio, nel modello di processo specificato in precedenza, hello file gruppo "ffmpeg-input" è specificato per la factory delle attività hello come percorso di hello hello video di file di origine copiato nodo hello per la transcodifica; file gruppo "ffmpeg-output di Hello" viene utilizzato come percorso in cui i file di output di hello transcodificato hello copiati nodo hello toofrom in esecuzione di ogni attività.

## <a name="summary"></a>Riepilogo

Supporto per il trasferimento di modello e un file attualmente sono stati aggiunti solo toohello CLI di Azure. obiettivo di Hello è pubblico hello tooexpand utilizzabile toousers Batch che non richiedono codice toodevelop utilizzando hello API Batch, ad esempio i ricercatori, gli utenti IT e così via. Senza la generazione di codice, gli utenti esperti di Azure, Batch e hello applicazioni toobe eseguire dal Batch possono creare modelli per la creazione di pool e processo. Con parametri di modello, gli utenti senza una conoscenza approfondita di Batch e hello applicazioni possono utilizzare i modelli di hello.

Provare a hello estensione Batch per hello CLI di Azure e fornire commenti o suggerimenti, entrambi hello in commenti per l'articolo o tramite hello [forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Passaggi successivi

- Vedere post sul blog di modelli di hello Batch: [i processi in esecuzione Batch di Azure mediante hello CLI di Azure: è richiesto alcun codice](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Installazione e utilizzo della documentazione, esempi e codice sorgente sono disponibili in hello [repository GitHub Azure](https://github.com/Azure/azure-batch-cli-extensions).
