## <a name="install-wordpress"></a>Installare WordPress

Se si desidera tootry lo stack, installare un'app di esempio. Ad esempio, alla procedura seguente hello installa open source di hello [WordPress](https://wordpress.org/) blog e siti Web toocreate di piattaforma. Includere altri carichi di lavoro di tootry [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/). 

Questa configurazione di WordPress è per il modello di verifica. Per ulteriori informazioni e le impostazioni per l'installazione di produzione, vedere hello [WordPress documentazione](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Installare il pacchetto di WordPress hello

Eseguire hello comando seguente:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Configurazione di WordPress

Configurare WordPress toouse MySQL e PHP. Eseguire hello successivo comando tooopen un editor di testo di propria scelta e creare file hello `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Hello copia file toohello le righe seguenti, sostituendo la password del database per *password* (lasciare gli altri valori invariati). Quindi salvare il file hello.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

In una cartella di lavoro, creare un file di testo `wordpress.sql` database WordPress di hello tooconfigure: 

```bash
sudo sensible-editor wordpress.sql
```

Aggiungere hello i comandi seguenti, sostituendo la password del database per *password* (lasciare gli altri valori invariati). Quindi salvare il file hello.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Eseguire hello database hello toocreate di comando seguente:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Al termine del comando di hello, eliminare il file hello `wordpress.sql`.

Spostare hello WordPress installazione toohello documento radice del server web:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Ora è possibile completare l'installazione di WordPress hello e pubblicare su piattaforma hello. Aprire un browser e andare troppo`http://yourPublicIPAddress/wordpress`. Sostituire l'indirizzo IP pubblico hello della macchina virtuale. Dovrebbe essere simile toothis immagine.

![Pagina di installazione di WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)