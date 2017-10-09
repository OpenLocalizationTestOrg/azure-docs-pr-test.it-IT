# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Ridimensionare i nodi agente in un cluster del servizio contenitore
Dopo aver [distribuzione di un cluster il servizio contenitore di Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), potrebbe essere necessario numero hello toochange dei nodi dell'agente. Ad esempio, potrebbero essere necessari più agenti in modo da eseguire più applicazioni o istanze contenitore. 

È possibile modificare il numero di hello di nodi dell'agente in un cluster di controller di dominio o del sistema operativo, Docker Swarm o Kubernetes utilizzando hello portale di Azure o hello CLI di Azure 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Scalabilità con hello portale di Azure

1. In hello [portale di Azure](https://portal.azure.com), cercare **servizi contenitore**, quindi fare clic su servizio di contenitore hello che si desidera toomodify.
2. In hello **servizio contenitore** pannello, fare clic su **agenti**.
3. In **conteggio VM**, immettere il numero desiderato di hello dei nodi di agenti.

    ![Ridimensionare un pool nel portale di hello](./media/container-service-scale/container-service-scale-portal.png)

4. configurazione di hello toosave, fare clic su **salvare**.

## <a name="scale-with-hello-azure-cli-20"></a>Scalabilità con hello Azure CLI 2.0

Assicurarsi che si [installato](/cli/azure/install-az-cli2) hello 2.0 CLI di Azure più recenti e registrato nel tooan account azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Vedere il numero di agenti corrente di hello
numero di hello toosee di agenti attualmente cluster hello, esegue hello `az acs show` comando. Verrà visualizzata configurazione cluster hello. Ad esempio, hello comando Mostra hello configurazione del servizio di contenitore hello denominato seguente `containerservice-myACSName` nel gruppo di risorse hello `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

comando Hello restituisce il numero di hello degli agenti in hello `Count` valore `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Utilizzare hello az comando scala acs
numero di hello toochange dei nodi di agente, eseguire hello `az acs scale` hello comando e specificare **gruppo di risorse**, **nome del servizio contenitore**, hello desiderato e **nuovo numero di agenti**. Se si specifica un numero più piccolo è possibile ridurre le prestazioni, mentre se si specifica un numero più grande è possibile aumentarle.

Ad esempio, toochange hello numero di agenti in hello too10 cluster precedente, hello tipo comando seguente:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hello Azure CLI 2.0 restituisce una stringa JSON che rappresenta la nuova hello-configurazione del servizio di contenitore hello, incluso il numero di hello nuovo agente.

Per ulteriori opzioni di comandi, eseguire `az acs scale --help`.

## <a name="scaling-considerations"></a>Considerazioni sulla scalabilità

* numero di Hello dei nodi dell'agente deve essere compreso tra 1 e 100 inclusi. 

* La quota di core è possibile limitare il numero di hello dei nodi dell'agente in un cluster.

* Le operazioni di ridimensionamento nodo agente vengono applicati tooan set di scalabilità della macchina virtuale di Azure che contiene il pool di agenti hello. In un cluster di controller di dominio o del sistema operativo, vengono ridimensionati solo i nodi dell'agente nel pool privata hello dalle operazioni hello illustrate in questo articolo.

* A seconda di orchestrator hello che la distribuzione del cluster, è possibile ridimensionare separatamente numero hello di istanze di un contenitore in esecuzione nel cluster hello. Ad esempio, in un cluster di controller di dominio o del sistema operativo, utilizzare hello [dell'interfaccia utente maratona](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) numero hello toochange di istanze di un'applicazione contenitore.

* Attualmente, non è supportata la scalabilità automatica dei nodi di agenti in un cluster del servizio contenitore.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [altri esempi](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) dell'uso di comandi dell'interfaccia della riga di comando di Azure 2.0 con il servizio contenitore di Azure.
* Ulteriori informazioni sui [pool di agenti DC/OS](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) del servizio contenitore di Azure.

