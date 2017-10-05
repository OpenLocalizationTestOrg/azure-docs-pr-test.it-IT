---
title: Configurare una rete virtuale di Azure (classica) usando un file di configurazione di rete | Microsoft Docs
description: Informazioni su come creare e modificare le reti virtuali (classiche) esportando, modificando e importando un file di configurazione di rete.
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
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="0582a-103">Configurare una rete virtuale (classica) usando un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="0582a-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0582a-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0582a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0582a-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="0582a-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="0582a-106">È consigliabile usare il modello di distribuzione di Resource Manager per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="0582a-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="0582a-107">È possibile creare e configurare una rete virtuale (classica) con un file di configurazione di rete usando l'interfaccia della riga di comando di Azure 1.0 o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0582a-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="0582a-108">Non è possibile creare o modificare una rete virtuale mediante il modello di distribuzione di Azure Resource Manager usando un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="0582a-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="0582a-109">Non è possibile usare il portale di Azure per creare o modificare una rete virtuale (classica) con un file di configurazione di rete, ma è possibile usare il portale di Azure per creare una rete virtuale (classica) senza usare un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="0582a-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="0582a-110">La creazione e la configurazione di una rete virtuale (classica) con un file di configurazione di rete prevede l'esportazione, la modifica e l'importazione del file.</span><span class="sxs-lookup"><span data-stu-id="0582a-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="0582a-111"><a name="export"></a>Esportare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="0582a-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="0582a-112">È possibile usare PowerShell o l'interfaccia della riga di comando di Azure per esportare un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="0582a-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="0582a-113">PowerShell esporta un file XML, mentre l'interfaccia della riga di comando di Azure esporta un file json.</span><span class="sxs-lookup"><span data-stu-id="0582a-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="0582a-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0582a-114">PowerShell</span></span>
 
