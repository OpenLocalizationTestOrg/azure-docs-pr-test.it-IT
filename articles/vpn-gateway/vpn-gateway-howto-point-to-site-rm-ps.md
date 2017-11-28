---
title: 'Connettere un computer a una rete virtuale di Azure da punto a sito con l''autenticazione del certificato: PowerShell | Microsoft Docs'
description: Connettere in modo sicuro un computer alla rete virtuale creando una connessione gateway VPN da punto a sito con l'autenticazione del certificato. Questo articolo si applica al modello di distribuzione di Resource Manager e usa PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 2e072ada13b8c742fe7f2e14737c9376f7677906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="34a4e-104">Configurare una connessione da punto a sito a una rete virtuale usando l'autenticazione del certificato: PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a4e-104">Configure a Point-to-Site connection to a VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="34a4e-105">Questo articolo illustra come creare una rete virtuale con una connessione da punto a sito nel modello di distribuzione Resource Manager usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34a4e-105">This article shows you how to create a VNet with a Point-to-Site connection in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="34a4e-106">Questa configurazione usa i certificati per autenticare il client di connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-106">This configuration uses certificates to authenticate the connecting client.</span></span> <span data-ttu-id="34a4e-107">È anche possibile creare questa configurazione usando strumenti o modelli di distribuzione diversi selezionando un'opzione differente nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="34a4e-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="34a4e-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="34a4e-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="34a4e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34a4e-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="34a4e-110">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="34a4e-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="34a4e-111">Un gateway VPN da punto a sito (P2S) consente di creare una connessione sicura alla rete virtuale da un singolo computer client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection to your virtual network from an individual client computer.</span></span> <span data-ttu-id="34a4e-112">Le connessioni VPN da punto a sito sono utili per connettersi alla rete virtuale da una posizione remota, ad esempio nel caso di telecomunicazioni da casa o durante una riunione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-112">Point-to-Site VPN connections are useful when you want to connect to your VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="34a4e-113">Una VPN P2S è anche una soluzione utile da usare al posto di una VPN da sito a sito quando solo pochi client devono connettersi a una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-113">A P2S VPN is also a useful solution to use instead of a Site-to-Site VPN when you have only a few clients that need to connect to a VNet.</span></span>

<span data-ttu-id="34a4e-114">P2S usa Secure Socket Tunneling Protocol (SSTP), un protocollo VPN basato su SSL.</span><span class="sxs-lookup"><span data-stu-id="34a4e-114">P2S uses the Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="34a4e-115">Una connessione VPN P2S viene stabilita avviandola dal computer client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-115">A P2S VPN connection is established by starting it from the client computer.</span></span>

