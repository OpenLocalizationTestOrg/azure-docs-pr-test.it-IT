---
title: aaaLinux e Open Source di calcolo in Azure | Documenti Microsoft
description: Elenco relativo ad articoli sul computing Linux e open source in Azure, incluse informazioni di base sull'utilizzo di Linux, alcuni concetti fondamentali sull'esecuzione o il caricamento di immagini Linux in Azure e altri contenuti relativi a tecnologie e ottimizzazioni specifiche.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Computing Linux e open source in Azure
Trovare tutta la documentazione necessari toocreate e la gestione basata su Linux di macchine virtuali nel modello di distribuzione classica hello hello.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="get-started"></a>Attività iniziali
* [Introduzione a Linux in Azure](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Domande frequenti su Azure virtuali creati con il modello di distribuzione classica hello](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informazioni sulle immagini per le macchine virtuali](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Caricamento di un'immagine di distribuzione personalizzata](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json), include anche istruzioni per l'uso di una [distribuzione supportata da Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Accedere tooa VM Linux usando hello portale di Azure classico](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Configurare
* [Installare l'interfaccia della riga di comando di Azure](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Esercitazioni
* [Installare hello Stack LAMP in una macchina virtuale di Linux in Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Applicazione Web Ruby on Rails in una VM di Azure](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [Procedura: installare Apache Qpid Proton-C per AMQP e bus di servizio](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Database
* [Ottimizzare le prestazioni di MySQL in Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Cluster MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Esecuzione di Cassandra con Linux in Azure e accesso da Node.js](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Creare un cluster multimaster di MariaDB](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Impostare un applicazioni MPI toorun di Linux RDMA cluster](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Utilizzo di hello estensione della macchina virtuale Docker da hello interfaccia della riga di comando di Azure (Azure CLI)](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Utilizzo di hello estensione della macchina virtuale Docker da hello portale di Azure](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Come macchina di docker toouse in Azure](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [Procedura: cluster MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Procedura: Node.js e Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [Procedura: installare ed eseguire MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [Procedura: come usare CoreOS in Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Pianificazione
* [Linee guida sull'implementazione dei servizi di infrastruttura di Azure](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Selezione dei nomi utente per Linux](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Come tooconfigure un gruppo di disponibilità per le macchine virtuali nel modello di distribuzione classica hello](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Come tooSchedule manutenzione pianificata di macchine virtuali di Azure](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Gestire la disponibilità di hello delle macchine virtuali](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Manutenzione pianificata per macchine virtuali Linux in Azure](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Distribuzione
* [Creare una macchina virtuale personalizzata che esegue Linux](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hello nozioni fondamentali: acquisizione tooMake una VM Linux un modello](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informazioni per le distribuzioni non approvate](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>gestione
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Come tooReset una Password o SSH proprietà per Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Uso di privilegi root](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Risorse di Azure
* [Hello agente Linux di Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Estensioni VM e funzionalità di Azure](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Inserire i dati personalizzati in toouse una macchina virtuale con Cloud init](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Archiviazione
* [Collegamento tooa un disco dati VM Linux](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Scollegare un disco dati da una VM Linux](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Rete
* [Come tooset degli endpoint in una macchina virtuale classica in Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Risoluzione dei problemi
* [Risoluzione dei problemi di Secure Shell (SSH) connessioni tooa basati su Linux macchina virtuale di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Risolvere i problemi della distribuzione classica con la creazione di una nuova macchina virtuale Linux in Azure](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Risolvere i problemi della distribuzione classica con il riavvio e il ridimensionamento di una macchina virtuale Linux esistente in Azure](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>riferimento
* [Comandi dell'interfaccia della riga di comando di Azure in modalità Gestione servizi di Azure (asm)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [API REST di gestione dei servizi di Azure](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Collegamenti generali
Hello seguenti collegamenti è per i blog di Microsoft, pagine di Technet e siti esterni piuttosto che documentazione Azure.com come illustrato in precedenza. Come Azure sia hello world elaborazione open source fast-sposta le destinazioni, è quasi certi che hello seguendo i collegamenti vengono aggiornati, *Nonostante* fatti hello facciamo ammettiamo la migliore toocontinually argomenti più recenti di aggiungere e rimuovere quelli non aggiornati. Se sono state saltate uno,. prendano conoscere nei commenti hello o inviare un tooour richiesta pull [repository GitHub](https://github.com/Azure/azure-content/).

* [Esecuzione di ASP.NET 5 in Linux mediante i contenitori Docker](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [Come tooDeploy un'immagine di macchina virtuale CentOS da OpenLogic](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [Infrastruttura di aggiornamento SUSE](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server per la SAP Cloud Appliance Library](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Linux a disponibilità elevata in Azure in 12 passaggi](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Automatizzare il provisioning di Linux in Azure con l'interfaccia della riga di comandi di Azure, node.js, jhawk](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [GlusterFS in Azure](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [Esecuzione di FreeBSD in Azure](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [Distribuzione di FreeBSD con facilità](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [Distribuzione di un'immagine personalizzata di FreeBSD](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky AV per Linux File Server](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [8 database NoSql open source per Azure](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech): esperienze con CouchDb in Azure](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [Esecuzione di CouchDB-as-a-Service con node.js, CORS e Grunt](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Redis in Windows in hello servizio Cache Redis di Azure](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [Annuncio del provider di stato della sessione ASP.NET per la versione di anteprima di Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog: RavenHQ ora disponibile in hello Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Big Data
* [Installazione di Hadoop nelle macchine virtuali Linux di Azure](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>Database relazionale
* [Architettura a disponibilità elevata di MySQL in Microsoft Azure](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Installazione di Postgres con corosync, pg_bouncer utilizzando ILB](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>HPC (High Performance Computing) in Linux
* [Modelli della guida introduttiva: avviare un cluster SLURM](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (e [post di blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Modello di Guida introduttiva: creare un cluster HPC con nodi di calcolo di Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>DevOps, gestione e ottimizzazione
Hello world di devops, gestione e dell'ottimizzazione è molto ampio e modifica molto rapidamente, è opportuno valutare elenco hello di sotto di un punto di partenza.

* [Video in Macchine virtuali di Azure, uso di Chef, Puppet e Docker per la gestione di VM Linux](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [Guida di distribuzione di cluster tooautomated Kubernetes con CoreOS e Intessitura completare](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Visualizzatore Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Plug-in slave di Jenkins per Azure](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [Repository GitHub: plug-in di archiviazione di Jenkins per Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Terze parti: plug-in slave di Hudson per Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Terze parti: plug-in di archiviazione di Hudson per Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Video: che cos'è Chef e come funziona?](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Video: Modalità tooUse automazione di Azure con le macchine virtuali Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog: Modalità toodo Powershell DSC per Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: DSC per client Docker](https://github.com/anweiss/DockerClientDSC)
* [Plug-in di Packer per Azure](https://github.com/msopentech/packer-azure)

