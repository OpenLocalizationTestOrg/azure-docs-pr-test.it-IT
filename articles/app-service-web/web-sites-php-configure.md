---
title: aaaConfigure PHP nelle App Web di servizio App di Azure | Documenti Microsoft
description: Informazioni su come tooconfigure hello installazione PHP predefinita o un'installazione personalizzata di PHP per le app Web in Azure App Service.
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a>Configurazione di PHP nelle app Web di Servizio app di Azure
## <a name="introduction"></a>Introduzione
Questa guida Mostra come tooconfigure hello runtime PHP predefiniti per le app Web in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fornire un runtime PHP personalizzato e abilitare le estensioni. Servizio App, toouse iscriversi hello [versione di valutazione gratuita]. hello tooget più da questa Guida, è necessario creare prima un'app web PHP nel servizio App.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Procedura: versione PHP modifica hello incorporata
Per impostazione predefinita, PHP 5.5 è installato e immediatamente disponibile per l'uso quando si crea un'app Web del servizio app di Azure. migliore toosee hello versione disponibile revisione, la configurazione predefinita, Hello ed estensioni abilitate hello è uno script che chiama hello toodeploy [phpinfo] (funzione).

Sono anche disponibili le versioni PHP 5.6 e PHP 7.0, che però non sono abilitate per impostazione predefinita. hello tooupdate versione PHP, seguire uno dei metodi seguenti:

