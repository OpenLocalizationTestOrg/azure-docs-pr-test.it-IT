---
title: una rete virtuale di Azure (versione classica) - file di configurazione di rete aaaConfigure | Documenti Microsoft
description: Informazioni su come toocreate e modificare le reti virtuali (classico) per l'esportazione, la modifica e l'importazione di un file di configurazione di rete.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Configurare una rete virtuale (classica) usando un file di configurazione di rete
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano modello di distribuzione di gestione risorse di hello più nuove distribuzioni.

È possibile creare e configurare una rete virtuale (versione classica) con un file di configurazione di rete mediante hello Azure interfaccia della riga di comando (CLI) 1.0 o Azure PowerShell. È possibile creare o modificare una rete virtuale e modello di distribuzione Azure Resource Manager hello usando un file di configurazione di rete. Impossibile utilizzare hello toocreate portale Azure o modificare una rete virtuale (classico) usando un file di configurazione di rete, ma è possibile utilizzare hello toocreate portale Azure una rete virtuale (classica), senza utilizzare un file di configurazione di rete.

Creazione e configurazione di una rete virtuale (versione classica) con un file di configurazione di rete richiede l'esportazione, la modifica e l'importazione di file hello.

## <a name="export"></a>Esportare un file di configurazione di rete

È possibile utilizzare PowerShell o hello tooexport CLI di Azure un file di configurazione di rete. PowerShell consente di esportare un file XML, mentre hello CLI di Azure consente di esportare un file json.

### <a name="powershell"></a>PowerShell
 
1. [Installare Azure PowerShell e accedere tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Cambiare directory hello (e verificare sia presente) e nome file nella hello seguendo comando come desiderato, quindi esecuzione hello comando tooexport hello rete file di configurazione:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

1. [Installare hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Completare hello rimanenti passaggi da un prompt dei comandi CLI di Azure 1.0.
2. Accedere tooAzure immettendo hello `azure login` comando.
3. Verificare che si è in modalità asm immettendo hello `azure config mode asm` comando.
4. Cambiare directory hello (e verificare sia presente) e nome file nella hello seguendo comando come desiderato, quindi esecuzione hello comando tooexport hello rete file di configurazione:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Creare o modificare un file di configurazione di rete

Un file di configurazione di rete è un file XML (quando si usa PowerShell) o un file json (quando si usa hello CLI di Azure). È possibile modificare il file hello in qualsiasi editor di testo, o XML/json. Hello [impostazioni dello schema di file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx) articolo include informazioni dettagliate per tutte le impostazioni. Per una spiegazione aggiuntiva delle impostazioni di hello, vedere [visualizzare le reti virtuali e le impostazioni](virtual-network-manage-network.md#view-vnet). Hello modifiche apportate toohello file:

- Deve essere conforme con schema hello o rete hello l'importazione avrà esito negativo file di configurazione.
- Sovrascrivono le impostazioni di rete esistenti per la sottoscrizione, pertanto è necessario prestare attenzione alle modifiche che si apportano. Ad esempio, fare riferimento a file di configurazione con i rete esempio hello che seguono. Ad esempio il file originale di hello contiene due **VirtualNetworkSite** istanze e si modifica, come illustrato negli esempi di hello. Quando si importa il file hello, Azure consente di eliminare la rete virtuale di hello per hello **VirtualNetworkSite** istanza è stata rimossa nel file hello. Questo scenario semplificato presuppone alcuna risorsa sono state nella rete virtuale hello, come se fossero presenti, non è stato possibile eliminare la rete virtuale hello e importazione hello avrà esito negativo.

> [!IMPORTANT]
> Azure considera una subnet è distribuito tooit come **in uso**. Quando una subnet è in uso, non può essere modificata. Prima di modificare le informazioni sulla subnet in un file di configurazione di rete, spostare tutto ciò che è stato distribuito toohello subnet tooa subnet che non venga modificata. Vedere [spostare una Subnet diversa di tooa macchina virtuale o istanza del ruolo](virtual-networks-move-vm-role-to-subnet.md) per informazioni dettagliate.

### <a name="example-xml-for-use-with-powershell"></a>XML di esempio da usare con PowerShell

Hello seguente file di configurazione di rete di esempio viene creata una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi *10.0.0.0/16* in hello *Stati Uniti orientali* Azure area. rete virtuale Hello contiene una subnet denominata *mySubnet* con un prefisso dell'indirizzo *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Se file di configurazione di rete hello esportato non contiene alcun contenuto, è possibile copiare hello XML nell'esempio precedente hello e incollarlo in un nuovo file.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Esempio JSON per l'utilizzo con hello Azure CLI 1.0

Hello seguente file di configurazione di rete di esempio viene creata una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi *10.0.0.0/16* in hello *Stati Uniti orientali* Azure area. rete virtuale Hello contiene una subnet denominata *mySubnet* con un prefisso dell'indirizzo *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Se file di configurazione di rete hello esportato non contiene alcun contenuto, è possibile copiare hello json nell'esempio precedente hello e incollarlo in un nuovo file.

## <a name="import"></a>Importare un file di configurazione di rete

È possibile utilizzare PowerShell o hello tooimport CLI di Azure un file di configurazione di rete. PowerShell Importa un file XML, mentre hello Azure CLI Importa un file json. Se hello importazione non riesce, verificare il file hello è conforme con hello [dello schema di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Installare Azure PowerShell e accedere tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Cambiare directory hello e il nome in hello seguente comando in base alle esigenze, quindi eseguire il file di configurazione rete hello comando tooimport hello:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Interfaccia della riga di comando di Azure 1.0

1. [Installare hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Completare hello rimanenti passaggi da un prompt dei comandi CLI di Azure 1.0.
2. Accedere tooAzure immettendo hello `azure login` comando.
3. Verificare che si è in modalità asm immettendo hello `azure config mode asm` comando.
4. Cambiare directory hello e il nome in hello seguente comando in base alle esigenze, quindi eseguire il file di configurazione rete hello comando tooimport hello:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
