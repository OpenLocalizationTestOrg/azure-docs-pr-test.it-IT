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
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="6befe-103">Configurare una rete virtuale (classica) usando un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="6befe-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6befe-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6befe-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="6befe-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="6befe-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6befe-106">Si consiglia di utilizzano modello di distribuzione di gestione risorse di hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="6befe-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="6befe-107">È possibile creare e configurare una rete virtuale (versione classica) con un file di configurazione di rete mediante hello Azure interfaccia della riga di comando (CLI) 1.0 o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6befe-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="6befe-108">È possibile creare o modificare una rete virtuale e modello di distribuzione Azure Resource Manager hello usando un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="6befe-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="6befe-109">Impossibile utilizzare hello toocreate portale Azure o modificare una rete virtuale (classico) usando un file di configurazione di rete, ma è possibile utilizzare hello toocreate portale Azure una rete virtuale (classica), senza utilizzare un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="6befe-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="6befe-110">Creazione e configurazione di una rete virtuale (versione classica) con un file di configurazione di rete richiede l'esportazione, la modifica e l'importazione di file hello.</span><span class="sxs-lookup"><span data-stu-id="6befe-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="6befe-111"><a name="export"></a>Esportare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="6befe-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="6befe-112">È possibile utilizzare PowerShell o hello tooexport CLI di Azure un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="6befe-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="6befe-113">PowerShell consente di esportare un file XML, mentre hello CLI di Azure consente di esportare un file json.</span><span class="sxs-lookup"><span data-stu-id="6befe-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="6befe-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6befe-114">PowerShell</span></span>
 