### <a name="azure-portal"></a>Portale di Azure
1. Esplorare app web tooyour hello [portale Azure](https://portal.azure.com) e fare clic su hello **impostazioni** pulsante.
   
    ![Impostazioni app Web][settings-button]
2. Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scegliere nuova versione PHP hello.
   
    ![Impostazioni dell'applicazione][application-settings]
3. Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.
   
    ![Salvare le impostazioni di configurazione][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (solo Windows).
1. Aprire Azure PowerShell e account di accesso tooyour:
   
        PS C:\> Login-AzureRmAccount
2. Impostare la versione di PHP hello per l'app web hello.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. versione PHP Hello è ora impostato. È possibile verificare queste impostazioni:
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Interfaccia della riga di comando di Azure (Linux, Mac, Windows)
toouse hello Azure interfaccia della riga di comando, è necessario **Node.js** installato nel computer.

1. Aprire Terminal e account di accesso tooyour.
   
        azure login
2. Impostare la versione di PHP hello per l'app web hello.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. versione PHP Hello è ora impostato. È possibile verificare queste impostazioni:
   
        azure site show {app-name}

> [!NOTE] 
> Hello [CLI di Azure 2.0](https://github.com/Azure/azure-cli) sono comandi che sono equivalente toohello precedente:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Procedura: modificare le configurazioni di PHP predefinite hello
Per qualsiasi runtime PHP predefiniti, è possibile modificare le opzioni di configurazione hello seguendo i passaggi di hello riportati di seguito. (per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Modifica delle impostazioni di configurazione PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL
1. Aggiungere un [. user.ini] tooyour directory radice del file.
2. Aggiungi configurazione impostazioni toohello `.user.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un `php.ini` file. Ad esempio, se si desidera hello tooturn `display_errors` impostazione e imposta `upload_max_filesize` too10M, impostando il `.user.ini` file conterrà questo testo:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Distribuire l'app Web.
4. Riavviare l'app web hello. (Il riavvio è necessario in quanto la frequenza di hello con cui PHP legge `.user.ini` file non sia disciplinato da hello `user_ini.cache_ttl` impostazione, che è 300 secondi (5 minuti) per impostazione predefinita ed è un'impostazione del livello di sistema. Il riavvio dell'applicazione web di hello forza PHP tooread hello nuove impostazioni in hello `.user.ini` file.)

Come un'alternativa toousing un `.user.ini` file, è possibile utilizzare hello [ini_set()] funzione nelle opzioni di configurazione tooset script che non sono direttive a livello di sistema.

### <a name="changing-phpinisystem-configuration-settings"></a>Modifica delle impostazioni di configurazione PHP\_INI\_SYSTEM
1. Aggiungere un tooyour di impostazione dell'App Web App con la chiave hello `PHP_INI_SCAN_DIR` e valore`d:\home\site\ini`
2. Creare un `settings.ini` file utilizzando la Console Kudu (http://&lt;nome sito&gt;. scm.azurewebsite.net) in hello `d:\home\site\ini` directory.
3. Aggiungi configurazione impostazioni toohello `settings.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un file php.ini. Ad esempio, se si desidera hello toopoint `curl.cainfo` impostazione tooa `*.crt` file e impostare 'wincache.maxfilesize' impostazione too512K, il `settings.ini` file conterrà questo testo:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Riavviare le modifiche di hello tooload App Web.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Procedura: abilitare le estensioni nel runtime PHP hello predefinito
Come indicato nella sezione precedente hello, versione PHP hello di toosee di hello migliore modalità predefinita, la configurazione predefinita e hello abilitato estensioni è uno script che chiama toodeploy [phpinfo]. tooenable estensioni aggiuntive, attenersi alla procedura hello riportata di seguito:

### <a name="configure-via-ini-settings"></a>Configurare tramite le impostazioni del file ini
1. Aggiungere un `ext` toohello directory `d:\home\site` directory.
2. Inserire `.dll` i file di estensione in hello `ext` directory (ad esempio, `php_xdebug.dll`). Assicurarsi che le estensioni di hello sono compatibili con la versione predefinita di PHP e sono VC9 compatibile non thread-safe (punta).
3. Aggiungere un tooyour di impostazione dell'App Web App con la chiave hello `PHP_INI_SCAN_DIR` e valore`d:\home\site\ini`
4. Creare un `ini` del file in `d:\home\site\ini` chiamato `extensions.ini`.
5. Aggiungi configurazione impostazioni toohello `extensions.ini` file utilizzando hello stessa sintassi si utilizzerebbe per un file php.ini. Ad esempio, se si desidera tooenable hello MongoDB e XDebug le estensioni, i `extensions.ini` file conterrà questo testo:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Riavviare le modifiche di hello tooload App Web.

### <a name="configure-via-app-setting"></a>Configurare tramite impostazione dell'applicazione
1. Aggiungere un `bin` toohello la directory di directory radice.
2. Inserire `.dll` i file di estensione in hello `bin` directory (ad esempio, `php_xdebug.dll`). Assicurarsi che le estensioni di hello sono compatibili con la versione predefinita di PHP e sono VC9 compatibile non thread-safe (punta).
3. Distribuire l'app Web.
4. Esplorare app web tooyour nel portale di Azure hello e fare clic su hello **impostazioni** pulsante.
   
    ![Impostazioni app Web][settings-button]
5. Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scorrere toohello **impostazioni App** sezione.
6. In hello **impostazioni App** sezione, creare un **PHP_EXTENSIONS** chiave. il valore di Hello per questa chiave deve corrispondere a una radice del percorso relativo toowebsite: **bin\your-ext-file**.
   
    ![Abilitare le estensioni nelle impostazioni app][php-extensions]
7. Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.
   
    ![Salvare le impostazioni di configurazione][save-button]

Con l'uso di una chiave **PHP_ZENDEXTENSIONS** sono supportate anche le estensioni Zend. tooenable più estensioni, includere un elenco delimitato da virgole di `.dll` file per valore dell'impostazione applicazione hello.

## <a name="how-to-use-a-custom-php-runtime"></a>Usare un runtime PHP personalizzato
Invece di runtime PHP predefinito hello, App Web del servizio App può usare un runtime PHP fornire tooexecute gli script PHP. runtime Hello specificata dall'utente può essere configurate da un `php.ini` file che fornisce anche. toouse un runtime PHP personalizzato con le app Web, seguire i passaggi di hello seguenti.

1. Ottenere una versione compatibile con VC9 o VC11 e non-thread-safe di PHP per Windows. Versioni recenti di PHP per Windows sono disponibili qui: [http://windows.php.net/download/]. Le versioni precedenti sono disponibili nell'archivio di hello qui: [http://windows.php.net/downloads/releases/archives/].
2. Modificare hello `php.ini` file per il runtime. Si noti che qualsiasi impostazione di configurazione che non sia una direttiva solo a livello di sistema verrà ignorata da App Web (per informazioni sulle direttive solo a livello di sistema, vedere la [Lista delle direttive php.ini]).
3. Facoltativamente, aggiungere le estensioni tooyour PHP runtime e abilitarli nel hello `php.ini` file.
4. Aggiungere un `bin` directory radice di directory tooyour e put hello directory che contiene il runtime PHP in essa contenuti (ad esempio, `bin\php`).
5. Distribuire l'app Web.
6. Esplorare app web tooyour nel portale di Azure hello e fare clic su hello **impostazioni** pulsante.
   
    ![Impostazioni app Web][settings-button]
7. Da hello **impostazioni** pannello selezionare **le impostazioni dell'applicazione** e scorrere toohello **Mapping gestori** sezione. Aggiungere `*.php` toohello estensione campo e aggiungere hello percorso toohello `php-cgi.exe` eseguibile. Se si inserisce il runtime PHP in hello `bin` directory nella directory radice dell'applicazione hello, percorso di hello sarà `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Specificare il gestore nei mapping gestore][handler-mappings]
8. Fare clic su hello **salvare** pulsante nella parte superiore di hello di hello **impostazioni app Web** blade.
   
    ![Salvare le impostazioni di configurazione][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Procedura: Abilitare l’automazione Composer in Azure
Per impostazione predefinita, il servizio app non esegue operazioni relative a composer.json, se questo è presente nel progetto PHP. Se si utilizza [distribuzione Git](app-service-deploy-local-git.md), è possibile abilitare composer.json durante l'elaborazione di `git push` abilitando l'estensione Composer hello.

> [!NOTE]
> È possibile [votare qui per il supporto Composer avanzato nel servizio app](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!
> 
> 

1. Nel PHP web pannello dell'app in hello [portale di Azure](https://portal.azure.com), fare clic su **strumenti** > **estensioni**.
   
    ![Tooenable pannello Impostazioni portale Azure automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Fare clic su **Aggiungi**, quindi su **Compositore**.
   
    ![Aggiungere l'automazione di Composer Composer estensione tooenable in Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Fare clic su **OK** tooaccept legali. Fare clic su **OK** nuovamente tooadd estensione di hello.
   
    Hello **estensioni installate** pannello verrà visualizzati estensione Composer hello.  
    ![Accettare i termini legali specifici tooenable Composer automazione Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. A questo punto, eseguire `git add`, `git commit`, e `git push` come nella sezione precedente hello. Si noterà che ora Composer installa le dipendenze definite in composer.json.
   
    ![Distribuzione Git con l’automazione Composer in Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro sviluppatori PHP](/develop/php/).

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

[versione di valutazione gratuita]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Lista delle direttive php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

