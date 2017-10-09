# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Creare un cluster, Kubernetes, controller di dominio o del sistema operativo o Docker Swarm tooa connessione remota
Dopo aver creato un cluster il servizio contenitore di Azure, è necessario tooconnect toohello cluster toodeploy e gestire i carichi di lavoro. In questo articolo viene descritto come tooconnect toohello master VM di hello cluster da un computer remoto. 

i cluster di Kubernetes, controller di dominio/OS e Docker Swarm Hello includono localmente gli endpoint HTTP. Per Kubernetes, questo endpoint viene esposto in modo sicuro su internet hello ed è possibile accedervi tramite l'esecuzione di hello `kubectl` strumento da riga di comando da qualsiasi computer connesso a internet. 

Per i controller di dominio/OS e Docker Swarm, è consigliabile creare un tunnel sicuro shell (SSH) dal sistema di Gestione cluster toohello computer locale. Dopo aver stabilito il tunnel hello, è possibile eseguire comandi che utilizzano gli endpoint HTTP hello e web dell'interfaccia di orchestrator hello visualizzazione (se disponibile) dal sistema locale. 

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Kubernetes, DC/OS o Docker Swarm [distribuito nel servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA file di chiave privata, corrispondente toohello pubblica toohello aggiunto chiave cluster durante la distribuzione. Questi comandi presuppongono la chiave SSH privata hello in `$HOME/.ssh/id_rsa` nel computer in uso. Per altre informazioni, vedere le istruzioni per [macOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) o per [Windows](../articles/virtual-machines/linux/ssh-from-windows.md). Se la connessione SSH hello non funziona, potrebbe essere troppo [reimpostare le chiavi SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Connettere il cluster di Kubernetes tooa

Seguire questi passaggi tooinstall e configurare `kubectl` nel computer in uso.

> [!NOTE] 
> In Linux o Mac OS, potrebbe essere necessario comandi hello toorun in questa sezione utilizzando `sudo`.
> 

### <a name="install-kubectl"></a>Installare kubectl
Un modo tooinstall questo strumento è hello toouse `az acs kubernetes install-cli` comando CLI di Azure 2.0. toorun questo comando, assicurarsi che si [installato](/cli/azure/install-az-cli2) hello 2.0 CLI di Azure più recenti e registrato nell'account Azure tooan (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

In alternativa, è possibile scaricare hello più recente `kubectl` client direttamente dal hello [Kubernetes rilascia pagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Per altre informazioni, vedere [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Installazione e configurazione di kubectl).

### <a name="download-cluster-credentials"></a>Scaricare le credenziali del cluster
Dopo aver `kubectl` installato, è necessario il computer tooyour le credenziali di toocopy hello del cluster. Le credenziali di un modo toodo get hello è con hello `az acs kubernetes get-credentials` comando. Passare il nome di hello hello del gruppo di risorse e il nome di hello della risorsa del servizio contenitore hello:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Questo comando Scarica le credenziali del cluster hello troppo`$HOME/.kube/config`, dove `kubectl` si aspetta che lo trova toobe.

In alternativa, è possibile utilizzare `scp` toosecurely copia del file hello da `$HOME/.kube/config` computer hello master VM tooyour locale. ad esempio:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Se si utilizza Windows, è possibile utilizzare Bash in Ubuntu in Windows, i client per copie di file sicuri PuTTy hello o uno strumento simile.

### <a name="use-kubectl"></a>Usare kubectl

Dopo aver `kubectl` configurato, testare la connessione hello elencare hello i nodi del cluster:

```bash
kubectl get nodes
```

È possibile provare altri comandi `kubectl`. Ad esempio, è possibile visualizzare Kubernetes Dashboard hello. Eseguire prima di tutto un proxy server dell'API Kubernetes toohello:

```bash
kubectl proxy
```

Hello UI Kubernetes è ora disponibile all'indirizzo: `http://localhost:8001/ui`.

Per ulteriori informazioni, vedere hello [Kubernetes introduttiva](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Connettere il cluster di controller di dominio o del sistema operativo o sciame tooa

hello toouse DC/OS e cluster Docker Swarm distribuiti dal servizio di contenitore di Azure, seguire questi toocreate istruzioni un tunnel SSH dal sistema di Windows, Linux o macOS locale. 

> [!NOTE]
> Queste istruzioni sono incentrate sul tunneling del traffico TCP su SSH. È anche possibile avviare una sessione interattiva di SSH con uno dei sistemi di gestione di hello interne al cluster, ma non ti consigliamo di questa. L'intervento diretto su un sistema interno comporta il rischio di modifiche accidentali alla configurazione.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Creare un tunnel SSH in Linux o macOS
Hello prima cosa è quando si crea un tunnel SSH in Linux o macOS è toolocate hello nome DNS pubblico di schemi con bilanciamento del carico hello. A tale scopo, seguire questa procedura:


1. In hello [portale di Azure](https://portal.azure.com), selezionare il gruppo di risorse toohello che contiene il cluster del servizio contenitore. Espandere il gruppo di risorse hello in modo che ogni risorsa è visualizzata. 

2. Fare clic su hello **servizio contenitore** risorse e fare clic su **Panoramica**. Hello **FQDN Master** di hello cluster viene visualizzato sotto **Essentials**. Salvare questo nome per usarlo in seguito. 

    ![Nome DNS pubblico](./media/container-service-connect/pubdns.png)

    In alternativa, eseguire hello `az acs show` comando sul servizio contenitore. Cercare hello **profilo Master: fqdn** proprietà nell'output del comando hello.

3. Aprire una shell ed eseguire hello `ssh` comando specificando hello seguenti valori: 

    **LOCAL_PORT** è sul lato servizio hello di hello tunnel tooconnect per la porta TCP hello. Per sciame, impostare questo too2375. Per i controller di dominio o del sistema operativo, impostare questo too80. 
    **REMOTE_PORT** hello porta dell'endpoint hello che si desidera tooexpose. Per Swarm, usare la porta 2375. Per DC/OS usare la porta 80.  
    **Nome utente** hello utente nome fornito al momento della distribuzione cluster hello.  
    **DNSPREFIX** è un prefisso DNS hello fornito al momento della distribuzione cluster hello.  
    **AREA** hello area in cui si trova il gruppo di risorse.  
    **PATH_TO_PRIVATE_KEY** [facoltativo] è hello percorso toohello chiave privata corrispondente toohello chiave pubblica fornita al momento della creazione del cluster di hello. Utilizzare questa opzione con hello `-i` flag.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > la porta di connessione SSH Hello è 2200 e non hello porta standard 22. In un cluster con più di una macchina virtuale master, si tratta di hello connessione porta toohello prima master macchina virtuale.
  > 

  comando Hello restituisce senza output.

Vedere esempi hello per controller di dominio/OS e sciame in hello le sezioni seguenti.    

### <a name="dcos-tunnel"></a>Tunnel DC/OS
tooopen un tunnel per gli endpoint di controller di dominio o del sistema operativo, eseguire un comando simile hello seguente:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Verificare che non sia presente un altro processo locale che associa la porta 80. Se necessario, è possibile specificare una porta locale diversa dalla porta 80, ad esempio la porta 8080. È tuttavia possibile che alcuni collegamenti dell'interfaccia utente Web non funzionino quando si usa questa porta.
>

È ora possibile accedere a endpoint di controller di dominio/OS hello dal sistema locale tramite hello URL (presupponendo che la porta locale 80) seguenti:

* Controller di dominio/sistema operativo: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Analogamente, è possibile raggiungere le API rest hello per ogni applicazione attraverso questo tunnel.

### <a name="swarm-tunnel"></a>Tunnel Swarm
tooopen un endpoint sciame toohello tunnel, eseguire un comando simile hello seguente:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Verificare che non sia presente un altro processo locale che associa la porta 2375. Ad esempio, se si esegue il daemon di Docker hello in locale, viene impostato dalla porta toouse predefinito 2375. Se necessario, è possibile specificare una porta locale diversa dalla porta 2375.
>

Ora è possibile accedere tramite l'interfaccia della riga di comando di Docker hello (Docker CLI) nel sistema locale cluster Docker Swarm hello. Per istruzioni sull'installazione, vedere [Install Docker](https://docs.docker.com/engine/installation/) (Installare Docker).

Impostare il toohello variabile di ambiente DOCKER_HOST porta locale che è configurato per il tunnel hello. 

```bash
export DOCKER_HOST=:2375
```

Eseguire i comandi di Docker cluster Docker Swarm toohello tunnel. ad esempio:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Creare un tunnel SSH in Windows
Esistono più opzioni per creare i tunnel SSH in Windows. Se si eseguono Bash Ubuntu in Windows o uno strumento simile, è possibile seguire istruzioni tunneling SSH hello illustrate in precedenza in questo articolo per macOS e Linux. In alternativa, in Windows, questa sezione viene descritto come tunnel di hello toouse toocreate PuTTY.

1. [Scaricare PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.

2. Eseguire un'applicazione hello.

3. Immettere un nome host è costituito da nome utente amministratore di cluster hello e nome DNS pubblico hello del database master prima di hello cluster hello. Hello **nome Host** simile troppo`azureuser@PublicDNSName`. Immettere 2200 per hello **porta**.

    ![Configurazione PuTTY 1](./media/container-service-connect/putty1.png)

4. Selezionare **SSH > Auth**. Aggiungere un percorso tooyour file di chiave privata (formato *.ppk) per l'autenticazione. È possibile utilizzare uno strumento come [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate questo file hello del cluster di hello toocreate utilizzati chiave SSH.

    ![Configurazione PuTTY 2](./media/container-service-connect/putty2.png)

5. Selezionare **SSH > tunnel** e configurare segue hello inoltrati porte:

    * **Source Port** (Porta di origine): usare 80 per DC/OS o 2375 per Swarm.
    * **Destination:** usare localhost:80 per il controller di dominio/sistema operativo o localhost:2375 per Swarm.

    Hello di esempio seguente è configurato per il controller di dominio o sistema operativo, ma sarà simile per Docker Swarm.

    > [!NOTE]
    > La porta 80 non deve essere usata quando si crea il tunnel.
    > 

    ![Configurazione PuTTY 3](./media/container-service-connect/putty3.png)

6. Al termine, fare clic su **sessione > salvare** configurazione della connessione toosave hello.

7. tooconnect toohello PuTTY sessione, fare clic su **aprire**. Quando ci si connette, è possibile visualizzare la configurazione della porta hello nel registro eventi PuTTY hello.

    ![Log eventi di PuTTY](./media/container-service-connect/putty4.png)

Dopo aver configurato i tunnel hello per controller di dominio o del sistema operativo, è possibile accedere hello relativi endpoint:

* Controller di dominio/sistema operativo: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Dopo aver configurato i tunnel hello per Docker Swarm, aprire il tooconfigure le impostazioni di Windows una variabile di ambiente system denominata `DOCKER_HOST` con un valore di `:2375`. Quindi, è possibile accedere cluster sciame hello tramite hello CLI di Docker.

## <a name="next-steps"></a>Passaggi successivi
Distribuire e gestire contenitori nel cluster:

* [Uso del servizio contenitore di Azure e Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Gestione di contenitori tramite l'API REST](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Utilizzo di hello Azure il servizio di contenitore e Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

