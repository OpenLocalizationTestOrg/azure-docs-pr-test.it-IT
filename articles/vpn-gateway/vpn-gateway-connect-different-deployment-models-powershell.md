---
title: 'Connettere le reti virtuali classiche tooAzure VNets Gestione risorse: PowerShell | Documenti Microsoft'
description: Informazioni su come toocreate una connessione VPN tra classico reti virtuali e Gestione risorse VNets tramite Gateway VPN e PowerShell
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
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="9393c-103">Connettere reti virtuali da diversi modelli di distribuzione usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="9393c-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="9393c-104">Questo articolo illustra come tooconnect tooResource di reti virtuali classiche tooallow Manager VNets hello risorse che si trovano in toocommunicate di modelli di distribuzione separata hello tra loro.</span><span class="sxs-lookup"><span data-stu-id="9393c-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="9393c-105">passaggi di Hello in questo articolo usano PowerShell, ma è anche possibile creare questa configurazione tramite il portale di Azure hello selezionando articolo hello da questo elenco.</span><span class="sxs-lookup"><span data-stu-id="9393c-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9393c-106">Portale</span><span class="sxs-lookup"><span data-stu-id="9393c-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="9393c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9393c-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="9393c-108">La connessione di un classico tooa di rete virtuale VNet Gestione risorse è simile tooconnecting un percorso di rete virtuale tooan locale del sito.</span><span class="sxs-lookup"><span data-stu-id="9393c-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="9393c-109">Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="9393c-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="9393c-110">È possibile creare una connessione tra reti virtuali in sottoscrizioni diverse e in aree diverse.</span><span class="sxs-lookup"><span data-stu-id="9393c-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="9393c-111">È inoltre possibile connettersi reti virtuali che dispone già di reti locali tooon di connessioni, come gateway hello che sono stati configurati con è dinamico o basato su route.</span><span class="sxs-lookup"><span data-stu-id="9393c-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="9393c-112">Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9393c-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="9393c-113">Se le reti virtuali si trovano in hello stessa area, è opportuno prendere in considerazione tooinstead collegarli tramite Peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="9393c-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="9393c-114">Peering reti virtuali non usa un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9393c-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="9393c-115">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9393c-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="9393c-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9393c-116">Before beginning</span></span>

<span data-ttu-id="9393c-117">Hello passaggi seguenti consentono di eseguire hello le impostazioni necessarie tooconfigure un gateway dinamico o basato su route per ogni rete virtuale e creare una connessione VPN tra i gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="9393c-118">Questa configurazione non supporta i gateway con routing statico o basati su criteri.</span><span class="sxs-lookup"><span data-stu-id="9393c-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9393c-119">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9393c-119">Prerequisites</span></span>

* <span data-ttu-id="9393c-120">Entrambe le reti virtuali sono già state create.</span><span class="sxs-lookup"><span data-stu-id="9393c-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="9393c-121">Hello intervalli di indirizzi per hello reti virtuali non possono sovrapporsi tra loro o coincidere con tutti gli intervalli hello per le altre connessioni che il gateway hello potrebbe essere connessa di.</span><span class="sxs-lookup"><span data-stu-id="9393c-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="9393c-122">È stato installato hello cmdlet più recenti di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9393c-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="9393c-123">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="9393c-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="9393c-124">Assicurarsi di installare hello servizio di gestione (SM) sia hello i cmdlet di gestione risorse (RM).</span><span class="sxs-lookup"><span data-stu-id="9393c-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="9393c-125"><a name="exampleref"></a>Impostazioni di esempio</span><span class="sxs-lookup"><span data-stu-id="9393c-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="9393c-126">È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9393c-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="9393c-127">**Impostazioni della rete virtuale classica**</span><span class="sxs-lookup"><span data-stu-id="9393c-127">**Classic VNet settings**</span></span>

