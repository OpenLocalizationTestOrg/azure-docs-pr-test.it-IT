## <a name="build-iot-edge"></a>Compilare IoT Edge

Questa esercitazione Usa personalizzata bordo IoT moduli toocommunicate con hello soluzione preconfigurata di monitoraggio remoto. Pertanto, è necessario moduli di Edge IoT hello toobuild dal codice sorgente personalizzato. Hello le sezioni seguenti descrivono come tooinstall IoT Edge e compilazione hello modulo IoT bordo personalizzato.

### <a name="install-iot-edge"></a>Installare IoT Edge

Hello passaggi seguenti descrivono come tooinstall hello precompilato software IoT bordo su hello NUC Intel:

1. Configurare repository pacchetto smart hello necessario eseguendo hello seguendo i comandi hello NUC Intel:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Immettere `y` quando hello comando richiede troppo**includere questo canale?**.

1. Gestione aggiornamenti hello smart pacchetto eseguendo hello comando seguente:

    ```bash
    smart update
    ```

1. Installare il pacchetto di Azure IoT Edge hello eseguendo hello comando seguente:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Verificare l'installazione di hello, in esecuzione: esempio hello "Hello world". In questo esempio scrive un file di log. txt hello world messaggio toohello ogni cinque secondi. Hello eseguire i comandi seguenti: esempio hello "Hello world":

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Ignora modifiche **argomento non valido** messaggi quando si arresta l'esempio hello.

    Comando che segue di hello utilizzare contenuto hello tooview hello del file di log:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Risoluzione dei problemi

Se viene visualizzato l'errore hello "alcun pacchetto vengono fornite util-linux-dev", provare a riavviare hello NUC Intel.
