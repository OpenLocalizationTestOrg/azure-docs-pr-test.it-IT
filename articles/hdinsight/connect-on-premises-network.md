---
title: rete di on-premise di aaaConnect HDInsight tooyour - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate un HDInsight cluster in una rete virtuale di Azure e quindi connetterla rete locale tooyour. Informazioni su come tooconfigure la risoluzione dei nomi tra HDInsight e la rete locale tramite un server DNS personalizzato.
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>La connessione di rete locale tooyour di HDInsight

Informazioni su come tooconnect HDInsight tooyour locale rete tramite reti virtuali di Azure e un gateway VPN. Questo documento fornisce le informazioni di pianificazione su:

* Utilizzo di HDInsight in una rete virtuale di Azure che si connette tooyour locale rete.

* Configurazione di risoluzione dei nomi DNS tra la rete virtuale hello e la rete locale.

* Configurazione di rete sicurezza gruppi toorestrict internet access tooHDInsight.

* Porte fornite da HDInsight nella rete virtuale hello.

## <a name="create-hello-virtual-network-configuration"></a>Creare una configurazione di rete virtuale hello

> [!IMPORTANT]
> Se si cercano informazioni aggiuntive dettagliate sulla connessione HDInsight tooyour locale rete tramite una rete virtuale di Azure, vedere hello [rete locale di connettersi a HDInsight tooyour](connect-on-premises-network.md) documento.

Seguente hello utilizzare documenti toolearn come una rete virtuale di Azure che è connesso tooyour toocreate locale rete:
    
