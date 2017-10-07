---
title: tooget interfaccia aaaUse Azure 2.0 da riga di comando avviato con l'archivio Azure Data Lake | Documenti Microsoft
description: Utilizzare una riga di comando multipiattaforma di Azure 2.0 toocreate un account archivio Data Lake ed eseguire operazioni di base
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Introduzione ad Azure Data Lake Store con l'interfaccia della riga di comando di Azure 2.0
> [!div class="op_single_selector"]
> * [Portale](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK per Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Interfaccia della riga di comando di Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Informazioni sulla modalità di memorizzazione una Data Lake di Azure di toocreate toouse CLI di Azure 2.0 account e di eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati, eliminare l'account, e così via. Per altre informazioni su Data Lake Store, vedere [Panoramica di Data Lake Store](data-lake-store-overview.md).

Hello Azure CLI 2.0 è una nuova esperienza della riga di comando di Azure per la gestione delle risorse di Azure. Può essere usata in macOS, Linux e Windows. Per altre informazioni, vedere [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview) (Panoramica dell'interfaccia della riga di comando di Azure 2.0). È anche possibile esaminare hello [riferimento di Azure Data Lake archivio CLI 2.0](https://docs.microsoft.com/cli/azure/dls) per un elenco completo di comandi e sintassi.


## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questo articolo, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Interfaccia della riga di comando di Azure 2.0**: per istruzioni, vedere [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).

## <a name="authentication"></a>Autenticazione

Questo articolo usa un approccio di autenticazione più semplice con Data Lake Store in cui si accede come utente finale. Hello accesso livello tooData Lake archivio account file system e quindi è disciplinato dal livello di accesso hello di hello utente connesso. Tuttavia, esistono altri approcci come ben tooauthenticate con archivio Data Lake, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Accedi tooyour sottoscrizione di Azure

1. Accedere alla propria sottoscrizione di Azure.

    ```azurecli
    az login
    ```

    Si ottiene un codice toouse nel passaggio successivo hello. Utilizzare un web browser tooopen hello pagina https://aka.ms/devicelogin e immettere tooauthenticate codice hello. Si è toolog richiesta utilizzando le credenziali.

2. Quando si accede, tutti gli elenchi di finestra hello hello sottoscrizioni Azure in cui sono associate all'account. Utilizzare hello successivo comando toouse una sottoscrizione specifica.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Creare un account di Azure Data Lake Store

1. Creare un nuovo gruppo di risorse. Nel comando seguente di hello, fornire hello valori di parametro che si desidera toouse. Se il nome di percorso hello contiene spazi, è necessario inserirlo tra virgolette. Ad esempio "Stati Uniti orientali 2". 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Creare account archivio Data Lake hello.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Creare delle cartelle in un account Archivio Data Lake

È possibile creare cartelle sotto la toomanage account archivio Azure Data Lake e archiviare i dati. Hello utilizzo successivo comando toocreate una cartella denominata **mynewfolder** radice hello hello archivio Data Lake.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Hello `--folder` parametro assicura che il comando hello crea una cartella. Se questo parametro non è presente, il comando di hello crea un file vuoto denominato mynewfolder radice hello hello account archivio Data Lake.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Caricamento account archivio Data Lake tooa di dati

È possibile caricare l'archivio del data Lake tooData direttamente in hello livello o tooa cartella radice che è stato creato all'interno di account hello. Hello i frammenti di codice riportato di seguito viene illustrato come tooupload cartella toohello alcuni dati di esempio (**mynewfolder**) creata nella sezione precedente hello.

Se si sta cercando alcuni tooupload di dati di esempio, è possibile ottenere hello **dati ambulanza** cartella hello [Git Repository di Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Scaricare il file hello e archiviarlo in una directory locale nel computer in uso, ad esempio C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Per la destinazione di hello, è necessario specificare percorso completo di hello compreso il nome del file hello.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Elencare i file in un account Data Lake Store

Utilizzare i seguenti comandi toolist hello file in un account archivio Data Lake hello.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

output di Hello di questo oggetto deve essere simile toohello seguenti:

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Rinominare, scaricare ed eliminare i dati da un account Data Lake Store 

* **un file toorename**, utilizzare hello comando seguente:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **un file toodownload**, utilizzare hello comando seguente. Verificare che il percorso di destinazione hello specificato già esiste.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > comando Hello Crea cartella di destinazione hello se non esiste.
    > 
    >

* **un file toodelete**, utilizzare hello comando seguente:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Se si desidera toodelete hello cartella **mynewfolder** e file hello **vehicle1_09142014_copy.csv** insieme in un comando, utilizzare hello - recurse parametro

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Utilizzare autorizzazioni ed elenchi di controllo di accesso per un account Data Lake Store

In questa sezione informazioni su come toomanage ACL e autorizzazioni mediante Azure CLI 2.0. Per una spiegazione dettagliata di come vengono implementati gli elenchi di controllo di accesso in Azure Data Lake Store, vedere [Controllo di accesso in Azure Data Lake Store](data-lake-store-access-control.md).

* **proprietario hello tooupdate di una file o alla cartella**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **le autorizzazioni di hello tooupdate per una file o alla cartella**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **tooget hello ACL per un determinato percorso**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    output di Hello deve essere simile toohello seguenti:

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* **una voce per un ACL tooset**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **una voce per un ACL tooremove**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **un ACL predefinito intero tooremove**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **un ACL non predefinito intero tooremove**, utilizzare hello comando seguente:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Eliminare un account Archivio Data Lake
Utilizzare hello successivo comando toodelete un account archivio Data Lake.

```azurecli
az dls account delete --account mydatalakestore
```

Quando richiesto, immettere **Y** account hello toodelete.

## <a name="next-steps"></a>Passaggi successivi

* [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) (Informazioni di riferimento sull'interfaccia della riga di comando di Azure Data Lake Store 2.0)
* [Proteggere i dati in Data Lake Store](data-lake-store-secure-data.md)
* [Usare Azure Data Lake Analytics con Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usare Azure HDInsight con Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
