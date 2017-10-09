## <span data-ttu-id="9cb8c-101"><a name="os-config"></a>Aggiungi sistema operativo IP indirizzi tooa VM</span><span class="sxs-lookup"><span data-stu-id="9cb8c-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="9cb8c-102">Connettersi e account di accesso tooa macchina virtuale creata con più indirizzi IP privati.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="9cb8c-103">È necessario aggiungere manualmente tutti hello indirizzi IP privati (primaria inclusa hello) aggiunto toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="9cb8c-104">Completare hello alla procedura seguente per il sistema operativo VM:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="9cb8c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="9cb8c-105">Windows</span></span>

1. <span data-ttu-id="9cb8c-106">Da un prompt dei comandi digitare *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="9cb8c-107">È possibile visualizzare solo hello *primario* indirizzo IP privato (tramite DHCP).</span><span class="sxs-lookup"><span data-stu-id="9cb8c-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="9cb8c-108">Tipo *ncpa.cpl* in hello tooopen prompt dei comandi di hello **connessioni di rete** finestra.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="9cb8c-109">Aprire le proprietà di hello di adapter appropriato hello: **connessione Area locale**.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="9cb8c-110">Fare doppio clic su Protocollo Intenret versione 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="9cb8c-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="9cb8c-111">Selezionare **hello utilizzare seguente indirizzo IP** e immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="9cb8c-112">**Indirizzo IP**: immettere hello *primario* indirizzo IP privato</span><span class="sxs-lookup"><span data-stu-id="9cb8c-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="9cb8c-113">**Subnet mask**: configurare questo valore in base alla subnet.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="9cb8c-114">Ad esempio, se hello subnet è un /24 subnet hello quindi di subnet mask è 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="9cb8c-115">**Gateway predefinito**: hello primo indirizzo IP nella subnet hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="9cb8c-116">Se la subnet è 10.0.0.0/24, indirizzo IP del gateway hello è 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="9cb8c-117">Fare clic su **hello utilizzare seguenti indirizzi server DNS** e immettere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="9cb8c-118">**Server DNS preferito**: immettere 168.63.129.16 se non si usa il proprio server DNS.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="9cb8c-119">Se si utilizza il proprio server DNS, immettere l'indirizzo IP hello del server.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="9cb8c-120">Fare clic su hello **avanzate** pulsante e aggiungere altri indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="9cb8c-121">Aggiungere tutti i hello secondari indirizzi IP elencati nel passaggio 8 toohello NIC con hello stessa subnet specificato per l'indirizzo IP primario hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="9cb8c-122">Se non si segue i passaggi di hello precedenti correttamente, si potrebbero perdere la connettività tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="9cb8c-123">Verificare le informazioni di hello immesse per il passaggio 5 sono accurate prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="9cb8c-124">Fare clic su **OK** tooclose le impostazioni TCP/IP hello e quindi **OK** nuovamente tooclose hello le impostazioni della scheda.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="9cb8c-125">Viene ristabilita la connessione RDP.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="9cb8c-126">Da un prompt dei comandi digitare *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="9cb8c-127">Tutti gli indirizzi IP aggiunti vengono visualizzati e DHCP viene disattivato.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="9cb8c-128">Convalida (Windows)</span><span class="sxs-lookup"><span data-stu-id="9cb8c-128">Validation (Windows)</span></span>

