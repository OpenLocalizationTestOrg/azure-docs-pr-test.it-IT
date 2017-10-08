---
title: Panoramica di agente VM Linux aaaAzure | Documenti Microsoft
description: Informazioni su come tooinstall e configurare l'agente Linux (waagent) toomanage l'interazione della macchina virtuale con il Controller di infrastruttura di Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Comprensione e l'utilizzo di hello agente Linux di Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introduzione
Hello Microsoft agente Linux di Azure (waagent) gestisce Linux e FreeBSD provisioning e interazione di VM con hello Controller di infrastruttura di Azure. Fornisce hello seguenti funzionalità per le distribuzioni di Linux e FreeBSD IaaS:

> [!NOTE]
> Vedere agente Linux di Azure hello [Leggimi](https://github.com/Azure/WALinuxAgent/blob/master/README.md) per altri dettagli.
> 
> 

* **Provisioning dell'immagine**
  
  * Creazione di un account utente
  * Configurazione dei tipi di autenticazione SSH
  * Distribuzione di coppie di chiavi e chiavi pubbliche SSH
  * Nome dell'impostazione hello host
  * Pubblicazione hello Nome toohello piattaforma host DNS
  * Piattaforma di toohello impronta digitale della chiave SSH host Reporting
  * Gestione del disco risorse
  * Formattazione e quindi montare il disco di risorsa hello
  * Configurazione dell'area di swap
* **Rete**
  
  * Gestisce le route tooimprove compatibilità con i server DHCP di piattaforma
  * Assicura la stabilità di hello del nome di interfaccia di rete hello
* **Kernel**
  
  * Configura un NUMA virtuale (disabilitare per kernel <2.6.37)
  * Usa l'entropia Hyper-V per /dev/random
  * Consente di configurare i timeout di SCSI per il dispositivo di primo livello hello (che può essere remoto)
* **Diagnostica**
  
  * Porta seriale toohello il reindirizzamento della console
* **Distribuzioni SCVMM**
  
  * Rileva e avvia l'agente VMM hello per Linux durante l'esecuzione in un ambiente System Center Virtual Machine Manager 2012 R2
* **Estensione VM**
  
  * Inserire i componenti creati da Microsoft e dai partner in automazione di software e la configurazione di tooenable VM Linux (IaaS)
  * Implementazione di riferimento di estensione VM in [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Comunicazione
flusso di informazioni Hello dall'agente di hello piattaforma toohello avviene tramite due canali:

* Un DVD collegato in fase di avvio per le distribuzioni IaaS. Il DVD include un file di configurazione conformi OVF che include tutte le informazioni di provisioning diverso da coppie di chiavi SSH effettivo hello.
* Un endpoint TCP espone un'API REST utilizzato tooobtain distribuzione e configurazione della topologia.

## <a name="requirements"></a>Requisiti
Hello sistemi seguenti sono stati testati e sono note toowork con hello agente Linux di Azure:

> [!NOTE]
> Questo elenco può differire dall'elenco ufficiale di hello dei sistemi supportati nella piattaforma Microsoft Azure, hello, come descritto qui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Altri sistemi supportati:

* FreeBSD 10+ (agente Linux di Azure v2.0.10+)

agente Linux di Hello dipende da alcuni pacchetti di sistema in ordine toofunction correttamente:

* Python 2.6+
* OpenSSL 1.0+
* OpenSSH 5.3+
* Utilità file system: sfdisk, fdisk, mkfs, separate
* Strumenti password: chpasswd, sudo
* Strumenti di elaborazione testo: sed, grep
* Strumenti di rete: ip-route
* Supporto di kernel per l'installazione di file system UDF.

## <a name="installation"></a>Installazione
Installazione utilizzando un RPM o un pacchetto DEB dal repository di pacchetti di distribuzione è il metodo di hello preferito di installazione e aggiornamento hello agente Linux di Azure. Hello tutti [approvate per i provider di distribuzione](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrare pacchetto dell'agente Linux di Azure hello in un repository e le immagini.

Consultare la documentazione di toohello in hello [repository agente Linux di Azure su GitHub](https://github.com/Azure/WALinuxAgent) per le opzioni di installazione avanzata, ad esempio l'installazione da posizioni di origine o toocustom o prefissi.

## <a name="command-line-options"></a>Opzioni da riga di comando
### <a name="flags"></a>Flag
* verbose: aumenta il livello di dettaglio del comando specificato
* force: ignora la conferma interattiva per determinati comandi

### <a name="commands"></a>Comandi:
* Guida in linea: Elenca i flag e i comandi di hello è supportato.
* deprovisioning: tentativo sistema hello tooclean e renderlo idoneo per il nuovo provisioning. Questa operazione eliminati seguente hello:
  
  * Tutte le chiavi host SSH (se Provisioning.RegenerateSshHostKeyPair 'y' nel file di configurazione hello)
  * Configurazione NameServer in /etc/resolv.conf
  * Password radice da /etc/shadow. (se Provisioning.DeleteRootPassword 'y' nel file di configurazione hello)
  * Lease client DHCP memorizzati nella cache
  * Reimposta host toolocalhost.localdomain nome

> [!WARNING]
> Deprovisioning non garantisce che l'immagine hello è deselezionata di tutte le informazioni riservate e adatto per la ridistribuzione.
> 
> 

* deprovisioning + utente: consente di eseguire tutto - deprovisioning (sopra) e anche Elimina account provisioning utente ultimo hello (ottenuto dal /var/lib/waagent) e i dati associati. Questo parametro viene usato per il deprovisioning di un'immagine precedentemente sottoposta a provisioning in Azure in modo che possa essere acquisita e riutilizzata.
* versione: Visualizza la versione di hello del comando waagent
* serialconsole: Configura GRUB toomark ttyS0 (hello prima porta seriale) come console di avvio hello. Ciò garantisce che i log di avvio del kernel siano inviati toothe della porta seriale e resi disponibili per il debug.
* daemon: runas waagent un'interazione toomanage daemon con piattaforma hello. Questo argomento è toowaagent specificato nello script di inizializzazione waagent hello.
* start: esegue waagent come processo in background

## <a name="configuration"></a>Configurazione
Un file di configurazione (/ etc/waagent.conf) controlli hello azioni di comando waagent. Di seguito è riportato un file di configurazione di esempio:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Hello che varie opzioni di configurazione sono descritti in dettaglio di seguito. Le opzioni di configurazione sono di tre tipi: Boolean, String o Integer. opzioni di configurazione booleano Hello possono essere specificate come "y" o "n". Hello parola chiave speciale "None" possono essere utilizzati per alcune stringa tipo voci di configurazione come descritto in dettaglio riportato di seguito.

**Provisioning.Enabled:**  
Tipo: booleano  
Predefinito: y

Questo consente hello utente tooenable o disabilitare il provisioning delle funzionalità nell'agente hello hello. I valori validi sono "y" o "n". Se il provisioning è disabilitato, le chiavi di host e dell'utente SSH nell'immagine hello vengono mantenute e viene ignorata qualsiasi configurazione specificata in hello Azure API di provisioning.

> [!NOTE]
> Hello `Provisioning.Enabled` troppo "n" in Ubuntu Cloud immagini che utilizzano cloud-inizializzazione per il provisioning di valori predefiniti dei parametri.
> 
> 

**Provisioning.DeleteRootPassword:**  
Tipo: booleano  
Predefinito: n

Se set, la password radice hello nel file hello e così via/shadow vengono cancellati durante hello processo di provisioning.

**Provisioning.RegenerateSshHostKeyPair:**  
Tipo: booleano  
Predefinito: y

Se impostato, tutti SSH host coppie di chiavi (ecdsa e dsa o rsa) viene eliminato durante hello da /etc/hosts ssh/processo di provisioning. e viene generata un'unica coppia di chiavi aggiornata.

tipo di crittografia Hello per hello nuova coppia di chiavi è configurabile hello Provisioning.SshHostKeyPairType voce. Si noti che alcune distribuzioni creerà nuovamente le coppie di chiavi SSH per qualsiasi tipo di crittografia mancante quando si riavvia il daemon SSH hello (ad esempio, dopo un riavvio).

**Provisioning.SshHostKeyPairType:**  
Tipo: String  
Predefinito: rsa

Tipo di algoritmo di crittografia tooan è supportato dal daemon SSH hello nella macchina virtuale hello può essere impostato. i valori Hello in genere supportato sono "rsa", "dsa" e "ecdsa". Si noti che "putty.exe" in Windows non supporta il tipo "ecdsa". In tal caso, se si intende toouse putty.exe Windows tooconnect tooa distribuzione Linux, utilizzare "rsa" o "dsa".

**Provisioning.MonitorHostName:**  
Tipo: booleano  
Predefinito: y

Se impostato, waagent eseguito il monitoraggio macchina virtuale di Linux hello per le modifiche di nome host (come restituito dal comando "hostname" hello) e Aggiorna configurazione di rete hello nella modifica di hello immagine tooreflect hello. In nome hello toopush modificare toohello i server DNS, rete verrà riavviata nella macchina virtuale hello. causando una breve interruzione nella connettività Internet.

**Provisioning.DecodeCustomData**  
Tipo: booleano  
Predefinito: n

Se impostato, waagent decodificherà CustomData da Base64.

**Provisioning.ExecuteCustomData**  
Tipo: booleano  
Predefinito: n

Se impostato, waagent eseguirà CustomData dopo il provisioning.

**Provisioning.PasswordCryptId**  
Tipo: stringa  
Predefinito: 6

Algoritmo usato dalla crittografia durante la generazione di hash della password.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Tipo: stringa  
Predefinito: 10

Lunghezza di salt casuale usata durante la generazione di hash della password.

**ResourceDisk.Format:**  
Tipo: booleano  
Predefinito: y

Se impostato, il disco di risorsa hello fornito dalla piattaforma hello verrà formattato e montato da waagent se il tipo di file System hello richiesto dall'utente hello in "ResourceDisk.Filesystem" è diverso da "ntfs". Una singola partizione di tipo Linux (83) verrà resa disponibile su disco hello. Si noti che la partizione non verrà formattata se è possibile montarla correttamente.

**ResourceDisk.Filesystem:**  
Tipo: String  
Predefinito: ext4

Specifica il tipo di file System hello per il disco di risorsa hello. I valori supportati variano in base alla distribuzione Linux. Se la stringa hello X, quindi mkfs. X devono essere presenti nell'immagine Linux hello. Le immagini SLES 11 in genere utilizzano il valore 'ext3'. Le immagini FreeBSD in questo caso devono usare il valore 'ufs2'.

**ResourceDisk.MountPoint:**  
Tipo: String  
Predefinito: /mnt/resource 

Specifica il percorso di hello in corrispondenza del quale è stato montato il disco di risorsa hello. Si noti il disco di risorsa hello è un *temporaneo* del disco e può essere svuotata quando hello VM è deprovisioning.

**ResourceDisk.MountOptions**  
Tipo: String  
Predefinito: nessuno

Specifica disco montaggio opzioni toobe passato toohello montaggio -o comando. È un elenco di valori delimitato da virgole, ad esempio nodev,nosuid. Vedere montaggio(8) per informazioni dettagliate.

**ResourceDisk.EnableSwap:**  
Tipo: booleano  
Predefinito: n

Se impostato, un file di swapping (o file di scambio) viene creato nel disco di risorsa hello e aggiungere spazio di swapping sistema toohello.

**ResourceDisk.SwapSizeMB:**  
Tipo: numero intero  
Predefinito: 0

dimensioni Hello del file di swapping hello in megabyte.

**Logs.Verbose:**  
Tipo: booleano  
Predefinito: n

Se questa voce è impostata, viene incrementato il livello di dettaglio del log. Comando Waagent registra too/var/log/waagent.log e sfrutta hello sistema logrotate funzionalità toorotate log.

**OS.EnableRDMA**  
Tipo: booleano  
Predefinito: n

Se impostato, hello agente verrà tenta tooinstall e quindi caricare un driver del kernel RDMA corrispondente versione di hello del firmware hello in hello hardware sottostante.

**OS.RootDeviceScsiTimeout:**  
Tipo: numero intero  
Predefinito: 300

Consente di configurare hello SCSI timeout in secondi in unità disco e i dati di hello del sistema operativo. Se non è impostato, il sistema hello vengono utilizzati valori predefiniti.

**OS.OpensslPath:**  
Tipo: String  
Predefinito: nessuno

Può essere utilizzato toospecify un percorso alternativo per toouse binario di openssl hello per le operazioni di crittografia.

**HttpProxy.Host, HttpProxy.Port**  
Tipo: String  
Predefinito: nessuno

Se impostato, hello agente utilizzerà questo proxy server tooaccess hello internet. 

## <a name="ubuntu-cloud-images"></a>Immagini di Ubuntu Cloud
Si noti che le immagini Cloud Ubuntu utilizzare [cloud init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform hello di molte attività di configurazione che, in caso contrario, viene gestita da agente Linux di Azure.  Si noti hello seguenti differenze:

* **Provisioning.Enabled** troppo "n" in Ubuntu Cloud immagini che utilizzano cloud init tooperform provisioning attività predefinite.
* Hello seguenti parametri di configurazione non hanno alcun effetto sulle immagini di Cloud Ubuntu che utilizzano cloud init toomanage hello risorsa spazio su disco e lo scambio:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Vedere hello dopo il punto di montaggio disco risorse tooconfigure hello risorse e scambiare spazio sulle immagini Cloud Ubuntu durante il provisioning:
  
  * [Ubuntu Wiki: Configurare partizioni di scambio](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Inserimento di dati personalizzati in una macchina virtuale di Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

