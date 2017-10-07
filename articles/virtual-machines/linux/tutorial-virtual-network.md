---
title: aaaAzure reti virtuali e macchine virtuali Linux | Documenti Microsoft
description: Esercitazione - gestire reti virtuali di Azure e macchine virtuali Linux con hello CLI di Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Gestire reti virtuali di Azure e macchine virtuali Linux con hello CLI di Azure

Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna. Questa esercitazione illustra la distribuzione di due macchine virtuali e la configurazione della rete di Azure per tali VM. esempi di Hello in questa esercitazione si presuppone che le macchine virtuali hello ospitano un'applicazione web con un database back-end, ma non viene distribuita un'applicazione di esercitazione hello. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Distribuire una rete virtuale
> * Creare una subnet in una rete virtuale
> * Associare subnet tooa macchine virtuali
> * Gestire gli indirizzi IP pubblici delle macchine virtuali
> * Proteggere il traffico Internet in ingresso
> * Proteggere il traffico tooVM VM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Panoramica della rete per le VM

Reti virtuali di Azure, consentire le connessioni di rete sicura tra macchine virtuali, hello internet e altri servizi di Azure, ad esempio database SQL di Azure. Le reti virtuali sono suddivise in segmenti logici denominati subnet. Subnet di flusso di rete toocontrol e come limite di sicurezza. Quando si distribuisce una macchina virtuale, in genere include un'interfaccia di rete virtuale, che è collegato tooa subnet.

## <a name="deploy-virtual-network"></a>Distribuire la rete virtuale

Per questa esercitazione viene creata una singola rete virtuale con due subnet: una subnet front-end per ospitare un'applicazione Web e una subnet back-end per ospitare un server di database.