<span data-ttu-id="9cb8c-129">tooensure si è in grado di tooconnect toohello internet dalla configurazione IP secondaria tramite hello che IP pubblico associato, dopo aver aggiunto correttamente mediante i passaggi sopra, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="9cb8c-130">Per le configurazioni IP secondarie, è possibile solo effettuare il ping toohello Internet se configurazione hello dispone di un indirizzo IP pubblico è associato.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="9cb8c-131">Per le configurazioni IP primarie, un indirizzo IP pubblico non è necessario tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="9cb8c-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="9cb8c-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="9cb8c-133">Aprire una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-133">Open a terminal window.</span></span>
2. <span data-ttu-id="9cb8c-134">Verificare che l'utente root hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-134">Make sure you are hello root user.</span></span> <span data-ttu-id="9cb8c-135">Se non si dispone, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="9cb8c-136">Aggiornare il file di configurazione hello hello dell'interfaccia di rete (presupponendo che 'eth0').</span><span class="sxs-lookup"><span data-stu-id="9cb8c-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="9cb8c-137">Mantenere hello voce esistente per dhcp.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="9cb8c-138">indirizzo IP primario Hello rimane configurato che aveva in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="9cb8c-139">Aggiungere una configurazione per un indirizzo IP statico aggiuntivo con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="9cb8c-140">Dovrebbe essere visualizzato un file con estensione cfg.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="9cb8c-141">File hello aperto.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-141">Open hello file.</span></span> <span data-ttu-id="9cb8c-142">È necessario visualizzare hello seguenti righe al fine di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="9cb8c-143">Aggiungere hello seguenti righe dopo le righe hello presenti in questo file:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="9cb8c-144">Salvare il file hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="9cb8c-145">Reimpostare l'interfaccia di rete hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9cb8c-146">Eseguire ifdown e ifup nella stessa riga se si utilizza una connessione remota hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="9cb8c-147">Verificare l'indirizzo IP hello viene aggiunta l'interfaccia di rete toohello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="9cb8c-148">Dovrebbe essere hello IP indirizzo aggiunto come parte dell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="9cb8c-149">Linux (Redhat, CentOS e altro)</span><span class="sxs-lookup"><span data-stu-id="9cb8c-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="9cb8c-150">Aprire una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-150">Open a terminal window.</span></span>
2. <span data-ttu-id="9cb8c-151">Verificare che l'utente root hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-151">Make sure you are hello root user.</span></span> <span data-ttu-id="9cb8c-152">Se non si dispone, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="9cb8c-153">Immettere la password e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="9cb8c-154">Una volta utente root hello, passare cartella degli script di rete toohello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="9cb8c-155">Hello elenco correlate file ifcfg utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="9cb8c-156">Dovrebbe essere *ifcfg eth0* come uno dei file hello.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="9cb8c-157">tooadd un indirizzo IP, creare un file di configurazione relativo, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="9cb8c-158">Si noti che è necessario creare un file per ogni configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="9cb8c-159">Aprire hello *ifcfg-eth0:0* file con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="9cb8c-160">Aggiungere il file di contenuto toohello *eth0:0* in questo caso, con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="9cb8c-161">Informazioni tooupdate che dipende dall'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="9cb8c-162">Salvare il file hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="9cb8c-163">Riavviare i servizi di rete hello e assicurarsi che le modifiche di hello hanno esito positivo eseguendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="9cb8c-164">Si dovrebbe essere aggiunto, l'indirizzo IP hello *eth0:0*, nell'elenco di hello restituito.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="9cb8c-165">Convalida (Linux)</span><span class="sxs-lookup"><span data-stu-id="9cb8c-165">Validation (Linux)</span></span>

<span data-ttu-id="9cb8c-166">si è in grado di tooconnect toohello tooensure internet dalla configurazione IP secondaria tramite indirizzo IP pubblico hello verrà associata, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="9cb8c-167">Per le configurazioni IP secondarie, è possibile solo effettuare il ping toohello Internet se configurazione hello dispone di un indirizzo IP pubblico è associato.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="9cb8c-168">Per le configurazioni IP primarie, un indirizzo IP pubblico non è necessario tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="9cb8c-169">Per le macchine virtuali Linux, durante il tentativo di toovalidate connettività in uscita da una scheda di rete secondaria, potrebbe essere necessario route appropriate tooadd.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="9cb8c-170">Esistono molti modi toodo questo.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-170">There are many ways toodo this.</span></span> <span data-ttu-id="9cb8c-171">Per informazioni sulla distribuzione Linux, vedere la documentazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="9cb8c-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="9cb8c-172">esempio Hello si tratta di un metodo tooaccomplish:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="9cb8c-173">Essere tooreplace che:</span><span class="sxs-lookup"><span data-stu-id="9cb8c-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="9cb8c-174">**10.0.0.5** con hello privata indirizzo con un indirizzo IP pubblico indirizzo IP associato tooit</span><span class="sxs-lookup"><span data-stu-id="9cb8c-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="9cb8c-175">**10.0.0.1** gateway predefinito tooyour</span><span class="sxs-lookup"><span data-stu-id="9cb8c-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="9cb8c-176">**eth2** toohello nome la scheda di rete secondaria</span><span class="sxs-lookup"><span data-stu-id="9cb8c-176">**eth2** toohello name of your secondary NIC</span></span>
