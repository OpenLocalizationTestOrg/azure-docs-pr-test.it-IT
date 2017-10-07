---
title: aaaDevelop e Azure esecuzione funzioni localmente | Documenti Microsoft
description: Informazioni su come toocode e test di Azure funziona nel computer locale prima di eseguire funzioni di Azure.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Scrivere codice per le funzioni di Azure e testarle in locale

Durante la hello [portale di Azure] fornisce una procedura completa di set di strumenti per lo sviluppo e test funzioni di Azure, molti sviluppatori preferiscono un'esperienza di sviluppo locale. Funzioni di Azure rende facile toouse i Preferiti codice editor e toodevelop strumenti di sviluppo locale e testare le funzioni nel computer locale. Le funzioni possono attivare gli eventi in Azure ed è possibile eseguire il debug delle funzioni JavaScript e C# nel computer locale. 

Se si sviluppatori di Visual Studio C#, Funzioni di Azure [si integra anche con Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Installare strumenti di base delle funzioni di hello Azure

Strumenti di base di funzioni di Azure è una versione locale del runtime di Azure funzioni hello che è possibile eseguire nel computer locale di Windows. Non è un emulatore o simulatore. È hello runtime stesso che supporta le funzioni in Azure.

Hello [strumenti di base di Azure funzioni] viene fornito come un pacchetto npm. È innanzitutto necessario [installare NodeJS](https://docs.npmjs.com/getting-started/installing-node), che include npm.  

>[!NOTE]
>In questo momento, pacchetto di strumenti di Azure funzioni principali di hello può essere installato solo nei computer Windows. Questa restrizione è a causa di limitazione temporanea tooa host funzioni hello.

[strumenti di base di Azure funzioni] aggiunge hello alias di comandi seguenti:
* **func**
* **azfun**
* **azurefunctions**

Tutti questi alias può essere usati al posto di `func` illustrato negli esempi di hello in questo argomento.

## <a name="create-a-local-functions-project"></a>Creare un progetto Funzioni locale

Quando si esegue in locale, un progetto di funzioni è una directory con local.settings.json e host.json file hello. Questa directory è hello equivalente di un'app di funzione in Azure. toolearn ulteriori informazioni sulla struttura di cartelle di Azure funzioni, hello vedere hello [Guida per sviluppatori di Azure funzioni](functions-reference.md#folder-structure).

Al prompt dei comandi eseguire hello comando seguente:

```
func init MyFunctionProj
```

output di Hello è simile hello di esempio seguente:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt fuori la creazione di un repository Git, utilizzare l'opzione hello `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>File di impostazioni locali

local.settings.json file Hello archivia le impostazioni dell'app, le stringhe di connessione e le impostazioni per strumenti di base di funzioni di Azure. Dispone di hello seguente struttura:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Impostazione      | Descrizione                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Quando impostato troppo**true**, tutti i valori sono crittografati utilizzando una chiave del computer locale. Usato con i comandi `func settings`. Il valore predefinito è **false**. |
| **Valori** | Raccolta di impostazioni dell'applicazione usate durante l'esecuzione in locale. Aggiungere l'oggetto toothis le impostazioni dell'applicazione.  |
| **AzureWebJobsStorage** | Set di hello toohello di stringa di connessione account di archiviazione di Azure che viene utilizzata internamente dal runtime di Azure funzioni hello. account di archiviazione Hello supporta i trigger della funzione. Questa impostazione di connessione per l'account di archiviazione è obbligatorio per tutte le funzioni ad eccezione delle funzioni attivate da HTTP.  |
| **AzureWebJobsDashboard** | Imposta hello connessione stringa toohello account di archiviazione Azure che viene utilizzato toostore hello funzione log. Questo valore facoltativo rende accessibile portale hello hello registri.|
| **Host** | Le impostazioni in questa sezione personalizzare processo host di funzioni hello durante l'esecuzione in locale. | 
| **LocalHttpPort** | Set di hello porta predefinita utilizzata quando si esegue l'host di funzioni locali hello (`func host start` e `func run`). Hello `--port` opzione della riga di comando ha la precedenza su questo valore. |
| **CORS** | Definisce le entità Origin hello consentita per [risorse multiorigine (CORS) di condivisione](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Le origini sono elencate in un elenco delimitato dalla virgola senza spazi. valore di carattere jolly Hello (**\***) è supportata, che consente le richieste provenienti da qualsiasi origine. |
| **ConnectionStrings** | Contiene le stringhe di connessione database hello per le funzioni. Le stringhe di connessione in questo oggetto vengono aggiunti ambiente toohello con tipo di provider di hello di **SqlClient**.  | 

La maggior parte dei trigger e le associazioni presentano un **connessione** proprietà che esegue il mapping toohello nome di un'impostazione di app o variabile di ambiente. Per ogni proprietà di connessione, deve essere definita un'impostazione dell'app nel file local.settings.json. 

Queste impostazioni possono anche essere lette nel codice come variabili di ambiente. In C# usare [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). In JavaScript usare `process.env`. Le impostazioni specificate come una variabile di ambiente del sistema hanno la precedenza sui valori nel file local.settings.json hello. 

Le impostazioni nel file local.settings.json hello vengono utilizzate solo per gli strumenti di funzioni durante l'esecuzione in locale. Per impostazione predefinita, queste impostazioni non vengono migrate automaticamente al progetto hello tooAzure pubblicato. Hello utilizzare `--publish-local-settings` passare [quando si pubblica](#publish) toomake che queste impostazioni vengono aggiunti toohello funzione app in Azure.

Quando in cui non è impostata alcuna stringa di connessione di archiviazione valida per **AzureWebJobsStorage**, hello seguente messaggio di errore viene visualizzato:  

>Valore mancante per AzureWebJobsStorage in local.settings.json. È necessario per tutti i trigger diversi da HTTP. È possibile eseguire "func azure functionary fetch-app-settings <functionAppName>" o specificare una stringa di connessione in local.settings.json.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Configurare le impostazioni applicazione

tooset un valore per le stringhe di connessione, è possibile eseguire una delle seguenti hello:
* Immettere la stringa di connessione hello da [Azure Storage Explorer](http://storageexplorer.com/).
* Utilizzare uno dei seguenti comandi hello:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Entrambi i comandi richiedono si toofirst Accedi tooAzure.

## <a name="create-a-function"></a>Creare una funzione

toocreate una funzione, eseguire hello comando seguente:

```
func new
``` 
`func new`hello supporta gli argomenti facoltativi seguenti:

| Argomento     | Descrizione                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | modello di Hello programmazione linguaggio, ad esempio c#, F # o JavaScript. |
| **`--template -t`** | nome del modello Hello. |
| **`--name -n`** | nome della funzione Hello. |

Ad esempio, toocreate un trigger di JavaScript HTTP, eseguire:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate una funzione di attivazione coda, eseguire:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Eseguire funzioni localmente

toorun un progetto di funzioni, hello funzioni host eseguito. host di Hello Abilita i trigger per tutte le funzioni nel progetto hello:

```
func host start
```

`func host start`hello supporta le opzioni seguenti:

| Opzione     | Descrizione                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Hello porta locale toolisten in. Valore predefinito: 7071. |
| **`--debug <type>`** | opzioni di Hello sono `VSCode` e `VS`. |
| **`--cors`** | Un elenco delimitato dalla virgola di origini CORS, senza spazi. |
| **`--nodeDebugPort -n`** | porta Hello hello nodo debugger toouse. Predefinito: un valore di launch.json o 5858. |
| **`--debugLevel -d`** | livello di traccia console Hello (disattivato, verbose, info, warning o error). Predefinito: Info.|
| **`--timeout -t`** | Hello timeout per l'avvio di hello funzioni host t o, in secondi. Impostazione predefinita: 20 secondi.|
| **`--useHttps`** | Associare toohttps://localhost: {porta} anziché toohttp://localhost: {porta}. Per impostazione predefinita, questa opzione crea un certificato attendibile nel computer in uso.|
| **`--pause-on-error`** | Sospendere un input aggiuntivo prima della chiusura processo hello. Utile quando si avvia Strumenti di base di Funzioni di Azure da un ambiente di sviluppo integrato (IDE).|

Quando viene avviato l'host di hello funzioni, funzioni di attivazione HTTP di URL hello restituisce come output:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Eseguire il debug in Visual Studio Code o Visual Studio

tooattach un debugger, passare hello `--debug` argomento. le funzioni JavaScript toodebug, utilizzare Visual Studio Code. Per le funzioni C#, usare Visual Studio.

le funzioni toodebug c#, utilizzare `--debug vs`. È anche possibile usare [Strumenti di Visual Studio 2017 per Funzioni di Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

toolaunch hello host e impostare il debug di JavaScript, eseguire:

```
func host start --debug vscode
```

Quindi, nel codice di Visual Studio, in hello **Debug** visualizzazione, selezionare **allegare tooAzure funzioni**. È possibile associare punti di interruzione, controllare variabili ed eseguire il codice passo per passo.

![Debug di JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Funzione tooa dati di test passaggio

È inoltre possibile richiamare una funzione direttamente tramite `func run <FunctionName>` e fornire i dati di input per la funzione hello. Questo comando è simile toorunning una funzione che usa hello **Test** scheda hello portale di Azure. Questo comando Avvia host funzioni intera hello.

`func run`hello supporta le opzioni seguenti:

| Opzione     | Descrizione                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Contenuto inline. |
| **`--debug -d`** | Collegare un processo host del debugger toohello prima di eseguire la funzione hello.|
| **`--timeout -t`** | Toowait tempo (in secondi) fino a quando l'host di funzioni locali hello è pronto.|
| **`--file -f`** | Hello toouse nome file come contenuto.|
| **`--no-interactive`** | Non richiede input. Utile per scenari di automazione.|

Ad esempio, toocall una funzione di attivazione HTTP e corpo del contenuto di passaggio, eseguire hello comando seguente:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Pubblicare tooAzure

un'app di funzione funzioni tooa progetto in Azure, utilizzare hello toopublish `publish` comando:

```
func azure functionapp publish <FunctionAppName>
```

È possibile utilizzare hello le opzioni seguenti:

| Opzione     | Descrizione                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Le impostazioni di pubblicazione in tooAzure local.settings.json, chiedere al toooverwrite se hello impostazione già esiste.|
| **`--overwrite-settings -y`** | Deve essere usato con `-i`. Sovrascrive AppSettings in Azure con il valore locale se diverso. Viene suggerito il valore predefinito.|

Hello `publish` comando Carica il contenuto di hello della directory di progetto funzioni hello. Se si eliminano i file localmente, hello `publish` comando non vengono eliminati da Azure. È possibile eliminare i file in Azure utilizzando hello [strumento Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [portale di Azure].

## <a name="next-steps"></a>Passaggi successivi

Strumenti di base di Funzioni di Azure è [open source ed è ospitato su GitHub](https://github.com/azure/azure-functions-cli).  
una richiesta di bug o funzionalità toofile [aprire un problema di GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[strumenti di base di Azure funzioni]: https://www.npmjs.com/package/azure-functions-core-tools
[portale di Azure]: https://portal.azure.com 
