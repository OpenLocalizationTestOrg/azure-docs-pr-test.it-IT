## <a name="install-wordpress"></a><span data-ttu-id="0431f-101">Installare WordPress</span><span class="sxs-lookup"><span data-stu-id="0431f-101">Install WordPress</span></span>

<span data-ttu-id="0431f-102">Per provare lo stack, installare un'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="0431f-102">If you want to try your stack, install a sample app.</span></span> <span data-ttu-id="0431f-103">Come esempio, con i passaggi seguenti viene installata la piattaforma open source [WordPress](https://wordpress.org/) per creare siti Web e blog.</span><span class="sxs-lookup"><span data-stu-id="0431f-103">As an example, the following steps install the open source [WordPress](https://wordpress.org/) platform to create websites and blogs.</span></span> <span data-ttu-id="0431f-104">Altri carichi di lavoro da provare includono [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="0431f-104">Other workloads to try include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="0431f-105">Questa configurazione di WordPress è per il modello di verifica.</span><span class="sxs-lookup"><span data-stu-id="0431f-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="0431f-106">Per altre informazioni e impostazioni per l'installazione di produzione, vedere la [documentazione di WordPress](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="0431f-106">For more information and settings for production installation, see the [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-the-wordpress-package"></a><span data-ttu-id="0431f-107">Installare il pacchetto WordPress</span><span class="sxs-lookup"><span data-stu-id="0431f-107">Install the WordPress package</span></span>

<span data-ttu-id="0431f-108">Eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0431f-108">Run the following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="0431f-109">Configurazione di WordPress</span><span class="sxs-lookup"><span data-stu-id="0431f-109">Configure WordPress</span></span>

<span data-ttu-id="0431f-110">Configurare WordPress per usare MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="0431f-110">Configure WordPress to use MySQL and PHP.</span></span> <span data-ttu-id="0431f-111">Usare il comando seguente per aprire un editor di testo di propria scelta e creare il file `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="0431f-111">Run the following command to open a text editor of your choice and create the file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="0431f-112">Copiare le righe seguenti nel file, sostituendo *yourPassword* con la password del database. Lasciare invariati gli altri valori.</span><span class="sxs-lookup"><span data-stu-id="0431f-112">Copy the following lines to the file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="0431f-113">Salvare quindi il file.</span><span class="sxs-lookup"><span data-stu-id="0431f-113">Then save the file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="0431f-114">In una directory di lavoro creare un file di testo `wordpress.sql` per configurare il database di WordPress:</span><span class="sxs-lookup"><span data-stu-id="0431f-114">In a working directory, create a text file `wordpress.sql` to configure the WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="0431f-115">Aggiungere i comandi seguenti, sostituendo *yourPassword* con la password del database. Lasciare invariati gli altri valori.</span><span class="sxs-lookup"><span data-stu-id="0431f-115">Add the following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="0431f-116">Salvare quindi il file.</span><span class="sxs-lookup"><span data-stu-id="0431f-116">Then save the file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
TO wordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="0431f-117">Eseguire il comando seguente per creare il database:</span><span class="sxs-lookup"><span data-stu-id="0431f-117">Run the following command to create the database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="0431f-118">Dopo aver eseguito il comando, eliminare il file `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="0431f-118">After the command completes, delete the file `wordpress.sql`.</span></span>

<span data-ttu-id="0431f-119">Spostare l'installazione di WordPress nella radice dei documenti del server Web:</span><span class="sxs-lookup"><span data-stu-id="0431f-119">Move the WordPress installation to the web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="0431f-120">È ora possibile completare la configurazione di WordPress e pubblicare sulla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0431f-120">Now you can complete the WordPress setup and publish on the platform.</span></span> <span data-ttu-id="0431f-121">Aprire un browser e passare a `http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="0431f-121">Open a browser and go to `http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="0431f-122">Sostituire l'indirizzo IP pubblico della VM.</span><span class="sxs-lookup"><span data-stu-id="0431f-122">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="0431f-123">Dovrebbe avere un aspetto simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="0431f-123">It should look similar to this image.</span></span>

![Pagina di installazione di WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)