Per poter creare una rete virtuale, creare prima di tutto un gruppo di risorse con [az group create](/cli/azure/group#create). esempio Hello crea un gruppo di risorse denominato *myRGNetwork* nel percorso eastus hello.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Creare una rete virtuale

Ci hello [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) toocreate comando una rete virtuale. In questo esempio è denominato rete hello *mvVnet* e viene assegnato un prefisso dell'indirizzo *10.0.0.0/16*. Viene anche creata una subnet con nome *mySubnetFrontEnd* e prefisso *10.0.1.0/24*. Più avanti in questa esercitazione una VM front-end è connesso toothis subnet. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Creare una subnet

Una nuova subnet viene aggiunto hello tramite la rete virtuale toohello [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create) comando. In questo esempio è denominato subnet hello *mySubnetBackEnd* e viene assegnato un prefisso dell'indirizzo *10.0.2.0/24*. Questa subnet verrà usata con tutti i servizi back-end.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

A questo punto, è stata creata una rete che è stata segmentata in due subnet, una per i servizi front-end e un'altra per i servizi back-end. Nella sezione successiva hello, macchine virtuali vengono create e subnet toothese collegate.

## <a name="understand-public-ip-address"></a>Informazioni sull'indirizzo IP pubblico

Un indirizzo IP pubblico consente toobe risorse di Azure accessibili su internet di hello. In questa sezione dell'esercitazione hello toodemonstrate come gli indirizzi toowork con indirizzo IP pubblico viene creata una VM.

### <a name="allocation-method"></a>Metodo di allocazione

Un indirizzo IP pubblico può essere allocato in modo dinamico o statico. Per impostazione predefinita, un indirizzo IP pubblico viene allocato in modo dinamico. Gli indirizzi IP dinamici vengono rilasciati quando una VM viene deallocata. Questo comportamento provoca toochange indirizzo IP di hello durante qualsiasi operazione che include la deallocazione di una macchina virtuale.

metodo di allocazione Hello può essere impostato toostatic, che assicura che l'indirizzo IP hello rimangono assegnati tooa macchina virtuale, anche durante uno stato deallocato. Quando si utilizza un indirizzo IP allocato in modo statico, non è specificato l'indirizzo IP hello stesso. e viene invece allocato da un pool di indirizzi disponibili.

### <a name="dynamic-allocation"></a>Allocazione dinamica

Quando si crea una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando hello predefinito pubblico IP indirizzo metodo di allocazione è dinamico. Nell'esempio seguente di hello, una macchina virtuale viene creata con un indirizzo IP dinamico. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Allocazione statica

Quando si crea una macchina virtuale utilizzando hello [creare vm az](/cli/azure/vm#create) comando, includere hello `--public-ip-address-allocation static` tooassign argomento un indirizzo IP pubblico statico. Questa operazione non viene dimostrata in questa esercitazione, tuttavia nella sezione successiva hello un indirizzo IP allocato in modo dinamico è tooa modificato in modo statico indirizzo allocato. 

### <a name="change-allocation-method"></a>Modificare il metodo di allocazione

metodo di allocazione degli indirizzi IP Hello può essere modificato utilizzando hello [aggiornamento public-ip di rete az](/cli/azure/network/public-ip#update) comando. In questo esempio hello metodo di allocazione degli indirizzi IP della VM front-end viene modificato hello toostatic.

In primo luogo, deallocare hello macchina virtuale.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Hello utilizzare [aggiornamento public-ip di rete az](/cli/azure/network/public-ip#update) metodo di allocazione hello tooupdate di comando. In questo caso, hello `--allocation-method` viene impostato troppo*statico*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Avviare hello macchina virtuale.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Nessun indirizzo IP pubblico

Spesso, una macchina virtuale non è necessario toobe accessibile tramite internet hello. una macchina virtuale senza un indirizzo IP pubblico, utilizzare hello toocreate `--public-ip-address ""` argomento con un set vuoto di virgolette doppie. Questa configurazione verrà illustrata più avanti in questa esercitazione.

## <a name="secure-network-traffic"></a>Proteggono il traffico di rete

Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooresources il traffico di rete connessa tooAzure reti virtuali (VNet). È possibile NSGs toosubnets associato o interfacce di rete singoli. Quando un gruppo è associata a un'interfaccia di rete, viene applicato solo hello associata macchina virtuale. Quando un gruppo è subnet tooa associato, hello regole tooall risorse toohello connesso subnet. 

### <a name="network-security-group-rules"></a>Regole dei gruppi di sicurezza di rete

Le regole dei gruppi di sicurezza di rete definiscono le porte di rete su cui il traffico viene consentito o negato. le regole di Hello possono includere intervalli di indirizzi IP di origine e di destinazione in modo che viene controllato il traffico tra sistemi specifici o subnet. Le regole dei gruppi di sicurezza di rete possono includere anche una priorità, compresa tra 1 e 4096. Le regole vengono valutate in ordine di hello di priorità. Una regola con priorità 100 viene valutata prima di una con priorità 200.

Tutti i gruppi di sicurezza di rete contengono un set di regole predefinite. le regole predefinite di Hello non possono essere eliminate, ma poiché vengono assegnati priorità più bassa hello, possono essere sostituite dalle regole di hello creati.

- **Rete virtuale**: il traffico che ha origine e termina in una rete virtuale è consentito sia in ingresso che in uscita.
- **Internet**: il traffico in uscita è consentito, mentre il traffico in ingresso viene bloccato.
- **Bilanciamento del carico** -integrità hello tooprobe di Azure consente carico bilanciamento del carico delle macchine virtuali e istanze del ruolo. Se non si usa un set con bilanciamento del carico, è possibile eseguire l'override di questa regola.

### <a name="create-network-security-groups"></a>Creare gruppi di sicurezza di rete

Un gruppo di sicurezza di rete può essere creato in hello stesso tempo come una macchina virtuale tramite hello [creare vm az](/cli/azure/vm#create) comando. In tal caso, hello NSG è associata a interfaccia di rete di macchine virtuali hello e una regola di gruppo viene creato automaticamente tooallow traffico sulla porta *22* da qualsiasi origine. In precedenza in questa esercitazione, hello NSG front-end è stato creato automaticamente con hello VM front-end. È stata anche creata automaticamente una regola del gruppo di sicurezza di rete per la porta 22. 

In alcuni casi, potrebbe essere utile toopre-creare un gruppo, ad esempio quando le regole SSH predefinite non possono essere create o quando hello gruppo deve essere collegato tooa subnet. 

Hello utilizzare [rete az creare](/cli/azure/network/nsg#create) comando toocreate un gruppo di sicurezza di rete.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Invece di associazione di interfaccia di rete tooa NSG hello è associata a una subnet. In questa configurazione, tutte le VM che è collegato toohello subnet eredita le regole NSG hello.

Aggiornare una subnet esistente di hello denominata *mySubnetBackEnd* con hello nuovo gruppo.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Creare una macchina virtuale, che è collegato toohello *mySubnetBackEnd*. Si noti che hello `--nsg` argomento ha un valore di virgolette doppie. Un gruppo non è necessario toobe creato con hello macchina virtuale. Hello VM è subnet back-end toohello collegati, che è protetta con hello back-end gruppo creato in precedenza. Questo gruppo si applica toohello macchina virtuale. Inoltre, noterete che hello `--public-ip-address` argomento ha un valore di virgolette doppie. Questa configurazione crea una VM senza un indirizzo IP pubblico. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Proteggere il traffico in ingresso

Quando hello VM front-end è stato creato, è stata creata una regola di NSG tooallow il traffico in entrata sulla porta 22. Questa regola consente toohello connessioni SSH macchina virtuale. Per questo esempio deve essere consentito il traffico anche sulla porta *80*. Questa configurazione consente una toobe di applicazione web accede hello macchina virtuale.

Hello utilizzare [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) toocreate comando una regola per la porta *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Hello VM front-end è ora accessibile solo sulla porta *22* e la porta *80*. Tutto il traffico in ingresso viene bloccato nel gruppo di sicurezza di rete hello. Potrebbe essere utile toovisualize configurazioni delle regole di hello gruppo. Configurazione delle regole di NSG hello restituito con hello [elenco regole di rete az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Output:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Proteggere il traffico tooVM VM

Le regole dei gruppi di sicurezza di rete possono essere applicate anche tra VM. In questo esempio hello VM front-end deve toocommunicate con hello VM back-end sulla porta *22* e *3306*. Questa configurazione consente le connessioni SSH da hello VM front-end e inoltre consentire un'applicazione hello toocommunicate VM front-end con un database MySQL di back-end. Bloccare tutto il traffico tra le macchine virtuali front-end e back-end hello.

Hello utilizzare [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) toocreate comando una regola per la porta 22. Si noti che hello `--source-address-prefix` argomento specifica un valore di *10.0.1.0/24*. Questa configurazione assicura che solo il traffico dalla subnet front-end hello è consentito attraverso hello gruppo.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Aggiungere ora una regola per il traffico MySQL sulla porta 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Infine, perché NSGs dispone di una regola predefinita che consente tutto il traffico tra macchine virtuali in hello stessa rete virtuale, creare una regola può essere per hello back-end NSGs tooblock tutto il traffico. Noterete che hello `--priority` viene assegnato un valore di *300*, che è inferiore che entrambi hello MySQL e gruppo di regole. Questa configurazione assicura che il traffico SSH e MySQL è ancora consentito attraverso hello gruppo.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Hello VM back-end è ora accessibile solo sulla porta *22* e la porta *3306* dalla subnet front-end hello. Tutto il traffico in ingresso viene bloccato nel gruppo di sicurezza di rete hello. Potrebbe essere utile toovisualize configurazioni delle regole di hello gruppo. Configurazione delle regole di NSG hello restituito con hello [elenco regole di rete az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Output:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è creato e protetto reti di Azure come macchine toovirtual correlati. Si è appreso come:

> [!div class="checklist"]
> * Distribuire una rete virtuale
> * Creare una subnet in una rete virtuale
> * Associare subnet tooa macchine virtuali
> * Gestire gli indirizzi IP pubblici delle macchine virtuali
> * Proteggere il traffico Internet in ingresso
> * Proteggere il traffico tooVM VM

Spostare toohello toolearn esercitazione successiva sulla protezione dei dati su macchine virtuali tramite backup di Azure. 

> [!div class="nextstepaction"]
> [Eseguire il backup di macchine virtuali Linux in Azure](./tutorial-backup-vms.md)
