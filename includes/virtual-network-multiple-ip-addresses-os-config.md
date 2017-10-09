## <a name="os-config"></a>Aggiungi sistema operativo IP indirizzi tooa VM

Connettersi e account di accesso tooa macchina virtuale creata con più indirizzi IP privati. È necessario aggiungere manualmente tutti hello indirizzi IP privati (primaria inclusa hello) aggiunto toohello macchina virtuale. Completare hello alla procedura seguente per il sistema operativo VM:

### <a name="windows"></a>Windows

1. Da un prompt dei comandi digitare *ipconfig /all*.  È possibile visualizzare solo hello *primario* indirizzo IP privato (tramite DHCP).
2. Tipo *ncpa.cpl* in hello tooopen prompt dei comandi di hello **connessioni di rete** finestra.
3. Aprire le proprietà di hello di adapter appropriato hello: **connessione Area locale**.
4. Fare doppio clic su Protocollo Intenret versione 4 (IPv4).
5. Selezionare **hello utilizzare seguente indirizzo IP** e immettere hello seguenti valori:

    * **Indirizzo IP**: immettere hello *primario* indirizzo IP privato
    * **Subnet mask**: configurare questo valore in base alla subnet. Ad esempio, se hello subnet è un /24 subnet hello quindi di subnet mask è 255.255.255.0.
    * **Gateway predefinito**: hello primo indirizzo IP nella subnet hello. Se la subnet è 10.0.0.0/24, indirizzo IP del gateway hello è 10.0.0.1.
    * Fare clic su **hello utilizzare seguenti indirizzi server DNS** e immettere hello seguenti valori:
        * **Server DNS preferito**: immettere 168.63.129.16 se non si usa il proprio server DNS.  Se si utilizza il proprio server DNS, immettere l'indirizzo IP hello del server.
    * Fare clic su hello **avanzate** pulsante e aggiungere altri indirizzi IP. Aggiungere tutti i hello secondari indirizzi IP elencati nel passaggio 8 toohello NIC con hello stessa subnet specificato per l'indirizzo IP primario hello.
        >[!WARNING] 
        >Se non si segue i passaggi di hello precedenti correttamente, si potrebbero perdere la connettività tooyour macchina virtuale. Verificare le informazioni di hello immesse per il passaggio 5 sono accurate prima di procedere.

    * Fare clic su **OK** tooclose le impostazioni TCP/IP hello e quindi **OK** nuovamente tooclose hello le impostazioni della scheda. Viene ristabilita la connessione RDP.

6. Da un prompt dei comandi digitare *ipconfig /all*. Tutti gli indirizzi IP aggiunti vengono visualizzati e DHCP viene disattivato.


### <a name="validation-windows"></a>Convalida (Windows)

tooensure si è in grado di tooconnect toohello internet dalla configurazione IP secondaria tramite hello che IP pubblico associato, dopo aver aggiunto correttamente mediante i passaggi sopra, utilizzare hello comando seguente:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Per le configurazioni IP secondarie, è possibile solo effettuare il ping toohello Internet se configurazione hello dispone di un indirizzo IP pubblico è associato. Per le configurazioni IP primarie, un indirizzo IP pubblico non è necessario tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Aprire una finestra del terminale.
2. Verificare che l'utente root hello. Se non si dispone, immettere hello comando seguente:

    ```bash
    sudo -i
    ```

3. Aggiornare il file di configurazione hello hello dell'interfaccia di rete (presupponendo che 'eth0').

    * Mantenere hello voce esistente per dhcp. indirizzo IP primario Hello rimane configurato che aveva in precedenza.
    * Aggiungere una configurazione per un indirizzo IP statico aggiuntivo con hello seguenti comandi:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Dovrebbe essere visualizzato un file con estensione cfg.
4. File hello aperto. È necessario visualizzare hello seguenti righe al fine di hello del file hello:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Aggiungere hello seguenti righe dopo le righe hello presenti in questo file:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Salvare il file hello utilizzando hello comando seguente:

    ```bash
    :wq
    ```

7. Reimpostare l'interfaccia di rete hello con hello comando seguente:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Eseguire ifdown e ifup nella stessa riga se si utilizza una connessione remota hello.
    >

8. Verificare l'indirizzo IP hello viene aggiunta l'interfaccia di rete toohello con hello comando seguente:

    ```bash
    ip addr list eth0
    ```

    Dovrebbe essere hello IP indirizzo aggiunto come parte dell'elenco di hello.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS e altro)

1. Aprire una finestra del terminale.
2. Verificare che l'utente root hello. Se non si dispone, immettere hello comando seguente:

    ```bash
    sudo -i
    ```

3. Immettere la password e seguire le istruzioni visualizzate. Una volta utente root hello, passare cartella degli script di rete toohello con hello comando seguente:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Hello elenco correlate file ifcfg utilizzando hello comando seguente:

    ```bash
    ls ifcfg-*
    ```

    Dovrebbe essere *ifcfg eth0* come uno dei file hello.

5. tooadd un indirizzo IP, creare un file di configurazione relativo, come illustrato di seguito. Si noti che è necessario creare un file per ogni configurazione IP.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Aprire hello *ifcfg-eth0:0* file con hello comando seguente:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Aggiungere il file di contenuto toohello *eth0:0* in questo caso, con hello comando seguente. Informazioni tooupdate che dipende dall'indirizzo IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Salvare il file hello con hello comando seguente:

    ```bash
    :wq
    ```

9. Riavviare i servizi di rete hello e assicurarsi che le modifiche di hello hanno esito positivo eseguendo hello seguenti comandi:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Si dovrebbe essere aggiunto, l'indirizzo IP hello *eth0:0*, nell'elenco di hello restituito.

### <a name="validation-linux"></a>Convalida (Linux)

si è in grado di tooconnect toohello tooensure internet dalla configurazione IP secondaria tramite indirizzo IP pubblico hello verrà associata, utilizzare hello comando seguente:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Per le configurazioni IP secondarie, è possibile solo effettuare il ping toohello Internet se configurazione hello dispone di un indirizzo IP pubblico è associato. Per le configurazioni IP primarie, un indirizzo IP pubblico non è necessario tooping toohello Internet.

Per le macchine virtuali Linux, durante il tentativo di toovalidate connettività in uscita da una scheda di rete secondaria, potrebbe essere necessario route appropriate tooadd. Esistono molti modi toodo questo. Per informazioni sulla distribuzione Linux, vedere la documentazione appropriata. esempio Hello si tratta di un metodo tooaccomplish:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Essere tooreplace che:
    - **10.0.0.5** con hello privata indirizzo con un indirizzo IP pubblico indirizzo IP associato tooit
    - **10.0.0.1** gateway predefinito tooyour
    - **eth2** toohello nome la scheda di rete secondaria