* [Utilizzo di hello portale di Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Uso di Azure PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Uso dell'interfaccia della riga di comando di Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Configurare la risoluzione dei nomi

tooallow HDInsight e risorse in toocommunicate rete hello unita in join in base al nome, è necessario eseguire hello seguenti azioni:

* Creare un server DNS personalizzato in hello rete virtuale di Azure.

* Configurare hello rete virtuale toouse hello server DNS personalizzato anziché predefinito hello Resolver ricorsivo di Azure.

* Configurare l'inoltro tra un server DNS personalizzato hello e il server DNS locale.

Questa configurazione consente hello seguente comportamento:

* Le richieste per i nomi di dominio completo che hanno il suffisso DNS hello __per la rete virtuale hello__ vengono inoltrati toohello un server DNS personalizzato. un server DNS personalizzato Hello inoltra quindi questi toohello richieste Resolver ricorsivo di Azure, che restituisce l'indirizzo IP hello.

* Tutte le altre richieste vengono inoltrate a server DNS di toohello locale. Anche le richieste di risorse internet pubblici, ad esempio microsoft.com vengono inoltrate server DNS locale di toohello per la risoluzione dei nomi.

Nel seguente diagramma di hello, linee verdi sono richieste per le risorse che terminano con il suffisso DNS hello della rete virtuale hello. Linee blu sono richieste per le risorse nella rete locale hello o nell'hello rete internet pubblica.

![Diagramma della modalità di risoluzione delle richieste DNS nella configurazione di hello utilizzato in questo documento](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Creare un server DNS personalizzato

> [!IMPORTANT]
> È necessario creare e configurare i server DNS hello prima di installare HDInsight in rete virtuale hello.

una VM Linux che utilizza hello toocreate [associare](https://www.isc.org/downloads/bind/) software DNS, utilizzare hello alla procedura seguente:

> [!NOTE]
> i passaggi seguenti Hello usano hello [portale di Azure](https://portal.azure.com) toocreate una macchina virtuale di Azure. Per altri modi toocreate una macchina virtuale, vedere hello [creare VM - CLI di Azure](../virtual-machines/linux/quick-create-cli.md) e [creare VM - Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documenti.

1. Da hello [portale di Azure](https://portal.azure.com)selezionare  __+__ , __calcolo__, e __Ubuntu Server 16.04 LTS__.

    ![Creare una macchina virtuale Ubuntu](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Da hello __nozioni di base__ immettere hello le seguenti informazioni:

    * __Nome__: nome descrittivo che identifica questa macchina virtuale. Ad esempio __DNSProxy__.
    * __Nome utente__: nome hello di hello account SSH.
    * __La chiave pubblica SSH__ o __Password__: hello metodo di autenticazione per hello account SSH. Si consiglia di usare le chiavi pubbliche, che sono più sicure. Per ulteriori informazioni, vedere hello [creare e usare le chiavi SSH per le macchine virtuali Linux](../virtual-machines/linux/mac-create-ssh-keys.md) documento.
    * __Gruppo di risorse__: selezionare __utilizzare esistente__, quindi selezionare gruppo di risorse hello che contiene hello di rete virtuale creata in precedenza.
    * __Percorso__: selezionare hello stesso percorso di rete virtuale hello.

    ![Configurazione di base della macchina virtuale](./media/connect-on-premises-network/vm-basics.png)

    Lasciare le altre voci in hello valori predefiniti e quindi selezionare __OK__.

3. Da hello __scegliere una dimensione__ sezione, dimensioni della macchina virtuale selezionare hello. Per questa esercitazione, selezionare più piccolo hello e opzione di costo più basso. toocontinue, utilizzare hello __selezionare__ pulsante.

4. Da hello __impostazioni__ immettere hello le seguenti informazioni:

    * __Rete virtuale__: selezionare hello rete virtuale creata in precedenza.

    * __Subnet__: selezionare hello predefinito subnet per la rete virtuale hello. Eseguire __non__ selezionare hello subnet usata dal gateway VPN hello.

    * __Account di archiviazione di diagnostica__: selezionare un account di archiviazione esistente o crearne uno nuovo.

    ![Impostazioni della rete virtuale](./media/connect-on-premises-network/virtual-network-settings.png)

    Mantenere hello altre voci hello valore predefinito, quindi selezionare __OK__ toocontinue.

5. Da hello __acquisto__ sezione, seleziona hello __acquisto__ macchina virtuale di hello toocreate pulsante.

6. Dopo aver creato, macchina virtuale hello relativo __Panoramica__ sezione viene visualizzata. Selezionare nell'elenco a sinistra di hello hello __proprietà__. Salvare hello __indirizzo IP pubblico__ e __indirizzo IP privato__ valori. Da utilizzare nella sezione successiva hello.

    ![Indirizzi IP pubblico e privato](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Installare e configurare Bind (software DNS)

1. Usare SSH tooconnect toohello __indirizzo IP pubblico__ della macchina virtuale hello. Hello di esempio seguente si connette a macchina virtuale tooa in 40.68.254.142:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Sostituire `sshuser` con account utente SSH hello specificata durante la creazione di cluster hello.

    > [!NOTE]
    > Sono disponibili un'ampia gamma di hello tooobtain modi `ssh` utilità. Su Linux, Unix e macOS, viene fornito come parte del sistema operativo hello. Se si utilizza Windows, è possibile utilizzare una delle seguenti opzioni hello:
    >
    > * [Azure Cloud Shell](../cloud-shell/quickstart.md)
    > * [Bash in Ubuntu su Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [Git (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall Bind, utilizzare hello comandi dalla sessione SSH hello seguenti:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure binding tooforward nome risoluzione richieste tooyour locale server DNS, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.options` file:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Sostituire i valori hello in hello `goodclients` sezione con intervallo di indirizzi IP hello di rete virtuale hello e rete locale. In questa sezione definisce gli indirizzi di hello che questo server DNS accetta richieste da.
    >
    > Sostituire hello `192.168.0.1` voce hello `forwarders` sezione con l'indirizzo IP hello del server DNS locale. Questo tooyour di richieste DNS route voce DNS server locale per la risoluzione.

    tooedit questo file, utilizzare hello comando seguente:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    file hello toosave, usare __Ctrl + X__, __Y__e quindi __invio__.

4. Dalla sessione SSH hello, utilizzare hello comando seguente:

    ```bash
    hostname -f
    ```

    Questo comando restituisce un toohello simile valore testo seguente:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` testo è hello __suffisso DNS__ per la rete virtuale. Salvare questo valore, che verrà usato in un secondo momento.

5. i nomi DNS di tooconfigure binding tooresolve delle risorse in rete virtuale hello, utilizzare hello segue testo come contenuto di hello di hello `/etc/bind/named.conf.local` file:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > È necessario sostituire hello `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` con il suffisso DNS hello recuperati in precedenza.

    tooedit questo file, utilizzare hello comando seguente:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    file hello toosave, usare __Ctrl + X__, __Y__e quindi __invio__.

6. toostart Bind, utilizzare hello comando seguente:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify che associano può risolvere i nomi di hello delle risorse nella rete locale, hello di utilizzare i comandi seguenti:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Sostituire `dns.mynetwork.net` con il nome di dominio completo hello (FQDN) di una risorsa nella rete locale.
    >
    > Sostituire `10.0.0.4` con hello __indirizzo IP interno__ del server DNS nella rete virtuale hello personalizzato.

    viene visualizzata la risposta di Hello toohello simile, il testo seguente:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Configurare hello toouse hello personalizzato DNS server di rete virtuale

tooconfigure hello rete virtuale toouse hello server DNS personalizzato anziché hello resolver ricorsivo Azure, utilizzare hello alla procedura seguente:

1. In hello [portale di Azure](https://portal.azure.com), selezionare la rete virtuale hello e quindi selezionare __server DNS__.

2. Selezionare __personalizzato__, quindi immettere hello __indirizzo IP interno__ del server DNS personalizzato hello. Infine, selezionare __Salva__.

    ![Impostare hello del server DNS personalizzato per la rete hello](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Configurare i server DNS locale di hello

Nella sezione precedente hello è configurato hello DNS server tooforward richieste toohello locale server DNS personalizzato. Successivamente, è necessario configurare hello locale DNS server tooforward richieste toohello server DNS personalizzato.

Per i passaggi specifici su come tooconfigure il server DNS, consultare la documentazione hello per il software del server DNS. Cercare la procedura di hello tooconfigure un __server d'inoltro condizionale__.

L'inoltro condizionale consente di inoltrare solo le richieste per un suffisso DNS specifico. In questo caso, è necessario configurare un server d'inoltro per il suffisso DNS hello della rete virtuale hello. Le richieste per questo suffisso devono essere inoltrate toohello di indirizzo IP del server DNS personalizzato hello. 

testo Hello è riportato un esempio di una configurazione di server d'inoltro condizionale per hello **associare** software DNS:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Per informazioni sull'utilizzo di DNS in **Windows Server 2016**, vedere hello [Aggiungi DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentazione...

Dopo aver configurato i server DNS di hello locale, è possibile utilizzare `nslookup` da tooverify di rete locale hello che è possibile risolvere i nomi nella rete virtuale hello. esempio di seguente Hello 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

In questo esempio utilizza hello server DNS locale in 196.168.0.4 tooresolve nome di hello del server DNS personalizzato hello. Sostituire l'indirizzo IP hello con hello per il server DNS locale di hello. Sostituire hello `dnsproxy` indirizzo con il nome di dominio completo hello del server DNS personalizzato hello.

## <a name="optional-control-network-traffic"></a>Facoltativo: Controllare il traffico di rete

È possibile utilizzare gruppi di sicurezza di rete (gruppo) o il traffico di rete toocontrol route definite dall'utente (UDR). NSGs consentono di toofilter in ingresso e in uscita, il traffico e consentire o negare il traffico di hello. UDRs consentono toocontrol come flussi di traffico tra le risorse nella rete virtuale hello hello internet e hello rete locale.

> [!WARNING]
> HDInsight richiede l'accesso in ingresso da indirizzi IP specifici nel cloud di Azure hello e accesso in uscita senza restrizioni. Quando si utilizza il traffico di toocontrol NSGs o UDRs, è necessario eseguire hello alla procedura seguente:
>
> 1. Trovare hello gli indirizzi IP per il percorso di hello che contiene la rete virtuale. Per un elenco di indirizzi IP necessari in base alla località, vedere [Indirizzi IP richiesti](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Consentire il traffico in ingresso da indirizzi IP hello.
>
>    * __GRUPPO__: Consenti __in ingresso__ il traffico sulla porta __443__ da hello __Internet__.
>    * __UDR__: hello Set __Hop successivo__ tipo too__Internet__ route hello.

Per un esempio di utilizzo di Azure PowerShell o hello Azure CLI toocreate NSGs, vedere hello [estendere HDInsight con reti virtuali di Azure](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) documento.

## <a name="create-hello-hdinsight-cluster"></a>Creare cluster HDInsight hello

> [!WARNING]
> È necessario configurare un server DNS personalizzato hello prima di installare la rete virtuale hello HDInsight.

Hello di utilizzare i passaggi in hello [creare un cluster HDInsight tramite il portale di Azure hello](./hdinsight-hadoop-create-linux-clusters-portal.md) toocreate documento un cluster HDInsight.

> [!WARNING]
> * Durante la creazione del cluster, è necessario scegliere il percorso hello contenente la rete virtuale.
>
> * In hello __impostazioni avanzate__ parte della configurazione, è necessario selezionare la rete virtuale hello e subnet creato in precedenza.

## <a name="connecting-toohdinsight"></a>Connessione tooHDInsight

La maggior parte delle documentazione su HDInsight si presuppone la presenza di cluster di accesso toohello su hello internet. Ad esempio, che è possibile connettersi cluster toohello https://CLUSTERNAME.azurehdinsight.net. Questo indirizzo Usa gateway hello pubblico, non è disponibile se è stato utilizzato NSGs o UDRs toorestrict accesso da hello internet.

toodirectly connessione tooHDInsight attraverso la rete virtuale hello, usare hello alla procedura seguente:

1. i nomi di dominio completo interno hello toodiscover hello HDInsight dei nodi del cluster, utilizzare uno dei seguenti metodi hello:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. porta hello toodetermine che un servizio è disponibile, vedere hello [porte utilizzate da servizi di Hadoop in HDInsight](./hdinsight-hadoop-port-settings-for-services.md) documento.

    > [!IMPORTANT]
    > Alcuni servizi ospitate nei nodi head hello attivi solo in un nodo alla volta. Se si tenta di accedere al servizio in un nodo head e si verifica un errore, passare toohello altro nodo head.
    >
    > Ambari, ad esempio, è attivo solo in un nodo head per volta. Se si tenta l'accesso a un nodo head Ambari e viene restituito un errore 404, tramite cui viene eseguito hello altro nodo head.

## <a name="next-steps"></a>Passaggi successivi

* Per altre informazioni sull'uso di HDInsight in una rete virtuale, vedere [Estendere le funzionalità di HDInsight usando Rete virtuale di Azure](./hdinsight-extend-hadoop-virtual-network.md).

* Per ulteriori informazioni su reti virtuali di Azure, vedere hello [Cenni preliminari sulla rete virtuale di Azure](../virtual-network/virtual-networks-overview.md).

* Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).

* Per altre informazioni sulle route definite dall'utente, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).
