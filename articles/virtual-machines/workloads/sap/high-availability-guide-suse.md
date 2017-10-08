---
title: "disponibilità elevata macchine virtuali per SAP NetWeaver in SUSE Linux Enterprise Server per le applicazioni SAP aaaAzure | Documenti Microsoft"
description: "Guida alla disponibilità elevata per SAP NetWeaver su SUSE Linux Enterprise Server per SAP applications"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>Disponibilità elevata per SAP NetWeaver su macchina virtuali di Azure in SUSE Linux Enterprise Server for SAP applications

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

In questo articolo viene descritto come macchine virtuali di toodeploy hello, configurare le macchine virtuali di hello, installare il framework di cluster hello e installare un sistema SAP NetWeaver 7,50 a disponibilità elevata.
Nelle configurazioni di esempio hello, i comandi di installazione e così via. vengono usati il numero di istanza ASCS 00, il numero di istanza ERS 02 e l'ID del sistema SAP NWS. Hello i nomi delle risorse di hello (ad esempio macchine virtuali, reti virtuali) nell'esempio hello si supponga di aver utilizzato hello [convergente modello] [ template-converged] con risorse di hello toocreate NWS ID sistema SAP.

Leggere hello seguenti prima di note su SAP e documenti

* Nota SAP [1928533], contenente:
  * Elenco di dimensioni di macchina virtuale di Azure sono supportati per la distribuzione del software SAP hello
  * Importanti informazioni sulla capacità per le dimensioni delle VM di Azure
  * Software SAP e combinazioni di sistemi operativi e database supportati
  * Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure

* La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.
* La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications
* La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications
* La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.
* Nota SAP [2191498] hello necessario versione dell'agente Host SAP per Linux in Azure.
* La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.
* La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.
* Nota SAP [1999351] contiene altre informazioni sulla risoluzione dei problemi per hello Azure Enhanced Monitoring Extension per SAP.
* [Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.
* [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]
* [SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] (Scenario di ottimizzazione delle prestazioni di SAP HANA SR)  
  Guida di Hello contiene tutte le informazioni necessarie tooset di SAP HANA sistema replica locale. Usare la guida per le indicazioni di base.
* [Elevata NFS spazio di archiviazione disponibile con DRBD e Pacemaker] [ suse-drbd-guide] Guida hello contiene tutte le informazioni necessarie tooset di un server NFS a disponibilità elevata. Usare la guida per le indicazioni di base.


## <a name="overview"></a>Panoramica

disponibilità elevata di tooachieve, SAP NetWeaver richiede un server NFS. server NFS Hello è configurato in un cluster separato e può essere utilizzato da più sistemi SAP.

![Panoramica della disponibilità elevata di SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

Hello del server NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver Hiamanti e database SAP HANA hello utilizzare nome host virtuale e gli indirizzi IP virtuali. In Azure, un bilanciamento del carico è necessario toouse un indirizzo IP virtuale. Hello elenco riportato di seguito viene illustrata hello configurazione di bilanciamento del carico hello.

### <a name="nfs-server"></a>Server NFS
* Configurazione front-end
  * Indirizzo IP 10.0.0.4
* Configurazione back-end
  * Interfacce di rete tooprimary di tutte le macchine virtuali che devono far parte del cluster NFS hello connesso
* Porta probe
  * Porta 61000
* Regole di bilanciamento del carico
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A)SCS
* Configurazione front-end
  * Indirizzo IP 10.0.0.10
* Configurazione back-end
  * Interfacce di rete connessa tooprimary di tutte le macchine virtuali che devono far parte del cluster di hello (A) SCS/Hiamanti
* Porta probe
  * Porta 620**&lt;nr&gt;**
* Regole di bilanciamento del carico
  * 32**&lt;nr&gt;** TCP
  * 36**&lt;nr&gt;** TCP
  * 39**&lt;nr&gt;** TCP
  * 81**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="ers"></a>ERS
* Configurazione front-end
  * Indirizzo IP 10.0.0.11
* Configurazione back-end
  * Interfacce di rete connessa tooprimary di tutte le macchine virtuali che devono far parte del cluster di hello (A) SCS/Hiamanti
* Porta probe
  * Porta 621**&lt;nr&gt;**
* Regole di bilanciamento del carico
  * 33**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* Configurazione front-end
  * Indirizzo IP 10.0.0.12
* Configurazione back-end
  * Interfacce di rete tooprimary di tutte le macchine virtuali che devono far parte del cluster HANA hello connesso
* Porta probe
  * Porta 625**&lt;nr&gt;**
* Regole di bilanciamento del carico
  * 3**&lt;nr&gt;**15 TCP
  * 3**&lt;nr&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>Configurazione di un server NFS a disponibilità elevata

### <a name="deploying-linux"></a>Distribuzione di Linux

Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP 12 di applicazioni che è possibile utilizzare toodeploy nuove macchine virtuali.
È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie. Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:

1. Aprire hello [modello di file server di SAP] [ template-file-server] in hello portale di Azure   
1. Immettere i seguenti parametri hello
   1. Prefisso della risorsa  
      Immettere il prefisso di hello da toouse. il valore di Hello viene utilizzato come prefisso per le risorse di hello che vengono distribuite.
   2. Tipo di sistema operativo  
      Selezionare una delle distribuzioni di Linux hello. Per questo esempio, selezionare SLES 12
   3. Nome utente e password amministratore  
      Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.
   4. ID subnet  
      ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a. Lasciare vuoto se si desidera toocreate una nuova rete virtuale o selezionare hello subnet della rete VPN o Express Route rete virtuale tooconnect hello macchina virtuale tooyour locale rete. ID Hello in genere è simile /Subscriptions/<ID**&lt;id sottoscrizione&gt;**/ResourceGroups /**&lt;nome gruppo di risorse&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome di rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**

### <a name="installation"></a>Installazione

Hello seguenti elementi sono preceduti da una **[A]** -nodi tooall applicabile, **[1]** -solo applicabile toonode 1 o **[2]** -solo applicabile toonode 2.

1. **[A]** Aggiornare SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Abilitare l'accesso SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Abilitare l'accesso SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Abilitare l'accesso SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Installare l'estensione per la disponibilità elevata
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** Configurare la risoluzione dei nomi host   

   È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi. Questo esempio mostra come toouse hello file /etc/hosts.
   Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Inserire hello seguenti righe troppo/ecc/host. Modificare l'ambiente di hello IP indirizzo e nome host toomatch   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** Installare il cluster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Aggiungi nodo toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Modifica hacluster password toohello stessa password

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurare corosync toouse altro trasporto e aggiungere nodelist. In caso contrario, il cluster non funzionerà.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Aggiungere i seguenti file grassetto toohello contenuto hello.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Riavviare il servizio di corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Installare i componenti drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Creare una partizione per il dispositivo drbd hello

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Creare le configurazioni LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**  Dispositivo drbd di crea hello NFS

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   Creare un dispositivo drbd hello e avviarla

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** Saltare la sincronizzazione iniziale

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Nodo primario del set hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**  Attendere finché non vengono sincronizzati i nuovi dispositivi drbd hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Creare sistemi di file in hello drbd dispositivi

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>Configurare il framework del cluster

1. **[1]**  Modificare le impostazioni predefinite di hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Configurazione cluster Aggiungi hello NFS drbd dispositivo toohello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Del server NFS hello crea

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Creare risorse di File System NFS hello

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Creare esportazioni NFS hello

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a>Creare il dispositivo STONITH

dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure. Seguire questi toocreate passaggi un'entità servizio.

1. Andare troppo<https://portal.azure.com>
1. Pannello di Azure Active Directory aprire hello  
   Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.
1. Fare clic su Registrazioni per l'app
1. Fare clic su Aggiungi.
1. Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea
1. URL Hello-sign-on non viene utilizzato e può essere un URL valido
1. Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello
1. Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva
1. Annotare hello valore. Viene utilizzato come hello **password** per hello dell'entità servizio
1. Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio

Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita. È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.

1. Passare toohttps://portal.azure.com
1. Apri hello tutti pannello risorse
1. Selezionare la macchina virtuale di hello
1. Fare clic su Controllo di accesso (IAM)
1. Fare clic su Aggiungi.
1. Selezionare il ruolo di hello proprietario
1. Immettere il nome di hello dell'applicazione hello creato in precedenza
1. Fare clic su OK.

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Creare hello STONITH dispositivi

Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Abilitare hello utilizzo di un dispositivo STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>Configurazione di (A)SCS

### <a name="deploying-linux"></a>Distribuzione di Linux

Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP 12 di applicazioni che è possibile utilizzare toodeploy nuove macchine virtuali. immagine del marketplace Hello contiene l'agente di risorsa hello per SAP NetWeaver.

È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie. Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:

1. Aprire hello [modello ASCS/SCS più SID] [ template-multisid-xscs] o hello [convergente modello] [ template-converged] sul modello solo di hello hello portale Azure ASCS/SCS Crea regole di bilanciamento del carico di hello per le istanze di Hiamanti (solo Linux) e SAP NetWeaver ASCS/SCS hello mentre hello convergente modello crea anche le regole di bilanciamento del carico di hello per un database (ad esempio Microsoft SQL Server o SAP HANA). Se si prevede di tooinstall un sistema basate su SAP NetWeaver e si desidera anche database hello tooinstall in hello stesse macchine, utilizzare hello [convergente modello][template-converged].
1. Immettere i seguenti parametri hello
   1. Prefisso di risorsa (solo modello ASCS/SCS a più SID)  
      Immettere il prefisso di hello da toouse. il valore di Hello viene utilizzato come prefisso per le risorse di hello che vengono distribuite.
   3. ID del sistema SAP (solo modello convergente)  
      Immettere il sistema SAP hello Id di sistema SAP si desidera tooinstall hello. Hello Id viene utilizzato come prefisso per le risorse di hello che vengono distribuite.
   4. Tipo di stack  
      Selezionare tipo di stack hello SAP NetWeaver
   5. Tipo di sistema operativo  
      Selezionare una delle distribuzioni di Linux hello. Per questo esempio, selezionare SLES 12 BYOS
   6. Tipo di database  
      Selezionare HANA
   7. Dimensioni del sistema SAP  
      quantità di Hello del nuovo sistema SAP hello fornisce. Se non si conoscono quanti valori SAPS hello sistema richiede, chiedere il Partner di tecnologia di SAP o l'integratore
   8. Disponibilità del sistema  
      Selezionare la disponibilità elevata.
   9. Nome utente e password amministratore  
      Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.
   10. ID subnet  
   ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a.  Lasciare vuoto se si desidera toocreate una nuova rete virtuale o selezionare hello stessa subnet utilizzata o creato come parte della distribuzione del server NFS hello. ID Hello in genere è simile /Subscriptions/<ID**&lt;id sottoscrizione&gt;**/ResourceGroups /**&lt;nome gruppo di risorse&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome di rete virtuale&gt;**/subnets/**&lt;nome subnet&gt;**

### <a name="installation"></a>Installazione

Hello seguenti elementi sono preceduti da una **[A]** -nodi tooall applicabile, **[1]** -solo applicabile toonode 1 o **[2]** -solo applicabile toonode 2.

1. **[A]** Aggiornare SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** Abilitare l'accesso SSH

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** Abilitare l'accesso SSH

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** Abilitare l'accesso SSH

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** Installare l'estensione per la disponibilità elevata
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]**  Aggiornare gli agenti delle risorse SAP  
   
   Una patch per il pacchetto di risorse agenti hello è obbligatorio toouse hello nuova configurazione descritta in questo articolo. È possibile controllare se patch hello è già installato con hello comando seguente

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   output di Hello dovrebbe essere simile a

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   Se il comando grep hello non viene trovato il parametro IS_ERS hello, è necessario patch hello tooinstall elencato in [hello SUSE pagina di download](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** Configurare la risoluzione dei nomi host   

   È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi. Questo esempio mostra come toouse hello file /etc/hosts.
   Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   Inserire hello seguenti righe troppo/ecc/host. Modificare l'ambiente di hello IP indirizzo e nome host toomatch   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** Installare il cluster
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**  Aggiungi nodo toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**  Modifica hacluster password toohello stessa password

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**  Configurare corosync toouse altro trasporto e aggiungere nodelist. In caso contrario, il cluster non funzionerà.
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   Aggiungere i seguenti file grassetto toohello contenuto hello.
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   Riavviare il servizio di corosync hello

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** Installare i componenti drbd

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**  Creare una partizione per il dispositivo drbd hello

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** Creare le configurazioni LVM

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**  Dispositivo drbd SCS hello di creazione

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   Creare un dispositivo drbd hello e avviarla

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**  Dispositivo drbd Hiamanti hello di creazione

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   Inserisci configurazione hello per il nuovo dispositivo di drbd hello e uscita

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   Creare un dispositivo drbd hello e avviarla

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** Saltare la sincronizzazione iniziale

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Nodo primario del set hello

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**  Attendere finché non vengono sincronizzati i nuovi dispositivi drbd hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]**  Creare sistemi di file in hello drbd dispositivi

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>Configurare il framework del cluster

**[1]**  Modificare le impostazioni predefinite di hello

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>Prepararsi per l'installazione di SAP NetWeaver

1. **[A]**  Hello Crea directory condivise

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** Configurare autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Creare un file con

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   Riavviare autofs toomount hello nuovi volumi o condivisioni

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]**  Configurare il file SWAP
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   La modifica di hello hello agente tooactivate

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>Installazione di SAP NetWeaver ASCS/ERS

1. **[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate. Non è importante in quali risorse hello nodo sono in esecuzione.

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** Installare SAP NetWeaver ASCS  

   Installazione di SAP NetWeaver ASCS come radice nel primo nodo hello utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per hello ASCS <b>nws ascs</b>, <b>10.0.0.10</b>e numero di istanza hello utilizzato per il probe hello di bilanciamento del carico hello, ad esempio <b>00</b>.

   È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**  Creare un probe di integrità servizio di bilanciamento del carico interno hello e una risorsa IP virtuale

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate. Non è importante in quali risorse hello nodo sono in esecuzione.

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** Installare SAP NetWeaver ERS  

   Installazione di SAP NetWeaver Hiamanti come radice nel secondo nodo hello utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per hello Hiamanti <b>nws hiamanti</b>, <b>10.0.0.11</b> numero di istanza hello utilizzato per il probe hello di bilanciamento del carico hello, ad esempio e <b>02</b>.

   È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > Usare SWPM SP 20 PL 05 o versione successiva. Le versioni precedenti non è impostato correttamente le autorizzazioni di hello e hello installazione avrà esito negativo.
   > 

1. **[1]**  Adattare i profili di istanza ASCS/SCS e Hiamanti hello
 
   * Profilo ASCS/SCS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * Profilo ERS

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]**  Configurare keep-alive

   la comunicazione tra il server applicazioni SAP NetWeaver hello e hello ASCS/SCS Hello viene instradata tramite un bilanciamento del carico software. servizio di bilanciamento del carico Hello disconnette le connessioni inattive dopo un timeout configurabile. tooprevent questo è necessario un parametro nel profilo di SAP NetWeaver ASCS/SCS hello tooset e modificare le impostazioni di sistema di hello Linux. Per altre informazioni, leggere la [nota SAP 1410736][1410736].
   
   Hello ASCS/SCS profilo accodare parametro/encni/set_so_keepalive è stato già aggiunto nell'ultimo passaggio hello.

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]**  Configurare utenti SAP hello dopo l'installazione di hello
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**  Aggiungi hello ASCS e SAP Hiamanti toohello sapservice file services

   Aggiungere hello ASCS servizio voce toohello secondo nodo e copia hello Hiamanti voce toohello primo nodo del servizio.

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**  Creare risorse del cluster di hello SAP

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate. Non è importante in quali risorse hello nodo sono in esecuzione.

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a>Creare il dispositivo STONITH

dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure. Seguire questi toocreate passaggi un'entità servizio.

1. Andare troppo<https://portal.azure.com>
1. Pannello di Azure Active Directory aprire hello  
   Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.
1. Fare clic su Registrazioni per l'app
1. Fare clic su Aggiungi.
1. Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea
1. URL Hello-sign-on non viene utilizzato e può essere un URL valido
1. Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello
1. Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva
1. Annotare hello valore. Viene utilizzato come hello **password** per hello dell'entità servizio
1. Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio

Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita. È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.

1. Passare toohttps://portal.azure.com
1. Apri hello tutti pannello risorse
1. Selezionare la macchina virtuale di hello
1. Fare clic su Controllo di accesso (IAM)
1. Fare clic su Aggiungi.
1. Selezionare il ruolo di hello proprietario
1. Immettere il nome di hello dell'applicazione hello creato in precedenza
1. Fare clic su OK.

#### <a name="1-create-hello-stonith-devices"></a>**[1]**  Creare hello STONITH dispositivi

Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]**  Abilitare hello utilizzo di un dispositivo STONITH

Abilitare l'utilizzo di hello di un dispositivo STONITH

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>Installare il database

In questo esempio viene installata e configurata una replica di sistema di SAP HANA. SAP HANA verrà eseguito in hello stesso cluster come hello ASCS/SCS di SAP NetWeaver e Hiamanti. È anche possibile installare SAP HANA in un cluster dedicato. Per altre informazioni, vedere [Disponibilità elevata di SAP HANA in macchine virtuali di Azure (VM)][sap-hana-ha].

### <a name="prepare-for-sap-hana-installation"></a>Prepararsi per l'installazione di SAP HANA

È in genere consigliabile usare LVM per i volumi che archiviano i dati e file di log. A scopo di test, è anche possibile scegliere toostore hello dati e log file direttamente su un disco normale.

1. **[A]** LVM  
   esempio Hello riportato di seguito presuppone che le macchine virtuali hello disponga di quattro dischi dati collegati che devono essere utilizzati toocreate due volumi.
   
   Creare volumi fisici per tutti i dischi che si desidera toouse.
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   Creare un gruppo di volumi per il file di dati di hello, un gruppo di volumi per il file di log hello e una directory condivisa hello SAP HANA
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   Creare hello volumi logici
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   Creare le directory di montaggio hello e copiare hello UUID di tutti i volumi logici
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   Creare le voci di autofs per hello tre volumi logici
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   Inserire la riga toosudo vi /etc/auto.direct
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   Montare i volumi di nuovo hello
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** Dischi normali  

   Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco. Hello seguenti comandi creare una partizione su /dev/sdc e formattarla con xfs.
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   Inserire questo too/etc/auto.direct riga
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   Creare la directory di destinazione hello e montare il disco di hello.
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>Installazione di SAP HANA

Hello passaggi seguenti si basano capitolo 4 di hello [SAP HANA SR prestazioni ottimizzate Scenario guide] [ suse-hana-ha-guide] tooinstall SAP HANA sistema di replica. Leggerlo prima di continuare l'installazione di hello.

1. **[A]**  Eseguire hdblcm da hello HANA DVD
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** Aggiornare l'agente host SAP

   Scaricare l'archivio agente Host SAP più recente hello da hello [SAP Softwarecenter] [ sap-swcenter] ed eseguiti hello seguenti comando tooupgrade hello agente. Sostituire hello percorso toohello archivio toopoint toohello file scaricato.
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** Creare la replica HANA (come root)  

   Eseguire hello comando seguente. Verificare che tooreplace grassetto stringhe (HANA sistema ID HDB e numero di istanza 03) con valori di hello dell'installazione di SAP HANA.
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** Creare una voce di archivio chiavi (come root)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** Eseguire il backup del database (come root)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**  Cambiare toohello HANA sapsid utente e creare il sito primario di hello.

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**  Cambiare toohello HANA sapsid utente e creare il sito secondario di hello.

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** Creare le risorse del cluster SAP HANA

   Innanzitutto, creare una topologia di hello.
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   Successivamente, creare risorse HANA hello
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   Assicurarsi che lo stato del cluster hello è accettabile e che tutte le risorse siano avviate. Non è importante in quali risorse hello nodo sono in esecuzione.

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**  Istanza del database SAP NetWeaver hello installazione

   Istanza del database SAP NetWeaver hello installa come radice utilizzando un nome host virtuale che esegue il mapping, ad esempio l'indirizzo IP toohello del configurazione front-end di bilanciamento del carico hello per database hello <b>nws db</b> e <b>10.0.0.12</b>.

   È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>Installazione del server applicazioni di SAP NetWeaver

Seguire questi tooinstall passaggi un server applicazioni SAP. Hello i passaggi seguenti presuppongono che si installa il server applicazioni di hello in un server diverso da hello ASCS/SCS e i server HANA. In caso contrario alcuni dei passaggi di hello sotto (ad esempio la configurazione di risoluzione del nome host) non sono necessarie.

1. Configurare la risoluzione dei nomi host    
   È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi. Questo esempio mostra come toouse hello file /etc/hosts.
   Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi
   ```bash
   sudo vi /etc/hosts
   ```
   Inserire hello seguenti righe troppo/ecc/host. Modificare l'ambiente di hello IP indirizzo e nome host toomatch    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. Creare la directory sapmnt hello

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. Configurare autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   Creare un nuovo file con

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   Riavviare autofs toomount hello nuovi volumi o condivisioni

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. Configurare il file SWAP
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   La modifica di hello hello agente tooactivate

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. Installare il server applicazioni di SAP NetWeaver

   Installare un server applicazioni di SAP NetWeaver primario o aggiuntivo.

   È possibile utilizzare hello sapinst parametro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst di tooconnect un utente non root.

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. Aggiornare l'archivio sicuro di SAP HANA

   Nome virtuale di toohello toopoint del programma di installazione di SAP HANA sistema replica hello dell'archivio hello aggiornamento SAP HANA sicura.
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>Passaggi successivi
* [Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in macchine virtuali di Azure, vedere [disponibilità elevata di SAP HANA in macchine virtuali di Azure (VM)][sap-hana-ha]
