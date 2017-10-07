---
title: aaaCreate Azure i ruoli web e di lavoro per PHP | Documenti Microsoft
description: Una Guida toocreating PHP ruoli web e di lavoro in un servizio cloud di Azure e configurazione hello PHP runtime.
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Come i ruoli di lavoro e web PHP toocreate
## <a name="overview"></a>Panoramica
Questa guida Mostra come toocreate PHP web ruoli di lavoro o in un ambiente di sviluppo di Windows, scegliere una specifica versione di PHP hello "incorporate" versioni disponibili, modificare la configurazione di PHP hello, abilitare le estensioni e infine distribuire tooAzure. Viene inoltre descritto come tooconfigure un toouse ruolo web o di lavoro un runtime PHP (con configurazione personalizzata e le estensioni) specificata dall'utente.

## <a name="what-are-php-web-and-worker-roles"></a>Cosa sono i ruoli Web e di lavoro PHP?
Azure offre tre modelli di calcolo per le applicazioni in esecuzione: Servizio App di Azure, Macchine virtuali di Azure e Servizi cloud di Azure. Tutti e tre i modelli supportano PHP. Servizi cloud, che include ruoli Web e di lavoro, fornisce la tecnologia *PaaS (Platform as a Service)*. All'interno di un servizio cloud, un ruolo web fornisce un web Internet Information Services (IIS) dedicato applicazioni front-end web toohost di server. Un ruolo di lavoro può eseguire attività asincrone, con esecuzione prolungata o perpetue indipendenti dall'interazione o dall'input dell'utente.

Per altre informazioni su queste opzioni, vedere [Opzioni di hosting di calcolo fornite da Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Scaricare hello Azure SDK per PHP
Hello [Azure SDK per PHP] è costituito da diversi componenti. Questo articolo verranno utilizzati due di essi: Azure PowerShell e hello emulatori di Azure. Questi due componenti possono essere installati tramite installazione guidata piattaforma Web di Microsoft hello. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Creare un progetto di servizi cloud
Hello primo passaggio per la creazione di un ruolo web o di lavoro PHP è toocreate un progetto di servizio di Azure. un progetto di servizio di Azure funge da contenitore logico per i ruoli web e di lavoro e del progetto hello contiene [definizione (con estensione csdef) servizio] e [configurazione del servizio (. cscfg)] file.

toocreate un nuovo progetto di servizio di Azure, eseguire Azure PowerShell come amministratore ed eseguire hello comando seguente:

    PS C:\>New-AzureServiceProject myProject

Questo comando crea una nuova directory (`myProject`) toowhich è possibile aggiungere ruoli web e di lavoro.

## <a name="add-php-web-or-worker-roles"></a>Aggiungere ruoli Web o di lavoro PHP
tooadd progetto tooa ruolo web PHP, eseguire hello seguente comando dalla directory radice del progetto hello:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Per un ruolo di lavoro, utilizzare il comando seguente:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Hello `roleName` parametro è facoltativo. Se viene omesso, verrà generato automaticamente il nome di ruolo hello. ruolo web prima di Hello creato sarà `WebRole1`, sarà secondo hello `WebRole2`e così via. Hello primo ruolo di lavoro creato sarà `WorkerRole1`, sarà secondo hello `WorkerRole2`e così via.
>
>

## <a name="specify-hello-built-in-php-version"></a>Specificare la versione PHP predefiniti hello
Quando si aggiunge un PHP web o lavoro tooa progetto di ruolo, i file di configurazione del progetto hello vengono modificati in modo che PHP venga installato in ogni istanza di web o di lavoro dell'applicazione quando viene distribuito. versione di hello toosee di PHP che verranno installati per impostazione predefinita, eseguire hello comando seguente:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Hello output di hello comando precedente avrà un aspetto simile toowhat è illustrato di seguito. In questo esempio hello `IsDefault` flag è impostato troppo`true` per PHP 5.3.17, che indica che saranno hello predefinito PHP versione installata.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

È possibile impostare hello PHP runtime versione tooany delle versioni PHP hello elencati. Ad esempio la versione PHP hello tooset (per un ruolo con nome hello `roleName`) too5.4.0, utilizzare hello comando seguente:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Le versioni PHP disponibili potrebbero cambiare in futuro hello.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Personalizzare il runtime PHP predefinito di hello
Si dispone di controllo completo sulla configurazione di hello di hello PHP runtime che viene installato quando si esegue la procedura hello sopra, compresa la modifica di `php.ini` impostazioni e l'abilitazione delle estensioni.

toocustomize hello incorporato runtime PHP, seguire questi passaggi:

1. Aggiungere una nuova cartella, denominata `php`, toohello `bin` directory di un ruolo web. Per un ruolo di lavoro, aggiungere la directory radice del ruolo toohello.
2. In hello `php` cartella, creare un'altra cartella denominata `ext`. Inserire alcun `.dll` i file di estensione (ad esempio, `php_mongo.dll`) che si desidera tooenable in questa cartella.
3. Aggiungere un `php.ini` file toohello `php` cartella. Abilitare eventuali estensioni personalizzate e impostare qualsiasi direttiva PHP in questo file. Ad esempio, se si desidera tooturn `display_errors` in e abilitare hello `php_mongo.dll` estensione, il contenuto di hello del `php.ini` sarà come segue:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Eventuali impostazioni non vengono impostate in modo esplicito in hello `php.ini` file fornisce verrà automaticamente essere impostare valori predefiniti tootheir. Si tenga tuttavia presente che è possibile aggiungere un file `php.ini` completo.
>
>

## <a name="use-your-own-php-runtime"></a>Utilizzare il proprio runtime PHP
In alcuni casi, anziché la selezione di un runtime PHP predefinito e configurarlo come descritto in precedenza, è consigliabile tooprovide la propria esecuzione PHP. Ad esempio, è possibile utilizzare hello stesso runtime PHP in un ruolo web o di lavoro in uso nell'ambiente di sviluppo. Questo rende più semplice tooensure applicazione hello non modificherà il comportamento nell'ambiente di produzione.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Configurare un toouse ruolo web la propria esecuzione PHP
tooconfigure un toouse ruolo web un runtime PHP che si fornisce, seguire questi passaggi:

1. Creare un progetto di servizio Azure e aggiungere un ruolo Web PHP come descritto precedentemente in questo argomento.
2. Creare un `php` cartella hello `bin` cartella che si trova nella directory radice del ruolo web, quindi aggiunta il toohello di runtime (tutti i file binari, i file di configurazione, le sottocartelle, e così via) PHP `php` cartella.
3. (FACOLTATIVO) Se il runtime PHP utilizza hello [Microsoft Drivers for PHP per SQL Server][sqlsrv drivers], sarà necessario tooconfigure il tooinstall ruolo web [SQL Server Native Client 2012] [ sql native client] quando è disponibile. toodo, aggiungere hello [sqlncli.msi x64 installer] toohello `bin` cartella nella directory radice del ruolo web. script di avvio Hello descritto nel passaggio successivo hello eseguirà automaticamente installer hello quando viene eseguito il provisioning ruolo hello. Se il runtime PHP non utilizza hello Microsoft Drivers for PHP per SQL Server, è possibile rimuovere hello successiva riga da script hello illustrato nel passaggio successivo hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definire un'attività di avvio che configura [Internet Information Services (IIS)] [ iis.net] toouse il toohandle runtime PHP richieste per `.php` pagine. toodo, aprire hello `setup_web.cmd` file (in hello `bin` file della directory radice del ruolo web) in un editor di testo e sostituire il contenuto con hello seguenti script:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Aggiungere una directory radice dell'applicazione file tooyour del ruolo web. Questo valore sarà una directory radice del server web hello.
6. Pubblicare l'applicazione, come descritto in hello [pubblicare l'applicazione](#publish-your-application) sezione riportata di seguito.

> [!NOTE]
> Hello `download.ps1` script (in hello `bin` cartella della directory radice del ruolo web hello) può essere eliminato al termine dei passaggi hello descritto in precedenza per l'utilizzo proprio PHP runtime.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Configurare un toouse ruolo di lavoro proprio runtime PHP
tooconfigure un toouse ruolo di lavoro un runtime PHP che si fornisce, seguire questi passaggi:

1. Creare un progetto di servizio Azure e aggiungere un ruolo di lavoro PHP come descritto precedentemente in questo argomento.
2. Creare un `php` cartella nella directory radice del ruolo di lavoro hello, quindi aggiungere il toohello di runtime (tutti i file binari, i file di configurazione, le sottocartelle, e così via) PHP `php` cartella.
3. (FACOLTATIVO) Se il runtime PHP utilizza [Microsoft Drivers for PHP per SQL Server][sqlsrv drivers], sarà necessario tooconfigure il tooinstall ruolo di lavoro [SQL Server Native Client 2012] [ sql native client] quando è disponibile. toodo, aggiungere hello [sqlncli.msi x64 installer] directory radice del ruolo di lavoro toohello. script di avvio Hello descritto nel passaggio successivo hello eseguirà automaticamente installer hello quando viene eseguito il provisioning ruolo hello. Se il runtime PHP non utilizza hello Microsoft Drivers for PHP per SQL Server, è possibile rimuovere hello successiva riga da script hello illustrato nel passaggio successivo hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Definire un'attività di avvio che aggiunge il `php.exe` variabile di ambiente PATH del ruolo di lavoro eseguibile toohello quando viene eseguito il provisioning ruolo hello. toodo, aprire hello `setup_worker.cmd` file (nella directory radice del ruolo di lavoro hello) in un editor di testo e sostituirne il contenuto con hello lo script seguente:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Aggiungere una directory radice del ruolo di applicazione file tooyour lavoro.
6. Pubblicare l'applicazione, come descritto in hello [pubblicare l'applicazione](#publish-your-application) sezione riportata di seguito.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Eseguire l'applicazione in hello emulatori di calcolo e archiviazione
Hello gli emulatori di Azure forniscono un ambiente locale in cui è possibile testare l'applicazione Azure prima di distribuirla toohello cloud. Esistono alcune differenze tra gli emulatori hello e hello ambiente Azure. toounderstand meglio, vedere [Usa hello emulatore di archiviazione Azure per sviluppo e test](storage/common/storage-use-emulator.md).

Si noti che è necessario che PHP installato localmente emulatore di calcolo toouse hello. emulatore di calcolo Hello utilizzerà il toorun di installazione di PHP locale dell'applicazione.

eseguire il progetto in emulatori hello toorun hello il seguente comando dalla directory radice del progetto:

    PS C:\MyProject> Start-AzureEmulator

Si noterà toothis simili di output:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

È possibile visualizzare l'applicazione in esecuzione nell'emulatore hello aprendo un browser web e di esplorazione toohello indirizzo locale illustrato nell'output di hello (`http://127.0.0.1:81` nell'output di esempio hello sopra).

emulatori di hello toostop, eseguire il comando seguente:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Pubblicare l'applicazione
toopublish l'applicazione, è necessario importare toofirst le impostazioni di pubblicazione utilizzando hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet. Quindi è possibile pubblicare l'applicazione utilizzando hello [pubblica AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet. Per informazioni sull'accesso, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).

[Azure SDK per PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[definizione (con estensione csdef) servizio]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configurazione del servizio (. cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
