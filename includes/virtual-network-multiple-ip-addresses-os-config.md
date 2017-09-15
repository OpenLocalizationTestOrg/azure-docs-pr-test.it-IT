## <span data-ttu-id="6b70c-101"><a name="os-config"></a>Add IP addresses to a VM operating system (Aggiungere indirizzi IP a un sistema operativo VM)</span><span class="sxs-lookup"><span data-stu-id="6b70c-101"><a name="os-config"></a>Add IP addresses to a VM operating system</span></span>

<span data-ttu-id="6b70c-102">Connettersi e accedere alla VM creata con più indirizzi IP privati.</span><span class="sxs-lookup"><span data-stu-id="6b70c-102">Connect and login to a VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="6b70c-103">È necessario aggiungere manualmente tutti gli indirizzi IP privati aggiunti alla VM, incluso l'indirizzo primario.</span><span class="sxs-lookup"><span data-stu-id="6b70c-103">You must manually add all the private IP addresses (including the primary) that you added to the VM.</span></span> <span data-ttu-id="6b70c-104">Completare i passaggi seguenti per il sistema operativo VM:</span><span class="sxs-lookup"><span data-stu-id="6b70c-104">Complete the following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="6b70c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="6b70c-105">Windows</span></span>

1. <span data-ttu-id="6b70c-106">Da un prompt dei comandi digitare *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="6b70c-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="6b70c-107">Viene visualizzato solo l'indirizzo IP privato *Primary* , tramite DHCP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-107">You only see the *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="6b70c-108">Digitare *ncpa.cpl* nel prompt dei comandi per aprire la finestra **Connessioni di rete**.</span><span class="sxs-lookup"><span data-stu-id="6b70c-108">Type *ncpa.cpl* in the command prompt to open the **Network connections** window.</span></span>
3. <span data-ttu-id="6b70c-109">Visualizzare le proprietà per la scheda appropriata: **Connessione alla rete locale (LAN)**.</span><span class="sxs-lookup"><span data-stu-id="6b70c-109">Open the properties for the appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="6b70c-110">Fare doppio clic su Protocollo Intenret versione 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="6b70c-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="6b70c-111">Selezionare **Utilizza il seguente indirizzo IP** e immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b70c-111">Select **Use the following IP address** and enter the following values:</span></span>

    * <span data-ttu-id="6b70c-112">**Indirizzo IP**: immettere l'indirizzo IP privato *Primary* .</span><span class="sxs-lookup"><span data-stu-id="6b70c-112">**IP address**: Enter the *Primary* private IP address</span></span>
    * <span data-ttu-id="6b70c-113">**Subnet mask**: configurare questo valore in base alla subnet.</span><span class="sxs-lookup"><span data-stu-id="6b70c-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="6b70c-114">Se, ad esempio, la subnet è di tipo /24, la subnet mask è 255.255.255.0.</span><span class="sxs-lookup"><span data-stu-id="6b70c-114">For example, if the subnet is a /24 subnet then the subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="6b70c-115">**Gateway predefinito**: primo indirizzo IP nella subnet.</span><span class="sxs-lookup"><span data-stu-id="6b70c-115">**Default gateway**: The first IP address in the subnet.</span></span> <span data-ttu-id="6b70c-116">Se la subnet è 10.0.0.0/24, l'indirizzo IP del gateway è 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="6b70c-116">If your subnet is 10.0.0.0/24, then the gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="6b70c-117">Fare clic su **Utilizza i seguenti indirizzi server DNS** e immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b70c-117">Click **Use the following DNS server addresses** and enter the following values:</span></span>
        * <span data-ttu-id="6b70c-118">**Server DNS preferito**: immettere 168.63.129.16 se non si usa il proprio server DNS.</span><span class="sxs-lookup"><span data-stu-id="6b70c-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="6b70c-119">Se si usa il proprio server DNS, immettere il relativo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-119">If you are using your own DNS server, enter the IP address for your server.</span></span>
    * <span data-ttu-id="6b70c-120">Fare clic sul pulsante **Avanzate** e aggiungere altri indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-120">Click the **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="6b70c-121">Aggiungere ogni indirizzo IP privato secondario elencato nel passaggio 8 all'interfaccia di rete con la stessa subnet specificata per l'indirizzo IP primario.</span><span class="sxs-lookup"><span data-stu-id="6b70c-121">Add each of the secondary private IP addresses listed in step 8 to the NIC with the same subnet specified for the primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="6b70c-122">Se non si segue correttamente la procedura precedente, è possibile che si perda la connettività alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b70c-122">If you do not follow the steps above correctly, you may lose connectivity to your VM.</span></span> <span data-ttu-id="6b70c-123">Prima di continuare, assicurarsi che le informazioni immesse per il passaggio 5 siano corrette.</span><span class="sxs-lookup"><span data-stu-id="6b70c-123">Ensure the information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="6b70c-124">Fare clic su **OK** per chiudere le impostazioni TCP/IP e quindi di nuovo su **OK** per chiudere le impostazioni della scheda.</span><span class="sxs-lookup"><span data-stu-id="6b70c-124">Click **OK** to close out the TCP/IP settings and then **OK** again to close the adapter settings.</span></span> <span data-ttu-id="6b70c-125">Viene ristabilita la connessione RDP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="6b70c-126">Da un prompt dei comandi digitare *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="6b70c-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="6b70c-127">Tutti gli indirizzi IP aggiunti vengono visualizzati e DHCP viene disattivato.</span><span class="sxs-lookup"><span data-stu-id="6b70c-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="6b70c-128">Convalida (Windows)</span><span class="sxs-lookup"><span data-stu-id="6b70c-128">Validation (Windows)</span></span>

