---
title: "aaaVM con più indirizzi IP mediante Azure CLI 1.0 hello | Documenti Microsoft"
description: "Informazioni su come tooassign più gli indirizzi IP tooa macchina virtuale utilizzando hello Azure CLI 1.0 | Gestore delle risorse."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Assegnare più indirizzi IP macchine toovirtual mediante Azure CLI 1.0

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

In questo articolo viene illustrato come una macchina virtuale (VM) tramite il modello di distribuzione Azure Resource Manager hello utilizzando toocreate hello Azure CLI 1.0. Impossibile assegnare più indirizzi IP tooresources creato tramite il modello di distribuzione classica hello. ulteriori informazioni sui modelli di distribuzione di Azure, leggere hello toolearn [comprendere i modelli di distribuzione](../resource-manager-deployment-model.md) articolo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Creare una macchina virtuale con più indirizzi IP

È possibile completare questa attività usando hello Azure CLI 1.0 (in questo articolo) o hello [CLI di Azure 2.0](virtual-network-multiple-ip-addresses-cli.md). passaggi di Hello che seguono viene illustrato come toocreate un esempio di macchina virtuale con più IP risolve, come descritto nello scenario di hello. Modificare i nomi delle variabili e i tipi di indirizzi IP come richiesto per l'implementazione.

1. Installare e configurare Azure CLI 1.0 da hello seguente passaggi hello in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo e accedere al proprio account Azure con hello `azure-login` comando.

2. Creare un gruppo di risorse:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Creare una rete virtuale:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Creare una subnet nella rete virtuale hello:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Creare un account di archiviazione per hello macchina virtuale. Prima di eseguire hello seguente comando, sostituire *mystorageaccount* con un nome univoco. nome Hello deve essere univoco in Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Creare hello le configurazioni IP, una scheda di rete e assegnare hello IP configurazioni toohello scheda NIC. È possibile aggiungere, rimuovere o modificare le configurazioni di hello in base alle esigenze. Hello le configurazioni seguenti è descritti nello scenario hello:

    **IPConfig-1**

    Immettere i comandi che seguono toocreate hello:

    - Una risorsa indirizzo IP pubblico con un indirizzo IP pubblico statico
    - Una scheda di rete, assegnazione di indirizzo IP pubblico hello e una tooit di indirizzo IP privato statico.
    
    Sostituire *mypublicdns* con un nome univoco all'interno di hello località di Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.

    **IPConfig-2**

     Immettere i seguenti comandi toocreate hello una nuova risorsa di indirizzo IP pubblica e una nuova configurazione IP con un indirizzo IP pubblico statico e un indirizzo IP privato statico:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Immettere i seguenti comandi toocreate una configurazione IP con un indirizzo IP privato statico e alcun indirizzo IP pubblico hello:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Anche se in questo articolo assegna tutti tooa di configurazioni IP singola scheda di rete, è inoltre possibile assegnare più tooany di configurazioni IP NIC in una macchina virtuale. la modalità di lettura di una macchina virtuale con più schede di rete, toocreate toolearn hello crea una macchina virtuale con più schede di rete articolo.

7. Creare una macchina virtuale Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello v2 tooStandard DS2 dimensioni di macchina virtuale, ad esempio, aggiungere semplicemente hello seguente proprietà `--vm-size Standard_DS3_v2` toohello `azure vm create` comando nel passaggio 6.

8. Immettere hello successivo comando tooview hello NIC e hello configurazioni IP associate:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Toohello macchina virtuale del sistema operativo di indirizzi IP privati di Aggiungi hello completando i passaggi di hello del sistema operativo in hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo.

## <a name="add"></a>Aggiungere tooa di indirizzi IP VM

È possibile aggiungere ulteriori pubbliche e private IP indirizzi tooan esistente NIC completando i passaggi di hello che seguono. esempi di Hello si basano su hello [scenario](#Scenario) descritto in questo articolo.

1. Aprire CLI di Azure e completa hello rimanenti passaggi in questa sezione all'interno di una singola sessione CLI. Se si dispone già di Azure CLI installato e configurato, hello completato i passaggi in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articolo e accedere al proprio account Azure.

2. Completare i passaggi di hello in uno di hello le sezioni, in base ai requisiti seguenti:

    - **Aggiungere un indirizzo IP privato**
    
        tooadd un tooa di indirizzo IP privato NIC, è necessario creare una configurazione IP utilizzando hello comando riportato di seguito. indirizzo statico Hello deve essere un indirizzo per subnet hello inutilizzato.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Creare tutte le configurazioni usando nomi di configurazione univoci e indirizzi IP privati (per le configurazioni con indirizzi IP statici).

    - **Aggiungere un indirizzo IP pubblico**
    
        Viene aggiunto un indirizzo IP pubblico associandolo tooeither una nuova configurazione IP o una configurazione IP esistente. Completare i passaggi di hello nelle sezioni che seguono, hello necessari.

        > [!NOTE]
        > Per gli indirizzi IP pubblici è prevista una tariffa nominale. ulteriori informazioni su IP indirizzo sui prezzi, toolearn leggere hello [dei prezzi di indirizzo IP](https://azure.microsoft.com/pricing/details/ip-addresses) pagina. È un toohello limita il numero di indirizzi IP pubblici che può essere usato in una sottoscrizione. informazioni sui limiti di hello, leggere hello toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) articolo.
        >

        **Associare hello risorsa tooa nuova configurazione IP**
    
        Ogni volta che si aggiunge un indirizzo IP pubblico a una nuova configurazione IP, è necessario aggiungere anche un indirizzo IP privato, perché tutte le configurazioni IP devono avere un indirizzo IP privato. È possibile aggiungere una risorsa indirizzo IP pubblico esistente o crearne una nuova. toocreate uno nuovo, immettere hello comando seguente:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        una nuova configurazione IP con un indirizzo IP privato statico e hello associata toocreate *myPublicIP3* indirizzo IP pubblico risorsa degli indirizzi, immettere hello comando seguente:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Associare risorse hello tooan esistente configurazione IP**

        Una risorsa di indirizzo IP pubblica può essere solo la configurazione IP tooan associato che non ha ancora associata. È possibile determinare se una configurazione IP è un indirizzo IP pubblico associato immettendo hello comando seguente:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Cerca un toohello simile di riga che segue per IPConfig-3 nell'output restituito hello:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Poiché hello **indirizzo IP pubblico** colonna per *IpConfig 3* è vuoto, nessuna risorsa dell'indirizzo IP pubblica è tooit attualmente associato. È possibile aggiungere un esistente pubblica IP indirizzo risorsa tooIpConfig-3 o immettere hello toocreate comando uno di seguito:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Immettere hello comando risorsa toohello configurazione IP esistente denominato di indirizzo IP pubblico di tooassociate hello seguente *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Visualizzare gli indirizzi IP privati hello e hello pubblica IP indirizzo risorse assegnato toohello NIC immettendo hello comando seguente:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Hello ha restituito l'output è simile toohello seguenti:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Aggiungere indirizzi IP privati hello è stato aggiunto il sistema operativo VM di toohello NIC toohello seguendo le istruzioni hello hello [aggiungere indirizzi del sistema operativo VM tooa](#os-config) sezione di questo articolo. Non aggiungere hello pubblica IP indirizzi toohello del sistema operativo.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