<span data-ttu-id="9393c-128">Nome rete virtuale = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="9393c-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="9393c-129">Località = Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="9393c-129">Location = West US</span></span> <br>
<span data-ttu-id="9393c-130">Spazi degli indirizzi della rete virtuale = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="9393c-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="9393c-131">Subnet-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="9393c-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="9393c-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="9393c-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="9393c-133">Nome della rete locale = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="9393c-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="9393c-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="9393c-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="9393c-135">**Impostazioni della rete virtuale di Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="9393c-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="9393c-136">Nome della rete virtuale = RMVNet </span><span class="sxs-lookup"><span data-stu-id="9393c-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="9393c-137">Gruppo di risorse= RG1</span><span class="sxs-lookup"><span data-stu-id="9393c-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="9393c-138">Spazi degli indirizzi della rete virtuale = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9393c-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="9393c-139">Subnet-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="9393c-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="9393c-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="9393c-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="9393c-141">Località = Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="9393c-141">Location = East US</span></span> <br>
<span data-ttu-id="9393c-142">Nome IP pubblico del gateway = gwpip</span><span class="sxs-lookup"><span data-stu-id="9393c-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="9393c-143">Gateway di rete locale = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="9393c-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="9393c-144">Nome gateway di rete virtuale = RMGateway</span><span class="sxs-lookup"><span data-stu-id="9393c-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="9393c-145">Configurazione di indirizzamento IP del gateway = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="9393c-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="9393c-146"><a name="createsmgw"></a>Sezione 1 - configurare hello classic rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9393c-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="9393c-147">Parte 1: Eseguire il download del file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="9393c-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="9393c-148">Accedi tooyour account Azure nella console di PowerShell hello con diritti elevati.</span><span class="sxs-lookup"><span data-stu-id="9393c-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="9393c-149">Hello seguente cmdlet richiede hello le credenziali di accesso per l'Account di Azure.</span><span class="sxs-lookup"><span data-stu-id="9393c-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="9393c-150">Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9393c-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="9393c-151">Utilizzare hello toocomplete cmdlet PowerShell di Service Manager questa parte della configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="9393c-152">Esportare il file di configurazione di rete di Azure eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9393c-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="9393c-153">È possibile modificare il percorso di hello hello tooexport tooa diversi della posizione del file se necessario.</span><span class="sxs-lookup"><span data-stu-id="9393c-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="9393c-154">File con estensione XML aperti hello scaricato tooedit è.</span><span class="sxs-lookup"><span data-stu-id="9393c-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="9393c-155">Per un esempio di file di configurazione di rete hello, vedere hello [dello Schema di configurazione di rete](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="9393c-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="9393c-156">Parte 2 - verificare la subnet gateway hello</span><span class="sxs-lookup"><span data-stu-id="9393c-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="9393c-157">In hello **VirtualNetworkSites** elemento, aggiungere un tooyour subnet gateway rete virtuale se non ne è stato creato.</span><span class="sxs-lookup"><span data-stu-id="9393c-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="9393c-158">Quando si utilizzano file di configurazione di rete hello, subnet del gateway hello devono essere denominati "GatewaySubnet" o Azure non è possibile riconoscere e utilizzarlo come una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="9393c-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="9393c-159">**Esempio:**</span><span class="sxs-lookup"><span data-stu-id="9393c-159">**Example:**</span></span>

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

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="9393c-160">Parte 3: aggiungere il sito di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="9393c-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="9393c-161">sito di rete locale Hello che è aggiungere rappresenta hello desiderato tooconnect toowhich di rete virtuale RM.</span><span class="sxs-lookup"><span data-stu-id="9393c-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="9393c-162">Aggiungere un **LocalNetworkSites** elemento toohello file se non ne esiste già uno.</span><span class="sxs-lookup"><span data-stu-id="9393c-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="9393c-163">A questo punto nella configurazione di hello, hello VPNGatewayAddress può essere qualsiasi indirizzo IP pubblico valido perché è non ancora creato il gateway di hello per hello VNet Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="9393c-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="9393c-164">Quando si crea gateway hello, è necessario sostituire l'indirizzo IP segnaposto con hello corretto indirizzo IP pubblico assegnato gateway RM toohello.</span><span class="sxs-lookup"><span data-stu-id="9393c-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="9393c-165">Parte 4: associare il sito di rete locale hello hello rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9393c-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="9393c-166">In questa sezione viene specificato il sito di rete locale hello che si desidera tooconnect hello tra.</span><span class="sxs-lookup"><span data-stu-id="9393c-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="9393c-167">In questo caso, è hello VNet Gestione risorse che si è fatto riferimento in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9393c-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="9393c-168">In modo che nomi hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="9393c-168">Make sure hello names match.</span></span> <span data-ttu-id="9393c-169">Questo passaggio non crea un gateway.</span><span class="sxs-lookup"><span data-stu-id="9393c-169">This step does not create a gateway.</span></span> <span data-ttu-id="9393c-170">Specifica rete locale hello hello gateway si connetterà.</span><span class="sxs-lookup"><span data-stu-id="9393c-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="9393c-171">Parte 5: salvare file hello e caricare</span><span class="sxs-lookup"><span data-stu-id="9393c-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="9393c-172">Salvare il file hello, quindi importarlo tooAzure eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9393c-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="9393c-173">Assicurarsi di modificare il percorso di file hello come necessario per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9393c-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="9393c-174">Verrà visualizzato un risultato simile che mostra che import hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="9393c-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="9393c-175">Parte 6: creare gateway hello</span><span class="sxs-lookup"><span data-stu-id="9393c-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="9393c-176">Prima di eseguire questo esempio, fare riferimento toohello file di configurazione di rete che è stato scaricato per hello esatto dei nomi da Azure prevede toosee.</span><span class="sxs-lookup"><span data-stu-id="9393c-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="9393c-177">file di configurazione di rete Hello contiene i valori hello per le reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="9393c-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="9393c-178">In alcuni casi i nomi di hello per reti virtuali vengono modificate nel file di configurazione di rete hello durante la creazione di impostazioni di rete virtuale classiche in classica hello portale di Azure a causa delle differenze toohello nei modelli di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="9393c-179">Ad esempio, se si utilizza hello toocreate portale Azure, una rete virtuale classica denominato 'VNet classico' e creati in un gruppo di risorse denominato 'ClassicRG', nome hello contenuta nel file di configurazione di rete hello è convertito too'Group rete virtuale classica ClassicRG'.</span><span class="sxs-lookup"><span data-stu-id="9393c-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="9393c-180">Quando si specifica il nome di hello di una rete virtuale che contiene spazi, utilizzare le virgolette per racchiudere valori hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="9393c-181">Utilizzare hello seguente esempio toocreate un gateway con routing dinamico:</span><span class="sxs-lookup"><span data-stu-id="9393c-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="9393c-182">È possibile controllare lo stato di hello del gateway hello utilizzando hello **Get-AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9393c-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="9393c-183"><a name="creatermgw"></a>Sezione 2: Configurare il gateway di rete virtuale RM hello</span><span class="sxs-lookup"><span data-stu-id="9393c-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="9393c-184">un gateway VPN per rete virtuale RM, hello toocreate seguire hello attenendosi alle istruzioni.</span><span class="sxs-lookup"><span data-stu-id="9393c-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="9393c-185">Non avviare passaggi hello fino a dopo aver recuperato l'indirizzo IP pubblico hello per gateway hello classic della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9393c-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="9393c-186">Accedi tooyour account Azure nella console di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="9393c-187">Hello seguente cmdlet richiede hello le credenziali di accesso per l'Account di Azure.</span><span class="sxs-lookup"><span data-stu-id="9393c-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="9393c-188">Dopo l'accesso, le impostazioni dell'account vengono scaricate in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9393c-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="9393c-189">Ottenere un elenco delle sottoscrizioni di Azure se si dispone di più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9393c-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="9393c-190">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="9393c-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="9393c-191">Creare un gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="9393c-191">Create a local network gateway.</span></span> <span data-ttu-id="9393c-192">In una rete virtuale, gateway di rete locale hello si riferisce solitamente percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="9393c-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="9393c-193">In questo caso, il gateway di rete locale hello fa riferimento tooyour rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="9393c-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="9393c-194">Assegnare un nome mediante il quale Azure può fare riferimento tooit e anche specificare prefisso dello spazio di indirizzo hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="9393c-195">Azure Usa prefisso dell'indirizzo IP hello è specificare tooidentify quali tooyour toosend traffico posizione locale.</span><span class="sxs-lookup"><span data-stu-id="9393c-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="9393c-196">Se è necessario in un secondo momento, informazioni di hello tooadjust qui prima di creare il gateway, è possibile modificare i valori hello ed esempio hello esecuzione nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9393c-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="9393c-197">**-Nome** è il nome di hello da gateway di rete locale tooassign toorefer toohello.</span><span class="sxs-lookup"><span data-stu-id="9393c-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="9393c-198">
   **AddressPrefix -** è hello spazio di indirizzi per una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="9393c-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="9393c-199">
