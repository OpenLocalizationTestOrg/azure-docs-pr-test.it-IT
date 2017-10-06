---
title: aaaOverview delle macchine virtuali Linux in Azure | Documenti Microsoft
description: Descrive i servizi di calcolo, archiviazione e rete di Azure con macchine virtuali Linux.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure e Linux
Microsoft Azure è una raccolta in continua crescita di servizi cloud pubblici integrati, che includono analisi, macchine virtuali, database, dispositivi mobili, rete, archiviazione, servizi cloud e Web&mdash;, ideali per l'hosting delle soluzioni.  Microsoft Azure offre una piattaforma scalabile di elaborazione che consente la retribuzione di tooonly per l'utilizzo, quando si desidera che - senza tooinvest in hardware locale.  Azure è pronto, quando si ha tooscale soluzioni di backup e out toowhatever scala necessari esigenze hello tooservice dei propri client.

Se si ha familiarità con hello diverse funzionalità di Amazon AWS, è possibile esaminare hello Azure vs AWS [documento di definizione di mapping](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/).

## <a name="regions"></a>Regioni
Risorse di Microsoft Azure vengono distribuite tra più aree geografiche in tutto il mondo hello.  Una "area" rappresenta più data center in una singola area geografica.  Abbiamo 34 aree in genere disponibili in tutto il mondo hello con un aree 4 aggiuntivi annunciato. Poiché stiamo continuando tooexpand il code coverage globale - mantiene che un elenco aggiornato nuovi ed esistenti annunciato aree.

