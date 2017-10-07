---
title: aaaSet backup ibrida con HPC Pack del cluster in Azure | Documenti Microsoft
description: Informazioni su come Microsoft HPC Pack toouse e tooset Azure fino a un piccolo, ad alte prestazioni elaborazione (HPC) cluster ibrido
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Configurare un cluster ibrido HPC (high performance computing) con Microsoft HPC Pack e nodi di calcolo di Azure su richiesta
Utilizzare Microsoft HPC Pack 2012 R2 e Azure tooset di una piccolo, ibrido elaborazione a elevate prestazioni cluster (HPC). cluster Hello illustrati in questo articolo è costituito da un nodo head di HPC Pack locale e alcuni servizio cloud su richiesta in un Azure distribuire nodi di calcolo. È quindi possibile eseguire processi di calcolo nel cluster ibrido hello.

![Cluster HPC ibrido][Overview] 

Questa esercitazione viene illustrato un approccio, talvolta definita cluster "burst toohello cloud," applicazioni complesse toorun di toouse scalabile su richiesta delle risorse di Azure.

Questa esercitazione non presuppone che si abbia esperienza nell'ambito dei cluster di calcolo o di HPC Pack. È previsto toohelp solo distribuire un cluster di calcolo ibrido rapidamente a scopo dimostrativo. Per considerazioni e passaggi toodeploy ibrida con HPC Pack del cluster su larga scala maggiore in un ambiente di produzione o toouse HPC Pack 2016, vedere hello [Guida dettagliata](http://go.microsoft.com/fwlink/p/?LinkID=200493). Per altri scenari con HPC Pack, inclusa la distribuzione automatica di cluster nelle macchine virtuali di Azure, vedere [Opzioni per creare e gestire un cluster HPC in Azure con Microsoft HPC Pack](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Prerequisiti
* **Sottoscrizione di Azure** : se non è disponibile una sottoscrizione di Azure, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.
* **Un computer locale che esegue Windows Server 2012 R2 o Windows Server 2012** -utilizzare questo computer come nodo head di hello del cluster HPC hello. Se Windows Server non è già in esecuzione, è possibile scaricare e installare una [versione di valutazione](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * computer Hello deve essere tooan aggiunti a un dominio di Active Directory. Per scopi di test, è possibile configurare i computer del nodo head hello come controller di dominio. tooadd hello ruolo server Servizi di dominio Active Directory e innalzare hello nodo head computer come controller di dominio, vedere la documentazione di hello per Windows Server.
  * toosupport HPC Pack, hello del sistema operativo deve essere installato in una di queste lingue: inglese, giapponese o cinese (semplificato).
  * Verificare che siano installati gli aggiornamenti importanti.
* **HPC Pack 2012 R2** - [scaricare](http://go.microsoft.com/fwlink/p/?linkid=328024) pacchetto di installazione hello hello ultima versione disponibile gratuitamente e copia hello file toohello computer nodo head. Scegliere i file di installazione in hello stessa lingua di installazione di Windows Server.

    >[!NOTE]
    > Se si desidera toouse HPC Pack 2016 invece di HPC Pack 2012 R2, è necessaria una configurazione aggiuntiva. Vedere hello [Guida dettagliata](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Account di dominio** -questo account deve essere configurato con le autorizzazioni di amministratore locale nel nodo head di hello tooinstall HPC Pack.
* **La connettività TCP sulla porta 443** da tooAzure nodo head hello.

## <a name="install-hpc-pack-on-hello-head-node"></a>Installare HPC Pack nel nodo head hello
Installare prima Microsoft HPC Pack in un computer locale che esegue Windows Server. Il computer diventa nodo head di hello del cluster di hello.

1. Accedere nel nodo head toohello utilizzando un account di dominio che dispone delle autorizzazioni di amministratore locale.

2. Avviare Installazione guidata di HPC Pack hello, eseguire Setup.exe dal file di installazione di HPC Pack hello.

3. In hello **il programma di installazione di HPC Pack 2012 R2** schermata, fare clic su **nuova installazione o aggiungere una nuova installazione esistente di funzionalità tooan**.

    ![Installazione di HPC Pack 2012][install_hpc1]

4. In hello **pagina Contratto di Microsoft Software utente**, fare clic su **Avanti**.

5. In hello **Selezione tipo di installazione** pagina, fare clic su **creare un nuovo cluster HPC creando un nodo head**, quindi fare clic su **Avanti**.

6. Creazione guidata di Hello esegue diversi test pre-installazione. Fare clic su **Avanti** su hello **regole di installazione** se tutti i test superati. In caso contrario, esaminare le informazioni di hello fornite e apportare le modifiche necessarie nell'ambiente in uso. Quindi eseguire nuovamente i test di hello o se necessario inizio hello nuovamente Installazione guidata.
7. In hello **configurazione DB HPC** assicurarsi **nodo Head** è selezionata per tutti i database HPC e quindi fare clic su **Avanti**. 

    ![Configurazione di database][install_hpc4]

8. Accettare le selezioni predefinite nelle pagine rimanenti di hello della procedura guidata hello. In hello **installare i componenti richiesti** pagina, fare clic su **installare**.
   
    ![Installa][install_hpc6]

9. Al termine dell'installazione di hello, deselezionare **avviare HPC Cluster Manager** e quindi fare clic su **fine**. HPC Cluster Manager viene avviato in un passaggio successivo.
   
    ![Finish][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Preparare hello sottoscrizione di Azure
Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com) con la sottoscrizione di Azure. Dopo aver completato questi passaggi, è possibile distribuire i nodi di Azure dal nodo head di hello in locale. 
  
  > [!NOTE]
  > Prendere anche nota dell'ID sottoscrizione di Azure, che sarà necessario in seguito. Trovare l'ID di hello in **sottoscrizioni** nel portale di hello.
  > 

### <a name="upload-hello-default-management-certificate"></a>Caricare il certificato di gestione predefinito hello
HPC Pack consente di installare un certificato autofirmato nel nodo head hello, chiamato hello predefinito Microsoft HPC Azure Management certificato, che è possibile caricare un certificato di gestione di Azure. Questo certificato è stato specificato per il test e le distribuzioni di prova toosecure hello concatenate hello nodo head e Azure.

1. Dal computer del nodo head hello, accedi toohello [portale di Azure](https://portal.azure.com).

2. Fare clic su **Sottoscrizioni** > *nome_della_sottoscrizione*.

3. Fare clic su **Certificati di gestione** > **Carica**. 4. Passare nel nodo head di hello per hello file c:\Programmi\Microsoft HPC Pack 2012\Bin\hpccert.cer. Fare quindi clic su **Carica**.

   
Hello **predefinito HPC Azure Management** certificato visualizzato nell'elenco di hello dei certificati di gestione.

### <a name="create-an-azure-cloud-service"></a>Creazione di un servizio cloud di Azure
> [!NOTE]
> Per prestazioni ottimali, creare account di archiviazione hello (in un passaggio successivo) e di servizio cloud hello in hello stessa area geografica.
> 
> 

1. Nel portale di hello, fare clic su **(classico) di servizi Cloud** > **+ Aggiungi**.

2.  Digitare un nome DNS per il servizio di hello, scegliere un gruppo di risorse e un percorso e quindi fare clic su **crea**.


### <a name="create-an-azure-storage-account"></a>Creare un account di archiviazione di Azure
1. Nel portale di hello, fare clic su **gli account di archiviazione (classico)** > **+ Aggiungi**.

2. Digitare un nome per l'account di hello e selezionare hello **classico** modello di distribuzione.

3. Scegliere un gruppo di risorse e mantenere i valori predefiniti per le altre impostazioni. Fare quindi clic su **Crea**.

## <a name="configure-hello-head-node"></a>Configurare un nodo head hello
toouse toodeploy HPC Cluster Manager nodi di Azure e i processi toosubmit, eseguire innanzitutto alcuni passaggi di configurazione del cluster richiesto.

1. Nel nodo head hello, avviare Gestione Cluster HPC. Se hello **Seleziona nodo Head** viene visualizzata la finestra di dialogo, fare clic su **Computer locale**. Hello **elenco attività di distribuzione** viene visualizzato.

2. In **Required deployment tasks** (Attività di distribuzione necessarie) fare clic su **Configure your network** (Configurare la rete).
   
    ![Configurazione della rete][config_hpc2]

3. Nella configurazione guidata rete hello, selezionare **tutti i nodi solo in una rete aziendale** (topologia 5). Questa configurazione di rete è hello più semplice per scopi dimostrativi.
   
    ![Topologia 5][config_hpc3]
   
4. Fare clic su **Avanti** i valori predefiniti di tooaccept nel hello restanti pagine della procedura guidata hello. Quindi, nella hello **revisione** scheda, fare clic su **configura** configurazione di rete toocomplete hello.

5. In hello **elenco attività di distribuzione**, fare clic su **fornire le credenziali di installazione**.

6. In hello **credenziali per l'installazione** nella finestra di dialogo digitare hello le credenziali dell'account di dominio hello utilizzato tooinstall HPC Pack. Fare quindi clic su **OK**. 
   
    ![Installation Credentials][config_hpc6]
   
7. In hello **elenco attività di distribuzione**, fare clic su **configurare hello denominazione di nuovi nodi**.

8. In hello **specificare serie di denominazione nodo** finestra di dialogo casella, accettare il valore predefinito hello denominazione serie e fare clic su **OK**. Completare questo passaggio, anche se hello nodi di Azure che è aggiungere in questa esercitazione vengono denominati automaticamente.
   
    ![Denominazione dei nodi][config_hpc8]
   
9. In hello **elenco attività di distribuzione**, fare clic su **creare un modello di nodo**. Più avanti nell'esercitazione di hello, utilizzare cluster toohello di hello nodo modello tooadd nodi di Azure.

10. In Creazione guidata modello di nodo di hello, eseguire hello seguenti:
    
    a. In hello **Scegli tipo di modello di nodo** pagina, fare clic su **il modello di nodo di Windows Azure**, quindi fare clic su **Avanti**.
    
    ![Modello di nodo][config_hpc10]
    
    b. Fare clic su **Avanti** nome del modello predefinito di tooaccept hello.
    
    c. In hello **forniscono informazioni sulla sottoscrizione** pagina, immettere l'ID sottoscrizione di Azure (disponibile nelle informazioni sull'account di Azure). In **Certificato di gestione**cercare **Default Microsoft HPC Azure Management**. Quindi fare clic su **Next**.
    
    ![Modello di nodo][config_hpc12]
    
    d. In hello **forniscono informazioni sul servizio** pagina, servizio cloud selezionare hello e account di archiviazione hello creato nel passaggio precedente. Quindi fare clic su **Next**.
    
    ![Modello di nodo][config_hpc13]
    
    e. Fare clic su **Avanti** i valori predefiniti di tooaccept nel hello restanti pagine della procedura guidata hello. Quindi, nella hello **revisione** scheda, fare clic su **crea** modello di nodo toocreate hello.
    
    > [!NOTE]
    > Per impostazione predefinita, hello Azure nodo modello include le impostazioni per è toostart (provisioning) e i nodi di hello stop manualmente, utilizzando Gestione Cluster HPC. È possibile configurare una pianificazione toostart e arrestare hello automaticamente i nodi di Azure.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Aggiungere nodi di Azure toohello cluster
Utilizzare cluster toohello di hello nodo modello tooadd nodi di Azure. Aggiunta di cluster di hello nodi toohello archivia le informazioni di configurazione in modo che è possibile avviare (provisioning) usarle in qualsiasi momento nel servizio cloud hello. Dopo che le istanze di hello sono in esecuzione nel servizio cloud hello, ottiene addebitata solo la sottoscrizione per i nodi di Azure.

Seguire questi passaggi tooadd due piccole nodi.

1. In HPC Cluster Manager (Gestione cluster HPC) fare clic su **Node Management** (Gestione nodi), denominato **Resource Management** (Gestione risorse) nelle versioni correnti di HPC Pack, > **Add Node** (Aggiungi nodo).
   
    ![Actions][add_node1]

2. In hello Aggiunta guidata nodi in hello **Selezione metodo di distribuzione** pagina, fare clic su **nodi di Azure aggiungere**, quindi fare clic su **Avanti**.
   
    ![Aggiunta di un nodo di Azure][add_node1_1]

3. In hello **specificare nuovi nodi** pagina, il modello di nodo di Azure selezionare hello creato in precedenza (chiamato per impostazione predefinita **modello AzureNode predefinito**). Specificare quindi **2** nodi di dimensioni **Small** e quindi fare clic su **Next** (Avanti).
   
    ![Specifica dei nodi][add_node2]
   
4. In hello **completamento hello Aggiunta guidata nodi** pagina, fare clic su **fine**.
    
     In Gestione cluster HPC saranno ora presenti due nodi di Azure denominati **AzureCN-0001** e **AzureCN-0002**. Sono entrambi hello **non distribuiti** stato.
   
    ![Nodi aggiunti][add_node3]

## <a name="start-hello-azure-nodes"></a>Avviare hello nodi di Azure
Quando si desidera toouse hello le risorse cluster in Azure, utilizzare Gestione Cluster HPC toostart (provisioning) hello nodi di Azure e connetterle nuovamente.

1. In Gestione Cluster HPC, fare clic su **nodo Gestione** (chiamato **la gestione delle risorse** nelle versioni correnti di HPC Pack), e selezionare hello nodi di Azure.

2. Fare clic su **Start** (Avvia) e quindi su **OK**.
   
   ![Avvio dei nodi][add_node4]
   
    nodi Hello transizione toohello **Provisioning** stato. Provisioning hello tootrack log stato provisioning hello di visualizzazione.
   
    ![Provisioning dei nodi][add_node6]

3. Dopo alcuni minuti, hello nodi di Azure completare il provisioning e sono in hello **Offline** stato. In questo stato, le istanze del ruolo hello sono in esecuzione ma non ancora accettano i processi cluster.

4. tooconfirm che hello istanze del ruolo sono in esecuzione, hello portale di Azure, fare clic su **servizi Cloud (classico)** > *your_cloud_service_name*.
   
   Dovrebbe essere due **HpcWorkerRole** istanze (nodi) in esecuzione nel servizio hello. HPC Pack distribuisce automaticamente anche due **HpcProxy** istanze comunicazione toohandle (dimensione media) tra Azure e hello del nodo head.

   ![Esecuzione delle istanze][view_instances1]

5. toorun online i nodi di Azure di hello toobring cluster processi, hello selezionare nodi, pulsante destro del mouse e quindi fare clic su **in linea**.
   
    ![Nodi offline][add_node7]
   
    Gestione Cluster HPC indica che i nodi di hello in hello **Online** stato.

## <a name="run-a-command-across-hello-cluster"></a>Eseguire un comando cluster hello
installazione di hello toocheck, utilizzare hello HPC Pack **clusrun** comando toorun un comando o l'applicazione in uno o più nodi del cluster. Un esempio semplice, utilizzare **clusrun** configurazione IP di hello tooget di hello nodi di Azure.

1. Nel nodo head hello, aprire un prompt dei comandi come amministratore.

2. Digitare hello comando seguente:
   
    `clusrun /nodes:azurecn* ipconfig`

3. Se richiesto, immettere la password dell'amministratore del cluster. Dovrebbe essere simile toohello seguenti di output del comando.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>Esecuzione di un processo di test
Inviare un processo di test in esecuzione su cluster ibrido hello. Questo esempio è un processo parametrico di organizzazione semplice, ovvero un tipo di calcolo intrinsecamente parallelo. Questo esempio viene eseguito sottoattività aggiungere tooitself un integer con hello **set /a** comando. Tutti i nodi nel cluster hello hello contribuiscono toofinishing hello sottoattività per numeri interi da 1 too100.

1. In HPC Cluster Manager (Gestione cluster HPC) fare clic su **Job Management** (Gestione processi) > **New Parametric Sweep Job** (Nuovo processo parametrico di organizzazione).
   
    ![Nuovo processo][test_job1]

2. In hello **nuovo processo di Sweep parametrico** della finestra di dialogo **riga di comando**, tipo `set /a *+*` (sovrascrivendo hello riga di comando predefinito visualizzato). Lasciare i valori predefiniti per hello rimanenti impostazioni e quindi fare clic su **Invia** processo hello toosubmit.
   
    ![Sweep parametrico][param_sweep1]

3. Termine del processo di hello, fare doppio clic su hello **attività durante lo Sweep My** processo.

4. Fare clic su **Visualizza attività**, quindi fare clic su un output di hello calcolato tooview sottoattività di tale sottoattività.
   
    ![Risultati delle attività][view_job361]

5. Fare clic su quale nodo eseguita calcolo hello tale sottoattività, toosee **allocata nodi**. (il nome del nodo nel proprio cluster potrebbe essere diverso).
   
    ![Risultati delle attività][view_job362]

## <a name="stop-hello-azure-nodes"></a>Arrestare hello nodi di Azure
Dopo aver tentato cluster hello, arrestare la account tooyour hello nodi di Azure tooavoid costi non necessari. Questo passaggio Arresta servizio cloud hello e rimuove le istanze del ruolo Azure hello.

1. In HPC Cluster Manager (Gestione cluster HPC) selezionare entrambi i nodi di Azure in **Node Management** (Gestione Nodi), denominato **Resource Management** (Gestione risorse) in versioni precedenti di HPC Pack. Fare quindi clic su **Stop** (Arresta).
   
    ![Interruzione dei nodi][stop_node1]

2. In hello **nodi di Azure Arresta** la finestra di dialogo, fare clic su **arrestare**. 
   
3. nodi Hello transizione toohello **arresto** stato. Dopo alcuni minuti, HPC Cluster Manager mostra che sono nodi hello **non distribuiti**.
   
    ![Nodi non distribuiti][stop_node4]

4. tooconfirm le istanze del ruolo hello non è più in esecuzione in Azure, in hello Azure fare clic su portale, **(classico) di servizi Cloud** > *your_cloud_service_name*. Nessuna istanza viene distribuita nell'ambiente di produzione hello. 
   
    Esercitazione hello è stata completata.

## <a name="next-steps"></a>Passaggi successivi
* Esplorare la documentazione di hello per [HPC Pack](https://technet.microsoft.com/library/cc514029).
* vedere tooset di una distribuzione di cluster HPC Pack su larga scala maggiore, ibrida [potenziamento tooAzure istanze del ruolo di lavoro con Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Per altri modi toocreate un cluster HPC Pack in Azure, incluse utilizzando i modelli di gestione risorse di Azure, vedere [opzioni cluster HPC con Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
