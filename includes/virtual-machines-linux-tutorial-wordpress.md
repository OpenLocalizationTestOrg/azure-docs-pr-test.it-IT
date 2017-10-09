## <a name="install-wordpress"></a><span data-ttu-id="5ced6-101">Installare WordPress</span><span class="sxs-lookup"><span data-stu-id="5ced6-101">Install WordPress</span></span>

<span data-ttu-id="5ced6-102">Se si desidera tootry lo stack, installare un'app di esempio.</span><span class="sxs-lookup"><span data-stu-id="5ced6-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="5ced6-103">Ad esempio, alla procedura seguente hello installa open source di hello [WordPress](https://wordpress.org/) blog e siti Web toocreate di piattaforma.</span><span class="sxs-lookup"><span data-stu-id="5ced6-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="5ced6-104">Includere altri carichi di lavoro di tootry [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="5ced6-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="5ced6-105">Questa configurazione di WordPress è per il modello di verifica.</span><span class="sxs-lookup"><span data-stu-id="5ced6-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="5ced6-106">Per ulteriori informazioni e le impostazioni per l'installazione di produzione, vedere hello [WordPress documentazione](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="5ced6-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="5ced6-107">Installare il pacchetto di WordPress hello</span><span class="sxs-lookup"><span data-stu-id="5ced6-107">Install hello WordPress package</span></span>

<span data-ttu-id="5ced6-108">Eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5ced6-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="5ced6-109">Configurazione di WordPress</span><span class="sxs-lookup"><span data-stu-id="5ced6-109">Configure WordPress</span></span>

<span data-ttu-id="5ced6-110">Configurare WordPress toouse MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="5ced6-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="5ced6-111">Eseguire hello successivo comando tooopen un editor di testo di propria scelta e creare file hello `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="5ced6-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="5ced6-112">Hello copia file toohello le righe seguenti, sostituendo la password del database per *password* (lasciare gli altri valori invariati).</span><span class="sxs-lookup"><span data-stu-id="5ced6-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="5ced6-113">Quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="5ced6-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="5ced6-114">In una cartella di lavoro, creare un file di testo `wordpress.sql` database WordPress di hello tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="5ced6-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="5ced6-115">Aggiungere hello i comandi seguenti, sostituendo la password del database per *password* (lasciare gli altri valori invariati).</span><span class="sxs-lookup"><span data-stu-id="5ced6-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="5ced6-116">Quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="5ced6-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="5ced6-117">Eseguire hello database hello toocreate di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5ced6-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="5ced6-118">Al termine del comando di hello, eliminare il file hello `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="5ced6-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="5ced6-119">Spostare hello WordPress installazione toohello documento radice del server web:</span><span class="sxs-lookup"><span data-stu-id="5ced6-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="5ced6-120">Ora è possibile completare l'installazione di WordPress hello e pubblicare su piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="5ced6-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="5ced6-121">Aprire un browser e andare troppo`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="5ced6-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="5ced6-122">Sostituire l'indirizzo IP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5ced6-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="5ced6-123">Dovrebbe essere simile toothis immagine.</span><span class="sxs-lookup"><span data-stu-id="5ced6-123">It should look similar toothis image.</span></span>

![Pagina di installazione di WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)