1. <span data-ttu-id="6befe-115">[Installare Azure PowerShell e accedere tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6befe-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="6befe-116">Cambiare directory hello (e verificare sia presente) e nome file nella hello seguendo comando come desiderato, quindi esecuzione hello comando tooexport hello rete file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="6befe-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="6befe-117">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6befe-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="6befe-118">[Installare hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6befe-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="6befe-119">Completare hello rimanenti passaggi da un prompt dei comandi CLI di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="6befe-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="6befe-120">Accedere tooAzure immettendo hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="6befe-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="6befe-121">Verificare che si è in modalità asm immettendo hello `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="6befe-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="6befe-122">Cambiare directory hello (e verificare sia presente) e nome file nella hello seguendo comando come desiderato, quindi esecuzione hello comando tooexport hello rete file di configurazione:</span><span class="sxs-lookup"><span data-stu-id="6befe-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="6befe-123">Creare o modificare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="6befe-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="6befe-124">Un file di configurazione di rete è un file XML (quando si usa PowerShell) o un file json (quando si usa hello CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="6befe-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="6befe-125">È possibile modificare il file hello in qualsiasi editor di testo, o XML/json.</span><span class="sxs-lookup"><span data-stu-id="6befe-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="6befe-126">Hello [impostazioni dello schema di file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx) articolo include informazioni dettagliate per tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6befe-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="6befe-127">Per una spiegazione aggiuntiva delle impostazioni di hello, vedere [visualizzare le reti virtuali e le impostazioni](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="6befe-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="6befe-128">Hello modifiche apportate toohello file:</span><span class="sxs-lookup"><span data-stu-id="6befe-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="6befe-129">Deve essere conforme con schema hello o rete hello l'importazione avrà esito negativo file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6befe-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="6befe-130">Sovrascrivono le impostazioni di rete esistenti per la sottoscrizione, pertanto è necessario prestare attenzione alle modifiche che si apportano.</span><span class="sxs-lookup"><span data-stu-id="6befe-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="6befe-131">Ad esempio, fare riferimento a file di configurazione con i rete esempio hello che seguono.</span><span class="sxs-lookup"><span data-stu-id="6befe-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="6befe-132">Ad esempio il file originale di hello contiene due **VirtualNetworkSite** istanze e si modifica, come illustrato negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="6befe-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="6befe-133">Quando si importa il file hello, Azure consente di eliminare la rete virtuale di hello per hello **VirtualNetworkSite** istanza è stata rimossa nel file hello.</span><span class="sxs-lookup"><span data-stu-id="6befe-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="6befe-134">Questo scenario semplificato presuppone alcuna risorsa sono state nella rete virtuale hello, come se fossero presenti, non è stato possibile eliminare la rete virtuale hello e importazione hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6befe-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6befe-135">Azure considera una subnet è distribuito tooit come **in uso**.</span><span class="sxs-lookup"><span data-stu-id="6befe-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="6befe-136">Quando una subnet è in uso, non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="6befe-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="6befe-137">Prima di modificare le informazioni sulla subnet in un file di configurazione di rete, spostare tutto ciò che è stato distribuito toohello subnet tooa subnet che non venga modificata.</span><span class="sxs-lookup"><span data-stu-id="6befe-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="6befe-138">Vedere [spostare una Subnet diversa di tooa macchina virtuale o istanza del ruolo](virtual-networks-move-vm-role-to-subnet.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="6befe-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="6befe-139">XML di esempio da usare con PowerShell</span><span class="sxs-lookup"><span data-stu-id="6befe-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="6befe-140">Hello seguente file di configurazione di rete di esempio viene creata una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi *10.0.0.0/16* in hello *Stati Uniti orientali* Azure area.</span><span class="sxs-lookup"><span data-stu-id="6befe-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="6befe-141">rete virtuale Hello contiene una subnet denominata *mySubnet* con un prefisso dell'indirizzo *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="6befe-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="6befe-142">Se file di configurazione di rete hello esportato non contiene alcun contenuto, è possibile copiare hello XML nell'esempio precedente hello e incollarlo in un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="6befe-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="6befe-143">Esempio JSON per l'utilizzo con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6befe-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="6befe-144">Hello seguente file di configurazione di rete di esempio viene creata una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi *10.0.0.0/16* in hello *Stati Uniti orientali* Azure area.</span><span class="sxs-lookup"><span data-stu-id="6befe-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="6befe-145">rete virtuale Hello contiene una subnet denominata *mySubnet* con un prefisso dell'indirizzo *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="6befe-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="6befe-146">Se file di configurazione di rete hello esportato non contiene alcun contenuto, è possibile copiare hello json nell'esempio precedente hello e incollarlo in un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="6befe-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="6befe-147"><a name="import"></a>Importare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="6befe-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="6befe-148">È possibile utilizzare PowerShell o hello tooimport CLI di Azure un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="6befe-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="6befe-149">PowerShell Importa un file XML, mentre hello Azure CLI Importa un file json.</span><span class="sxs-lookup"><span data-stu-id="6befe-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="6befe-150">Se hello importazione non riesce, verificare il file hello è conforme con hello [dello schema di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="6befe-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="6befe-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6befe-151">PowerShell</span></span>
 
1. <span data-ttu-id="6befe-152">[Installare Azure PowerShell e accedere tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6befe-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="6befe-153">Cambiare directory hello e il nome in hello seguente comando in base alle esigenze, quindi eseguire il file di configurazione rete hello comando tooimport hello:</span><span class="sxs-lookup"><span data-stu-id="6befe-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="6befe-154">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6befe-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="6befe-155">[Installare hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6befe-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="6befe-156">Completare hello rimanenti passaggi da un prompt dei comandi CLI di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="6befe-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="6befe-157">Accedere tooAzure immettendo hello `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="6befe-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="6befe-158">Verificare che si è in modalità asm immettendo hello `azure config mode asm` comando.</span><span class="sxs-lookup"><span data-stu-id="6befe-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="6befe-159">Cambiare directory hello e il nome in hello seguente comando in base alle esigenze, quindi eseguire il file di configurazione rete hello comando tooimport hello:</span><span class="sxs-lookup"><span data-stu-id="6befe-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