![Connettere un computer a una rete virtuale di Azure: diagramma di connessione da punto a sito](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="34a4e-117">Le connessioni da punto a sito con l'autenticazione del certificato richiedono gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="34a4e-117">Point-to-Site certificate authentication connections require the following:</span></span>

* <span data-ttu-id="34a4e-118">Un gateway VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="34a4e-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="34a4e-119">La chiave pubblica (file CER) per un certificato radice, caricato in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-119">The public key (.cer file) for a root certificate, which is uploaded to Azure.</span></span> <span data-ttu-id="34a4e-120">Il certificato, dopo essere stato caricato, viene considerato un certificato attendibile e viene usato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-120">Once the certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="34a4e-121">Un certificato client generato dal certificato radice e installato in ogni computer client che si connetterà alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-121">A client certificate that is generated from the root certificate and installed on each client computer that will connect to the VNet.</span></span> <span data-ttu-id="34a4e-122">Questo certificato viene usato per l'autenticazione client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="34a4e-123">Un pacchetto di configurazione del client VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-123">A VPN client configuration package.</span></span> <span data-ttu-id="34a4e-124">Il pacchetto di configurazione del client VPN contiene le informazioni necessarie per la connessione del client alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-124">The VPN client configuration package contains the necessary information for the client to connect to the VNet.</span></span> <span data-ttu-id="34a4e-125">Il pacchetto configura il client VPN esistente, nativo del sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="34a4e-125">The package configures the existing VPN client that is native to the Windows operating system.</span></span> <span data-ttu-id="34a4e-126">Ogni client che si connette deve essere configurato usando il pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-126">Each client that connects must be configured using the configuration package.</span></span>

<span data-ttu-id="34a4e-127">Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="34a4e-128">La connessione VPN viene creata tramite SSTP (Secure Sockets Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="34a4e-128">The VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="34a4e-129">Sul lato server sono supportate le versioni 1.0, 1.1 e 1.2 di SSTP.</span><span class="sxs-lookup"><span data-stu-id="34a4e-129">On the server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="34a4e-130">Il client decide quale versione usare.</span><span class="sxs-lookup"><span data-stu-id="34a4e-130">The client decides which version to use.</span></span> <span data-ttu-id="34a4e-131">Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2.</span><span class="sxs-lookup"><span data-stu-id="34a4e-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="34a4e-132">Per altre informazioni sulla connettività da punto a sito, consultare le [Domande frequenti sulla connettività da punto a sito](#faq) alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-132">For more information about Point-to-Site connections, see the [Point-to-Site FAQ](#faq) at the end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="34a4e-133">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="34a4e-133">Before beginning</span></span>

* <span data-ttu-id="34a4e-134">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="34a4e-135">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="34a4e-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="34a4e-136">Installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34a4e-136">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="34a4e-137">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="34a4e-137">For more information about installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="34a4e-138"><a name="example"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="34a4e-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="34a4e-139">È possibile usare i valori di esempio per creare un ambiente di test o fare riferimento a questi valori per comprendere meglio gli esempi di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-139">You can use the example values to create a test environment, or refer to these values to better understand the examples in this article.</span></span> <span data-ttu-id="34a4e-140">Le variabili sono state impostate nella sezione [1](#declare) di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-140">We set the variables in section [1](#declare) of the article.</span></span> <span data-ttu-id="34a4e-141">È possibile seguire la procedura dettagliata e usare i valori senza modificarle oppure modificarli in base all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="34a4e-141">You can either use the steps as a walk-through and use the values without changing them, or change them to reflect your environment.</span></span> 

* <span data-ttu-id="34a4e-142">**Nome: VNet1**</span><span class="sxs-lookup"><span data-stu-id="34a4e-142">**Name: VNet1**</span></span>
* <span data-ttu-id="34a4e-143">**Spazio degli indirizzi: 192.168.0.0/16** e **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="34a4e-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="34a4e-144">Per questo esempio, si usa più di uno spazio indirizzi per mostrare che la configurazione funziona con più spazi indirizzi,</span><span class="sxs-lookup"><span data-stu-id="34a4e-144">For this example, we use more than one address space to illustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="34a4e-145">ma per questa configurazione non sono necessari più spazi indirizzi.</span><span class="sxs-lookup"><span data-stu-id="34a4e-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="34a4e-146">**Nome subnet: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="34a4e-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="34a4e-147">**Intervallo di indirizzi subnet: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="34a4e-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="34a4e-148">**Nome subnet: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="34a4e-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="34a4e-149">**Intervallo di indirizzi subnet: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="34a4e-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="34a4e-150">**Nome subnet: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="34a4e-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="34a4e-151">Il nome subnet *GatewaySubnet* è obbligatorio per il funzionamento del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-151">The Subnet name *GatewaySubnet* is mandatory for the VPN gateway to work.</span></span>
  * <span data-ttu-id="34a4e-152">**Intervallo di indirizzi subnet del gateway: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="34a4e-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="34a4e-153">**Pool di indirizzi client VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="34a4e-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="34a4e-154">I client VPN che si connettono alla rete virtuale con questa connessione da punto a sito ricevono un indirizzo IP dal pool di indirizzi client VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-154">VPN clients that connect to the VNet using this Point-to-Site connection receive an IP address from the VPN client address pool.</span></span>
* <span data-ttu-id="34a4e-155">**Sottoscrizione:** se si hanno più sottoscrizioni, verificare di usare quella corretta.</span><span class="sxs-lookup"><span data-stu-id="34a4e-155">**Subscription:** If you have more than one subscription, verify that you are using the correct one.</span></span>
* <span data-ttu-id="34a4e-156">**Gruppo di risorse: TestRG**</span><span class="sxs-lookup"><span data-stu-id="34a4e-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="34a4e-157">**Località: Stati Uniti orientali**</span><span class="sxs-lookup"><span data-stu-id="34a4e-157">**Location: East US**</span></span>
* <span data-ttu-id="34a4e-158">**Server DNS: indirizzo IP** del server DNS che si vuole usare per la risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="34a4e-158">**DNS Server: IP address** of the DNS server that you want to use for name resolution.</span></span>
* <span data-ttu-id="34a4e-159">**Nome del gateway: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="34a4e-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="34a4e-160">**Nome dell'IP pubblico: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="34a4e-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="34a4e-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="34a4e-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="34a4e-162"><a name="declare"></a>1. Accedere e impostare le variabili</span><span class="sxs-lookup"><span data-stu-id="34a4e-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="34a4e-163">In questa sezione si accede e si dichiarano i valori usati per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-163">In this section, you log in and declare the values used for this configuration.</span></span> <span data-ttu-id="34a4e-164">I valori dichiarati saranno usati negli script di esempio.</span><span class="sxs-lookup"><span data-stu-id="34a4e-164">The declared values are used in the sample scripts.</span></span> <span data-ttu-id="34a4e-165">È possibile modificare i valori in base all'ambiente personalizzato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-165">Change the values to reflect your own environment.</span></span> <span data-ttu-id="34a4e-166">In alternativa, è possibile usare i valori dichiarati e seguire la procedura come un esercizio.</span><span class="sxs-lookup"><span data-stu-id="34a4e-166">Or, you can use the declared values and go through the steps as an exercise.</span></span>

1. <span data-ttu-id="34a4e-167">Aprire la console di PowerShell con privilegi elevati e accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-167">Open your PowerShell console with elevated privileges, and log in to your Azure account.</span></span> <span data-ttu-id="34a4e-168">Il cmdlet richiederà le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="34a4e-168">This cmdlet prompts you for the login credentials.</span></span> <span data-ttu-id="34a4e-169">Dopo l'accesso, vengono scaricate le impostazioni dell'account in modo che siano disponibili per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34a4e-169">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="34a4e-170">Ottenere un elenco delle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="34a4e-171">Specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="34a4e-171">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="34a4e-172">Dichiarare le variabili da usare.</span><span class="sxs-lookup"><span data-stu-id="34a4e-172">Declare the variables that you want to use.</span></span> <span data-ttu-id="34a4e-173">Usare l'esempio seguente, sostituendo i valori con quelli personalizzati, se necessario.</span><span class="sxs-lookup"><span data-stu-id="34a4e-173">Use the following sample, substituting the values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="34a4e-174"><a name="ConfigureVNet"></a>2. Configurare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="34a4e-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="34a4e-175">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="34a4e-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="34a4e-176">Creare le configurazioni delle subnet per la rete virtuale, denominandole *FrontEnd*, *BackEnd* e *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="34a4e-176">Create the subnet configurations for the virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="34a4e-177">Questi prefissi devono fare parte dello spazio indirizzi della rete virtuale dichiarato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-177">These prefixes must be part of the VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="34a4e-178">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-178">Create the virtual network.</span></span>

  <span data-ttu-id="34a4e-179">In questo esempio il server DNS è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-179">In this example, the DNS server is optional.</span></span> <span data-ttu-id="34a4e-180">Se si specifica un valore, non verrà creato un nuovo server DNS.</span><span class="sxs-lookup"><span data-stu-id="34a4e-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="34a4e-181">L'indirizzo IP del server DNS specificato deve essere un server DNS in grado di risolvere i nomi per le risorse a cui ci si connette.</span><span class="sxs-lookup"><span data-stu-id="34a4e-181">The DNS server IP address that you specify should be a DNS server that can resolve the names for the resources you are connecting to.</span></span> <span data-ttu-id="34a4e-182">Per questo esempio, è stato usato un indirizzo IP privato, ma è probabile che non si tratti dell'indirizzo IP del server DNS.</span><span class="sxs-lookup"><span data-stu-id="34a4e-182">For this example, we used a private IP address, but it is likely that this is not the IP address of your DNS server.</span></span> <span data-ttu-id="34a4e-183">Assicurarsi di usare valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-183">Be sure to use your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="34a4e-184">Specificare le variabili per la rete virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="34a4e-184">Specify the variables for the virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="34a4e-185">Un gateway VPN deve avere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="34a4e-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="34a4e-186">È necessario richiedere prima di tutto la risorsa dell'indirizzo IP e quindi farvi riferimento durante la creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-186">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="34a4e-187">L'indirizzo IP viene assegnato dinamicamente alla risorsa durante la creazione del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-187">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="34a4e-188">Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*.</span><span class="sxs-lookup"><span data-stu-id="34a4e-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="34a4e-189">Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici.</span><span class="sxs-lookup"><span data-stu-id="34a4e-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="34a4e-190">Ciò non significa tuttavia che l'indirizzo IP venga modificato dopo l'assegnazione al gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-190">However, it doesn't mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="34a4e-191">L'indirizzo IP pubblico viene modificato solo quando il gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-191">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="34a4e-192">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="34a4e-193">Richiedere un indirizzo IP pubblico assegnato dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="34a4e-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="34a4e-194"><a name="creategateway"></a>3. Creare il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="34a4e-194"><a name="creategateway"></a>3. Create the VPN gateway</span></span>

<span data-ttu-id="34a4e-195">Configurare e creare il gateway di rete virtuale per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-195">Configure and create the virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="34a4e-196">*-GatewayType* deve essere **Vpn** e *-VpnType* deve essere **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="34a4e-196">The *-GatewayType* must be **Vpn** and the *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="34a4e-197">Per il completamento di un gateway VPN possono essere necessari fino a 45 minuti, in base allo [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md) selezionato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-197">A VPN gateway can take up to 45 minutes to complete, depending on the [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="34a4e-198"><a name="addresspool"></a>4. Aggiungere il pool di indirizzi client VPN</span><span class="sxs-lookup"><span data-stu-id="34a4e-198"><a name="addresspool"></a>4. Add the VPN client address pool</span></span>

<span data-ttu-id="34a4e-199">Al termine della creazione del gateway VPN, è possibile aggiungere il pool di indirizzi del client VPN.</span><span class="sxs-lookup"><span data-stu-id="34a4e-199">After the VPN gateway finishes creating, you can add the VPN client address pool.</span></span> <span data-ttu-id="34a4e-200">Il pool di indirizzi client VPN è l'intervallo da cui i client VPN ricevono un indirizzo IP al momento della connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-200">The VPN client address pool is the range from which the VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="34a4e-201">Usare un intervallo di indirizzi IP privati che non si sovrapponga con la posizione locale da cui viene effettuata la connessione o con la rete virtuale a cui ci si vuole connettere.</span><span class="sxs-lookup"><span data-stu-id="34a4e-201">Use a private IP address range that does not overlap with the on-premises location that you connect from, or with the VNet that you want to connect to.</span></span> <span data-ttu-id="34a4e-202">In questo esempio, il pool di indirizzi client VPN viene dichiarato come [variabile](#declare) nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="34a4e-202">In this example, the VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="34a4e-203"><a name="Certificates"></a>5. Generare i certificati</span><span class="sxs-lookup"><span data-stu-id="34a4e-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="34a4e-204">I certificati vengono usati da Azure per autenticare i client VPN per VPN da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="34a4e-204">Certificates are used by Azure to authenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="34a4e-205">È necessario caricare le informazioni della chiave pubblica del certificato radice in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-205">You upload the public key information of the root certificate to Azure.</span></span> <span data-ttu-id="34a4e-206">La chiave pubblica viene quindi considerata "attendibile".</span><span class="sxs-lookup"><span data-stu-id="34a4e-206">The public key is then considered 'trusted'.</span></span> <span data-ttu-id="34a4e-207">I certificati client devono essere generati dal certificato radice attendibile e quindi installati in ogni computer client nell'archivio certificati Certificati - Utente corrente/Personale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-207">Client certificates must be generated from the trusted root certificate, and then installed on each client computer in the Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="34a4e-208">Il certificato viene usato per l'autenticazione del client all'avvio di una connessione alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-208">The certificate is used to authenticate the client when it initiates a connection to the VNet.</span></span> 

<span data-ttu-id="34a4e-209">Se usati, i certificati autofirmati devono essere creati con parametri specifici.</span><span class="sxs-lookup"><span data-stu-id="34a4e-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="34a4e-210">È possibile creare un certificato autofirmato seguendo le istruzioni per [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md) oppure è possibile usare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) se Windows 10 non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="34a4e-210">You can create a self-signed certificate using the instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="34a4e-211">È importante seguire i passaggi delle istruzioni quando si generano certificati radice autofirmati e certificati client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-211">It's important that you follow the steps in the instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="34a4e-212">In caso contrario, i certificati generati non saranno compatibili con le connessioni P2S e si riceverà un errore di connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-212">Otherwise, the certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="34a4e-213"><a name="cer"></a>1. Ottenere il file CER per il certificato radice</span><span class="sxs-lookup"><span data-stu-id="34a4e-213"><a name="cer"></a>1. Obtain the .cer file for the root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="34a4e-214"><a name="generate"></a>2. Generazione di un certificato client</span><span class="sxs-lookup"><span data-stu-id="34a4e-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="34a4e-215"><a name="upload"></a>6. Caricare le informazioni sulla chiave pubblica del certificato radice</span><span class="sxs-lookup"><span data-stu-id="34a4e-215"><a name="upload"></a>6. Upload the root certificate public key information</span></span>

<span data-ttu-id="34a4e-216">Verificare che la creazione del gateway VPN sia stata completata.</span><span class="sxs-lookup"><span data-stu-id="34a4e-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="34a4e-217">In tal caso sarà possibile caricare il file CER, contenente le informazioni sulla chiave pubblica, per un certificato radice attendibile in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-217">Once it has completed, you can upload the .cer file (which contains the public key information) for a trusted root certificate to Azure.</span></span> <span data-ttu-id="34a4e-218">Al termine del caricamento di un file CER, Azure lo può usare per autenticare i client che hanno installato un certificato client generato dal certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="34a4e-218">Once a.cer file is uploaded, Azure can use it to authenticate clients that have installed a client certificate generated from the trusted root certificate.</span></span> <span data-ttu-id="34a4e-219">È possibile caricare fino a 20 file di certificato radice attendibile aggiuntivi in un secondo momento, se necessario.</span><span class="sxs-lookup"><span data-stu-id="34a4e-219">You can upload additional trusted root certificate files - up to a total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="34a4e-220">Dichiarare la variabile per il nome del certificato, sostituendo il valore con il proprio.</span><span class="sxs-lookup"><span data-stu-id="34a4e-220">Declare the variable for your certificate name, replacing the value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="34a4e-221">Sostituire il percorso file con il proprio e quindi eseguire i cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34a4e-221">Replace the file path with your own, and then run the cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="34a4e-222">Caricare le informazioni sulla chiave pubblica in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-222">Upload the public key information to Azure.</span></span> <span data-ttu-id="34a4e-223">Dopo aver caricato le informazioni sul certificato, Azure lo considera un certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="34a4e-223">Once the certificate information is uploaded, Azure considers this to be a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="34a4e-224"><a name="clientconfig"></a>7. Scaricare il pacchetto di configurazione del client VPN</span><span class="sxs-lookup"><span data-stu-id="34a4e-224"><a name="clientconfig"></a>7. Download the VPN client configuration package</span></span>

<span data-ttu-id="34a4e-225">Per connettersi a una rete virtuale usando la VPN da punto a sito, ogni client deve installare un pacchetto di configurazione del client che configura il client VPN nativo con le impostazioni e i file necessari per connettersi alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-225">To connect to a VNet using a Point-to-Site VPN, each client must install a client configuration package that configures the native VPN client with the settings and files that are necessary to connect to the virtual network.</span></span> <span data-ttu-id="34a4e-226">Il pacchetto di configurazione del client VPN configura il client VPN Windows nativo, non installa un client VPN nuovo o diverso.</span><span class="sxs-lookup"><span data-stu-id="34a4e-226">The VPN client configuration package configures the native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="34a4e-227">È possibile usare lo stesso pacchetto di configurazione del client VPN in ogni computer client, a condizione che la versione corrisponda all'architettura del client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-227">You can use the same VPN client configuration package on each client computer, as long as the version matches the architecture for the client.</span></span> <span data-ttu-id="34a4e-228">Per l'elenco dei sistemi operativi client supportati, vedere [Domande frequenti sulla connettività da punto a sito](#faq) alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-228">For the list of client operating systems that are supported, see the [Point-to-Site connections FAQ](#faq) at the end of this article.</span></span>

1. <span data-ttu-id="34a4e-229">Dopo aver creato il gateway, è possibile generare e scaricare il pacchetto di configurazione client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-229">After the gateway has been created, you can generate and download the client configuration package.</span></span> <span data-ttu-id="34a4e-230">Questo esempio scarica il pacchetto per i client a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="34a4e-230">This example downloads the package for 64-bit clients.</span></span> <span data-ttu-id="34a4e-231">Per scaricare il client a 32 bit, sostituire "Amd64" con "x86".</span><span class="sxs-lookup"><span data-stu-id="34a4e-231">If you want to download the 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="34a4e-232">È anche possibile scaricare il client VPN usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-232">You can also download the VPN client by using the Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="34a4e-233">Copiare e incollare il collegamento restituito in un Web browser per scaricare il pacchetto, facendo attenzione a rimuovere le virgolette che racchiudono il collegamento.</span><span class="sxs-lookup"><span data-stu-id="34a4e-233">Copy and paste the link that is returned to a web browser to download the package, taking care to remove the quotes surrounding the link.</span></span> 
3. <span data-ttu-id="34a4e-234">Scaricare e installare il pacchetto nel computer client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-234">Download and install the package on the client computer.</span></span> <span data-ttu-id="34a4e-235">Se viene visualizzato un popup SmartScreen, fare clic su **Altre informazioni** e quindi su **Esegui comunque** per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="34a4e-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="34a4e-236">È anche possibile salvare il pacchetto per l'installazione su altri computer client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-236">You can also save the package to install on other client computers.</span></span>
4. <span data-ttu-id="34a4e-237">Nel computer client passare a **Impostazioni di rete** e fare clic su **VPN**.</span><span class="sxs-lookup"><span data-stu-id="34a4e-237">On the client computer, navigate to **Network Settings** and click **VPN**.</span></span> <span data-ttu-id="34a4e-238">La connessione VPN viene visualizzata con il nome della rete virtuale a cui si connette.</span><span class="sxs-lookup"><span data-stu-id="34a4e-238">The VPN connection shows the name of the virtual network that it connects to.</span></span>

## <span data-ttu-id="34a4e-239"><a name="clientcertificate"></a>8. Installare un certificato client esportato</span><span class="sxs-lookup"><span data-stu-id="34a4e-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="34a4e-240">Se si vuole creare una connessione da punto a sito da un computer client diverso da quello usato per generare i certificati client, è necessario installare un certificato client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-240">If you want to create a P2S connection from a client computer other than the one you used to generate the client certificates, you need to install a client certificate.</span></span> <span data-ttu-id="34a4e-241">Quando si installa un certificato client, è necessaria la password che è stata creata durante l'esportazione del certificato client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-241">When installing a client certificate, you need the password that was created when the client certificate was exported.</span></span> <span data-ttu-id="34a4e-242">In genere è sufficiente fare doppio clic sul certificato e installarlo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-242">Typically, it is just a matter of double-clicking the certificate and installing it.</span></span>

<span data-ttu-id="34a4e-243">Verificare che il certificato client sia stato esportato come PFX con l'intera catena di certificati (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="34a4e-243">Make sure the client certificate was exported as a .pfx along with the entire certificate chain (which is the default).</span></span> <span data-ttu-id="34a4e-244">In caso contrario, le informazioni del certificato radice non sono presenti nel computer client e il client non potrà essere autenticato correttamente.</span><span class="sxs-lookup"><span data-stu-id="34a4e-244">Otherwise, the root certificate information isn't present on the client computer and the client won't be able to authenticate properly.</span></span> <span data-ttu-id="34a4e-245">Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="34a4e-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="34a4e-246"><a name="connect"></a>9. Connect to Azure</span><span class="sxs-lookup"><span data-stu-id="34a4e-246"><a name="connect"></a>9. Connect to Azure</span></span>

1. <span data-ttu-id="34a4e-247">Per connettersi alla rete virtuale, nel computer client passare alle connessioni VPN e individuare quella creata,</span><span class="sxs-lookup"><span data-stu-id="34a4e-247">To connect to your VNet, on the client computer, navigate to VPN connections and locate the VPN connection that you created.</span></span> <span data-ttu-id="34a4e-248">che ha lo stesso nome della rete virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="34a4e-248">It is named the same name as your virtual network.</span></span> <span data-ttu-id="34a4e-249">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="34a4e-249">Click **Connect**.</span></span> <span data-ttu-id="34a4e-250">È possibile che venga visualizzato un messaggio popup che fa riferimento all'uso del certificato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-250">A pop-up message may appear that refers to using the certificate.</span></span> <span data-ttu-id="34a4e-251">Fare clic su **Continua** per usare privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-251">Click **Continue** to use elevated privileges.</span></span> 
2. <span data-ttu-id="34a4e-252">Nella pagina **Stato connessione** fare clic su **Connetti** per avviare la connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-252">On the **Connection** status page, click **Connect** to start the connection.</span></span> <span data-ttu-id="34a4e-253">Se viene visualizzato un **Seleziona certificato** dello schermo, verificare che il certificato client visualizzato sia quello che si desidera utilizzare per la connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-253">If you see a **Select Certificate** screen, verify that the client certificate showing is the one that you want to use to connect.</span></span> <span data-ttu-id="34a4e-254">In caso contrario, usare la freccia a discesa per selezionare il certificato corretto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="34a4e-254">If it is not, use the drop-down arrow to select the correct certificate, and then click **OK**.</span></span>

  ![Connessione del client VPN ad Azure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="34a4e-256">Verrà stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-256">Your connection is established.</span></span>

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="34a4e-258">Risoluzione dei problemi delle connessioni P2S</span><span class="sxs-lookup"><span data-stu-id="34a4e-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="34a4e-259"><a name="verify"></a>10. Verificare la connessione</span><span class="sxs-lookup"><span data-stu-id="34a4e-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="34a4e-260">Per verificare che la connessione VPN è attiva, aprire un prompt dei comandi con privilegi elevati ed eseguire *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="34a4e-260">To verify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="34a4e-261">Visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-261">View the results.</span></span> <span data-ttu-id="34a4e-262">Si noti che l'indirizzo IP ricevuto è uno degli indirizzi compresi nel pool di indirizzi del client VPN da punto a sito specificato al momento della configurazione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-262">Notice that the IP address you received is one of the addresses within the Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="34a4e-263">I risultati sono simili a questo esempio:</span><span class="sxs-lookup"><span data-stu-id="34a4e-263">The results are similar to this example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="34a4e-264"><a name="connectVM"></a>Connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="34a4e-264"><a name="connectVM"></a>Connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="34a4e-265"><a name="addremovecert"></a>Aggiungere o rimuovere un certificato radice</span><span class="sxs-lookup"><span data-stu-id="34a4e-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="34a4e-266">È possibile aggiungere e rimuovere certificati radice attendibili da Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="34a4e-267">Quando si rimuove un certificato radice, i client con un certificato generato da tale certificato radice non possono eseguire l'autenticazione e non potranno connettersi.</span><span class="sxs-lookup"><span data-stu-id="34a4e-267">When you remove a root certificate, clients that have a certificate generated from the root certificate can't authenticate and won't be able to connect.</span></span> <span data-ttu-id="34a4e-268">Per consentire ai client di eseguire l'autenticazione e connettersi, è necessario installare un nuovo certificato client generato da un certificato radice considerato attendibile (caricato) in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-268">If you want a client to authenticate and connect, you need to install a new client certificate generated from a root certificate that is trusted (uploaded) to Azure.</span></span>

### <span data-ttu-id="34a4e-269"><a name="addtrustedroot"></a>Per aggiungere un certificato radice attendibile</span><span class="sxs-lookup"><span data-stu-id="34a4e-269"><a name="addtrustedroot"></a>To add a trusted root certificate</span></span>

<span data-ttu-id="34a4e-270">In Azure è possibile aggiungere fino a 20 file CER di certificato radice.</span><span class="sxs-lookup"><span data-stu-id="34a4e-270">You can add up to 20 root certificate .cer files to Azure.</span></span> <span data-ttu-id="34a4e-271">La procedura seguente consente di aggiungere un certificato radice:</span><span class="sxs-lookup"><span data-stu-id="34a4e-271">The following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="34a4e-272"><a name="certmethod1"></a>Metodo 1</span><span class="sxs-lookup"><span data-stu-id="34a4e-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="34a4e-273">Si tratta del metodo più efficiente per caricare un certificato radice.</span><span class="sxs-lookup"><span data-stu-id="34a4e-273">This is the most efficient method to upload a root certificate.</span></span>

1. <span data-ttu-id="34a4e-274">Preparare il file CER da caricare:</span><span class="sxs-lookup"><span data-stu-id="34a4e-274">Prepare the .cer file to upload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="34a4e-275">Caricare il file.</span><span class="sxs-lookup"><span data-stu-id="34a4e-275">Upload the file.</span></span> <span data-ttu-id="34a4e-276">È possibile caricare un solo file alla volta.</span><span class="sxs-lookup"><span data-stu-id="34a4e-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="34a4e-277">Per verificare che il file del certificato sia stato caricato:</span><span class="sxs-lookup"><span data-stu-id="34a4e-277">To verify that the certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="34a4e-278"><a name="certmethod2"></a>Metodo 2</span><span class="sxs-lookup"><span data-stu-id="34a4e-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="34a4e-279">Questo metodo prevede più passaggi rispetto al Metodo 1, ma permette di ottenere lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-279">This method is has more steps than Method 1, but has the same result.</span></span> <span data-ttu-id="34a4e-280">Viene incluso qualora si voglia visualizzare i dati del certificato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-280">It is included in case you need to view the certificate data.</span></span>

1. <span data-ttu-id="34a4e-281">Creare e preparare il nuovo certificato da aggiungere in Azure.</span><span class="sxs-lookup"><span data-stu-id="34a4e-281">Create and prepare the new root certificate to add to Azure.</span></span> <span data-ttu-id="34a4e-282">Esportare la chiave pubblica come file CER con codifica Base 64 X.509 e aprirla con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-282">Export the public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="34a4e-283">Copiare i valori, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="34a4e-283">Copy the values, as shown in the following example:</span></span>

  ![certificato](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="34a4e-285">Durante la copia dei dati del certificato, assicurarsi di copiare il testo come unica riga continua senza ritorni a capo o avanzamenti riga.</span><span class="sxs-lookup"><span data-stu-id="34a4e-285">When copying the certificate data, make sure that you copy the text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="34a4e-286">Potrebbe essere necessario modificare la visualizzazione nell'editor di testo in "Show Symbol/Show all characters" (Mostra simbolo/Mostra tutti i caratteri) per visualizzare i ritorni a capo e gli avanzamenti riga.</span><span class="sxs-lookup"><span data-stu-id="34a4e-286">You may need to modify your view in the text editor to 'Show Symbol/Show all characters' to see the carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="34a4e-287">Specificare il nome del certificato e le informazioni sulla chiave come variabile.</span><span class="sxs-lookup"><span data-stu-id="34a4e-287">Specify the certificate name and key information as a variable.</span></span> <span data-ttu-id="34a4e-288">Sostituire le informazioni con i propri dati, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="34a4e-288">Replace the information with your own, as shown in the following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="34a4e-289">Aggiungere il nuovo certificato radice.</span><span class="sxs-lookup"><span data-stu-id="34a4e-289">Add the new root certificate.</span></span> <span data-ttu-id="34a4e-290">È possibile aggiungere solo un certificato alla volta.</span><span class="sxs-lookup"><span data-stu-id="34a4e-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="34a4e-291">È possibile verificare che il nuovo certificato sia stato aggiunto correttamente usando l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="34a4e-291">You can verify that the new certificate was added correctly by using the following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="34a4e-292"><a name="removerootcert"></a>Per rimuovere un certificato radice</span><span class="sxs-lookup"><span data-stu-id="34a4e-292"><a name="removerootcert"></a>To remove a root certificate</span></span>

1. <span data-ttu-id="34a4e-293">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="34a4e-293">Declare the variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="34a4e-294">Rimuovere il certificato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-294">Remove the certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="34a4e-295">Usare l'esempio seguente per verificare che il certificato sia stato rimosso correttamente.</span><span class="sxs-lookup"><span data-stu-id="34a4e-295">Use the following example to verify that the certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="34a4e-296"><a name="revoke"></a>Revocare un certificato client</span><span class="sxs-lookup"><span data-stu-id="34a4e-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="34a4e-297">È possibile revocare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-297">You can revoke client certificates.</span></span> <span data-ttu-id="34a4e-298">L'elenco di revoche di certificati consente di negare in modo selettivo la connettività da punto a sito basata sui singoli certificati client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-298">The certificate revocation list allows you to selectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="34a4e-299">Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="34a4e-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="34a4e-300">Se si rimuove un file con estensione cer del certificato radice attendibile da Azure, viene revocato l'accesso per tutti i certificati client generati o firmati dal certificato radice revocato.</span><span class="sxs-lookup"><span data-stu-id="34a4e-300">If you remove a trusted root certificate .cer from Azure, it revokes the access for all client certificates generated/signed by the revoked root certificate.</span></span> <span data-ttu-id="34a4e-301">La revoca di un certificato client, anziché del certificato radice, consente di continuare a usare gli altri certificati generati dal certificato radice per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-301">Revoking a client certificate, rather than the root certificate, allows the other certificates that were generated from the root certificate to continue to be used for authentication.</span></span>

<span data-ttu-id="34a4e-302">La regola generale è quella di usare il certificato radice per gestire l'accesso a livello di team o organizzazione, usando i certificati client revocati per il controllo di accesso con granularità fine su singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="34a4e-302">The common practice is to use the root certificate to manage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="34a4e-303"><a name="revokeclientcert"></a>Per revocare un certificato client</span><span class="sxs-lookup"><span data-stu-id="34a4e-303"><a name="revokeclientcert"></a>To revoke a client certificate</span></span>

1. <span data-ttu-id="34a4e-304">Ottenere l'identificazione personale del certificato client.</span><span class="sxs-lookup"><span data-stu-id="34a4e-304">Retrieve the client certificate thumbprint.</span></span> <span data-ttu-id="34a4e-305">Per altre informazioni, vedere [Procedura: recuperare l'identificazione personale di un certificato](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="34a4e-305">For more information, see [How to retrieve the Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="34a4e-306">Copiare le informazioni in un editor di testo e rimuovere tutti gli spazi in modo che sia una stringa continua.</span><span class="sxs-lookup"><span data-stu-id="34a4e-306">Copy the information to a text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="34a4e-307">Questa stringa viene dichiarata come variabile nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="34a4e-307">This string is declared as a variable in the next step.</span></span>
3. <span data-ttu-id="34a4e-308">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="34a4e-308">Declare the variables.</span></span> <span data-ttu-id="34a4e-309">Assicurarsi di dichiarare l'identificazione personale ottenuta nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="34a4e-309">Make sure to declare the thumbprint you retrieved in the previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="34a4e-310">Aggiungere l'identificazione personale all'elenco dei certificati revocati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-310">Add the thumbprint to the list of revoked certificates.</span></span> <span data-ttu-id="34a4e-311">Viene visualizzato il messaggio "Operazione completata" quando l'identificazione personale è stata aggiunta.</span><span class="sxs-lookup"><span data-stu-id="34a4e-311">You see "Succeeded" when the thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="34a4e-312">Verificare che l'identificazione personale sia stata aggiunta all'elenco di revoche di certificati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-312">Verify that the thumbprint was added to the certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="34a4e-313">Dopo aver aggiunto l'identificazione personale, il certificato non può più essere usato per la connessione.</span><span class="sxs-lookup"><span data-stu-id="34a4e-313">After the thumbprint has been added, the certificate can no longer be used to connect.</span></span> <span data-ttu-id="34a4e-314">Ai client che provano a connettersi con questo certificato verrà visualizzato un messaggio che informa che il certificato non è più valido.</span><span class="sxs-lookup"><span data-stu-id="34a4e-314">Clients that try to connect using this certificate receive a message saying that the certificate is no longer valid.</span></span>

### <span data-ttu-id="34a4e-315"><a name="reinstateclientcert"></a>Per reintegrare un certificato client</span><span class="sxs-lookup"><span data-stu-id="34a4e-315"><a name="reinstateclientcert"></a>To reinstate a client certificate</span></span>

<span data-ttu-id="34a4e-316">È possibile reintegrare un certificato client rimuovendo l'identificazione personale dall'elenco dei certificati client revocati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-316">You can reinstate a client certificate by removing the thumbprint from the list of revoked client certificates.</span></span>

1. <span data-ttu-id="34a4e-317">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="34a4e-317">Declare the variables.</span></span> <span data-ttu-id="34a4e-318">Assicurarsi di dichiarare l'identificazione personale corretta per il certificato che si vuole reintegrare.</span><span class="sxs-lookup"><span data-stu-id="34a4e-318">Make sure you declare the correct thumbprint for the certificate that you want to reinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="34a4e-319">Rimuovere l'identificazione personale del certificato dall'elenco di revoche di certificati.</span><span class="sxs-lookup"><span data-stu-id="34a4e-319">Remove the certificate thumbprint from the certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="34a4e-320">Verificare che l'identificazione personale sia stata rimossa dall'elenco di quelle revocate.</span><span class="sxs-lookup"><span data-stu-id="34a4e-320">Check if the thumbprint is removed from the revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="34a4e-321"><a name="faq"></a>Domande frequenti sulla connettività da punto a sito</span><span class="sxs-lookup"><span data-stu-id="34a4e-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="34a4e-322">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="34a4e-322">Next steps</span></span>
<span data-ttu-id="34a4e-323">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="34a4e-323">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="34a4e-324">Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="34a4e-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="34a4e-325">Per altre informazioni sulla rete e sulle macchine virtuali, vedere [Panoramica di rete delle macchine virtuali Linux e Azure](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34a4e-325">To understand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>