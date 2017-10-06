---
title: Avvio rapido - aaaAzure creare VM portale | Documenti Microsoft
description: Avvio rapido in Azure - Creare un portale di VM
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>Creare una macchina virtuale Linux con hello portale di Azure

Macchine virtuali di Azure può essere create tramite hello portale di Azure. Questo metodo fornisce un'interfaccia utente basata sul browser per la creazione e la configurazione delle macchine virtuali e di tutte le risorse correlate. Questa procedura di avvio rapido tramite la creazione di una macchina virtuale e l'installazione di un server Web in hello VM.

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

## <a name="create-ssh-key-pair"></a>Creare una coppia di chiavi SSH

È necessario un toocomplete coppia di chiavi SSH questa Guida introduttiva. Se è già disponibile una coppia di chiavi SSH, questo passaggio può essere ignorato.

Da una shell Bash, eseguire questo comando e seguire hello le direzioni. output del comando Hello include il nome file hello del file di chiave pubblica hello. Copiare hello contenuto degli Appunti toohello di hello file di chiave pubblica.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>Accedi tooAzure 

Accedi toohello portale di Azure all'indirizzo http://portal.azure.com.

## <a name="create-virtual-machine"></a>Crea macchina virtuale

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Selezionare **Calcolo** e quindi **Ubuntu Server 16.04 LTS**. 

3. Immettere le informazioni di hello macchina virtuale. In **Tipo di autenticazione** selezionare **Chiave pubblica SSH**. Durante l'operazione Incolla nella propria chiave pubblica SSH, prestare attenzione tooremove tutti gli spazi iniziali o finali. Al termine fare clic su **OK**.

    ![Immettere le informazioni di base di una macchina virtuale nel pannello portale hello](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. Selezionare una dimensione per hello macchina virtuale. Selezionare altre dimensioni, toosee **visualizzare tutti** o modificare hello **il tipo di disco supportati** filtro. 

    ![Screenshot che mostra le dimensioni delle VM](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Nel pannello impostazioni hello, mantenere i valori predefiniti di hello e fare clic su **OK**.

6. Nella pagina Riepilogo hello, fare clic su **Ok** distribuzione della macchina virtuale toostart hello.

7. Hello VM sarà bloccato toohello dashboard del portale di Azure. Una volta completata la distribuzione di hello, verrà aperta automaticamente pannello riepilogo di hello macchina virtuale.


## <a name="connect-toovirtual-machine"></a>Connettere la macchina toovirtual

Creare una connessione SSH con la macchina virtuale hello.

1. Fare clic su hello **Connetti** pulsante sul pannello delle macchine virtuali hello. Hello connettersi pulsante consente di visualizzare una stringa di connessione SSH che può essere una macchina virtuale di toohello tooconnect utilizzato.

    ![Portale 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. Comando che segue di esecuzione hello toocreate una sessione SSH. Sostituire la stringa di connessione hello con hello che uno è stato copiato da hello portale di Azure.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>Installare NGINX

Seguente hello utilizzare origini dei pacchetti tooupdate script bash e installare il pacchetto NGINX più recente di hello. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

Al termine, uscire dalla sessione SSH hello e restituire le proprietà della VM hello in hello portale di Azure.


## <a name="open-port-80-for-web-traffic"></a>Aprire la porta 80 per il traffico Web 

Un gruppo di sicurezza di rete (NSG) consente il traffico in ingresso e in uscita. Quando una macchina virtuale viene creata dal portale di Azure hello, viene creata una regola in entrata sulla porta 22 per le connessioni SSH. Poiché questa macchina virtuale ospita un server Web, una regola di gruppo deve toobe creato per la porta 80.

1. Nella macchina virtuale hello, fare clic sul nome hello di hello **gruppo di risorse**.
2. Seleziona hello **il gruppo di sicurezza di rete**. Hello gruppo può essere identificato utilizzando hello **tipo** colonna. 
3. Nel menu a sinistra di hello, in impostazioni, fare clic su **sicurezza regole connessioni in entrata**.
4. Fare clic su **Aggiungi**.
5. In **Nome** digitare **http**. Assicurarsi che **intervallo di porte** è impostato too80 e **azione** è troppo**Consenti**. 
6. Fare clic su **OK**.


## <a name="view-hello-nginx-welcome-page"></a>Pagina iniziale di visualizzazione hello NGINX

Con NGINX installato e la porta 80 aprire tooyour VM, server Web hello è ora possibile accedere da hello internet. Aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale. indirizzo IP pubblico Hello è reperibile nel pannello VM hello in hello portale di Azure.

![Sito NGINX predefinito](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Pulire le risorse

Quando non è più necessario, eliminare il gruppo di risorse hello, macchina virtuale e tutte le risorse correlate. toodo in tal caso, selezionare il gruppo di risorse di hello dal pannello della macchina virtuale hello e fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web. toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali Linux.

> [!div class="nextstepaction"]
> [Esercitazioni per le macchine virtuali di Linux in Azure](./tutorial-manage-vm.md)