<span data-ttu-id="6b70c-129">Per assicurarsi che sia possibile connettersi a Internet dalla configurazione dell'indirizzo IP secondaria tramite l'indirizzo IP ad essa associato, usare il comando seguente dopo averlo aggiunto correttamente seguendo la procedura precedente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-129">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, once you have added it correctly using steps above, use the following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="6b70c-130">Per le configurazioni IP secondarie, è possibile effettuare il ping a Internet solo se alla configurazione è associato un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="6b70c-130">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="6b70c-131">Per le configurazioni IP primarie, non è necessario un indirizzo IP pubblico per il ping a Internet.</span><span class="sxs-lookup"><span data-stu-id="6b70c-131">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="6b70c-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="6b70c-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="6b70c-133">Aprire una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="6b70c-133">Open a terminal window.</span></span>
2. <span data-ttu-id="6b70c-134">Assicurarsi di essere l'utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="6b70c-134">Make sure you are the root user.</span></span> <span data-ttu-id="6b70c-135">In caso contrario, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-135">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="6b70c-136">Aggiornare il file di configurazione dell'interfaccia di rete, presupponendo 'eth0'.</span><span class="sxs-lookup"><span data-stu-id="6b70c-136">Update the configuration file of the network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="6b70c-137">Mantenere la voce esistente per dhcp.</span><span class="sxs-lookup"><span data-stu-id="6b70c-137">Keep the existing line item for dhcp.</span></span> <span data-ttu-id="6b70c-138">L'indirizzo IP primario conserva la configurazione precedente.</span><span class="sxs-lookup"><span data-stu-id="6b70c-138">The primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="6b70c-139">Aggiungere una configurazione per un indirizzo IP statico aggiuntivo con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b70c-139">Add a configuration for an additional static IP address with the following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="6b70c-140">Dovrebbe essere visualizzato un file con estensione cfg.</span><span class="sxs-lookup"><span data-stu-id="6b70c-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="6b70c-141">Open the file.</span><span class="sxs-lookup"><span data-stu-id="6b70c-141">Open the file.</span></span> <span data-ttu-id="6b70c-142">Dovrebbero essere visualizzate le righe seguenti alla fine del file:</span><span class="sxs-lookup"><span data-stu-id="6b70c-142">You should see the following lines at the end of the file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="6b70c-143">Aggiungere le righe seguenti dopo le righe esistenti nel file:</span><span class="sxs-lookup"><span data-stu-id="6b70c-143">Add the following lines after the lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="6b70c-144">Salvare il file usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-144">Save the file by using the following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="6b70c-145">Reimpostare l'interfaccia di rete con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-145">Reset the network interface with the following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="6b70c-146">Eseguire ifdown e ifup nella stessa riga se si usa una connessione remota.</span><span class="sxs-lookup"><span data-stu-id="6b70c-146">Run both ifdown and ifup in the same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="6b70c-147">Verificare che l'indirizzo IP venga aggiunto all'interfaccia di rete con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-147">Verify the IP address is added to the network interface with the following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="6b70c-148">L'indirizzo IP aggiunto dovrebbe essere incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="6b70c-148">You should see the IP address you added as part of the list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="6b70c-149">Linux (Redhat, CentOS e altro)</span><span class="sxs-lookup"><span data-stu-id="6b70c-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="6b70c-150">Aprire una finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="6b70c-150">Open a terminal window.</span></span>
2. <span data-ttu-id="6b70c-151">Assicurarsi di essere l'utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="6b70c-151">Make sure you are the root user.</span></span> <span data-ttu-id="6b70c-152">In caso contrario, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-152">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="6b70c-153">Immettere la password e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="6b70c-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="6b70c-154">Quando si è l'utente ROOT, passare alla cartella degli script di rete con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-154">Once you are the root user, navigate to the network scripts folder with the following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="6b70c-155">Elencare i file ifcfg correlati usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-155">List the related ifcfg files using the following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="6b70c-156">Uno dei file visualizzati dovrebbe essere *ifcfg-eth0* .</span><span class="sxs-lookup"><span data-stu-id="6b70c-156">You should see *ifcfg-eth0* as one of the files.</span></span>