**-GatewayIpAddress** è hello indirizzo IP pubblico del gateway hello classic della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9393c-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="9393c-200">Assicurarsi che l'indirizzo IP corretto di tooreflect hello di esempio seguenti hello toochange.</span><span class="sxs-lookup"><span data-stu-id="9393c-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="9393c-201">Richiedere un pubblico IP indirizzo toobe toohello allocato gateway di rete virtuale per Gestione risorse VNet hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="9393c-202">È possibile specificare l'indirizzo IP hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="9393c-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="9393c-203">indirizzo IP Hello viene allocata dinamicamente toohello gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9393c-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="9393c-204">Tuttavia, ciò non significa modifiche all'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="9393c-205">tempo di Hello solo modifiche all'indirizzo IP gateway hello rete virtuale quando è hello gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="9393c-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="9393c-206">Non modifica in ridimensionamento, reimpostare o altri interni/aggiornamenti del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="9393c-207">In questo passaggio viene anche impostata una variabile che verrà usata in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="9393c-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="9393c-208">Verificare che la rete virtuale disponga di una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="9393c-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="9393c-209">Se non esiste alcuna subnet del gateway, aggiungerne una.</span><span class="sxs-lookup"><span data-stu-id="9393c-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="9393c-210">Assicurarsi di subnet del gateway hello è denominata *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="9393c-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="9393c-211">Recuperare subnet hello usata per il gateway hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9393c-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="9393c-212">In questo passaggio, è inoltre possibile impostare una variabile toobe utilizzata nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="9393c-213">**-Nome** nome hello di VNet il gestore delle risorse.</span><span class="sxs-lookup"><span data-stu-id="9393c-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="9393c-214">
   **-ResourceGroupName** è il gruppo di risorse hello che hello rete virtuale è associato.</span><span class="sxs-lookup"><span data-stu-id="9393c-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="9393c-215">subnet del gateway Hello deve esistere per la rete virtuale e deve essere denominato *GatewaySubnet* toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="9393c-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="9393c-216">Creare una configurazione di indirizzamento IP del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="9393c-217">configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="9393c-218">Utilizzare hello toocreate di esempio seguente la configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="9393c-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="9393c-219">In questo passaggio, hello **- struttura** e **- PublicIpAddressId** parametri devono essere passati proprietà id hello da hello subnet e oggetti di indirizzo IP, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="9393c-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="9393c-220">Non è possibile usare una semplice stringa.</span><span class="sxs-lookup"><span data-stu-id="9393c-220">You can't use a simple string.</span></span> <span data-ttu-id="9393c-221">Queste variabili vengono impostate in hello passaggio toorequest un indirizzo IP pubblico e hello passaggio tooretrieve hello subnet.</span><span class="sxs-lookup"><span data-stu-id="9393c-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="9393c-222">Creare i gateway di rete virtuale di gestione risorse di hello eseguendo hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9393c-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="9393c-223">Hello `-VpnType` deve essere *tipo RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="9393c-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="9393c-224">Può richiedere più di 45 minuti per toocreate gateway hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="9393c-225">Copiare l'indirizzo IP pubblico hello dopo aver creato gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="9393c-226">Utilizzare quando si configurano le impostazioni di rete locale hello per una rete virtuale classica.</span><span class="sxs-lookup"><span data-stu-id="9393c-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="9393c-227">È possibile utilizzare hello seguente indirizzo IP pubblico di cmdlet tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="9393c-228">Hello indirizzo IP pubblico è elencato nella hello restituito come *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="9393c-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="9393c-229">Sezione 3: Modificare le impostazioni di hello classiche rete virtuale del sito locale</span><span class="sxs-lookup"><span data-stu-id="9393c-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="9393c-230">In questa sezione, è possibile utilizzare con hello classic rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9393c-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="9393c-231">Sostituire l'indirizzo IP di segnaposto hello utilizzato quando si specificano le impostazioni di sito locale hello che verrà utilizzato tooconnect toohello gateway di gestione risorse VNet.</span><span class="sxs-lookup"><span data-stu-id="9393c-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="9393c-232">Esportare i file di configurazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="9393c-233">Utilizzando un editor di testo, modificare il valore di hello per VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="9393c-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="9393c-234">Sostituire l'indirizzo IP segnaposto hello con indirizzo IP pubblico hello del gateway di gestione risorse di hello e quindi salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="9393c-235">Hello importazione modificato tooAzure file configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="9393c-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="9393c-236"><a name="connect"></a>Sezione 4: Creare una connessione tra gateway hello</span><span class="sxs-lookup"><span data-stu-id="9393c-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="9393c-237">Creazione di una connessione tra gateway hello richiede PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9393c-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="9393c-238">Potrebbe essere necessario tooadd la versione classica di hello toouse Account Azure hello di cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9393c-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="9393c-239">toodo in tal caso, utilizzare **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="9393c-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="9393c-240">Nella console di PowerShell hello, impostare la chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="9393c-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="9393c-241">Prima di eseguire i cmdlet di hello, fare riferimento toohello file di configurazione di rete che è stato scaricato per hello esatto dei nomi da Azure prevede toosee.</span><span class="sxs-lookup"><span data-stu-id="9393c-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="9393c-242">Quando si specifica il nome di hello di una rete virtuale che contiene spazi, utilizzare le virgolette singole per racchiudere valori hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="9393c-243">Nell'esempio seguente, **- VNetName** nome hello di hello rete virtuale classica e **- LocalNetworkSiteName** hello nome specificato per il sito di rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="9393c-244">Hello **- SharedKey** è un valore che si generano e si specifica.</span><span class="sxs-lookup"><span data-stu-id="9393c-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="9393c-245">Nell'esempio hello, abbiamo utilizzato "abc123", ma è possibile generare e utilizzare un nome più complesse.</span><span class="sxs-lookup"><span data-stu-id="9393c-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="9393c-246">Hello importante cosa è il valore di hello specificato qui deve essere hello che stesso valore specificato nel passaggio successivo hello quando si crea la connessione.</span><span class="sxs-lookup"><span data-stu-id="9393c-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="9393c-247">Hello restituito mostreranno **stato: ha esito positivo**.</span><span class="sxs-lookup"><span data-stu-id="9393c-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="9393c-248">Creare una connessione VPN hello eseguendo i seguenti comandi hello:</span><span class="sxs-lookup"><span data-stu-id="9393c-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="9393c-249">Impostare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="9393c-250">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="9393c-250">Create hello connection.</span></span> <span data-ttu-id="9393c-251">Si noti che hello **- ConnectionType** IPSec, non Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="9393c-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="9393c-252">Sezione 5: Verificare le connessioni</span><span class="sxs-lookup"><span data-stu-id="9393c-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="9393c-253">connessione hello tooverify il classico tooyour di rete virtuale VNet Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="9393c-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="9393c-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9393c-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="9393c-255">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9393c-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="9393c-256">connessione hello tooverify il tooyour VNet Gestione risorse di rete virtuale classica</span><span class="sxs-lookup"><span data-stu-id="9393c-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="9393c-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9393c-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="9393c-258">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9393c-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="9393c-259"><a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9393c-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

