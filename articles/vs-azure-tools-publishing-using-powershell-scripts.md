---
title: aaaUsing tooDev tooPublish script di Windows PowerShell e gli ambienti di Test | Documenti Microsoft
description: Informazioni su come Windows PowerShell toouse gli script da ambienti di test e di toodevelopment toopublish Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>Utilizzo di Windows PowerShell consente di generare script toopublish toodev e test ambienti
Quando si crea un'applicazione web in Visual Studio, è possibile generare uno script di Windows PowerShell che è possibile usare la pubblicazione di hello tooautomate successive di tooAzure il sito Web come un'App Web nel servizio App di Azure o di una macchina virtuale. È possibile modificare ed estendere i requisiti di script di Windows PowerShell hello in toosuit editor di Visual Studio hello oppure integrarlo script hello compilazione esistente, test e script di pubblicazione.

Utilizzando questi script, è possibile eseguire il provisioning (noto anche come ambienti di sviluppo e test) di versioni personalizzate del sito per un utilizzo temporaneo. Ad esempio, è possibile configurare una particolare versione del sito Web in una macchina virtuale di Azure o hello slot toorun un sito Web di gestione temporanea un gruppo di test, riprodurre un bug, testare una correzione di bug, valutare una modifica proposta o configurare un ambiente personalizzato per una demo o una presentazione. Dopo aver creato uno script che pubblica il progetto, è possibile ricreare ambienti identici eseguendo nuovamente script hello, in base alle esigenze o eseguire script hello con build del toocreate di applicazione web un ambiente di test personalizzato.

## <a name="what-you-need"></a>Elementi necessari
* Azure SDK 2.3 o versioni successive Per altre informazioni vedere [Scaricare Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).

Gli script hello toogenerate di hello Azure SDK non è necessario per i progetti web. Questa funzionalità è per i progetti web, non per i ruoli web nei servizi cloud.

* Azure PowerShell 0.7.4 o versione successiva Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) o versione successiva.

