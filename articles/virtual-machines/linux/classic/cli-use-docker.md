---
title: hello aaaUsing estensione della macchina virtuale Docker per Linux in Azure
description: Descrive Docker ed estensioni di macchine virtuali di Azure hello e tooprogrammatically per la creazione di macchine virtuali in Azure che sono host docker dalla riga di comando di hello tramite hello CLI di Azure.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a>Utilizzo di hello estensione della macchina virtuale Docker da hello interfaccia della riga di comando di Azure (Azure CLI)
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sull'utilizzo di estensione della macchina virtuale Docker hello con modello di gestione risorse di hello, vedere [qui](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In questo argomento viene descritto come una macchina virtuale con hello estensione della macchina virtuale Docker da hello toocreate servizio la modalità di gestione (asm) in Azure CLI su qualsiasi piattaforma. [Docker](https://www.docker.com/) è uno dei hello approcci di virtualizzazione più diffusi che utilizza [contenitori di Linux](http://en.wikipedia.org/wiki/LXC) anziché le macchine virtuali come modalità di isolamento dei dati e di elaborazione per le risorse condivise. È possibile utilizzare l'estensione della macchina virtuale Docker hello e hello [agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate una macchina virtuale Docker che ospita qualsiasi numero di contenitori per le applicazioni in Azure. toosee una descrizione di alto livello dei contenitori e i relativi vantaggi, vedere hello [Docker elevato livello di lavagna](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a>Come toouse hello estensione della macchina virtuale Docker con Azure
estensione della macchina virtuale Docker toouse hello con Azure, è necessario installare una versione di hello [interfaccia della riga di comando di Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) superiore 0.8.6 (come di questo hello scrittura corrente versione 0.10.0). È possibile installare hello CLI di Azure in Windows, Mac e Linux.

processo completo di Hello toouse Docker in Azure è semplice:

* Installare hello CLI di Azure e le relative dipendenze nel computer di hello da cui si desidera toocontrol Azure (in Windows, questa è una distribuzione di Linux in esecuzione come macchina virtuale)
* Utilizzare toocreate i comandi di Docker CLI di Azure hello un host macchina virtuale Docker in Azure
* Utilizzare hello locale Docker comandi toomanage ai contenitori di Docker nella macchina virtuale Docker in Azure.

### <a name="install-hello-azure-command-line-interface-azure-cli"></a>Installare hello interfaccia della riga di comando di Azure (Azure CLI)
tooinstall e configurare hello CLI di Azure, vedere [come tooinstall hello interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md). installazione di hello tooconfirm, tipo `azure` al prompt dei comandi di hello e dopo un breve istante dovrebbe hello Azure CLI ASCII art, in cui sono elencati hello basic comandi tooyou disponibili. Se l'installazione hello funzionava correttamente, dovrebbe essere in grado di tootype `azure help vm` e verificare che uno dei comandi elencato hello è "docker".

> [!NOTE]
> Docker include strumenti per Windows, [Docker macchina](https://docs.docker.com/installation/windows/), che è anche possibile usare la creazione di hello tooautomate di un client di docker che è possibile utilizzare toowork con macchine virtuali di Azure come host docker.
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a>Connettersi hello Azure CLI tootooyour Account di Azure
Prima di poter usare hello CLI di Azure è necessario associare le credenziali dell'account Azure hello CLI di Azure sulla piattaforma. Hello sezione [come tooconnect tooyour sottoscrizione di Azure](../../../xplat-cli-connect.md) illustra tooeither scaricare e importare il **publishsettings** file o associare la CLI di Azure con un id organizzazione.

> [!NOTE]
> Esistono alcune differenze nel comportamento quando si utilizza uno o hello altri metodi di autenticazione, pertanto essere certi tooread hello documento sopra toounderstand funzionalità diverse di hello.
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a>Installare Docker e utilizzare hello estensione della macchina virtuale Docker per Azure
Seguire hello [le istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation) tooinstall Docker in locale nel computer.

toouse Docker con una macchina virtuale di Azure, immagine di Linux hello utilizzata per hello macchina virtuale deve avere hello [agente VM Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installato. Al momento esistono solo due tipi di immagine che offrono queste funzionalità:

* Un'immagine Ubuntu da hello raccolta immagini di Azure o
* Un'immagine personalizzata di Linux che è stato creato con l'agente VM Linux di Azure hello installato e configurato. Vedere [agente VM Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per ulteriori informazioni su come toobuild una VM Linux personalizzato con hello agente VM di Azure.

### <a name="using-hello-azure-image-gallery"></a>Utilizzo di hello raccolta immagini di Azure
Da una sessione Terminal o Bash, utilizzare il comando CLI di Azure toolocate hello immagine Ubuntu più recente in hello VM raccolta toouse digitando seguente hello

`azure vm image list | grep Ubuntu-14_04`

e selezionare uno dei nomi di immagine hello, ad esempio `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, e il comando che segue hello utilizzare toocreate una nuova macchina virtuale utilizzando tale immagine.

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

dove:

* *&lt;nome VM cloudservice&gt;*  nome hello di hello VM che verranno configurati come computer di host contenitore Docker hello in Azure
* *&lt;nome utente&gt;*  hello nomeutente dell'utente di radice predefinito hello di hello VM
* *&lt;password&gt;*  password hello di hello *username* account conforme agli standard di hello di complessità per Azure

> [!NOTE]
> Attualmente, una password deve essere di almeno 8 caratteri e contenere una lettera minuscola e una lettera maiuscola, un numero e un carattere speciale, ad esempio uno dei seguenti caratteri hello: `!@#$%^&+=`. No, il periodo di hello alla fine hello hello prima frase non è un carattere speciale.
> 
> 

Se il comando hello ha esito positivo, dovrebbe essere simile alla seguente hello, a seconda di argomenti di preciso hello e le opzioni utilizzate:

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> La creazione di una macchina virtuale può richiedere alcuni minuti, ma dopo è stato eseguito il provisioning (il valore di stato hello è `ReadyRole`) hello avvio di Docker daemon (Buongiorno servizio Docker) ed è possibile connettersi toohello host del contenitore Docker.
> 
> 

hello tootest macchina virtuale Docker è stato creato in Azure, tipo

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

dove  *&lt;vm-name--utilizzati&gt;*  hello nome della macchina virtuale hello utilizzato nella chiamata troppo`azure vm docker create`. Dovrebbe essere simile toohello seguenti, che indica che la macchina virtuale Host Docker sia attivo e in esecuzione in Azure e in attesa per i comandi. 

Ora è possibile provare tooconnect utilizzando le informazioni di tooobtain client docker (in alcune installazioni di client Docker, ad esempio che nel Mac, è possibile toouse `sudo`):

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

Solo toobe assicurarsi che sia di funzionare, è possibile esaminare hello macchina virtuale per l'estensione Docker hello:

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a>Autenticazione della VM host di Docker
Inoltre toocreating hello VM Docker, hello `azure vm docker create` comando crea automaticamente anche tooallow certificati necessari hello client computer tooconnect toohello Azure contenitore host Docker con HTTPS e i certificati di hello vengono archiviati sia Hello computer client e host, come appropriato. Durante i successivi tentativi, i certificati esistenti hello vengono riutilizzati e condivise con nuovo host hello.

Per impostazione predefinita, i certificati vengono inseriti nella `~/.docker`, e Docker sarà toorun configurato sulla porta **2376**. Se si desidera toouse una porta diversa o una directory, quindi è possibile utilizzare uno dei seguenti hello `azure vm docker create` tooconfigure opzioni della riga di comando del Docker contenitore host VM toouse una porta diversa o certificati diversi per la connessione client:

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

è configurato toolisten per Hello daemon Docker nell'host di hello e autenticare le connessioni sul hello specificato porta tramite hello certificati generati da hello client `azure vm docker create` comando. computer client Hello deve disporre di questi host Docker toohello di certificati toogain accesso.

> [!NOTE]
> Un host di rete in esecuzione senza questi certificati sarà vulnerabile tooanyone che può essere tooconnect toohello macchina. Prima di modificare una configurazione predefinita di hello, assicurarsi di aver compreso hello rischi tooyour computer e applicazioni.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Si è pronti toogo toohello [manuale dell'utente Docker] e usare la macchina virtuale Docker. toocreate una macchina virtuale Docker abilitati nel nuovo portale di hello, vedere [come toouse hello estensione della macchina virtuale Docker con hello portale].
* Hello estensione della macchina virtuale Docker di Azure supporta Docker Compose, che utilizza un dichiarativa YAML file tootake, un'applicazione modellata sviluppatore in qualsiasi ambiente e generare una distribuzione uniforme. Vedere [Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure].  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[come toouse hello estensione della macchina virtuale Docker con hello portale]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[manuale dell'utente Docker]:https://docs.docker.com/userguide/

[Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure]:../docker-compose-quickstart.md
