---
title: aaaDeploy Deis 3 nodi cluster | Documenti Microsoft
description: Questo articolo viene descritto come toocreate 3 nodi Deis cluster in Azure utilizzando un modello di gestione risorse di Azure
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Distribuire e configurare un cluster Deis a 3 nodi in Azure
In questo articolo viene illustrato il provisioning di un cluster [Deis](http://deis.io/) su Azure. Copre tutti i passaggi di hello creazione hello toodeploying di certificati necessari e la scalabilità di un campione **passare** applicazione in cluster appena sottoposti a provisioning hello.

Hello diagramma seguente mostra hello architettura del sistema hello distribuito. Un amministratore di sistema gestisce hello cluster mediante Deis strumenti, ad esempio **deis** e **deisctl**. Le connessioni vengono stabilite tramite un servizio di bilanciamento del carico di Azure, che inoltra i nodi nel cluster hello tooone connessioni hello del membro hello. Hello ai client di accedere alle applicazioni tramite anche bilanciamento del carico hello. In questo caso, bilanciamento del carico hello inoltra hello traffico tooa Deis reticolato router, che routs ulteriormente i contenitori di Docker toocorresponding traffico ospitati nel cluster hello.

  ![Diagramma dell'architettura del cluster Deis distribuito](./media/deis-cluster/architecture-overview.png)

In ordine toorun tramite hello alla procedura seguente, è necessario:

* Una sottoscrizione di Azure attiva. Se non si dispone di una sottoscrizione, è possibile ottenere una versione di valutazione gratuita su [azure.com](https://azure.microsoft.com/).
* Un lavoro o i gruppi di risorse di Azure toouse id dell'istituto di istruzione. Se si dispone di un account personale e accedere con un id Microsoft, è necessario troppo[creare un id di lavoro da quello personale](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Uno - a seconda del sistema operativo client - hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) o hello [CLI di Azure per Mac, Linux e Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL è toogenerate utilizzati certificati hello.
* Un client Git, come [Git Bash](https://git-scm.com/).
* applicazione di esempio hello tootest, è inoltre necessario un server DNS. È possibile utilizzare tutti i server o i servizi DNS che supportano i record A con carattere jolly.
* Un computer toorun Deis gli strumenti client. È possibile utilizzare una macchina locale o una macchina virtuale. È possibile eseguire questi strumenti in quasi tutte le distribuzioni di Linux, ma le istruzioni seguenti hello utilizzano Ubuntu.

## <a name="provision-hello-cluster"></a>Cluster hello effettuare il provisioning
In questa sezione, si userà un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modello dal repository di origine aprire hello [modelli di azure-Guida introduttiva](https://github.com/Azure/azure-quickstart-templates). In primo luogo, si copierà modello hello verso il basso. Quindi, verrà creata una nuova coppia di chiavi SSH per l'autenticazione e verrà configurato un nuovo identificatore per il cluster. E, infine, si utilizzerà script della Shell hello o cluster di hello PowerShell script tooprovision hello.

1. Repository di hello clone: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Cartella modello toohello passare:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Creare una nuova coppia di chiavi SSH utilizzando ssh-keygen:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Generare un certificato utilizzando hello sopra la chiave privata:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Andare troppo[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nuovo token di cluster, che ha un aspetto simile:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Ogni cluster CoreOS deve toohave un token univoco da questo servizio gratuito. Vedere [Documentazione CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) per ulteriori dettagli.
6. Modificare hello **cloud config.yaml** file tooreplace hello esistente **individuazione** token con il nuovo token di hello:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Modificare hello **azuredeploy parameters.json** file: il certificato aprire hello creato nel passaggio 4 in un editor di testo. Copiare tutto il testo tra `----BEGIN CERTIFICATE-----` e `-----END CERTIFICATE-----` in hello **sshKeyData** parametro (sarà necessario tooremove tutti i caratteri di nuova riga).
8. Modificare hello **newStorageAccountName** parametro. Si tratta di account di archiviazione hello per i dischi del sistema operativo VM. Questo nome dell'account è univoco globale toobe.
9. Modificare hello **publicDomainName** parametro. Che diventerà parte del nome DNS hello associato IP pubblico del servizio di bilanciamento carico di hello. Hello FQDN finale avrà il formato di hello di *[valore di questo parametro]*. *[region]* . cloudapp.azure.com. Ad esempio, se si specifica il nome di hello come deishbai32 e gruppo di risorse hello area Stati Uniti occidentali toohello distribuito, quindi hello finale bilanciamento del carico FQDN tooyour sarà deishbai32.westus.cloudapp.azure.com.
10. Salvare il file di parametro hello. E quindi è possibile eseguire il provisioning di cluster hello tramite Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    o l’interfaccia della riga di comando di Azure:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Una volta che il gruppo di risorse hello viene eseguito il provisioning, è possibile visualizzare tutte le risorse hello hello gruppo nel portale di Azure classico. Come illustrato nella seguente schermata hello hello gruppo di risorse contiene una rete virtuale con tre macchine virtuali, che vengono unite toohello stesso set di disponibilità. gruppo di Hello contiene inoltre un bilanciamento del carico, con un indirizzo IP pubblico associato.
    
    ![gruppo di risorse di provisioning di Hello nel portale di Azure classico](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Installare il client hello
È necessario **deisctl** toocontrol il Deis cluster. Sebbene deisctl viene installato automaticamente in tutti i nodi del cluster di hello, è un deisctl toouse buona norma in un computer di amministrazione separato. Inoltre, poiché tutti i nodi sono configurati con solo gli indirizzi IP privati, è necessario toouse SSH tunneling tramite bilanciamento del carico di hello, che ha un indirizzo IP pubblico, le macchine nodo toohello tooconnect. Hello seguenti sono hello passaggi di configurazione di deisctl in una macchina virtuale o un Ubuntu fisico separato.

1. Installare deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Aggiungere l'agente toossh chiave privata:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Configurare deisctl:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

modello di Hello definisce le regole NAT in ingresso che eseguono il mapping 2223 tooinstance 1, tooinstance 2224 2 e 2225 tooinstance 3. Questo fornisce la ridondanza per lo strumento deisctl hello. È possibile esaminare queste regole sul portale di Azure classico:

![Regole NAT nel servizio di bilanciamento del carico hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Modello hello supporta attualmente solo 3 nodi cluster. Ciò a causa di un limite nella definizione delle regole NAT del modello di Gestione risorse di Azure, che non supporta la sintassi del ciclo.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Installare e avviare hello Deis piattaforma
È ora possibile utilizzare deisctl tooinstall e avviare hello Deis piattaforma:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Piattaforma hello iniziale richiede un certo tempo (fino a 10 minuti). In particolare, l'avvio del servizio generatore hello può richiedere molto tempo. E può talvolta richiedere alcuni tentativi toosucceed: se l'operazione di hello sembra toohang, provare a digitare `ctrl+c` toobreak esecuzione del comando hello e riprovare.
> 
> 

È possibile utilizzare `deisctl list` tooverify se tutti i servizi sono in esecuzione:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Congratulazioni. Ora si dispone di un cluster Deis in esecuzione su Azure. Successivamente, consente di distribuire un esempio Go cluster hello toosee di applicazione in azione.

## <a name="deploy-and-scale-a-hello-world-application"></a>Distribuzione e scalabilità di un'applicazione Hello World
Hello passaggi seguenti viene illustrato come toodeploy "Hello World" Vai cluster toohello dell'applicazione. passaggi di Hello dipendono [Deis documentazione](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Per hello routing mesh toowork correttamente, è necessario un record con caratteri jolly A toohave per il dominio che punta toohello indirizzo IP pubblico del servizio di bilanciamento del carico hello. Hello cattura di schermata seguente mostra hello un record per la registrazione di un dominio di esempio su GoDaddy:
   
    ![Record A GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Per installare deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Creare una nuova chiave SSH e quindi aggiungere hello tooGitHub di chiave pubblica (Naturalmente, è inoltre possibile riutilizzare le chiavi esistenti). toocreate una coppia di chiavi SSH nuovo, utilizzare:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Aggiungere id_rsa.pub o chiave pubblica di hello di propria scelta, tooGitHub. È possibile farlo tramite hello aggiungere SSH pulsante chiave nella schermata Configurazione chiavi SSH:
   
   ![Chiave GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Per registrare un nuovo utente:
   
        deis register http://deis.[your domain]
   <p />
6. Aggiungere la chiave SSH hello:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Creare un'applicazione.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.push git Hello attiverà toobe di immagini Docker compilato e distribuito, che potrebbe richiedere alcuni minuti. L'esperienza, in alcuni casi, potrebbe bloccarsi passaggio 10 (repository di tooprivate Pushing immagine). In questo caso, è possibile arrestare il processo di hello, remove hello applicazione utilizzando ' deis App:: destroy <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nome hello dell'applicazione. Se tutto funziona, dovrebbe essere simile alla seguente hello alla fine di hello dell'output dei comandi:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Verificare se un'applicazione hello funzioni:
   
        curl -S http://[your application name].[your domain]
   Dovrebbe essere visualizzato:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Istanze too3 dell'applicazione hello scala:
    
        deis scale cmd=3
    <p />
11. Facoltativamente, è possibile utilizzare deis info tooexamine dettagli dell'applicazione. Hello gli output seguenti sono la distribuzione dell'applicazione:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è descritta in dettaglio tutti i tooprovision passaggi hello Deis un nuovo cluster in Azure utilizzando un modello di gestione risorse di Azure. il modello di Hello supporta ridondanza in strumenti di connessioni, nonché il bilanciamento del carico per le applicazioni distribuite. modello Hello consente anche di evitare l'utilizzo di indirizzi IP pubblici su nodi di membro, che consente di risparmiare preziose risorse IP pubbliche e offre un ambiente più sicuro toohost applicazioni. toolearn informazioni, vedere hello seguenti articoli:

[Panoramica di Azure Resource Manager][resource-group-overview]  
[Come toouse hello CLI di Azure][azure-command-line-tools]  
[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager] (Uso di Azure PowerShell con Azure Resource Manager)  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