## <a name="additional-tools"></a>Strumenti aggiuntivi
Sono disponibili altri strumenti e risorse per l'utilizzo di PowerShell in Visual Studio per lo sviluppo in Azure. Vedere [PowerShell Tools per Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Hello di generazione script di pubblicazione
È possibile generare hello script di pubblicazione per una macchina virtuale che ospita il sito Web quando si crea un nuovo progetto seguendo [queste istruzioni](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). È possibile anche [generare script di pubblicazione per le app Web del Servizio app di Azure](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Script generati da Visual Studio
Visual Studio genera una cartella a livello di soluzione denominata **PublishScripts** che contiene due file di Windows PowerShell, uno script di pubblicazione per la macchina virtuale o del sito Web e un modulo che contiene funzioni che è possibile utilizzare in hello script. Visual Studio genera anche un file in formato JSON hello che specifica i dettagli di hello del progetto hello che si sta distribuendo.

### <a name="windows-powershell-publish-script"></a>Pubblicazione di script da parte di Windows PowerShell
script di pubblicazione Hello contiene specifico pubblicare i passaggi per la distribuzione del sito Web tooa o una macchina virtuale. Visual Studio fornisce la colorazione della sintassi per lo sviluppo di Windows PowerShell . La Guida per le funzioni hello è disponibile ed è possibile modificare liberamente le funzioni hello in hello script toosuit propri requisiti.

### <a name="windows-powershell-module"></a>Modulo di Windows PowerShell
Hello modulo generato da Visual Studio contiene le funzioni hello di Windows PowerShell Usa script di pubblicazione. Queste sono funzioni di Azure PowerShell e non sono previsti toobe modificato. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.

### <a name="json-configuration-file"></a>File di configurazione JSON.
file JSON di Hello viene creato in hello **configurazioni** cartella e contiene i dati di configurazione che specifica esattamente quali tooAzure toodeploy risorse. nome di Hello del file hello generato da Visual Studio è progetto-nome-WAWS-DEV se è stato creato un sito Web o progetto nome-VM-DEV se è stata creata una macchina virtuale. Di seguito è riportato un esempio di un file di configurazione JSON generato quando si crea un sito Web. La maggior parte dei valori hello sono di chiara interpretazione. nome del sito Web Hello viene generato da Azure, pertanto potrebbe non corrispondere al nome del progetto.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
Quando si crea una macchina virtuale, il file di configurazione JSON hello ricerca simili toohello seguente. Si noti che viene creato un servizio cloud come contenitore per la macchina virtuale hello. macchina virtuale Hello contiene i consueti endpoint di hello per l'accesso al web tramite HTTP e HTTPS, oltre agli endpoint per distribuzione Web, che consente di pubblicare toohello sito Web dal computer locale, Desktop remoto e Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

È possibile modificare hello JSON configurazione toochange cosa accade quando si esegue hello script di pubblicazione. Hello `cloudService` e `virtualMachine` le sezioni sono obbligatorie, ma è possibile eliminare hello `databases` sezione se non è necessario. proprietà Hello vuota nel file di configurazione predefinita di hello generato da Visual Studio sono facoltative. che hanno valori nel file di configurazione predefinito hello sono obbligatori.

Se si dispone di un sito Web che dispone di più ambienti di distribuzione (noti come slot) anziché un unico sito di produzione in Azure, è possibile includere nome dello slot hello in nome hello del sito Web di hello nel file di configurazione JSON hello. Ad esempio, se si dispone di un sito Web denominato **mysite** e uno slot denominato **test** quindi hello URI è mysite test.cloudapp.net, ma hello nome corretto toouse nel file di configurazione hello è MySite (test) . È possibile farlo solo se gli slot e il sito Web di hello esistano già nella sottoscrizione. In caso contrario, Crea sito Web di hello eseguendo script hello senza specificare slot hello, quindi creare uno slot hello hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885), e successivamente eseguire script hello con il nome del sito Web modificato hello. Per altre informazioni sugli slot di distribuzione per le app Web, vedere [Configurare ambienti di gestione temporanea per le app Web del Servizio app di Azure](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Come toorun hello pubblica script
Se non è stato eseguito uno script di Windows PowerShell prima di, è innanzitutto necessario impostare hello esecuzione criteri tooenable script toorun. Si tratta di un utenti tooprevent funzionalità di protezione dall'esecuzione di script di Windows PowerShell se sono vulnerabili toomalware o virus che comportano l'esecuzione di script.

### <a name="run-hello-script"></a>Eseguire script hello
1. Creare pacchetto di distribuzione Web hello per il progetto. Un pacchetto di distribuzione Web è un archivio compresso (file con estensione zip) che contengono i file che si desidera sito Web tooyour toocopy o macchina virtuale. È possibile creare pacchetti di distribuzione Web in Visual Studio per qualsiasi applicazione web.

![Creare pacchetto di distribuzione web](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Per ulteriori informazioni, vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). È inoltre possibile automatizzare la creazione di hello del pacchetto di distribuzione Web, come descritto nella sezione hello **personalizzazione ed estensione hello pubblica script** più avanti in questo argomento.

1. In **Esplora**, aprire il menu di scelta hello per script hello e quindi scegliere **aprire con PowerShell ISE**.
2. Se si tratta di hello prima volta che si eseguono script di Windows PowerShell nel computer, aprire una finestra del prompt dei comandi con privilegi di amministratore e hello tipo comando seguente:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Accedi tooAzure utilizzando hello comando seguente.

    ```powershell
    Add-AzureAccount
    ```

    Quando richiesto, fornire nome utente e password.

    Si noti che quando si automatizza script hello, questo metodo per fornire le credenziali di Azure non funzionerà. In alternativa, è necessario utilizzare le credenziali tooprovide di file con estensione publishsettings hello. Una volta, è sufficiente usare il comando hello **Get-AzurePublishSettingsFile** hello toodownload file da Azure e successivamente usare **Import-AzurePublishSettingsFile** file hello tooimport. Per istruzioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

4. (Facoltativo) Se si desidera toocreate Azure le risorse, ad esempio hello virtual machine, database e del sito Web senza pubblicare l'applicazione web, utilizzare hello **Publish-WebApplication.ps1** con hello **-configurazione** argomento impostato toohello file di configurazione JSON. Questo comando Usa hello JSON configurazione file toodetermine toocreate le risorse. Poiché utilizza le impostazioni predefinite di hello per gli altri argomenti della riga di comando, crea risorse hello, ma non di pubblicare l'applicazione web. Hello-opzione /verbose offre ulteriori informazioni su ciò che accade.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Hello utilizzare **Publish-WebApplication.ps1** comando come illustrato in uno degli esempi tooinvoke hello script seguente hello e pubblicare l'applicazione web. Se è necessario toooverride le impostazioni predefinite di hello per le hello altri argomenti, ad esempio nome della sottoscrizione hello, nome del pacchetto, le credenziali di macchina virtuale o le credenziali del server database di pubblicazione, è possibile specificare tali parametri. Hello utilizzare **-Verbose** opzione toosee ulteriori informazioni sullo stato di avanzamento hello di hello processo di pubblicazione.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    Se si crea una macchina virtuale, il comando di hello è simile al seguente hello. Questo esempio mostra anche come hello toospecify le credenziali per più database. Per le macchine virtuali hello create da questi script, certificati SSL hello non da un'autorità radice attendibile. È pertanto necessario hello toouse **-AllowUntrusted** opzione.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    Hello script può creare database, ma non crea server di database. Se si desidera toocreate un server di database, è possibile utilizzare hello **New-AzureSqlDatabaseServer** funzione nel modulo Azure hello.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Personalizzazione ed estensione hello pubblica script
È possibile personalizzare hello pubblicare script e file di configurazione JSON. Hello funzioni nel modulo di Windows PowerShell hello **AzureWebAppPublishModule.psm1** non sono previsti toobe modificato. Se si appena desidera toospecify un database diverso o modificare alcune delle proprietà hello della macchina virtuale hello, modificare il file di configurazione JSON hello. Se si vuole la funzionalità di hello tooextend di hello script tooautomate compilazione e test del progetto, è possibile implementare stub di funzioni in **Publish-WebApplication.ps1**.

tooautomate compilazione del progetto, aggiungere il codice che chiama MSBuild troppo`New-WebDeployPackage` come illustrato nell'esempio di codice. Hello percorso toohello comando MSBuild è diversa a seconda della versione di hello di Visual Studio è installato. percorso corretto hello tooget, è possibile utilizzare la funzione hello **Get-MSBuildCmd**, come illustrato in questo esempio.

### <a name="tooautomate-building-your-project"></a>compilazione del progetto tooautomate
1. Aggiungere hello `$ProjectFile` parametro nella sezione parametri globali hello.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copy (funzione) hello `Get-MSBuildCmd` nel file di script.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Sostituire `New-WebDeployPackage` con hello seguente di codice e sostituire il segnaposto hello nella costruzione di riga hello `$msbuildCmd`. Questo codice è per Visual Studio 2015. Se si utilizza Visual Studio 2013, modificare hello **VisualStudioVersion** proprietà seguente troppo`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild l'applicazione web, usare MsBuild.exe. Per informazioni, vedere il riferimento della riga di comando di MSBuild all'indirizzo: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Avvia l'esecuzione del comando di compilazione hello

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Chiamare hello `New-WebDeployPackage` funzione prima di questa riga: `$Config = Read-ConfigFile $Configuration` per le app web o `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` per le macchine virtuali.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Richiamare hello personalizzato script dalla riga di comando utilizzando il passaggio hello `$Project` argomento, come hello seguente riga di comando di esempio.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate il test dell'applicazione, aggiungere il codice troppo`Test-WebApplication`. Essere toouncomment che righe hello **Publish-WebApplication.ps1** in cui queste funzioni vengono chiamate. Se non si fornisce un'implementazione, è possibile creare manualmente il progetto con Visual Studio, di pubblicare script toopublish tooAzure hello esecuzione.

## <a name="publishing-function-summary"></a>Riepilogo della funzione di pubblicazione
tooget della Guida per le funzioni che è possibile usare al prompt dei comandi di Windows PowerShell hello, utilizzare il comando di hello `Get-Help function-name`. Guida di Hello sono inclusi esempi e informazioni sui parametri. stesso testo della Guida è disponibile anche nei file di origine script hello, Hello **AzureWebAppPublishModule.psm1** e **Publish-WebApplication.ps1**. Guida in linea e script hello è localizzati nella lingua di Visual Studio.

**AzureWebAppPublishModule**

| Nome della funzione | Description |
| --- | --- |
| Aggiungere AzureSQLDatabase |Creare un nuovo database SQL Azure. |
| Aggiungere AzureSQLDatabases |Crea database SQL di Azure dai valori hello nel file di configurazione JSON hello generato da Visual Studio. |
| Aggiungere-AzureVM |Crea una macchina virtuale di Azure e restituisce il che URL hello di hello distribuito macchina virtuale. Hello funzione imposta i prerequisiti di hello e quindi hello chiamate **New-AzureVM** funzione toocreate (modulo Azure) una nuova macchina virtuale. |
| Aggiungere AzureVMEndpoints |Aggiunge una nuova macchina virtuale di tooa gli endpoint di input e restituisce hello di macchina virtuale con nuovo endpoint hello. |
| Aggiungere AzureVMStorage |Crea un nuovo account di archiviazione di Azure nella sottoscrizione corrente hello. nome Hello dell'account di hello inizia con "devtest" seguito da una stringa alfanumerica univoca. funzione Hello restituisce il nome di hello del nuovo account di archiviazione hello. È necessario specificare un percorso o un gruppo di affinità per il nuovo account di archiviazione hello. |
| Aggiungere-AzureWebsite |Crea un sito Web con percorso e il nome specificato hello. Questa funzione chiama hello **New-AzureWebsite** funzione nel modulo Azure hello. Se la sottoscrizione hello non include già un sito Web con nome specificato hello, questa funzione Crea sito Web di hello e restituisce un oggetto sito Web. In caso contrario, restituirà `$null`. |
| Backup-Sottoscrizione |Consente di risparmiare hello sottoscrizione Azure corrente nella hello `$Script:originalSubscription` variabile nell'ambito dello script. Questa funzione Salva la sottoscrizione di Azure corrente di hello (ottenuta da `Get-AzureSubscription -Current`) e il relativo account di archiviazione, nonché hello sottoscrizione viene modificato da questo script (archiviata nella variabile hello `$UserSpecifiedSubscription`) e il relativo account di archiviazione, nell'ambito dello script. Salvando i valori hello, è possibile utilizzare una funzione, ad esempio `Restore-Subscription`, toorestore hello corrente sottoscrizione e l'archiviazione account toocurrent stato originale se è stato modificato lo stato corrente di hello. |
| Trovare-AzureVM |Ottiene hello specificato macchina virtuale di Azure. |
| Formato DevTestMessageWithTime |Antepone data e ora tooa messaggio. Questa funzione è progettata per i messaggi scritti toohello flussi di errore e dettagliato. |
| Get-AzureSQLDatabaseConnectionString |Assembla un database SQL di Azure di tooan tooconnect di stringa di connessione. |
| Get-AzureVMStorage |Nome dell'account di archiviazione prima di hello con modello di nome hello di hello restituisce "devtest*" (tra maiuscole e minuscole) nel gruppo di affinità o percorso specificato hello. Se hello "devtest*" account di archiviazione non corrisponde al percorso di hello o un gruppo di affinità, viene ignorato dalla funzione hello. È necessario specificare un percorso o un gruppo di affinità. |
| Get-MSDeployCmd |Restituisce uno strumento di comando toorun hello MsDeploy.exe. |
| Nuovo AzureVMEnvironment |Trova o crea una macchina virtuale nella sottoscrizione di hello che corrispondono ai valori nel file di configurazione JSON hello hello. |
| Pubblicare-WebPackage |Usa MsDeploy.exe e un sito web di pubblicazione del pacchetto. Sito Web tooa di ZIP file toodeploy risorse. Questa funzione non genera alcun output. Se hello chiamata tooMSDeploy.exe non riesce, la funzione hello genera un'eccezione. tooget più dettagliati di output, utilizzare hello **-Verbose** opzione. |
| Pubblicar-WebPackageToVM |Verificare i valori di parametro hello e quindi chiama hello **Publish-WebPackage** (funzione). |
| Leggere-configFile |Convalida il file di configurazione JSON hello e restituisce una tabella hash di valori selezionati. |
| Ripristina-Subscription |Reimposta hello sottoscrizione toohello originale abbonamento. |
| Test-AzureModule |Restituisce `$true` se hello installato la versione del modulo Azure è 0.7.4 o successiva. Restituisce `$false` se il modulo di hello non è installato o è una versione precedente. Questa funzione non ha parametri. |
| Test-AzureModuleVersion |Restituisce `$true` se hello versione di hello modulo Azure è 0.7.4 o successiva. Restituisce `$false` se il modulo di hello non è installato o è una versione precedente. Questa funzione non ha parametri. |
| Test-HttpsUrl |Converte l'oggetto System. Uri tooa hello input URL. Restituisce `$True` se hello URL è assoluto e relativo schema è https. Restituisce `$false` se hello URL è relativo, lo schema non è HTTPS o stringa di input hello non può essere convertito tooa URL. |
| Test- Member |Restituisce `$true` se una proprietà o metodo è un membro dell'oggetto hello. In caso contrario, restituisce `$false`. |
| Scrivere-ErrorWithTime |Scrive un messaggio di errore preceduto hello ora corrente. Questa funzione chiama hello **Format-DevTestMessageWithTime** ora hello tooprepend di funzione prima di scrivere il flusso di errore toohello messaggio hello. |
| Scrivere-HostWithTime |Scrive un programma host di messaggio toohello (**Write-Host**) preceduti hello ora corrente. Hello effetto della scrittura del programma host toohello varia. La maggior parte dei programmi che ospitano Windows PowerShell di scrittura questi messaggi toostandard output. |
| Scrivere-VerboseWithTime |Scrive un messaggio dettagliato preceduto hello ora corrente. Poiché chiama **Write-Verbose**, il messaggio hello viene visualizzato solo quando viene eseguito uno script hello con hello **Verbose** parametro o quando hello **VerbosePreference** preferenza è impostare troppo**continua**. |

**Pubblicare-WebApplication**

| Nome della funzione | Description |
| --- | --- |
| Nuovo-AzureWebApplicationEnvironment |Crea risorse di Azure, ad esempio una macchina virtuale o un sito Web. |
| Nuovo-WebDeployPackage |Questa funzione non è implementata. È possibile aggiungere comandi in toobuild questa funzione al progetto. |
| Pubblicare-AzureWebApplication |Pubblica un tooAzure di applicazione web. |
| Pubblicare-WebApplication |Crea e distribuisce le app Web, le macchine virtuali, i database SQL e gli account di archiviazione per un progetto web Visual Studio. |
| Test-WebApplication |Questa funzione non è implementata. È possibile aggiungere comandi in questo tootest funzione dell'applicazione. |

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sulla creazione di script PowerShell leggendo [Scripting con Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) e vedere altri script di PowerShell di Azure in hello [Script Center](https://azure.microsoft.com/documentation/scripts/).
