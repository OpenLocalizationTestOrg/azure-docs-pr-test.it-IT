---
title: aaaUse hello API REST tooget avviato con l'archivio Data Lake | Documenti Microsoft
description: Utilizzare le API REST WebHDFS tooperform operazioni in archivio Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Introduzione ad Archivio Azure Data Lake con API REST
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

In questo articolo si apprenderà come account toouse WebHDFS REST API e le API REST di Data Lake archivio tooperform gestione nonché operazioni di file System in archivio Azure Data Lake. Archivio Azure Data Lake espone le proprie API REST per operazioni di gestione account. Tuttavia, dal momento che Archivio Data Lake è compatibile con l'ecosistema Hadoop e HDFS, supporta le operazioni del file system tramite le API REST WebHDFS.

> [!NOTE]
> Per informazioni dettagliate sul supporto di API REST hello per archivio Data Lake, vedere [Azure Data Lake archivio REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Creare un'applicazione di Azure Active Directory**. Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD. Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**. Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). In questo articolo Usa toodemonstrate cURL come toomake API REST chiama rispetto a un account archivio Data Lake.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Come si esegue l'autenticazione tramite Azure Active Directory?
È possibile utilizzare due approcci tooauthenticate, tramite Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticazione dell'utente finale (interattiva)
In questo scenario, l'applicazione hello chiede toolog utente hello in e tutte le operazioni hello vengono eseguite nel contesto di hello dell'utente hello. Eseguire hello alla procedura seguente per l'autenticazione interattiva.

1. Tramite l'applicazione, il reindirizzamento hello utente toohello URL seguente:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI di reindirizzamento > deve toobe codificati per l'uso in un URL. Per https://localhost, usare quindi `https%3A%2F%2Flocalhost`
   > 
   > 
   
    A scopo di hello di questa esercitazione, è possibile sostituire i valori segnaposto hello nell'URL hello in precedenza e incollarlo nella barra degli indirizzi del web browser. Sarà reindirizzato tooauthenticate utilizzando l'account di accesso di Azure. Una volta che riesce ad accedere, risposta hello viene visualizzato nella barra degli indirizzi del browser hello. risposta Hello sarà in hello seguente formato:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Acquisire il codice di autorizzazione hello dalla risposta hello. Per questa esercitazione, è possibile copiare il codice di autorizzazione hello dalla barra degli indirizzi del browser web hello hello e passarlo in hello POST richiesta toohello endpoint token, come illustrato di seguito:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > In questo caso, hello \<URI di reindirizzamento > non devono essere codificati.
   > 
   > 
3. risposta Hello è un oggetto JSON che contiene un token di accesso (ad esempio, `"access_token": "<ACCESS_TOKEN>"`) e un token di aggiornamento (ad esempio, `"refresh_token": "<REFRESH_TOKEN>"`). L'applicazione utilizza il token di accesso di hello quando si accede a un archivio Azure Data Lake e hello aggiornamento token tooget un altro token di accesso quando scade un token di accesso.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Quando il token di accesso hello scade, è possibile richiedere un nuovo token di accesso usando il token di aggiornamento di hello, come illustrato di seguito:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Per altre informazioni sull'autenticazione utente interattiva, vedere [Flusso di concessione del codice di autorizzazione](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticazione da servizio a servizio (non interattiva)
In questo scenario, un'applicazione hello hello fornisce operazioni hello tooperform le proprie credenziali. A tale scopo, è necessario inviare una richiesta POST come hello illustrato di seguito. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

output di Hello della richiesta includerà un token di autorizzazione (indicato da `access-token` nell'output di hello riportato di seguito) che verranno successivamente passati con le chiamate API REST. Salvare questo token di autenticazione in un file di testo, che sarà necessario più avanti in questo articolo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Questo articolo Usa hello **interattivo** approccio. Per ulteriori informazioni sulle modalità interattiva (chiamate service to service), vedere [tooservice chiamate utilizzando le credenziali del servizio](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Creare un account Archivio Data Lake
Questa operazione è basata su chiamata API REST hello definito [qui](https://msdn.microsoft.com/library/mt694078.aspx).

Utilizzare hello cURL comando seguente. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza. payload della richiesta Hello per questo comando è contenuto in hello **input.json** file fornito per hello `-d` parametro precedente. il contenuto di Hello del file input.json hello nella figura seguente hello:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Creare delle cartelle in un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Utilizzare hello cURL comando seguente. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza. Questo comando crea una directory denominata **mytempdir** nella cartella radice hello del tuo account archivio Data Lake.

Se il completamento dell'operazione hello dovrebbe essere una risposta simile alla seguente:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Elencare le cartelle in un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Utilizzare hello cURL comando seguente. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

In hello in precedenza di comando, sostituire \< `REDACTED` \> con token di autorizzazione hello recuperati in precedenza.

Se il completamento dell'operazione hello dovrebbe essere una risposta simile alla seguente:

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Caricare dati in un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Utilizzare hello cURL comando seguente. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

In hello sopra sintassi **-T** parametro è il percorso di hello si sta caricando file hello.

output di Hello è simile toohello seguenti:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Leggere i dati da un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

La lettura dei dati da un account Archivio Data Lake è un processo in due fasi.

* È prima di inviare una richiesta GET endpoint hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Verrà restituito una percorso toosubmit hello GET richiesta successiva.
* È quindi inviare la richiesta di recupero hello endpoint hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Verrà visualizzato il contenuto di hello del file hello.

Tuttavia, poiché non esiste alcuna differenza hello parametri di input tra hello hello e innanzitutto secondo passaggio, è possibile utilizzare hello `-L` parametro toosubmit hello della prima richiesta. `-L`opzione essenzialmente combina due richieste in un e renderà cURL Ripeti richiesta hello nella nuova posizione hello. Infine, hello output di tutte le chiamate richiesta hello viene visualizzato, come illustrato di seguito. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Verrà visualizzato un segue toohello simili di output:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Rinominare un file in un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Seguente hello usare cURL comando toorename un file. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Verrà visualizzato un segue toohello simili di output:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Eliminare un file da un account Archivio Data Lake
Questa operazione è basata su chiamata API REST WebHDFS hello definito [qui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Seguente hello usare cURL comando toodelete un file. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Verrà visualizzato un output simile hello seguente:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Eliminare un account Archivio Data Lake
Questa operazione è basata su chiamata API REST hello definito [qui](https://msdn.microsoft.com/library/mt694075.aspx).

Seguente hello usare cURL comando toodelete un account archivio Data Lake. Sostituire **\<yourstorename>** con il nome di Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Verrà visualizzato un output simile hello seguente:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Vedere anche
* [Aprire le applicazioni Big Data di origine che funzionano con Archivio Azure Data Lake](data-lake-store-compatible-oss-other-applications.md)

