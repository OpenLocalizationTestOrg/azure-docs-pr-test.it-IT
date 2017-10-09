---
title: aaaBuild un'app web PHP e MySQL in Azure | Documenti Microsoft
description: Informazioni su come tooget un'applicazione PHP Usa Azure, con connessione tooa MySQL di database in Azure.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a>Creare un'app Web PHP e MySQL in Azure

Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa esercitazione viene illustrato come toocreate PHP web app in Azure e connetterla tooa di database MySQL. Al termine, sarà disponibile un'app [Laravel](https://laravel.com/) in esecuzione nelle app Web del servizio app di Azure.

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un database MySQL in Azure
> * Connettersi a un tooMySQL app PHP
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Eseguire lo streaming dei log di diagnostica in Azure
> * Gestire app hello in hello portale di Azure

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

* [Installare Git](https://git-scm.com/)
* [Installare PHP 5.6.4 o versione successiva](http://php.net/downloads.php)
* [Installare Composer](https://getcomposer.org/doc/00-intro.md)
* Abilitare hello seguenti estensioni di PHP esigenze Laravel: OpenSSL, PDO MySQL, Mbstring, Tokenizer, XML
* [Installare e avviare MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a>Preparare MySQL in locale

In questo passaggio, si crea un database nel server locale di MySQL da usare in questa esercitazione.

### <a name="connect-toolocal-mysql-server"></a>Connettere toolocal MySQL server

In una finestra terminale, connettersi tooyour locale MySQL server. In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.

```bash
mysql -u root -p
```

Se viene chiesto di immettere una password, immettere la password di hello per hello `root` account. Se non si ricorda la password dell'account radice, vedere [MySQL: modalità tooReset hello Password Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Se il comando viene eseguito correttamente, il server MySQL è in esecuzione. In caso contrario, assicurarsi che il server MySQL locale viene eseguito da hello seguente [passaggi successivi all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database-locally"></a>Creare un database in locale

In hello `mysql` richiedono, creare un database.

```sql 
CREATE DATABASE sampledb;
```

Chiudere la connessione al server digitando `quit`.

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a>Creare un'app PHP in locale
In questo passaggio si ottiene un'applicazione di esempio Laravel, se ne configurare la connessione al database e la si esegue in locale. 

### <a name="clone-hello-sample"></a>Esempio hello clone

Nella finestra terminal hello `cd` tooa directory di lavoro.

Eseguire hello seguenti repository di esempio di comando tooclone hello.

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

`cd`directory clonato tooyour.
Installare i pacchetti hello necessario.

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a>Configurare la connessione di MySQL

Nella radice del repository hello, creare un file denominato *.env*. Hello copia seguenti variabili in hello *.env* file. Sostituire hello  _&lt;root_password >_ segnaposto con la password dell'utente di hello MySQL radice.

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

Per informazioni sulle modalità di utilizzo hello Laravel _.env_ file, vedere [la configurazione dell'ambiente Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).

### <a name="run-hello-sample-locally"></a>Eseguire in locale: esempio hello

Eseguire [migrazioni database Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello tabelle hello esigenze dell'applicazione. le tabelle vengono create nelle migrazioni hello, cercare in hello toosee _database/migrazioni_ directory nel repository Git hello.

```bash
php artisan migrate
```

Generare una nuova chiave per l'applicazione Laravel.

```bash
php artisan key:generate
```

Eseguire un'applicazione hello.

```bash
php artisan serve
```

Passare troppo`http://localhost:8000` in un browser. Nella pagina di hello, aggiungere alcune attività.

![PHP si connette correttamente tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Digitare toostop PHP, `Ctrl + C` in hello terminal.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a>Creare MySQL in Azure

In questo passaggio viene creato un database MySQL nel [database di Azure per MySQL (anteprima)](/azure/mysql). In un secondo momento, configurare il database toothis tooconnect di hello PHP dell'applicazione.

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a>Creare un server MySQL

Creare un server nel Database di Azure per MySQL (anteprima) con hello [creare server mysql az](/cli/azure/mysql/server#create) comando.

In hello seguente comando, sostituire il nome del server MySQL in cui si vedere hello  _&lt;mysql_server_name >_ segnaposto (i caratteri validi sono `a-z`, `0-9`, e `-`). Questo nome fa parte del nome host del server MySQL hello (`<mysql_server_name>.database.windows.net`), è necessario toobe univoco globale.

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

Creazione di server MySQL hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a>Configurare il firewall del server

Creare una regola del firewall per il client di MySQL server tooallow connessioni tramite hello [az mysql regola firewall del server-creare](/cli/azure/mysql/server/firewall-rule#create) comando.

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Il Database di Azure per MySQL (anteprima) non attualmente limita servizi tooAzure solo le connessioni. Come vengono assegnati dinamicamente agli indirizzi IP in Azure, è preferibile tooenable tutti gli indirizzi IP. servizio Hello è in anteprima. Verranno resi disponibili metodi migliori per la protezione del database.
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a>Connettersi tooproduction MySQL server in locale

Nella finestra terminal hello connettersi toohello MySQL server in Azure. Utilizzare il valore di hello specificato in precedenza per  _&lt;mysql_server_name >_.

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

Quando viene richiesto di immettere una password, utilizzare _tr0ngPa $$ w0rd!_, specificato al momento della creazione del database hello.

### <a name="create-a-production-database"></a>Creare un database di produzione

In hello `mysql` richiedono, creare un database.

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a>Creare un utente con autorizzazioni

Creare un utente di database denominato _phpappuser_ e assegnare tutti i privilegi in hello `sampledb` database.

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

Chiudere una connessione al server hello digitando `quit`.

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a>Connettere l'app tooAzure MySQL

In questo passaggio è connettersi hello PHP toohello MySQL database dell'applicazione creato nel Database di Azure per MySQL (anteprima).

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a>Configurare una connessione al database hello

Nella radice del repository hello, creare un _. env.production_ file e copia hello seguenti variabili al suo interno. Sostituire il segnaposto hello  _&lt;mysql_server_name >_.

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

Salvare le modifiche di hello.

> [!TIP]
> le informazioni di connessione MySQL, questo file sono già esclusa dal repository Git hello toosecure (vedere _con estensione gitignore_ nella radice del repository hello). Successivamente, viene illustrato come variabili di ambiente tooconfigure nel servizio App tooconnect tooyour database nel Database di Azure per MySQL (anteprima). Con le variabili di ambiente, non devi hello *.env* file nel servizio App.
>

### <a name="configure-ssl-certificate"></a>Configurare il certificato SSL

Per impostazione predefinita, Database di Azure per MySQL impone le connessioni SSL dai client. database di MySQL tooconnect tooyour in Azure, è necessario utilizzare un _PEM_ certificato SSL.

Aprire _config/database.php_ e aggiungere hello _sslmode_ e _opzioni_ parametri troppo`connections.mysql`, come illustrato nel seguente codice hello.

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

toolearn come toogenerate questo _certificate.pem_, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](../mysql/howto-configure-ssl.md).

> [!TIP]
> percorso Hello _/ssl/certificate.pem_ punta esistente tooan _certificate.pem_ file nel repository Git hello. Il file è già incluso per ragioni di praticità in questa esercitazione. È consigliabile non eseguire il commit dei certificati _.pem_ nel controllo del codice sorgente. 
>

### <a name="test-hello-application-locally"></a>Testare l'applicazione hello in locale

Eseguire migrazioni database Laravel con _. env.production_ come hello ambiente file toocreate hello tabelle del database MySQL nel Database di Azure per MySQL (anteprima). Tenere presente che _. env.production_ dispone di database di MySQL tooyour informazioni connessione hello in Azure.

```bash
php artisan migrate --env=production --force
```

_.env.production_ non dispone ancora di una chiave applicazione valida. Generarne uno nuovo per tale in hello terminal.

```bash
php artisan key:generate --env=production --force
```

Eseguire l'applicazione di esempio hello con _. env.production_ come file di ambiente hello.

```bash
php artisan serve --env=production
```

Passare troppo`http://localhost:8000`. Se la pagina hello viene caricata senza errori, hello applicazione PHP connessione toohello database MySQL in Azure.

Nella pagina di hello, aggiungere alcune attività.

![PHP si connette correttamente tooAzure Database MySQL (anteprima)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

Digitare toostop PHP, `Ctrl + C` in hello terminal.

### <a name="commit-your-changes"></a>Eseguire il commit delle modifiche

Eseguire hello toocommit comandi Git dopo le modifiche:

```bash
git add .
git commit -m "database.php updates"
```

L'app è pronta toobe distribuito.

## <a name="deploy-tooazure"></a>Distribuire tooAzure

In questo passaggio, si distribuisce hello connesso MySQL PHP applicazione tooAzure servizio App.

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Creare un'app Web

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a>Imposta la versione di hello PHP

Versione PHP hello set che hello applicazione richiede mediante hello [az webapp config set](/cli/azure/webapp/config#set) comando.

Hello il comando seguente imposta too_7.0_ versione di hello PHP.

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a>Configurare le impostazioni del database

Come evidenziato in precedenza, è possibile connettere il database di MySQL Azure tooyour utilizzando variabili di ambiente nel servizio App.

Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config/appsettings#set) comando.

il comando seguente Hello Configura impostazioni app hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`. Sostituire i segnaposto hello  _&lt;appname >_ e  _&lt;mysql_server_name >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

È possibile utilizzare hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess metodo hello impostazioni. Hello Laravel codice utilizza un [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper su hello PHP `getenv`. Ad esempio, hello MySQL configurazione _config/database.php_ simile hello seguente codice:

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a>Configurare le variabili di ambiente di Laravel

Laravel richiede una chiave di applicazione nel servizio app. È possibile configurarla con le impostazioni dell'app.

Utilizzare `php artisan` toogenerate una nuova chiave dell'applicazione senza salvarla too_.env_.

```bash
php artisan key:generate --show
```

Impostare chiave applicazione hello hello servizio App di app web utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config/appsettings#set) comando. Sostituire i segnaposto hello  _&lt;appname >_ e  _&lt;outputofphpartisankey: generare >_.

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

`APP_DEBUG="true"`indica Laravel tooreturn informazioni di debug quando hello distribuito l'app web rileva errori. Quando si esegue un'applicazione di produzione, impostarlo troppo`false`, che è più sicuro.

### <a name="set-hello-virtual-application-path"></a>Percorso dell'applicazione virtuale hello insieme

Impostare il percorso virtuale applicazione hello per l'app web hello. Questo passaggio è obbligatorio perché hello [ciclo di vita dell'applicazione Laravel](https://laravel.com/docs/5.4/lifecycle) inizia in hello _pubblica_ directory anziché directory radice dell'applicazione hello. Altri framework PHP il cui ciclo di vita Avvia nella directory radice hello può funzionare senza la configurazione manuale del percorso virtuale applicazione hello.

Percorso dell'applicazione virtuale hello insieme utilizzando hello [aggiornamento risorse az](/cli/azure/resource#update) comando. Sostituire hello  _&lt;appname >_ segnaposto.

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

Per impostazione predefinita, Azure App Service punti percorso dell'applicazione virtuale radice hello (_/_) toohello directory radice di hello distribuiti i file dell'applicazione (_sites\wwwroot_).

### <a name="configure-a-deployment-user"></a>Configurare un utente della distribuzione

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a>Configurare la distribuzione con l'istanza Git locale

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a>Eseguire il push tooAzure da Git

Aggiungere un repository Git locale tooyour remoto di Azure.

```bash
git remote add azure <paste_copied_url_here>
```

Effettuare il push dell'applicazione PHP di hello Azure toodeploy remoto toohello. Viene chiesto di immettere la password di hello fornito in precedenza come parte della creazione di hello dell'utente di distribuzione hello.

```bash
git push azure master
```

Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> È possibile notare che il processo di distribuzione hello installa [Composer](https://getcomposer.org/) pacchetti alla fine di hello. Servizio App non esegue tali automazioni durante la distribuzione predefinita, pertanto questo repository di esempio ha tre ulteriori file nella relativa tooenable directory radice:
>
> - `.deployment`-Questo file indica al servizio App toorun `bash deploy.sh` come script di distribuzione personalizzata hello.
> - `deploy.sh`-hello script di distribuzione personalizzati. Se si esamina il file hello, si noterà che l'esecuzione `php composer.phar install` dopo `npm install`.
> - `composer.phar`-gestione di pacchetti hello Composer.
>
> È possibile utilizzare questo approccio tooadd qualsiasi tooApp di distribuzione basati su Git tooyour di passaggio del servizio. Per altre informazioni, vedere [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Script di distribuzione personalizzata).
>

### <a name="browse-toohello-azure-web-app"></a>Sfoglia toohello Azure web app

Sfoglia troppo`http://<app_name>.azurewebsites.net` e aggiungere alcune attività toohello elenco.

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

L'app PHP basata su dati è in esecuzione nel servizio app di Azure.

## <a name="update-model-locally-and-redeploy"></a>Aggiornare il modello in locale e rieseguire la distribuzione

In questo passaggio, si apportata toohello una semplice modifica `task` modello di dati e hello webapp e quindi pubblicare tooAzure aggiornamento hello.

Scenario di attività hello, modificare un'applicazione hello in modo che è possibile contrassegnare un'attività come completata.

### <a name="add-a-column"></a>Aggiungere una colonna

In hello terminal, passare toohello radice del repository Git hello.

Generare una nuova migrazione di database per hello `tasks` tabella:

```bash
php artisan make:migration add_complete_column --table=tasks
```

Questo comando Mostra hello nome del file di migrazione hello che viene generato. Trovare il file in _database/migrations_ e aprirlo.

Sostituire hello `up` metodo con hello seguente codice:

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

Hello precedente consente di aggiungere una colonna booleana hello `tasks` tabella denominata `complete`.

Sostituire hello `down` metodo con hello seguente codice per l'azione di rollback hello:

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

In hello terminal, eseguire le modifiche hello Laravel del database le migrazioni toomake nel database locale hello.

```bash
php artisan migrate
```

In base a hello [convenzione di denominazione Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modello hello `Task` (vedere _app/Task.php_) viene eseguito il mapping toohello `tasks` tabella per impostazione predefinita.

### <a name="update-application-logic"></a>Aggiornare la logica dell'applicazione

Aprire hello *routes/web.php* file. un'applicazione Hello definisce le route e qui la logica di business.

Alla fine di hello del file hello, aggiungere una route con hello seguente codice:

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

Hello codice precedente crea un modello di dati semplice aggiornamento toohello attivando e disattivando il valore di hello di `complete`.

### <a name="update-hello-view"></a>Aggiornare la vista hello

Aprire hello *resources/views/tasks.blade.php* file. Trovare hello `<tr>` tag di apertura e sostituirlo con:

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

Hello precedente codice colore riga hello di modifiche a seconda se l'attività hello è stata completata.

Nella riga successiva hello, è necessario hello seguente codice:

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

Sostituire l'intera riga hello con hello seguente codice:

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

Hello codice precedente aggiunge pulsante submit hello che fa riferimento a route hello è definito in precedenza.

### <a name="test-hello-changes-locally"></a>Testare le modifiche di hello in locale

Dalla directory radice di hello del repository Git hello, eseguire il server di sviluppo hello.

```bash
php artisan serve
```

hello toosee modifica dello stato delle attività, passare troppo`http://localhost:8000` e hello selezionare la casella di controllo.

![Casella di controllo aggiunte tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

Digitare toostop PHP, `Ctrl + C` in hello terminal.

### <a name="publish-changes-tooazure"></a>Pubblicare le modifiche tooAzure

In hello terminal, eseguire le migrazioni database Laravel con hello produzione connessione stringa toomake hello modifica hello il database di Azure.

```bash
php artisan migrate --env=production --force
```

Eseguire il commit di tutte le modifiche di hello in Git e quindi push tooAzure modifiche di codice hello.

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

Una volta hello `git push` è completo, passare toohello Azure web app e prova hello nuove funzionalità.

![Le modifiche apportate al modello e il database pubblicato tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

Se si aggiungono tutte le attività, vengono mantenuti nel database di hello. Schema di data toohello aggiornamenti intatti i dati esistenti.

## <a name="stream-diagnostic-logs"></a>Eseguire lo streaming dei log di diagnostica

Mentre è in esecuzione in Azure App Service hello applicazione PHP, è possibile ottenere hello console registri reindirizzato tooyour terminal. In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.

log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

Una volta avviato il flusso di log, aggiornare l'app web di Azure hello in hello browser tooget traffico web. È ora possibile visualizzare terminal toohello inoltrato tramite pipe i registri di console. Se i log di console non sono immediatamente visibili, controllare nuovamente dopo 30 secondi.

log toostop streaming in qualsiasi momento, tipo `Ctrl` + `C`.

> [!TIP]
> Un'applicazione PHP può utilizzare standard di hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console. applicazione di esempio Hello viene utilizzato questo approccio in _app/Http/routes.php_.
>
> Come un framework web [Laravel Usa Monolog](https://laravel.com/docs/5.4/errors) come provider di log hello. toosee come tooget Monolog toooutput messaggi toohello console, vedere [PHP: modalità toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).
>
>

## <a name="manage-hello-azure-web-app"></a>Gestire app web di Azure hello

Passare toohello [portale di Azure](https://portal.azure.com) toomanage hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

Verrà visualizzata la pagina di panoramica dell'app Web. Nella pagina è possibile eseguire attività di gestione di base come l'arresto, l'avvio, il riavvio e l'eliminazione.

menu a sinistra di Hello fornisce le pagine di configurazione app.

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un database MySQL in Azure
> * Connettersi a un tooMySQL app PHP
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Eseguire lo streaming dei log di diagnostica in Azure
> * Gestire app hello in hello portale di Azure

Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooa web app.

> [!div class="nextstepaction"]
> [Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md)
