---
title: 'Eliminare un gateway di rete virtuale: PowerShell: Azure classico | Microsoft Docs'
description: Eliminare un gateway di rete virtuale usando PowerShell nel modello di distribuzione classico.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="59c0c-103">Eliminare un gateway di rete virtuale usando PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="59c0c-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="59c0c-104">Resource Manager - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="59c0c-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="59c0c-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="59c0c-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="59c0c-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="59c0c-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="59c0c-107">Questo articolo illustra come eliminare un gateway VPN nel modello di distribuzione classica tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c0c-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="59c0c-108">Dopo aver eliminato il gateway di rete virtuale, modificare il file di configurazione di rete per rimuovere gli elementi che non sono più in uso.</span><span class="sxs-lookup"><span data-stu-id="59c0c-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="59c0c-109"><a name="connect"></a>Passaggio 1: Connettersi ad Azure</span><span class="sxs-lookup"><span data-stu-id="59c0c-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="59c0c-110">1. Installare i cmdlet di PowerShell più recenti.</span><span class="sxs-lookup"><span data-stu-id="59c0c-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="59c0c-111">Scaricare e installare la versione più recente dei cmdlet di PowerShell per Gestione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="59c0c-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="59c0c-112">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59c0c-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="59c0c-113">2. Connettersi all'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="59c0c-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="59c0c-114">Aprire la console di PowerShell con diritti elevati e connettersi all'account.</span><span class="sxs-lookup"><span data-stu-id="59c0c-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="59c0c-115">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="59c0c-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="59c0c-116"><a name="export"></a>Passaggio 2: Esportare e visualizzare il file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="59c0c-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="59c0c-117">Creare una directory nel computer ed esportarvi il file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="59c0c-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="59c0c-118">Usare questo file per visualizzare le informazioni di configurazione correnti e modificare la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="59c0c-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="59c0c-119">In questo esempio il file di configurazione di rete viene esportato in C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="59c0c-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="59c0c-120">Aprire il file con un editor di testo e visualizzare il nome di una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="59c0c-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="59c0c-121">Quando si crea una rete virtuale nel portale di Azure, il nome completo che usa Azure non è visibile nel portale.</span><span class="sxs-lookup"><span data-stu-id="59c0c-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="59c0c-122">Ad esempio, una rete virtuale che nel portale di Azure sembra avere il nome di "ClassicVNet1" potrebbe avere un nome molto più lungo nel file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="59c0c-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="59c0c-123">Il nome potrebbe essere simile a: "Gruppo ClassicRG1 ClassicVNet1".</span><span class="sxs-lookup"><span data-stu-id="59c0c-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="59c0c-124">I nomi delle reti virtuali sono elencati come **"VirtualNetworkSite name ="**.</span><span class="sxs-lookup"><span data-stu-id="59c0c-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="59c0c-125">Usare i nomi nel file di configurazione di rete durante l'esecuzione dei cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59c0c-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="59c0c-126"><a name="delete"></a>Passaggio 3: Eliminare il gateway di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="59c0c-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="59c0c-127">Quando si elimina un gateway di rete virtuale, vengono interrotte tutte le connessioni alla rete virtuale tramite il gateway.</span><span class="sxs-lookup"><span data-stu-id="59c0c-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="59c0c-128">Se ci sono client P2S connessi alla rete virtuale, verranno disconnessi senza alcun avviso.</span><span class="sxs-lookup"><span data-stu-id="59c0c-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="59c0c-129">Questo esempio elimina il gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="59c0c-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="59c0c-130">Usare il nome completo della rete virtuale dal file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="59c0c-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="59c0c-131">Se ha esito positivo, il risultato mostra quanto segue:</span><span class="sxs-lookup"><span data-stu-id="59c0c-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="59c0c-132"><a name="modify"></a>Passaggio 4: Modificare il file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="59c0c-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="59c0c-133">Quando si elimina un gateway di rete virtuale, il cmdlet non modifica il file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="59c0c-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="59c0c-134">È necessario modificare il file per rimuovere gli elementi che non sono più in uso.</span><span class="sxs-lookup"><span data-stu-id="59c0c-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="59c0c-135">Le sezioni seguenti consentono di modificare il file di configurazione di rete che è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="59c0c-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="59c0c-136"><a name="lnsref"></a>Riferimenti al sito di rete locale</span><span class="sxs-lookup"><span data-stu-id="59c0c-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="59c0c-137">Per rimuovere le informazioni di riferimento al sito, apportare modifiche alla configurazione in **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="59c0c-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="59c0c-138">La rimozione di un riferimento al sito locale induce Azure a eliminare un tunnel.</span><span class="sxs-lookup"><span data-stu-id="59c0c-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="59c0c-139">A seconda della configurazione che è stata creata, **LocalNetworkSiteRef** potrebbe non essere elencato.</span><span class="sxs-lookup"><span data-stu-id="59c0c-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="59c0c-140">Esempio:</span><span class="sxs-lookup"><span data-stu-id="59c0c-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="59c0c-141"><a name="lns"></a>Siti di rete locale</span><span class="sxs-lookup"><span data-stu-id="59c0c-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="59c0c-142">Rimuovere tutti i siti locali che non sono più in uso.</span><span class="sxs-lookup"><span data-stu-id="59c0c-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="59c0c-143">A seconda della configurazione creata, è possibile che **LocalNetworkSite** non sia elencato.</span><span class="sxs-lookup"><span data-stu-id="59c0c-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="59c0c-144">In questo esempio viene rimosso solo Site3.</span><span class="sxs-lookup"><span data-stu-id="59c0c-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="59c0c-145"><a name="clientaddresss"></a>Pool di indirizzi client</span><span class="sxs-lookup"><span data-stu-id="59c0c-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="59c0c-146">Se era presente una connessione P2S sulla rete virtuale, si avrà **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="59c0c-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="59c0c-147">Rimuovere i pool di indirizzi client che corrispondono al gateway di rete virtuale che è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="59c0c-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="59c0c-148">Esempio:</span><span class="sxs-lookup"><span data-stu-id="59c0c-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="59c0c-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="59c0c-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="59c0c-150">Eliminare il **GatewaySubnet** corrispondente alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="59c0c-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="59c0c-151">Esempio:</span><span class="sxs-lookup"><span data-stu-id="59c0c-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="59c0c-152"><a name="upload"></a>Passaggio 5: Caricare il file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="59c0c-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="59c0c-153">Salvare le modifiche e caricare la configurazione di rete in Azure.</span><span class="sxs-lookup"><span data-stu-id="59c0c-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="59c0c-154">Assicurarsi di modificare il percorso del file in base al proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="59c0c-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="59c0c-155">Se ha esito positivo, il valore restituito è simile a quello mostrato in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="59c0c-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded