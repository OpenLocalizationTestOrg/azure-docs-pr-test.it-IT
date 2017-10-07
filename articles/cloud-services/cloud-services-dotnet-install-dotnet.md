---
title: aaaInstall .NET per i ruoli di servizi Cloud di Azure | Documenti Microsoft
description: In questo articolo viene descritto come toomanually installarvi hello .NET Framework i ruoli web e di lavoro dei servizi cloud
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a>Installare .NET nei ruoli di Servizi cloud di Azure
In questo articolo viene descritto come tooinstall versioni di .NET Framework che non provengono con hello del sistema operativo Guest Azure. È possibile utilizzare .NET su hello del sistema operativo Guest tooconfigure i ruoli web e di lavoro del servizio cloud.

Ad esempio, è possibile installare .NET 4.6.1 in hello famiglia di sistemi operativi Guest 4, non disponibili con qualsiasi versione di .NET 4.6. (hello famiglia del sistema operativo Guest 5 viene fornito con .NET 4.6). Per informazioni più recenti di hello in hello versioni del sistema operativo Guest Azure, vedere hello [notizie di versione del sistema operativo Guest Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 contiene una restrizione sulla distribuzione per la famiglia di sistemi operativi Guest hello 4 o versioni precedente di .NET 4.6. È disponibile in hello una correzione per la restrizione di hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) sito.

tooinstall .NET nei ruoli di lavoro e web, includono hello web programma d'installazione .NET come parte del progetto servizio cloud. Avviare Installazione guidata di hello come parte delle attività di avvio del ruolo hello. 

## <a name="add-hello-net-installer-tooyour-project"></a>Aggiungi progetto tooyour programma di installazione di .NET hello
programma di installazione di toodownload hello web per .NET Framework, hello scegliere versione hello che si desidera tooinstall:

* [Programma di installazione Web di .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298)
* [Programma di installazione Web di .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729)

il programma di installazione di tooadd hello per un *web* ruolo:
  1. In **Ruoli** del progetto di servizio cloud in **Esplora soluzioni** fare clic con il pulsante destro del mouse sul ruolo *Web* e scegliere **Aggiungi** > **Nuova cartella**. Creare una cartella denominata **bin**.
  2. Fare clic sulla cartella bin hello e selezionare **Aggiungi** > **elemento esistente**. Selezionare il programma di installazione di hello .NET e aggiungerlo toohello nella cartella bin.
  
il programma di installazione di tooadd hello per un *lavoro* ruolo:
* Fare clic con il pulsante destro del mouse sul ruolo *di lavoro* e scegliere **Aggiungi** > **Elemento esistente**. Selezionare il programma di installazione di hello .NET e aggiungerlo toohello ruolo. 

Quando vengono aggiunti file nella cartella del contenuto in questo modo toohello ruolo, vengono aggiunte automaticamente tooyour pacchetto del servizio cloud. vengono quindi distribuito tooa posizione coerente sulla macchina virtuale hello, i file Hello. Ripetere questo processo per ogni ruolo web e di lavoro nel servizio cloud in modo che tutti i ruoli sono una copia del programma di installazione hello.

> [!NOTE]
> Anche se l'applicazione è destinata a .NET 4.6, è necessario installare .NET 4.6.1 nel ruolo del servizio cloud. Hello del sistema operativo Guest include hello Knowledge Base [aggiornare 3098779](https://support.microsoft.com/kb/3098779) e [aggiornare 3097997](https://support.microsoft.com/kb/3097997). Durante l'esecuzione delle applicazioni .NET se .NET 4.6 è installata nella parte superiore di aggiornamenti della Knowledge Base hello, possono verificarsi i problemi. tooavoid questi problemi, installare .NET 4.6.1 anziché versione 4.6. Per ulteriori informazioni, vedere hello [articolo della Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Contenuto del ruolo con i file del programma di installazione][1]

## <a name="define-startup-tasks-for-your-roles"></a>Definire le attività di avvio per i ruoli
È possibile utilizzare le operazioni di avvio attività tooperform prima dell'avvio di un ruolo. L'installazione di .NET Framework hello come parte dell'attività di avvio hello assicura tale framework hello viene installato prima di eseguita qualsiasi codice dell'applicazione. Per altre informazioni sulle attività di avvio, vedere [Eseguire attività di avvio in Azure](cloud-services-startup-tasks.md). 

1. Aggiungere i seguenti file servicedefinition. Csdef toohello contenuto in hello hello **WebRole** o **WorkerRole** nodo per tutti i ruoli:
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    Hello configurazione precedente viene eseguito il comando di console hello `install.cmd` con tooinstall di privilegi di amministratore hello .NET Framework. configurazione di Hello crea anche un **LocalStorage** elemento denominato **NETFXInstall**. script di avvio Hello imposta hello cartella temporanea toouse questa risorsa di archiviazione locale. 
    
    > [!IMPORTANT]
    > tooensure corretta installazione di framework hello, hello dimensioni del set di tooat questa risorsa almeno 1024 MB.
    
    Per altre informazioni sulle attività di avvio, vedere [Attività di avvio comuni del servizio cloud](cloud-services-startup-tasks-common.md).

2. Creare un file denominato **Install** e aggiungere i seguenti hello installare file di script toohello.

    script Hello controlla se versione specificata di hello di hello .NET Framework è già installato nel computer di hello eseguendo una query del Registro di sistema di hello. Se la versione di .NET hello non è installata, viene aperto il programma di installazione di hello .NET web. toohelp risolvere eventuali problemi, lo script di hello registra tutte le attività toohello file startuptasklog-(data e ora correnti). txt che viene archiviato in **InstallLogs** archiviazione locale.

    > [!IMPORTANT]
    > Usare un semplice editor di testo come blocco note di Windows toocreate hello Install file. Se si utilizza Visual Studio toocreate un file di testo e modificare hello estensione too.cmd, file hello potrebbe ancora contenere un contrassegno di ordine dei byte UTF-8. Questo contrassegno può provocare un errore quando viene eseguito prima riga di hello dello script hello. tooavoid questo errore, verificare prima riga di hello di hello script un'istruzione REM che possa essere ignorata dall'elaborazione dell'ordine di byte di hello. 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > Questo script illustra modalità tooinstall .NET 4.5.2 o 4.6 di versione per la continuità, anche se .NET 4.5.2 è già disponibile nel hello del sistema operativo Guest Azure. È necessario installare direttamente .NET 4.6.1 anziché versione 4.6, come descritto in hello [articolo della Knowledge Base 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Ruolo Aggiungi hello Install file tooeach utilizzando **Aggiungi** > **elemento esistente** in **Esplora** come descritto in precedenza in questo argomento. 

    Dopo aver completato questo passaggio, tutti i ruoli devono avere file di programma di installazione .NET hello e file Install hello.

   ![Contenuto del ruolo con tutti i file][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Configurare l'archiviazione di diagnostica tootransfer avvio registri tooBlob
toosimplify risoluzione dei problemi di installazione, è possibile configurare diagnostica Azure tootransfer qualsiasi file di log generati dall'avvio hello lo script o hello archiviazione Blob tooAzure programma di installazione di .NET. Usando questo approccio, è possibile visualizzare i registri di hello il download dei file di log di hello dall'archiviazione Blob anziché tooremote desktop in ruolo hello.

Diagnostica tooconfigure, aprire il file Diagnostics. wadcfgx hello e aggiungere hello dopo contenuto in hello **directory** nodo: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Questo codice XML consente di configurare i file di diagnostica tootransfer hello nella directory log hello in hello **NETFXInstall** toohello risorse account di archiviazione di diagnostica di hello **netfx installazione** contenitore blob.

## <a name="deploy-your-cloud-service"></a>Distribuire il servizio cloud
Quando si distribuisce il servizio cloud, le attività di avvio hello installare .NET Framework hello se non è già installato. I ruoli dei servizi cloud sono in hello *occupato* stato durante l'installazione di framework hello. Se l'installazione di framework hello richiede un riavvio, potrebbe essere riavviato anche i ruoli del servizio hello. 

## <a name="additional-resources"></a>Risorse aggiuntive
* [L'installazione di .NET Framework hello][Installing hello .NET Framework]
* [Determinare quali sono le versioni di .NET Framework installate][How to: Determine Which .NET Framework Versions Are Installed]
* [Risoluzione dei problemi di installazione di .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
