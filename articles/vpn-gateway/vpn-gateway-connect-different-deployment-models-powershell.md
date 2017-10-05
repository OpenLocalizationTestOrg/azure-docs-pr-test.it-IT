---
title: 'Connettere le reti virtuali classiche alle reti virtuali di Azure Resource Manager: PowerShell | Microsoft Docs'
description: Informazioni su come creare una connessione VPN tra le reti virtuali classiche e le reti virtuali di Resource Manager usando il gateway VPN e PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 842a32e5304977af92706cdda464286983122247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="e6c4f-103">Connettere reti virtuali da diversi modelli di distribuzione usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6c4f-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="e6c4f-104">Questo articolo descrive come connettere reti virtuali classiche a reti virtuali di Resource Manager per consentire alle risorse presenti nei modelli di distribuzione separati di comunicare tra di loro.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="e6c4f-105">La procedura descritta in questo articolo usa PowerShell, tuttavia è inoltre possibile creare questa configurazione tramite il portale di Azure selezionando l'articolo da questo elenco.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-105">The steps in this article use PowerShell, but you can also create this configuration using the Azure portal by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6c4f-106">Portale</span><span class="sxs-lookup"><span data-stu-id="e6c4f-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="e6c4f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6c4f-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="e6c4f-108">La connessione di una rete virtuale classica a una rete virtuale di Resource Manager è simile alla connessione di una rete virtuale a una posizione del sito locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="e6c4f-109">Entrambi i tipi di connettività utilizzano un gateway VPN per fornire un tunnel sicuro tramite IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="e6c4f-110">È possibile creare una connessione tra reti virtuali in sottoscrizioni diverse e in aree diverse.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="e6c4f-111">È anche possibile connettere reti virtuali che già dispongono di connessioni alle reti locali, purché il gateway con cui sono state configurate sia dinamico o basato su route.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="e6c4f-112">Per altre informazioni sulle connessioni da rete virtuale a rete virtuale, vedere la sezione [Domande frequenti relative alla connessione da rete virtuale a rete virtuale](#faq) alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="e6c4f-113">Se le reti virtuali si trovano nella stessa area, è consigliabile considerare invece la possibilità di connetterle tramite peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="e6c4f-114">Peering reti virtuali non usa un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="e6c4f-115">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e6c4f-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="e6c4f-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e6c4f-116">Before beginning</span></span>

<span data-ttu-id="e6c4f-117">I passaggi seguenti illustrano le impostazioni necessarie per configurare un gateway dinamico o basato su route per ogni rete virtuale e creare una connessione VPN tra i gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-117">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="e6c4f-118">Questa configurazione non supporta i gateway con routing statico o basati su criteri.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e6c4f-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e6c4f-119">Prerequisites</span></span>

* <span data-ttu-id="e6c4f-120">Entrambe le reti virtuali sono già state create.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="e6c4f-121">Gli intervalli di indirizzi per le reti virtuali non si sovrappongono l'uno con l'altro o non si sovrappongano con gli intervalli delle eventuali altre connessioni a cui i gateway potrebbero essere collegati.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-121">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="e6c4f-122">Sono stati installati i cmdlet di PowerShell più recenti.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-122">You have installed the latest PowerShell cmdlets.</span></span> <span data-ttu-id="e6c4f-123">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="e6c4f-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="e6c4f-124">Assicurarsi di installare sia i cmdlet di Gestione dei servizi (SM) che i cmdlet di Resource Manager (RM).</span><span class="sxs-lookup"><span data-stu-id="e6c4f-124">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="e6c4f-125"><a name="exampleref"></a>Impostazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="e6c4f-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="e6c4f-126">È possibile usare questi valori per creare un ambiente di test o farvi riferimento per comprendere meglio gli esempi di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-126">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="e6c4f-127">**Impostazioni della rete virtuale classica**</span><span class="sxs-lookup"><span data-stu-id="e6c4f-127">**Classic VNet settings**</span></span>

<span data-ttu-id="e6c4f-128">Nome rete virtuale = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="e6c4f-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="e6c4f-129">Località = Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="e6c4f-129">Location = West US</span></span> <br>
<span data-ttu-id="e6c4f-130">Spazi degli indirizzi della rete virtuale = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="e6c4f-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="e6c4f-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="e6c4f-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="e6c4f-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="e6c4f-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="e6c4f-133">Nome della rete locale = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="e6c4f-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="e6c4f-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="e6c4f-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="e6c4f-135">**Impostazioni della rete virtuale di Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="e6c4f-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="e6c4f-136">Nome della rete virtuale = RMVNet </span><span class="sxs-lookup"><span data-stu-id="e6c4f-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="e6c4f-137">Gruppo di risorse= RG1</span><span class="sxs-lookup"><span data-stu-id="e6c4f-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="e6c4f-138">Spazi degli indirizzi della rete virtuale = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="e6c4f-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="e6c4f-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="e6c4f-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="e6c4f-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="e6c4f-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="e6c4f-141">Località = Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="e6c4f-141">Location = East US</span></span> <br>
<span data-ttu-id="e6c4f-142">Nome IP pubblico del gateway = gwpip</span><span class="sxs-lookup"><span data-stu-id="e6c4f-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="e6c4f-143">Gateway di rete locale = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="e6c4f-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="e6c4f-144">Nome gateway di rete virtuale = RMGateway</span><span class="sxs-lookup"><span data-stu-id="e6c4f-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="e6c4f-145">Configurazione di indirizzamento IP del gateway = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="e6c4f-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="e6c4f-146"><a name="createsmgw"></a>Sezione 1: Configurare una rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="e6c4f-146"><a name="createsmgw"></a>Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="e6c4f-147">Parte 1: Eseguire il download del file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="e6c4f-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="e6c4f-148">Accedere all'account Azure nella console di PowerShell con diritti elevati.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-148">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="e6c4f-149">Il cmdlet seguente richiede le credenziali di accesso per l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-149">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="e6c4f-150">Dopo l'accesso, vengono scaricate le impostazioni dell'account in modo che siano disponibili per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-150">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="e6c4f-151">Per completare questa parte della configurazione, si usano i cmdlet PowerShell di Gestione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-151">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="e6c4f-152">Esportare il file di configurazione di rete di Azure eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-152">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="e6c4f-153">Se necessario è possibile modificare il percorso del file da esportare.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-153">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="e6c4f-154">Aprire il file XML scaricato per modificarlo.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-154">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="e6c4f-155">Per un esempio del file di configurazione di rete, vedere lo [Schema di configurazione di rete](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6c4f-155">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="e6c4f-156">Parte 2: Verificare la subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="e6c4f-156">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="e6c4f-157">Nell'elemento **VirtualNetworkSites** aggiungere una subnet del gateway alla rete virtuale se non ne è ancora stato creato uno.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-157">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="e6c4f-158">Quando si lavora con il file di configurazione di rete, la subnet del gateway DEVE essere denominata "GatewaySubnet", altrimenti Azure non potrà riconoscerla e utilizzarla come una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-158">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="e6c4f-159">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="e6c4f-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="e6c4f-160">Parte 3: Aggiungere il sito di rete locale</span><span class="sxs-lookup"><span data-stu-id="e6c4f-160">Part 3 - Add the local network site</span></span>
<span data-ttu-id="e6c4f-161">Il sito di rete locale aggiunto rappresenta la rete virtuale di Resource Manager a cui si desidera connettersi.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-161">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="e6c4f-162">Aggiungere un elemento **LocalNetworkSites** al file, se non ne esiste già uno.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-162">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="e6c4f-163">A questo punto nella configurazione, il parametro VPNGatewayAddress può essere qualsiasi indirizzo IP pubblico valido poiché non è stato ancora creato il gateway per la rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-163">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="e6c4f-164">Dopo aver creato il gateway, l'indirizzo IP segnaposto verrà sostituito con l'indirizzo IP pubblico corretto assegnato al gateway di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-164">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="e6c4f-165">Parte 4: Associare la rete locale al sito della rete locale</span><span class="sxs-lookup"><span data-stu-id="e6c4f-165">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="e6c4f-166">Questa sezione descrive come specificare il sito di rete locale a cui si desidera connettere la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-166">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="e6c4f-167">In questo caso, è la rete virtuale di Resource Manager a cui si è fatto riferimento in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-167">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="e6c4f-168">Assicurarsi che i nomi corrispondano.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-168">Make sure the names match.</span></span> <span data-ttu-id="e6c4f-169">Questo passaggio non crea un gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-169">This step does not create a gateway.</span></span> <span data-ttu-id="e6c4f-170">Specifica la rete locale a cui il gateway si collegherà.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-170">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="e6c4f-171">Parte 5: Salvare il file e caricarlo</span><span class="sxs-lookup"><span data-stu-id="e6c4f-171">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="e6c4f-172">Salvare il file, quindi importarlo in Azure eseguendo il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-172">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="e6c4f-173">Assicurarsi di modificare il percorso del file in base al proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-173">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="e6c4f-174">Viene visualizzato un risultato simile che mostra che l'importazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-174">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="e6c4f-175">Parte 6: creare il gateway</span><span class="sxs-lookup"><span data-stu-id="e6c4f-175">Part 6 - Create the gateway</span></span>

<span data-ttu-id="e6c4f-176">Prima di eseguire questo esempio, vedere i nomi esatti previsti da Azure nel file di configurazione di rete scaricato.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-176">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="e6c4f-177">Il file di configurazione di rete contiene i valori per le reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-177">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="e6c4f-178">In alcuni casi, i nomi di rete virtuale classica vengono modificati nel file di configurazione di rete durante la creazione di impostazioni di rete virtuale classica nel portale di Azure, a causa delle differenze nei modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-178">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="e6c4f-179">Ad esempio, se è stato usato il portale di Azure per creare una rete virtuale classica denominata "Classic VNet"' in un gruppo di risorse denominato "ClassicRG", il nome contenuto nel file di configurazione di rete viene convertito in "Group ClassicRG Classic VNet".</span><span class="sxs-lookup"><span data-stu-id="e6c4f-179">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="e6c4f-180">Quando si specifica il nome di una rete virtuale che contiene spazi, racchiudere il valore tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-180">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="e6c4f-181">Usare l'esempio seguente per creare un gateway con routing dinamico:</span><span class="sxs-lookup"><span data-stu-id="e6c4f-181">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="e6c4f-182">È possibile controllare lo stato del gateway tramite il cmdlet **Get-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-182">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="e6c4f-183"><a name="creatermgw"></a>Sezione 2: configurazione del gateway della rete virtuale di Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e6c4f-183"><a name="creatermgw"></a>Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="e6c4f-184">Per creare un gateway VPN per la rete virtuale di Resource Manager, seguire le istruzioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-184">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="e6c4f-185">Non eseguire i passaggi fino a quando non si è recuperato l'indirizzo IP pubblico del gateway della rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-185">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="e6c4f-186">Accedere all'account Azure nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-186">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="e6c4f-187">Il cmdlet seguente richiede le credenziali di accesso per l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-187">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="e6c4f-188">Dopo l'accesso, vengono scaricate le impostazioni dell'account in modo che siano disponibili per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-188">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="e6c4f-189">Ottenere un elenco delle sottoscrizioni di Azure se si dispone di più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="e6c4f-190">Specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-190">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="e6c4f-191">Creare un gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-191">Create a local network gateway.</span></span> <span data-ttu-id="e6c4f-192">In una rete virtuale il gateway di rete locale in genere fa riferimento al percorso locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-192">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="e6c4f-193">In questo caso, il gateway di rete locale fa riferimento alla rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-193">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="e6c4f-194">Assegnargli un nome che Azure possa usare come riferimento e specificare il prefisso dello spazio indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-194">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="e6c4f-195">Azure usa il prefisso di indirizzo IP che viene specificato per identificare il traffico da inviare al percorso locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-195">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="e6c4f-196">Se si desidera modificare le informazioni prima di creare il gateway, è possibile modificare i valori ed eseguire nuovamente l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-196">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="e6c4f-197">**-Name** è il nome da assegnare per fare riferimento al gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-197">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br><span data-ttu-id="e6c4f-198">
   **-AddressPrefix** è lo spazio degli indirizzi per una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-198">
   **-AddressPrefix** is the Address Space for your classic VNet.</span></span><br><span data-ttu-id="e6c4f-199">
**-GatewayIpAddress** è l'indirizzo IP pubblico del gateway della rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-199">
**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="e6c4f-200">Assicurarsi di modificare l'esempio seguente in modo da riflettere l'indirizzo IP corretto.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-200">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="e6c4f-201">Richiedere un indirizzo IP pubblico da allocare al gateway di rete virtuale per la rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-201">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="e6c4f-202">Non è possibile specificare l'indirizzo IP che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-202">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="e6c4f-203">L'indirizzo IP viene allocato in modo dinamico al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-203">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="e6c4f-204">Ciò non significa però che l'indirizzo IP verrà modificato.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-204">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="e6c4f-205">L'indirizzo IP del gateway di rete virtuale viene modificato solamente quando il gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-205">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="e6c4f-206">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="e6c4f-207">In questo passaggio viene anche impostata una variabile che verrà usata in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="e6c4f-208">Verificare che la rete virtuale disponga di una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="e6c4f-209">Se non esiste alcuna subnet del gateway, aggiungerne una.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="e6c4f-210">Assicurarsi che la subnet del gateway sia denominata *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-210">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="e6c4f-211">Recuperare la subnet usata per il gateway tramite il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-211">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="e6c4f-212">In questo passaggio, è anche possibile impostare una variabile da usare nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-212">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="e6c4f-213">**-Name** è il nome della rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-213">**-Name** is the name of your Resource Manager VNet.</span></span><br><span data-ttu-id="e6c4f-214">
   **-ResourceGroupName** è il gruppo di risorse a cui la rete virtuale è associata.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-214">
**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="e6c4f-215">Per poter funzionare correttamente, la subnet del gateway deve esistere già per questa rete virtuale e deve essere denominata *GatewaySubnet* .</span><span class="sxs-lookup"><span data-stu-id="e6c4f-215">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="e6c4f-216">Creare la configurazione di indirizzamento IP del gateway.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-216">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="e6c4f-217">La configurazione del gateway definisce la subnet e l'indirizzo IP pubblico da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-217">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="e6c4f-218">Per creare la configurazione del gateway, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-218">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="e6c4f-219">In questo passaggio i parametri **-SubnetId** e **-PublicIpAddressId** devono essere passati alla proprietà id dalla subnet e dagli oggetti dell'indirizzo IP rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-219">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="e6c4f-220">Non è possibile usare una semplice stringa.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-220">You can't use a simple string.</span></span> <span data-ttu-id="e6c4f-221">Queste variabili vengono impostate nel passaggio per richiedere un indirizzo IP pubblico e nel passaggio per recuperare la subnet.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-221">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="e6c4f-222">Creare il gateway di rete virtuale di Resource Manager tramite il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-222">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="e6c4f-223">`-VpnType` deve essere *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-223">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="e6c4f-224">La creazione del gateway può richiedere oltre 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-224">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="e6c4f-225">Dopo che il gateway della rete privata virtuale è stato creato, copiare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-225">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="e6c4f-226">Verrà usato al momento della configurazione delle impostazioni di rete locale per la rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-226">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="e6c4f-227">È possibile usare il cmdlet seguente per recuperare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-227">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="e6c4f-228">L'indirizzo IP pubblico viene elencato nel valore restituito come *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-228">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="e6c4f-229">Sezione 3: Modificare le impostazioni del sito locale della rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="e6c4f-229">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="e6c4f-230">In questa sezione viene usata la rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-230">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="e6c4f-231">Viene sostituito l'indirizzo IP segnaposto usato nella specifica delle impostazioni del sito locale, che verrà usato per connettersi al gateway di rete virtuale di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-231">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="e6c4f-232">Esportare il file di configurazione della rete.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-232">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="e6c4f-233">In un editor di testo modificare il valore di VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-233">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="e6c4f-234">Sostituire l'indirizzo IP segnaposto con l'indirizzo IP pubblico del gateway di Resource Manager e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-234">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="e6c4f-235">Importare il file di configurazione di rete modificato in Azure.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-235">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="e6c4f-236"><a name="connect"></a>Sezione 4: creazione di una connessione tra i gateway</span><span class="sxs-lookup"><span data-stu-id="e6c4f-236"><a name="connect"></a>Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="e6c4f-237">La creazione di una connessione tra i gateway richiede PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-237">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="e6c4f-238">Potrebbe essere necessario aggiungere l'account Azure per usare la versione classica dei cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-238">You may need to add your Azure Account to use the classic version of the  PowerShell cmdlets.</span></span> <span data-ttu-id="e6c4f-239">A tale scopo, usare **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-239">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="e6c4f-240">Nella console di PowerShell impostare la chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-240">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="e6c4f-241">Prima di eseguire i cmdlet, vedere i nomi esatti previsti da Azure nel file di configurazione di rete scaricato.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-241">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="e6c4f-242">Quando si specifica il nome di una rete virtuale che contiene spazi, racchiudere il valore tra virgolette singole.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-242">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="e6c4f-243">Nell'esempio seguente **-VNetName** è il nome della rete virtuale classica, mentre **-LocalNetworkSiteName** è il nome specificato per il sito della rete locale.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-243">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="e6c4f-244">**-SharedKey** è un valore che è possibile generare e specificare.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-244">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="e6c4f-245">Per questo esempio è stato usato "abc123", ma è possibile generare e usare un elemento più complesso.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-245">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="e6c4f-246">È importante che il valore specificato qui sia lo stesso valore specificato nel passaggio successivo quando si crea la connessione.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-246">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="e6c4f-247">Il valore restituito deve mostrare lo **stato: Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-247">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="e6c4f-248">Creare la connessione VPN eseguendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6c4f-248">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="e6c4f-249">Impostare le variabili.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-249">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="e6c4f-250">Creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-250">Create the connection.</span></span> <span data-ttu-id="e6c4f-251">Si noti che **-ConnectionType** è IPsec, non Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="e6c4f-251">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="e6c4f-252">Sezione 5: Verificare le connessioni</span><span class="sxs-lookup"><span data-stu-id="e6c4f-252">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="e6c4f-253">Per verificare la connessione dalla rete virtuale classica alla rete virtuale di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6c4f-253">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="e6c4f-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6c4f-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="e6c4f-255">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e6c4f-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="e6c4f-256">Per verificare la connessione dalla rete virtuale di Resource Manager alla rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="e6c4f-256">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="e6c4f-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6c4f-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="e6c4f-258">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e6c4f-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="e6c4f-259"><a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e6c4f-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

