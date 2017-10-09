---
title: SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux aaaTesting | Documenti Microsoft
description: Test di SAP NetWeaver nelle VM SUSE Linux di Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a>Esecuzione di SAP NetWeaver nelle VM SUSE Linux di Microsoft Azure
Questo articolo descrive i vari aspetti tooconsider quando si esegue SAP NetWeaver in macchine virtuali di Microsoft Azure SUSE Linux (VM). A partire dal 19 maggio 2016 SAP NetWeaver è ufficialmente supportato nelle macchine virtuali SUSE Linux in Azure. Tutti i dettagli riguardanti le versioni di Linux, le versioni del kernel SAP e così via, sono reperibili nella nota 1928533 di SAP "SAP Applications on Azure: Supported Products and Azure VM types" (Applicazioni SAP in Azure: prodotti supportati e i tipi di VM di Azure).
Altra documentazione su SAP nelle VM Linux è disponibili qui: [Uso di SAP in macchine virtuali (VM) Linux](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello le seguenti informazioni consentono di evitare alcuni problemi potenziali.

## <a name="suse-images-on-azure-for-running-sap"></a>Immagini SUSE in Azure per l'esecuzione di SAP
Per l'esecuzione di SAP NetWeaver in Azure, usare solo SUSE Linux Enterprise Server SLES 12 (SPx). Vedere anche la nota 1928533 di SAP. È un'immagine SUSE speciale in hello Azure Marketplace ("SLES 11 SP3 per SAP CAL"), ma questo non è per uso generale. Non utilizzare questa immagine perché è riservato per hello [SAP Cloud accessorio libreria](https://cal.sap.com/) soluzione.  

È consigliabile usare Azure Resource Manager per tutti i nuovi test e installazioni da condurre in Azure. toolook per immagini SUSE SLES e versioni tramite Azure PowerShell o hello Azure interfaccia della riga di comando (CLI), hello di utilizzare i comandi seguenti. È quindi possibile utilizzare output di hello, ad esempio, toodefine hello immagine di sistema operativo un modello JSON per la distribuzione di una nuova macchina virtuale di SUSE Linux.
I comandi di PowerShell seguenti sono validi per Azure PowerShell versione 1.0.1 e successive.

Sebbene sia comunque possibile toouse hello standard SLES immagini per le installazioni di SAP, è consigliabile utilizzare toomake di hello SLES nuove per le immagini SAP che sono disponibili ora su hello Azure dell'immagine della raccolta. Ulteriori informazioni su queste immagini possono trovarsi in hello corrispondente [pagina Azure Marketplace]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) o hello [pagina web di domande frequenti su SUSE su SLES per SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).


* Cercare i server di pubblicazione esistenti tra cui SUSE:
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* Cercare offerte esistenti da parte di SUSE:
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* Cercare offerte SUSE SLES:
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* Cercare una versione specifica di una SKU SLES:
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a>Installazione di WALinuxAgent in una VM SUSE
agente di Hello chiamato WALinuxAgent fa parte di immagini SLES hello in hello Azure Marketplace. Per informazioni sull'installazione manuale, ad esempio durante il caricamento di un disco rigido virtuale (VHD) del sistema operativo SLES da locale, vedere:

* [OpenSUSE](http://software.opensuse.org/package/WALinuxAgent)
* [Azzurro](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SUSE](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a>"Enhanced monitoring" di SAP
SAP "monitoraggio avanzato" è un toorun prerequisito obbligatorio SAP in Azure. Consultare i dettagli nella nota 2191498 di SAP "SAP on Linux with Azure: Enhanced Monitoring" (SAP su Linux con Azure: Enhanced Monitoring).

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a>Collegamento di dischi di dati di Azure tooan VM Linux di Azure
È non consigliabile montare mai tooan dischi dati di Azure VM Linux di Azure utilizzando l'ID del dispositivo hello. Utilizzare invece l'identificatore univoco universale hello (UUID). Prestare attenzione quando si utilizzano dischi di dati di Azure toomount strumenti grafici, ad esempio. Verificare le voci di hello in /etc/fstab..

problema di Hello con ID dispositivo hello è che è possibile modificare e quindi hello macchina virtuale di Azure potrebbe bloccarsi hello procedura di avvio. problema di hello toomitigate, è possibile aggiungere il parametro nofail hello in /etc/fstab.. Ma, prestare attenzione con nofail perché le applicazioni potrebbero utilizzare punto di montaggio hello come prima e potrebbero scrivere nel file system di hello radice nel caso in cui non è stato montato un disco dati esterni di Azure durante l'avvio di hello.

Hello unica eccezione toomounting tramite UUID si connette un disco del sistema operativo per la risoluzione dei problemi, come descritto nella seguente sezione hello.

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a>Risoluzione dei problemi di una VM SUSE non più accessibile
Potrebbero esistere situazioni in cui una VM SUSE in Azure si blocca nel processo di avvio hello (ad esempio, con un errore correlato al montaggio dei dischi). È possibile verificare il problema tramite funzionalità di diagnostica di avvio hello per le macchine virtuali di Azure v2 in hello portale di Azure. Per altre informazioni, vedere l'articolo relativo alla [diagnostica di avvio](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).

Problema di hello toosolve unidirezionale è disco del sistema operativo di hello tooattach da hello danneggiato VM tooanother SUSE VM in Azure. Quindi, apportare modifiche quali la modifica di /etc/fstab. o la rimozione di regole udev di rete, come descritto nella sezione successiva hello.

Non vi è un aspetto importante tooconsider. Distribuzione di più macchine virtuali SUSE dalla stessa immagine di Azure Marketplace (ad esempio, SP4 11 SLES) provoca hello hello del sistema operativo tooalways disco montato mediante hello lo stesso UUID. Pertanto, l'utilizzo hello UUID tooattach un disco del sistema operativo da una macchina virtuale diverso che è stata distribuita tramite hello stessa immagine di Azure Marketplace comporterà due UUID identici. Questo causa problemi e potrebbe significare che hello VM per la risoluzione dei problemi in realtà si avvierà da hello collegato e danneggiato disco del sistema operativo anziché hello originale.

Esistono due modi tooavoid questo:

* Utilizzare un'immagine diversa di Azure Marketplace per hello risoluzione dei problemi di macchina virtuale (ad esempio, SLES 11 SPx anziché SLES 12).
* Non collegare disco del sistema operativo hello danneggiato da un'altra macchina virtuale utilizzando l'UUID: utilizzare un altro.

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a>Caricamento di una VM SUSE da tooAzure locale
Per una descrizione di tooupload passaggi hello una VM SUSE da tooAzure locale, vedere [preparare una macchina virtuale SLES o openSUSE per Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Se si desidera tooupload una macchina virtuale senza effettuarne il deprovisioning hello passaggio alla fine di hello (ad esempio, tookeep un'installazione esistente di SAP, nonché il nome host hello), controllare hello seguenti elementi:

* Verificare che tale disco hello del sistema operativo è montato usando un ID dispositivo UUID e non hello. Modifica tooUUID just-in /etc/fstab. non è sufficiente per il disco del sistema operativo hello. Inoltre, non dimenticare caricatore di avvio hello tooadapt mediante YaST o modificando /boot/grub/menu.lst.
* Se si utilizza il formato di file VHDX hello per disco del sistema operativo SUSE hello e convertirlo tooVHD per il caricamento tooAzure, è molto probabile che il dispositivo di rete hello passerà da ' eth0 tooeth1. tooavoid problemi quando si esegue l'avvio in Azure in un secondo momento, modificare tooeth0 indietro, come descritto in [correzione eth0 in clonato SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).

Inoltre toowhat descritto nell'articolo hello, è consigliabile rimuovere questa:

   /lib/udev/rules.d/75-persistent-net-generator.rules

È anche possibile installare hello agente Linux di Azure (waagent) toohelp evitare potenziali problemi, fino a quando non sono presenti più schede di rete.

## <a name="deploying-a-suse-vm-on-azure"></a>Distribuzione di una VM SUSE in Azure
È necessario creare nuove macchine virtuali SUSE utilizzando file di modello JSON nel nuovo modello di gestione risorse di Azure hello. Dopo aver creato il file di modello di hello JSON, è possibile distribuire hello VM utilizzando il comando CLI come un'alternativa tooPowerShell seguente hello:

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
Per altre informazioni sui file modello JSON, vedere [Creazione di modelli di Azure Resource Manager](../../../resource-group-authoring-templates.md) e [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).

Per ulteriori informazioni su CLI e Gestione risorse di Azure, vedere [hello utilizzare CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../../../xplat-cli-azure-resource-manager.md).

## <a name="sap-license-and-hardware-key"></a>Licenza SAP e chiave hardware
Per la certificazione SAP Azure ufficiale di hello, un nuovo meccanismo è stato introdotto toocalculate hello SAP hardware chiave utilizzata per licenza SAP hello. kernel SAP Hello era toobe adattato toomake utilizzo di questo oggetto. Le versioni precedenti del kernel SAP per Linux non comprendono tale modifica del codice. Pertanto, in alcuni casi (ad esempio, macchina virtuale di Azure ridimensionamento), modificare la chiave di hello SAP hardware e licenze SAP hello è non essere più validi. Questo viene risolto nel kernel Linux SAP più recente di hello. Per i dettagli vedere la nota 1928533 di SAP.

## <a name="suse-sapconf-package--tuned-adm"></a>Pacchetto sapconf di SUSE e strumento tuned-adm
SUSE offre un pacchetto denominato "sapconf" che gestisce un set di impostazioni specifiche di SAP. Per ulteriori dettagli su quale questo pacchetto non e come tooinstall e usarlo, vedere [utilizzando sapconf tooprepare un sistemi SAP di SUSE Linux Enterprise Server toorun](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) e [novità sapconf o come tooprepare un SUSE Linux Enterprise Server per l'esecuzione di sistemi SAP? ](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).

Hello frattempo prevede un nuovo strumento che sostituisce sapconf - ottimizzare-adm. Una possibile trovare altre informazioni su questo strumento seguenti hello due collegamenti seguenti.

La documentazione SLES sull'uso di tuned-adm profile sap-hana è reperibile [qui](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html) 

Informazioni su come ottimizzare i sistemi per i carichi di lavoro SAP con lo strumento tuned-adm è reperibile [qui](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) , nel capitolo 6.2

## <a name="nfs-share-in-distributed-sap-installations"></a>Condivisione NFS in installazioni SAP distribuite
Se si dispone di un'installazione distribuita, ad esempio, in cui si desidera tooinstall hello database e i server applicazioni SAP in macchine virtuali separate: hello è possibile condividere directory /sapmnt hello tramite File System NFS (Network). Se si verificano problemi con i passaggi di installazione hello dopo la creazione di condivisioni NFS per /sapmnt hello, controllare toosee se "no_root_squash" è impostato per la condivisione di hello.

## <a name="logical-volumes"></a>Volumi logici
Nelle ultime hello se è necessaria una grande volume logico su più dischi dati di Azure (ad esempio, per i database SAP hello), è consigliabile toouse mdadm come lvm non è stato completamente convalidato ancora in Azure. toolearn tooset backup RAID Linux in Azure utilizzando mdadm, vedere [configurare software RAID su Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). In hello frattempo al momento di inizio di maggio 2016 anche lvm è completamente supportato in Azure e può essere utilizzato come un toomdadm alternativo. Per altre informazioni su lvm in Azure vedere [Configurare LVM in una VM Linux in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="azure-suse-repository"></a>Repository SUSE di Azure
Se si dispone di un problema con accesso toohello standard SUSE Azure del repository, è possibile utilizzare un comando semplice di tooreset è. Questa situazione può verificarsi se si crea un'immagine del sistema operativo privata in un'area di Azure e quindi copia hello tooa diversa area dell'immagine in cui si desidera toodeploy nuove macchine virtuali basate su questa immagine del sistema operativo privata. Eseguire semplicemente hello comando all'interno di hello VM seguente:

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a>Gnome Desktop
Se si desidera toouse hello Gnome desktop tooinstall sistema SAP demo completo all'interno di una singola macchina virtuale, tra cui un'interfaccia utente grafica di SAP, browser e console di gestione di SAP, utilizzare tooinstall questo suggerimento su più immagini di Azure SLES hello:

   Per SLES 11:

   ```
   zypper in -t pattern gnome
   ```

   Per SLES 12:

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a>Supporto di SAP per Oracle in Linux nel cloud hello
Non esiste alcuna limitazione di supporto da parte di Oracle su Linux in ambienti virtualizzati. Anche se non si tratta di un argomento specifici di Azure, è importante toounderstand. SAP non supporta Oracle su SUSE o Red Hat in un cloud pubblico come Azure. toodiscuss in questo argomento, contattare direttamente Oracle.