* [Aree di Azure](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Disponibilità
È stata annunciata che una settore iniziali istanza singola macchina virtuale di contratto di servizio pari al 99,9% fornito che è distribuire hello macchina virtuale con archiviazione premium per tutti i dischi.  Affinché il tooqualify di distribuzione per il 99,95% di standard VM Service Level Agreement, è comunque necessario toodeploy due o più macchine virtuali in esecuzione il carico di lavoro all'interno di un set di disponibilità. In questo modo le macchine virtuali vengono distribuite tra più domini di errore nei centri dati Microsoft e anche in host con finestre di manutenzione diverse. Hello completo [SLA di Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) illustra hello garantita la disponibilità di Azure nel suo complesso.

## <a name="managed-disks"></a>Managed Disks

Creazione di account e per la gestione in background hello gli handle di archiviazione di Azure e assicura che non si dispone tooworry sui limiti di scalabilità hello hello dell'account di archiviazione di dischi gestiti di. È sufficiente specificare dimensioni del disco hello e livello di prestazioni hello (Standard o Premium) e Azure crea e gestisce disco hello per l'utente. Anche se si aggiungono dischi o applicare la scalabilità verticale hello VM, non è tooworry sull'archiviazione hello in uso. Se si creano nuove macchine virtuali, [utilizzare hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o hello toocreate portale Azure le macchine virtuali con dischi gestiti del sistema operativo e dati. Se si dispone di macchine virtuali con dischi non gestiti, è possibile [convertire toobe le macchine virtuali eseguito con i dischi gestiti](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

È anche possibile gestire immagini personalizzate in un account di archiviazione per ogni area di Azure e usarli toocreate centinaia di macchine virtuali in hello stessa sottoscrizione. Per ulteriori informazioni sui dischi gestiti, vedere hello [Panoramica di dischi gestiti](../windows/managed-disks-overview.md).

## <a name="azure-virtual-machines--instances"></a>Macchine virtuali di Azure e istanze
Microsoft Azure supporta l'esecuzione di numerose distribuzioni comuni di Linux fornite e gestite da diversi partner.  Sono disponibili le distribuzioni, ad esempio Red Hat Enterprise, CentOS, Debian, Ubuntu, CoreOS, RancherOS, FreeBSD e ulteriori hello Azure Marketplace. Attivamente Collaboriamo con vari Linux community tooadd anche altre versioni toohello [Linux Distros approvate per Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) elenco.

Se la distribuzione di Linux preferito di scelta non è attualmente presente nella raccolta di hello, è possibile "Bring proprio Linux" macchina virtuale con [creazione e caricamento di un VHD Linux in Azure](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Macchine virtuali di Azure consentono di toodeploy un'ampia gamma di soluzioni di elaborazione in modo flessibile. È possibile distribuire praticamente qualsiasi carico di lavoro e in qualsiasi lingua in quasi tutti i sistemi operativi come Windows, Linux oppure crearne uno personalizzato da uno dei nostri partner in costante aumento. Se ancora non si trova ciò che si sta cercando,  è anche possibile usare immagini personalizzate dall'ambiente locale.

## <a name="vm-sizes"></a>Dimensioni delle VM
Quando si distribuisce una macchina virtuale in Azure, si sta tooselect una dimensione di macchina virtuale all'interno di uno dei nostri serie le dimensioni di carico di lavoro tooyour adatto. dimensioni Hello influisce anche sulle hello potenza di elaborazione, memoria e la capacità di archiviazione della macchina virtuale hello. Verrà addebitato in base all'ammontare hello di hello ora macchina virtuale è in esecuzione e utilizzano le risorse allocate. Elenco completo delle [dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Ecco alcune linee guida fondamentali per la selezione delle dimensioni di una VM da una delle serie disponibili (A, D, DS, G e GS).
* Le VM serie A sono VM di fascia bassa con prezzi vantaggiosi per carichi di lavoro leggeri e scenari di sviluppo e test. Sono ampiamente disponibile in tutte le aree e possono connettersi e utilizzare tutte le macchine toovirtual disponibili risorse standard.
* Le dimensioni della serie A (A8 - A11) sono speciali configurazioni a elevato utilizzo di calcolo adatte per applicazioni di cluster di calcolo ad alte prestazioni.
* Macchine virtuali serie D sono progettate toorun applicazioni che richiedono maggiore potenza di calcolo e le prestazioni del disco temporaneo. Macchine virtuali serie D offrono processori più veloci, un rapporto memoria-core superiore e un'unità SSD (unità SSD) per il disco temporaneo hello.
* Dv2-series, è più recente della nostra serie D-hello, una CPU più potente funzionalità. Hello Dv2 serie CPU è circa 35% più rapida rispetto hello serie D CPU. Si basa su hello ultima generazione 2,4 GHz Intel Xeon® E5-2673 v3 processore (Haskell) e con hello Intel turbina Boost tecnologia 2.0, possono aumentare fino too3.2 GHz. Hello Dv2 serie è hello stesse configurazioni di memoria e disco come hello serie D.
* Macchine virtuali serie G offrono hello maggior quantità di memoria ed eseguiti su host che dispongono di processori della famiglia Intel Xeon E5 V3.

Nota: Serie DS e GS-series VM necessario accesso tooPremium archiviazione, l'unità SSD archiviazione a prestazioni elevate, bassa latenza per carichi di lavoro con utilizzo intensivo dei / o di backup. L'archiviazione Premium è disponibile solo in determinate aree geografiche. Per informazioni dettagliate, vedere:

* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>Automazione
tooachieve corretto DevOps determinate impostazioni cultura, tutta l'infrastruttura deve contenere codice.  Quando tutti hello infrastruttura risiede nel codice può essere facilmente ricreati (Phoenix server).  Azure funziona con tutti automazione principali di hello tooling come Ansible, Chef, SaltStack e Puppet.  Azure dispone di strumenti di automazione propri:

* [Modelli di Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure sta implementando il supporto per [cloud-init](http://cloud-init.io/) nella maggior parte delle implementazioni Linux che lo supportano.  Attualmente le VM Ubuntu di Canonical vengono distribuite con cloud-init abilitato per impostazione predefinita.  Fedora supportano cloud init, tuttavia hello Azure, in CentOS e Red Hat RHEL gestite da RedHat immagini non sono installato cloud-init.  toouse cloud-durante l'inizializzazione di una famiglia di RedHat del sistema operativo, è necessario creare un'immagine personalizzata con cloud-init installato.

* [Uso di cloud-init nelle macchine virtuali Linux di Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>Quote
Ogni sottoscrizione Azure dispone di limiti di quota predefiniti che potrebbe influire sulla distribuzione di hello di un numero elevato di macchine virtuali per il progetto. il limite corrente di Hello su una base per ogni sottoscrizione è 20 macchine virtuali per ogni area.  È possibile aumentare i limiti di quota in modo semplice e rapido creando un ticket di supporto in cui si richiede appunto un aumento del limite.  Per altre informazioni sui limiti di quota:

* [Limiti del servizio di sottoscrizione di Azure](../../azure-subscription-service-limits.md)

## <a name="partners"></a>Partner
Microsoft collabora a stretto contatto con i partner immagini hello tooensure disponibili sono aggiornate e ottimizzate per un runtime di Azure.  Per altre informazioni sui partner, controllare le pagine relative a Marketplace.

* Linux in Azure - [Distribuzioni supportate](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [Azure Marketplace - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat - [Azure Marketplace - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [Azure Marketplace - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Marketplace - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Azure Marketplace - CoreOS (Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [Bitnami Library for Azure](https://azure.bitnami.com/)
* Mesosphere - [Azure Marketplace - Mesosphere DC/OS on Azure](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Marketplace - Azure Container Service con Docker Swarm](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>Introduzione a Linux in Azure
toobegin tramite Azure, è necessario un account Azure, hello Azure CLI installato e una coppia di chiavi pubblica e privata SSH.

### <a name="sign-up-for-an-account"></a>Iscriversi per ottenere un account
Hello utilizzando hello Cloud di Azure è innanzitutto toosign a un account Azure.  Passare toohello [abbonamento Azure](https://azure.microsoft.com/pricing/free-trial/) pagina tooget avviato.

### <a name="install-hello-cli"></a>Installare hello CLI
Con il nuovo account di Azure, è possibile iniziare immediatamente utilizzando hello portale di Azure, è un pannello di amministrazione basata sul web.  toomanage hello Cloud di Azure tramite hello della riga di comando, si installa hello `azure-cli`.  Installare hello [CLI di Azure 2.0](/cli/azure/install-azure-cli) nella workstation Mac o Linux.

### <a name="create-an-ssh-key-pair"></a>Creare una coppia di chiavi SSH
A questo punto si dispone di un account Azure, portale web di Azure hello e hello CLI di Azure.  passaggio successivo Hello è toocreate una coppia di chiavi SSH è tooSSH utilizzati in Linux senza utilizzare una password.  [Creare chiavi SSH su Mac e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooenable senza password degli account di accesso e migliora la sicurezza.

### <a name="create-a-vm-using-hello-cli"></a>Creare una macchina virtuale utilizzando hello CLI
Creazione di una VM Linux utilizzando hello CLI è toodeploy un modo rapido una macchina virtuale senza uscire da hello terminal che si utilizza.  Tutto ciò che è possibile specificare nel portale web hello è disponibile tramite un flag della riga di comando o un commutatore.  

* [Creare una VM Linux di hello CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>Creare una macchina virtuale nel portale di hello
Creazione di una VM Linux nel portale web di Azure hello è un modo tramite un clic del mouse tooeasily hello tooa distribuzione tooget di varie opzioni.  Anziché utilizzare il flag della riga di comando o commutatori, si è in grado di tooview un layout web nice di varie opzioni e impostazioni.  Tutti gli elementi disponibili tramite l'interfaccia della riga di comando hello è disponibili anche nel portale di hello.

* [Creare una VM Linux di hello portale](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>Accesso tramite SSH senza una password
Hello macchina virtuale è in esecuzione in Azure e si è pronti toolog in.  L'utilizzo di password toolog in via SSH è non sicuro e richiedere tempo.  Utilizzo delle chiavi SSH è hello in modo più sicuro e anche toologin modo più rapido hello.  Quando si creano VM Linux tramite il portale di hello o hello CLI, sono disponibili due opzioni di autenticazione.  Se si sceglie una password per SSH, Azure Configura account di accesso di hello VM tooallow tramite password.  Se si sceglie toouse una chiave pubblica SSH, Azure Configura hello VM tooonly consentire gli account di accesso tramite SSH chiavi e disabilita gli account di accesso di password. consentire accessi chiavi SSH, utilizzare le VM Linux da solo toosecure hello opzione della chiave pubblica SSH durante la creazione di VM nel portale di hello o CLI hello.

## <a name="related-azure-components"></a>Componenti di Azure correlati
## <a name="storage"></a>Archiviazione
* [Introduzione tooMicrosoft di archiviazione di Azure](../../storage/common/storage-introduction.md)
* [Aggiungere un tooa disco VM Linux utilizzando hello azure-cli](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Funzionamento dei dischi tooa VM Linux nel portale di Azure hello tooattach un tipo di dati](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Rete
* [Panoramica di Rete virtuale.](../../virtual-network/virtual-networks-overview.md)
* [Indirizzi IP in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [Apertura di porte tooa VM Linux in Azure](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Creare un nome di dominio completo nel portale di Azure hello](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>Contenitori
* [Macchine virtuali e contenitori in Azure](containers.md)
* [Introduzione al servizio contenitore di Azure](../../container-service/container-service-intro.md)
* [Distribuire un cluster del servizio contenitore di Azure](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>Passaggi successivi
Quella descritta è panoramica di Linux in Azure.  passaggio successivo Hello è toodive in e creare alcune macchine virtuali.

* [Esplorare l'elenco crescente di script di esempio per l'esecuzione di attività comuni tramite l'interfaccia della riga di comando di Azure](cli-samples.md)