1. <span data-ttu-id="0582a-115">[Installare Azure PowerShell e accedere ad Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0582a-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0582a-116">Modificare la directory (e verificare che sia presente) e il nome file nel comando seguente nel modo desiderato, quindi eseguire il comando per esportare il file di configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="0582a-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0582a-117">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0582a-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0582a-118">[Installare l'interfaccia della riga di comando di Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0582a-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0582a-119">Completare i passaggi rimanenti dal prompt dei comandi dell'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="0582a-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0582a-120">Accedere ad Azure immettendo il comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="0582a-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="0582a-121">Verificare di essere in modalità asm immettendo il comando `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="0582a-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0582a-122">Modificare la directory (e verificare che sia presente) e il nome file nel comando seguente nel modo desiderato, quindi eseguire il comando per esportare il file di configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="0582a-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="0582a-123">Creare o modificare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="0582a-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="0582a-124">Un file di configurazione di rete è un file XML (quando si usa PowerShell) o un file json (quando si usa l'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="0582a-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="0582a-125">Il file può essere modificato in qualsiasi editor di testo o editor XML/json.</span><span class="sxs-lookup"><span data-stu-id="0582a-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="0582a-126">L'articolo relativo alle [impostazioni dello schema del file di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx) include i dettagli di tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="0582a-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="0582a-127">Per una spiegazione aggiuntiva delle impostazioni, vedere [View virtual networks and settings](virtual-network-manage-network.md#view-vnet) (Visualizzare le reti virtuali e le impostazioni).</span><span class="sxs-lookup"><span data-stu-id="0582a-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="0582a-128">Le modifiche che vengono apportate al file:</span><span class="sxs-lookup"><span data-stu-id="0582a-128">The changes you make to the file:</span></span>

- <span data-ttu-id="0582a-129">Devono essere conformi allo schema altrimenti l'importazione del file di configurazione di rete non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="0582a-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="0582a-130">Sovrascrivono le impostazioni di rete esistenti per la sottoscrizione, pertanto è necessario prestare attenzione alle modifiche che si apportano.</span><span class="sxs-lookup"><span data-stu-id="0582a-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="0582a-131">Fare riferimento, ad esempio, ai file di configurazione di rete di esempio che seguono.</span><span class="sxs-lookup"><span data-stu-id="0582a-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="0582a-132">Si supponga che il file di origine contenga due istanze di **VirtualNetworkSite** e che lo si modifichi come illustrato negli esempi.</span><span class="sxs-lookup"><span data-stu-id="0582a-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="0582a-133">Quando si importa il file, Azure elimina la rete virtuale per l'istanza **VirtualNetworkSite** che è stata rimossa nel file.</span><span class="sxs-lookup"><span data-stu-id="0582a-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="0582a-134">Questo scenario semplificato presuppone che non vi siano risorse nella rete virtuale, perché se fossero presenti, non sarebbe possibile eliminare la rete virtuale e l'importazione avrebbe esito negativo.</span><span class="sxs-lookup"><span data-stu-id="0582a-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0582a-135">Azure considera una subnet con un elemento distribuito come **in uso**.</span><span class="sxs-lookup"><span data-stu-id="0582a-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="0582a-136">Quando una subnet è in uso, non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="0582a-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="0582a-137">Prima di modificare le informazioni sulla subnet in un file di configurazione di rete, spostare tutti gli elementi distribuiti nella subnet in una subnet diversa che non deve essere modificata.</span><span class="sxs-lookup"><span data-stu-id="0582a-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="0582a-138">Vedere [Spostare una VM o un'istanza del ruolo in un'altra subnet](virtual-networks-move-vm-role-to-subnet.md).</span><span class="sxs-lookup"><span data-stu-id="0582a-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="0582a-139">XML di esempio da usare con PowerShell</span><span class="sxs-lookup"><span data-stu-id="0582a-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="0582a-140">L'esempio di file di configurazione di rete seguente illustra come creare una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi di *10.0.0.0/16* nell'area di Azure *Stati Uniti Orientali*.</span><span class="sxs-lookup"><span data-stu-id="0582a-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="0582a-141">La rete virtuale contiene una subnet denominata *mySubnet* con un prefisso di indirizzo *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0582a-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="0582a-142">Se il file di configurazione di rete esportato non include alcun contenuto, è possibile copiare il codice XML dell'esempio precedente e incollarlo in un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="0582a-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="0582a-143">JSON di esempio da usare con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0582a-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="0582a-144">L'esempio di file di configurazione di rete seguente illustra come creare una rete virtuale denominata *myVirtualNetwork* con uno spazio di indirizzi di *10.0.0.0/16* nell'area di Azure *Stati Uniti Orientali*.</span><span class="sxs-lookup"><span data-stu-id="0582a-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="0582a-145">La rete virtuale contiene una subnet denominata *mySubnet* con un prefisso di indirizzo *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0582a-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="0582a-146">Se il file di configurazione di rete esportato non include alcun contenuto, è possibile copiare il codice json dell'esempio precedente e incollarlo in un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="0582a-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="0582a-147"><a name="import"></a>Importare un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="0582a-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="0582a-148">È possibile usare PowerShell o l'interfaccia della riga di comando di Azure per importare un file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="0582a-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="0582a-149">PowerShell importa un file XML, mentre l'interfaccia della riga di comando di Azure importa un file json.</span><span class="sxs-lookup"><span data-stu-id="0582a-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="0582a-150">Se l'importazione non riesce, verificare che il file sia conforme allo [schema di configurazione di rete](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="0582a-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="0582a-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0582a-151">PowerShell</span></span>
 
1. <span data-ttu-id="0582a-152">[Installare Azure PowerShell e accedere ad Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0582a-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="0582a-153">Modificare la directory e il nome file nel comando seguente in base alle esigenze, quindi eseguire il comando per importare il file di configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="0582a-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="0582a-154">Interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0582a-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="0582a-155">[Installare l'interfaccia della riga di comando di Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0582a-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="0582a-156">Completare i passaggi rimanenti dal prompt dei comandi dell'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="0582a-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="0582a-157">Accedere ad Azure immettendo il comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="0582a-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="0582a-158">Verificare di essere in modalità asm immettendo il comando `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="0582a-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="0582a-159">Modificare la directory e il nome file nel comando seguente in base alle esigenze, quindi eseguire il comando per importare il file di configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="0582a-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
