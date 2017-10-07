---
title: le app web tecnologie aaaOpen origine domande frequenti su Azure | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti sulle tecnologie open source in funzionalità App Web hello di servizio App di Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Domande frequenti sulle tecnologie open source per App Web in Azure

In questo articolo ha toofrequently risposte domande frequenti (FAQ) sui problemi relativi a tecnologie open source per hello [funzionalità App Web di Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Il database ClearDB è inattivo. Come posso risolvere il problema?

Per i problemi relativi ai database, contattare il [supporto tecnico di ClearDB](https://www.cleardb.com/developers/help/support). 

Per le risposte toocommon domande ClearDB, vedere [domande frequenti su ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Perché il database ClearDB non è elencato nel portale di hello?

Se si crea un database ClearDB in hello [portale di Azure](http://portal.azure.com/), database hello non viene visualizzato in hello [portale di Azure classico](http://manage.windowsazure.com/). toowork il problema, è possibile collegare manualmente l'app web toohello di database.

Analogamente, se si crea un database ClearDB in hello [portale di Azure classico](http://manage.windowsazure.com/), non verrà visualizzato il database in hello [portale di Azure](http://portal.azure.com/). In questo caso non sono disponibili soluzioni alternative. 

Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Per quale ragione non è stata eseguita la migrazione del database ClearDB durante la migrazione della sottoscrizione?

Quando si esegue la migrazione delle risorse tra le sottoscrizioni, esistono alcune limitazioni. Il database MySQL ClearDB è un servizio di terze parti e non viene sottoposto a migrazione durante la migrazione di una sottoscrizione di Azure.

Se non si gestisce la migrazione di hello del database MySQL prima della migrazione delle risorse di Azure, il database ClearDB MySQL potrebbe non essere disponibile. tooavoid questo, in primo luogo, eseguire manualmente la migrazione del database ClearDB e quindi eseguire la migrazione hello sottoscrizione di Azure per l'app web.

Per altre informazioni, vedere [Domande frequenti per i database MySQL ClearDB con il Servizio app di Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Come attivare la registrazione di problemi PHP tootroubleshoot PHP?

tooturn registrazione PHP:

1. Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Nel menu in alto hello selezionare **Debug Console** > **CMD**.
3. Seleziona hello **sito** cartella.
4. Seleziona hello **wwwroot** cartella.
5. Seleziona hello  **+**  icona e quindi selezionare **nuovo File**.
6. Impostare il nome di file hello troppo**. user.ini**.
7. Selezionare l'icona matita hello Avanti troppo**. user.ini**.
8. Nel file hello, aggiungere questo codice:`log_errors=on`
9. Selezionare **Salva**.
10. Selezionare l'icona matita hello Avanti troppo**wp config.php**.
11. Modificare toohello testo hello seguente codice:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Nel portale di Azure, nel menu di app web hello, hello riavviare l'app web.

Per altre informazioni, vedere [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Abilitare i log degli errori di WordPress).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Come si registrano gli errori delle applicazioni Python in app ospitate nel servizio app?

errori di applicazione Python toocapture:

1. Nel portale di Azure nell'app web hello selezionare **impostazioni**.
2. In hello **impostazioni** , selezionare **le impostazioni dell'applicazione**.
3. In **impostazioni App**, immettere hello seguenti coppia chiave/valore:
    * Chiave : WSGI_LOG
    * Valore : D:\home\site\wwwroot\logs.txt (immettere il nome file scelto)

Errori nel file logs.txt hello nella cartella wwwroot hello dovrebbe.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Come è possibile modificare la versione hello di hello applicazione Node.js è ospitato nel servizio App?

versione di hello toochange di hello applicazione Node.js, è possibile utilizzare una delle seguenti opzioni hello:

*   Nel portale di Azure hello, utilizzare **impostazioni App**.
    1. Nel portale di Azure hello, andare tooyour web app.
    2. In hello **impostazioni** pannello seleziona **le impostazioni dell'applicazione**.
    3. In **impostazioni App**, è possibile includere WEBSITE_NODE_DEFAULT_VERSION come chiave hello e hello versione di Node. js si vuole usare come valore di hello.
    4. Passare tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck hello versione di Node. js, immettere hello comando seguente:  
   ```
   node -v
   ```
*   Modificare il file di iisnode.yml hello. Versione di Node. js hello modifica nel file iisnode.yml hello imposta solo ambiente di runtime hello che iisnode utilizza. Il cmd Kudu e altri ancora utilizzare versione di Node. js hello impostato in **impostazioni App** in hello portale di Azure.

    tooset hello iisnode.yml manualmente, creare un file di iisnode.yml nella cartella radice dell'applicazione. Nel file hello, includere hello seguente riga:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Impostare file iisnode.yml hello utilizzando package. JSON durante la distribuzione di origine del controllo.
    processo di distribuzione di origine Azure controllo Hello prevede hello alla procedura seguente:
    1. Sposta l'app web di Azure toohello contenuto.
    2. Crea uno script di distribuzione predefinito, se questo non è disponibile (deploy, .deployment file) nella cartella radice di hello web app.
    3. Esegue uno script di distribuzione in cui viene creato un file iisnode.yml se hai accennato versione di Node. js hello nel file package. JSON hello > motore di`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. file iisnode.yml Hello è hello successiva riga di codice:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Viene visualizzato il messaggio di hello "Errore di connessione al database" nell'applicazione WordPress ospitato nel servizio App. Come si risolve il problema?

Se viene visualizzato questo errore in app di Azure WordPress, tooenable php_errors.log e debug. log, descritti in dettaglio i passaggi di completamento hello in [log degli errori di WordPress abilitare](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Quando sono abilitati i registri di hello, riprodurre l'errore hello e quindi controllare hello registri toosee se si esaurisce le connessioni:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Se viene visualizzato questo errore nei file di debug. log o php_errors.log, l'app ha superato il numero di hello di connessioni. Se si ospita sul ClearDB, verificare il numero di hello di connessioni disponibili nel [piano di servizio](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Come si esegue il debug di un'app Node.js ospitata nel servizio app?

1.  Passare tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Cartella logs tooyour passare applicazione (D:\home\LogFiles\Application).
3.  Nel file logging_errors.txt hello, la presenza di contenuto.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Come si installano i moduli Python nativi in un'app Web o in un'app per le API del servizio app?

È possibile che alcuni pacchetti non vengano installati tramite PIP in Azure. pacchetto di Hello potrebbe non essere disponibile in hello indice del pacchetto Python o un compilatore potrebbe essere necessario (un compilatore non è disponibile nel computer di hello che esegue l'app web hello nel servizio App). Per informazioni sull'installazione dei moduli nativi nelle app Web e nelle app per le API del servizio app, vedere [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (Installare moduli Python nel servizio app).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Come distribuire un tooApp app Django servizio tramite Git e nuova versione di Python hello?

Per informazioni sull'installazione Django, vedere [la distribuzione di un tooApp app Django servizio](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Dove si trovano i file di log Tomcat hello?

Per Azure Marketplace e per le distribuzioni personalizzate:

* Percorso della cartella: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* File rilevanti:
    * catalina.*aaaa-mm-gg*.log
    * host-manager.*aaaa-mm-gg*.log
    * localhost.*aaaa-mm-gg*.log
    * manager.*aaaa-mm-gg*.log
    * site_access_log.*aaaa-mm-gg*.log


Per distribuzioni di tipo **Impostazioni dell'app** nel portale:

* Percorso della cartella: D:\home\LogFiles
* File rilevanti:
    * catalina.*aaaa-mm-gg*.log
    * host-manager.*aaaa-mm-gg*.log
    * localhost.*aaaa-mm-gg*.log
    * manager.*aaaa-mm-gg*.log
    * site_access_log.*aaaa-mm-gg*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Come si risolvono gli errori di connessione del driver JDBC?

Verrà visualizzato hello segue messaggio log Tomcat:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

Errore di hello tooresolve:

1. Rimuovere file sqljdbc*.jar hello dalla cartella app/lib.
2. Se si utilizza server web Tomcat o Azure Marketplace Tomcat personalizzata hello, copiare questa cartella di lib JAR file toohello Tomcat.
3. Se si sta abilitando Java da hello portale di Azure (selezionare **Java 1.8** > **server Tomcat**), file jar di copia hello sqljdbc.* in cartella hello app tooyour parallelo. Aggiungere quindi hello seguenti il file Web. config di classpath impostazione toohello:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Motivo per cui è non vengono visualizzati errori quando si tentano di file di log in tempo reale toocopy?

Se si tenta di file di log in tempo reale toocopy per un'applicazione Java (ad esempio, Tomcat), verrà visualizzato l'errore FTP:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

messaggio di errore Hello potrebbe variare, in base al client FTP hello.

Tutte le app Java presentano questo errore di blocco. Solo Kudu supporta il download del file durante l'esecuzione di app hello.

Arresto applicazione hello consente l'accesso FTP toothese dei file.

Un'altra soluzione alternativa è toowrite un processo Web in esecuzione su una pianificazione e copia le directory dei file tooa diversi. Per un progetto di esempio, vedere hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) progetto.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Dove trovare i file di log hello per Jetty?

Marketplace e le distribuzioni personalizzate, i file di log hello è nella cartella D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello. Si noti che il percorso di cartella hello dipende dalla versione di hello di Jetty in uso. Ad esempio, fornire il percorso di hello è qui per Jetty 9.1.2. Cercare jetty_*AAAA_MM_GG*.stderrout.log.

Per le distribuzioni di impostazione dell'App del portale, i file di log hello è D:\home\LogFiles. Cercare jetty_*AAAA_MM_GG*.stderrout.log.

## <a name="can-i-send-email-from-my-azure-web-app"></a>È possibile inviare messaggi di posta elettronica dall'app Web di Azure?

Il servizio app non include alcuna funzionalità di posta elettronica predefinita. Per alternative valide per l'invio di messaggi di posta elettronica dall'app, vedere questa [discussione su Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Perché sito personale WordPress URL di reindirizzamento tooanother?

Se la migrazione di recente tooAzure, WordPress potrebbe reindirizzare toohello URL di dominio precedente. Ciò è causato da un'impostazione nel database di MySQL hello.

WordPress Buddy + non è un'estensione del sito di Azure che è possibile utilizzare l'URL di reindirizzamento hello tooupdate direttamente nel database di hello. Per altre informazioni sull'uso di WordPress Buddy+, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).

In alternativa, se si preferisce l'URL di reindirizzamento toomanually aggiornamento hello tramite query SQL o PHPMyAdmin, vedere [WordPress: reindirizzamento URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Come si modifica la password di accesso di WordPress?

Se si dimentica la propria password di accesso di WordPress, è possibile utilizzare WordPress Buddy + tooupdate è. tooreset la password, hello installazione sito WordPress Buddy + Azure estensione e le procedure hello completa quindi descritto in [WordPress strumenti e la migrazione di MySQL con WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Impossibile accedere tooWordPress. Come posso risolvere il problema?

Se non è possibile accedere a WordPress dopo l'installazione recente di un plug-in, è possibile che il plug-in sia danneggiato. WordPress Buddy+ è un'estensione del sito di Azure che consente di disabilitare i plug-in in WordPress. Per altre informazioni, vedere [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Strumenti di WordPress e migrazione di MySQL con WordPress Buddy+).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Come si esegue la migrazione del database di WordPress?

Sono disponibili più opzioni per la migrazione dei database MySQL hello di sito Web WordPress tooyour connessa:

* Sviluppatori: Hello utilizzare [prompt dei comandi o PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Non sviluppatori: usare [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Come si migliora la protezione di WordPress?

toolearn sulle procedure consigliate di sicurezza per WordPress, vedere [procedure consigliate per la sicurezza di WordPress in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Si sta tentando di toouse PHPMyAdmin e viene visualizzato il messaggio hello "Accesso negato". Come posso risolvere il problema?

Questo problema potrebbe verificarsi se funzionalità nell'applicazione di hello MySQL non è ancora in esecuzione in questa istanza di servizio App. tooresolve hello problema, provare a tooaccess il sito Web. Verrà avviata processi hello necessario, tra cui il processo di hello MySQL in app. tooverify che MySQL nell'applicazione è in esecuzione, Process Explorer, assicurarsi che mysqld.exe è elencato in processi hello.

Dopo avere verificato che MySQL in-app è in esecuzione, provare a toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Quando si tenta tooimport o Esporta il database di MySQL in-app con PHPMyadmin, viene visualizzato un errore HTTP 403. Come posso risolvere il problema?

Se si usa una versione precedente di Chrome, è possibile che si riscontri un bug noto. problema di hello tooresolve, tooa aggiornamento versione più recente di Chrome. Provare anche utilizzando un browser diverso, ad esempio Internet Explorer o Edge, in cui hello non si verifica.