5. <span data-ttu-id="6b70c-157">Per aggiungere un indirizzo IP, creare un file di configurazione come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6b70c-157">To add an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="6b70c-158">Si noti che è necessario creare un file per ogni configurazione IP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="6b70c-159">Aprire il file *ifcfg-eth0:0* con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-159">Open the *ifcfg-eth0:0* file with the following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="6b70c-160">Aggiungere contenuto al file, in questo caso *eth0:0*, con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6b70c-160">Add content to the file, *eth0:0* in this case, with the following command.</span></span> <span data-ttu-id="6b70c-161">Assicurarsi di aggiornare le informazioni in base all'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="6b70c-161">Be sure to update information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="6b70c-162">Salvare il file usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-162">Save the file with the following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="6b70c-163">Riavviare i servizi di rete e assicurarsi che le modifiche siano riuscite eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b70c-163">Restart the network services and make sure the changes are successful by running the following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="6b70c-164">L'indirizzo IP aggiunto, *eth0:0*, dovrebbe essere incluso nell'elenco restituito.</span><span class="sxs-lookup"><span data-stu-id="6b70c-164">You should see the IP address you added, *eth0:0*, in the list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="6b70c-165">Convalida (Linux)</span><span class="sxs-lookup"><span data-stu-id="6b70c-165">Validation (Linux)</span></span>

<span data-ttu-id="6b70c-166">Per assicurarsi che sia possibile connettersi a Internet dalla configurazione dell'indirizzo IP secondaria tramite l'indirizzo IP ad essa associato, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6b70c-166">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, use the following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="6b70c-167">Per le configurazioni IP secondarie, è possibile effettuare il ping a Internet solo se alla configurazione è associato un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="6b70c-167">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="6b70c-168">Per le configurazioni IP primarie, non è necessario un indirizzo IP pubblico per il ping a Internet.</span><span class="sxs-lookup"><span data-stu-id="6b70c-168">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

<span data-ttu-id="6b70c-169">Per le macchine virtuali Linux, quando si prova a convalidare la connettività in uscita da una scheda di interfaccia di rete secondaria, potrebbe essere necessario aggiungere le route appropriate.</span><span class="sxs-lookup"><span data-stu-id="6b70c-169">For Linux VMs, when trying to validate outbound connectivity from a secondary NIC, you may need to add appropriate routes.</span></span> <span data-ttu-id="6b70c-170">Per eseguire questa operazione è possibile procedere in molti modi.</span><span class="sxs-lookup"><span data-stu-id="6b70c-170">There are many ways to do this.</span></span> <span data-ttu-id="6b70c-171">Per informazioni sulla distribuzione Linux, vedere la documentazione appropriata.</span><span class="sxs-lookup"><span data-stu-id="6b70c-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="6b70c-172">Ecco un metodo per ottenere questo risultato:</span><span class="sxs-lookup"><span data-stu-id="6b70c-172">The following is one method to accomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="6b70c-173">Assicurarsi di sostituire:</span><span class="sxs-lookup"><span data-stu-id="6b70c-173">Be sure to replace:</span></span>
    - <span data-ttu-id="6b70c-174">**10.0.0.5** con l'indirizzo IP privato a cui è associato un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="6b70c-174">**10.0.0.5** with the private IP address that has a public IP address associated to it</span></span>
    - <span data-ttu-id="6b70c-175">**10.0.0.1** con il gateway predefinito</span><span class="sxs-lookup"><span data-stu-id="6b70c-175">**10.0.0.1** to your default gateway</span></span>
    - <span data-ttu-id="6b70c-176">**eth2** con il nome della scheda di interfaccia di rete secondaria</span><span class="sxs-lookup"><span data-stu-id="6b70c-176">**eth2** to the name of your secondary NIC</span></span>
