# <a name="securing-docker-containers-in-azure-container-service"></a>Protezione dei contenitori Docker nel servizio contenitore di Azure

Questo articolo introduce considerazioni e indicazioni per la sicurezza dei contenitori Docker distribuiti nel servizio contenitore di Azure. Molte di queste considerazioni si applicano in genere contenitori tooDocker distribuiti in Azure o in altri ambienti. 

## <a name="image-security"></a>Sicurezza dell'immagine

I contenitori sono costituiti da immagini archiviati in una o più repository. Questi archivi possono appartenere toopublic o i registri di contenitore privato. Un esempio di registro pubblico è [Hub Docker](https://hub.docker.com/). Un esempio di un registro di sistema privato è hello [registro attendibile Docker](https://docs.docker.com/datacenter/dtr/2.0/), che può essere installato in locale o in un cloud privato virtuale. Sono inoltre disponibili servizi del registro contenitori privato basato su cloud che include [Registro contenitori di Azure](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Immagini pubbliche e private
In generale, come con qualsiasi pacchetto software pubblicato, un'immagine del contenitore pubblica non garantisce la sicurezza. Le immagini del contenitore sono costituite da più livelli di software e ogni livello di software potrebbe avere vulnerabilità. È origine hello toounderstand chiave dell'immagine contenitore hello, tra cui hello proprietario dell'immagine di hello (toodetermine se non è una fonte attendibile o non), hello livelli software da che è costituito e hello versioni del software. 

Ad esempio, se si passa toohello ufficiale [nginx repository](https://hub.docker.com/_/nginx/) nell'Hub Docker e passare toohello **tag** scheda, viene visualizzato con codifica a colori le vulnerabilità in ogni immagine. Ogni colore viene illustrata la vulnerabilità hello di un livello di software dell'immagine di hello. Per altre informazioni sulle vulnerabilità dell'analisi in Hub Docker, vedere [Informazioni ufficiali sulle repository in Hub Docker](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/).

![Immagini di nginx in Hub Docker](./media/container-service-security/docker-hub-nginx.png)

Le aziende attenzione eccessivamente sulla sicurezza e tooprotect autonomamente dagli attacchi di sicurezza deve archiviare e recuperare le immagini dal Registro di sistema privata, ad esempio del Registro di sistema di Azure contenitore o registro attendibile Docker. In aggiunta tooproviding un registro di sistema privato gestito, Registro di sistema contenitore di Azure supporta [l'autenticazione basata su entità di servizio](../articles/container-registry/container-registry-authentication.md) tramite Azure Active Directory per i flussi di autenticazione di base, incluso l'accesso basato sui ruoli per sola lettura, scrittura, mentre le autorizzazioni del proprietario.

### <a name="image-security-scanning"></a>Analisi della sicurezza dell'immagine

Anche quando si usa un registro di sistema privato, è un'immagine di toouse buona l'analisi di soluzioni per la convalida di sicurezza aggiuntive. Ogni livello del software in un'immagine contenitore è potenzialmente soggetto toovulnerabilities indipendente da altri livelli di immagine contenitore hello. Come sempre più società avviare la distribuzione i carichi di lavoro di produzione in base alle tecnologie dei contenitori, l'analisi di immagine diventa importante tooensure prevenzione di minacce alla protezione contro le organizzazioni. 

Sicurezza di monitoraggio e l'analisi di soluzioni, ad esempio [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) e [sicurezza azzurro](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), ad esempio, possibile tooscan utilizzate immagini contenitore in un registro di sistema privata e identificare potenziali vulnerabilità. È importante fornire profondità hello toounderstand di analisi che hello diverse soluzioni. Ad esempio, alcune soluzioni potrebbero eseguire dei controlli incrociati solo sui livelli dell'immagine rispetto alle vulnerabilità note. Queste soluzioni potrebbero non essere tooverify in grado di software di livello immagine mediante alcuni software di gestione del pacchetto. Altre soluzioni dispongono dell'integrazione di analisi più approfondite e possono rilevare vulnerabilità in qualsiasi software nel pacchetto.

### <a name="production-deployment-rules-and-audit"></a>Controllo e regole di distribuzione di produzione
Quando un'applicazione viene distribuita nell'ambiente di produzione, è essenziale tooset alcune regole tooensure che le immagini utilizzate negli ambienti di produzione sono protette e non contenere alcun vulnerabilità.

* Di norma, le immagini con vulnerabilità, anche secondaria, non dovrebbero essere consentite toorun in un ambiente di produzione. Inoltre, tutte le immagini distribuite nell'ambiente di produzione devono idealmente essere salvate in privato del Registro di sistema select tooa accessibile pochi. È inoltre importante tookeep numero di hello di tooensure piccole immagini di produzione che possono essere gestiti in modo efficace.

* Poiché si tratta di origine di hello toopinpoint disco del software da un'immagine contenitore disponibile pubblicamente, è un'immagine di toobuild buona conoscenza di origine tooensure di origine hello del livello di hello. Quando una superficie di vulnerabilità in un'immagine contenitore self-compilato, i clienti possono trovare una più rapida risoluzione tooa percorso. Con un'immagine pubblica, i clienti avrà bisogno di radice hello toofind toofix un'immagine pubblica, oppure per ottenere un'altra immagine protetta dal server di pubblicazione hello.

* Un'immagine accuratamente digitalizzata distribuita nell'ambiente di produzione non è garantita toobe backup toodate per durata hello dell'applicazione hello. Le vulnerabilità di sicurezza potrebbero essere riportate per i livelli dell'immagine di hello non sono stati noto in precedenza o sono stati introdotti dopo la distribuzione di produzione hello. Il controllo periodico di immagini distribuite nell'ambiente di produzione è necessario tooidentify immagini che non sono aggiornati o non sono state aggiornate in tempo. Una possibile usare le metodologie di distribuzione verde-blu e le immagini contenitore tooupdate di meccanismi di aggiornamento senza tempi di inattività in sequenza. L'analisi di immagine può essere eseguita con gli strumenti descritti nella precedente sezione hello. 

* Una pipeline di integrazione continua (CI) toobuild immagini e l'analisi di sicurezza integrata consente di mantenere protetti registri privati con immagini contenitore protetto. Hello analisi delle vulnerabilità incorporato in una soluzione di integrazione Continuata hello assicura che le immagini di superano tutti i test di hello vengono inserite privato del Registro di sistema di toohello dalla produzione a cui vengono distribuiti i carichi di lavoro. Un errore di pipeline CI assicura che vulnerabile immagini non vengono inserite nel Registro di hello privato usato per le distribuzioni di produzione del carico di lavoro. Inoltre consente di automatizzare l'analisi di sicurezza dell'immagine se è presente un numero significativo di immagini. Altrimenti il controllo manuale delle immagini per le vulnerabilità di sicurezza può risultare lungo e dettagliato e tendente all'errore.

## <a name="host-level-container-isolation"></a>Isolamento del contenitore a livello di host
Quando un cliente distribuisce le applicazioni del contenitore nelle risorse di Azure, queste vengono distribuite a livello di sottoscrizione nei gruppi di risorse e non sono multi-tenant. Ciò significa che se un cliente condivide una sottoscrizione con altri utenti, esistono limiti che possono essere compilati tra due distribuzioni di hello stessa sottoscrizione. Pertanto, la sicurezza a livello di contenitore non viene garantita. 

È inoltre toounderstand critici che contenitori condividano kernel hello e risorse di hello dell'host hello (che nel servizio contenitore di Azure è una macchina virtuale di Azure in un cluster). Pertanto, è necessario eseguire i contenitori in esecuzione nell'ambiente di produzione in modalità utente senza privilegi. Esecuzione di un contenitore con privilegi radice può compromettere l'intero ambiente hello. Con accesso a livello di radice in un contenitore, un pirata informatico può accedere privilegi radice completi toohello nell'host di hello. Inoltre, è importante toorun contenitori con i sistemi di file di sola lettura. Ciò impedisce a un utente che ha accesso toohello compromesso contenitore toowrite script dannosi toohello file system e accedere a file tooother. Analogamente, è importante toolimit hello risorse (ad esempio memoria, CPU e della larghezza di banda di rete) tooa contenitore. Questo consente di impedire agli hacker di occupare risorse e che esercitano le attività non valide, ad esempio carta di credito o di data mining bitcoin, che potrebbe impedire l'esecuzione in host hello o cluster altri contenitori.

## <a name="orchestrator-considerations"></a>Considerazioni sull'orchestrator

Ogni orchestrator disponibile nel servizio contenitore di Azure ha proprie considerazioni sulla sicurezza. Ad esempio, è consigliabile limitare nodi tooorchestrator con SSH accesso diretti nel servizio contenitore. È consigliabile utilizzare gli strumenti da riga di comando o dell'interfaccia utente di ogni orchestrator (ad esempio `kubectl` per Kubernetes) dell'ambiente contenitore hello toomanage senza l'accesso agli host hello. Per ulteriori informazioni, vedere [creare un cluster remoto tooa Kubernetes, controller di dominio o del sistema operativo o Docker Swarm](../articles/container-service/kubernetes/container-service-connect.md).

Per informazioni sulla protezione di orchestrator specifiche aggiuntive, vedere hello seguenti risorse:

* **Kubernetes**: [Security Best Practices for Kubernetes Deployment](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html) (Pratiche consigliate di sicurezza per la distribuzione di Kubernetes)

* **DC/OS**: [Securing Your Cluster](https://dcos.io/docs/1.8/administration/securing-your-cluster/) (Protezione del cluster)

* **Docker Swarm**: [Docker Security](https://www.docker.com/docker-security) (Sicurezza Docker)

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sulla sicurezza di architettura e contenitore Docker, vedere [tooContainer introduzione sicurezza](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Per informazioni sulla sicurezza della piattaforma Azure, vedere hello [Centro sicurezza di Azure](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
