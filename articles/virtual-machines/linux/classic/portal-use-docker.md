---
title: Estensione della macchina virtuale Docker per Linux aaaUsing | Documenti Microsoft
description: Viene descritto Docker e alle estensioni di macchine virtuali di Azure hello e come macchine virtuali di Azure che sono host docker utilizzando toocreate hello CLI di Azure nel modello di distribuzione classica.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a>Con estensione della macchina virtuale Docker hello hello portale di Azure classico
> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

[Docker](https://www.docker.com/) è uno dei hello approcci di virtualizzazione più diffusi che utilizza [contenitori di Linux](http://en.wikipedia.org/wiki/LXC) anziché le macchine virtuali come modalità di isolamento dei dati e di elaborazione per le risorse condivise. È possibile utilizzare l'estensione della macchina virtuale Docker hello gestiti da [agente Linux di Azure] toocreate una macchina virtuale Docker che ospita qualsiasi numero di contenitori per le applicazioni in Azure.

> [!NOTE]
> In questo argomento viene descritto come toocreate una macchina virtuale Docker da hello portale di Azure classico. toosee toocreate una macchina virtuale Docker hello riga di comando, vedere [come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello]. toosee una descrizione di alto livello dei contenitori e i relativi vantaggi, vedere hello [Docker elevato livello di lavagna](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a>Creare una nuova macchina virtuale da hello raccolta immagini
primo passaggio Hello richiede una macchina virtuale di Azure da un'immagine Linux che supporta hello estensione della macchina virtuale Docker, utilizzando un'immagine Ubuntu 14.04 LTS da hello raccolta immagini come un'immagine server di esempio e Ubuntu 14.04 Desktop come un client. Nel portale di hello, fare clic su **+ nuovo** in hello in basso a sinistra angolo toocreate una nuova istanza della macchina virtuale e selezionare un'immagine Ubuntu 14.04 LTS selezioni hello disponibile o da hello completare la raccolta di immagini, come illustrato di seguito.

> [!NOTE]
> Attualmente, solo le immagini Ubuntu 14.04 LTS più recenti di luglio 2014 supportano hello estensione della macchina virtuale Docker.
> 
> 

![Creare una nuova immagine Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a>Creare i certificati Docker
Dopo avere hello che VM è stato creato, assicurarsi che Docker sia installato nel computer client. (per informazioni dettagliate, vedere le [istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation)).

Creare i file di certificato e la chiave per la comunicazione di Docker in base troppo hello[in esecuzione di Docker con https] e posizionarli nel hello  **`~/.docker`**  directory sul computer client.

> [!NOTE]
> attualmente, Hello Docker estensione della macchina virtuale nel portale di hello richiede credenziali con codificata base 64.
> 
> 

Riga di comando hello, utilizzare  **`base64`**  o preferito di un'altra codifica negli argomenti strumento toocreate con codifica base64. Eseguire questa operazione con un semplice set di file di certificato e la chiave potrebbe essere toothis simile:

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a>Aggiungere l'estensione della macchina virtuale Docker hello
tooadd hello estensione della macchina virtuale Docker, individuare l'istanza VM hello creata e scorrere verso il basso troppo**estensioni** e farvi clic sopra toobring estensioni VM, come illustrato di seguito.

> [!NOTE]
> Questa funzionalità è supportata nel portale di anteprima hello solo: https://portal.azure.com/
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a>Aggiungere un'estensione
Fare clic su hello **+ Aggiungi** toodisplay hello possibili estensioni VM è possibile aggiungere toothis macchina virtuale.

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a>Selezionare l'estensione della macchina virtuale Docker hello
Scegliere l'estensione della macchina virtuale Docker, che comporta la descrizione di Docker hello e collegamenti importanti, hello e quindi fare clic su **crea** alla procedura di installazione hello toobegin hello inferiore.

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a>Aggiungere il certificato e i file di chiave:
Nei campi modulo hello, immettere le versioni hello con codifica base64 del certificato CA, il certificato Server e la chiave del Server, come illustrato nella seguente immagine hello.

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> Si noti che (ad esempio hello prima immagine) hello 2376 viene compilato per impostazione predefinita. È possibile immettere qui qualsiasi endpoint, ma passaggio successivo hello sarà tooopen backup hello endpoint corrispondente. Se si modifica l'impostazione predefinita di hello, assicurarsi che tooopen backup hello corrispondenti endpoint nel passaggio successivo hello.
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a>Aggiungere hello Endpoint di comunicazione di Docker
Quando si visualizza il gruppo di risorse hello è stato creato, selezionare il gruppo di sicurezza di rete associato con la macchina virtuale hello e fare clic su **le regole di sicurezza in ingresso** tooview hello regole come illustrato di seguito.

![](media/portal-use-docker/AddingEndpoint.png)

Fare clic su **+ Aggiungi** tooadd un'altra regola, nel caso predefinito hello, immettere un nome per l'endpoint di hello (in questo esempio, **Docker**) e 2376 'intervallo porte di destinazione'. Impostare con valore di protocollo hello **TCP**, fare clic su **OK** regola hello toocreate.

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a>Testare il client Docker e l'host Docker di Azure
Individuare e copiare hello nome di dominio della macchina virtuale e nella riga di comando hello del computer client, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (dove *dockerextension* viene sostituito da hello sottodominio per la macchina virtuale).

risultato Hello dovrebbe apparire simile toothis:

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

Dopo aver completato hello sopra passaggi, è ora un host Docker completamente funzionale in esecuzione in una macchina virtuale di Azure, configurato toobe connesso tooremotely da altri client.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
Si è pronti toogo toohello [manuale dell'utente Docker] e usare la macchina virtuale Docker. Se si desidera tooautomate creazione host Docker in macchine virtuali di Azure tramite l'interfaccia della riga di comando, vedere [come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello]

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux di Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[in esecuzione di Docker con https]:http://docs.docker.com/articles/https/
[manuale dell'utente Docker]:https://docs.docker.com/userguide/
