---
title: 'Connettersi a una rete virtuale di Azure utilizzando Point-to-Site di tooan computer e l''autenticazione del certificato: PowerShell | Documenti Microsoft'
description: Consente di connettersi in modo sicuro una rete virtuale di tooyour computer mediante la creazione di una connessione di gateway VPN Point-to-Site utilizzando l'autenticazione del certificato. In questo articolo si applica al modello di distribuzione di gestione delle risorse toohello e utilizza PowerShell.
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
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="e2450-104">Configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2450-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="e2450-105">In questo articolo viene illustrato come una rete virtuale con una connessione Point-to-Site nella distribuzione di gestione risorse di hello toocreate modello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2450-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e2450-106">Questa configurazione utilizza hello tooauthenticate certificati connessione del client.</span><span class="sxs-lookup"><span data-stu-id="e2450-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="e2450-107">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="e2450-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2450-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e2450-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e2450-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2450-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="e2450-110">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="e2450-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="e2450-111">Un gateway VPN da punto a sito (P2S) consente di creare una rete virtuale tooyour di connessione protetta da un computer client.</span><span class="sxs-lookup"><span data-stu-id="e2450-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="e2450-112">Le connessioni VPN Point-to-Site sono utili quando si desidera tooconnect tooyour rete virtuale da una posizione remota, ad esempio quando sono il telelavoro da casa o di una conferenza.</span><span class="sxs-lookup"><span data-stu-id="e2450-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="e2450-113">Una VPN P2S è anche un toouse soluzione utile anziché una VPN da sito a sito quando si dispone solo alcuni client che richiedono tooconnect tooa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="e2450-114">Usa P2S hello SSTP Secure Socket Tunneling Protocol (), che è un protocollo di rete VPN basata su SSL.</span><span class="sxs-lookup"><span data-stu-id="e2450-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="e2450-115">Viene stabilita una connessione di VPN P2S avviandolo dal computer client hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Connettersi a una rete virtuale di Azure - diagramma di connessione Point-to-Site di tooan computer](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="e2450-117">Connessioni di autenticazione Point-to-Site certificato requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="e2450-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="e2450-118">Un gateway VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="e2450-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="e2450-119">Hello chiave pubblica (file con estensione cer) per un certificato radice, ovvero tooAzure caricato.</span><span class="sxs-lookup"><span data-stu-id="e2450-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="e2450-120">Una volta caricato il certificato di hello, viene considerato un certificato attendibile e viene utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e2450-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="e2450-121">Un certificato client è generato dal certificato radice hello e installato in ogni computer client che si connetteranno toohello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="e2450-122">Questo certificato viene usato per l'autenticazione client.</span><span class="sxs-lookup"><span data-stu-id="e2450-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="e2450-123">Un pacchetto di configurazione del client VPN.</span><span class="sxs-lookup"><span data-stu-id="e2450-123">A VPN client configuration package.</span></span> <span data-ttu-id="e2450-124">pacchetto di configurazione client VPN Hello contiene le informazioni necessarie hello per hello client tooconnect toohello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="e2450-125">pacchetto di Hello Configura hello esistente client VPN è toohello nativo del sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="e2450-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="e2450-126">Ogni client che si connette devono essere configurate tramite il pacchetto di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="e2450-127">Le connessioni da punto a sito non richiedono un dispositivo VPN o un indirizzo IP pubblico locale.</span><span class="sxs-lookup"><span data-stu-id="e2450-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="e2450-128">connessione VPN Hello viene creato tramite SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="e2450-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="e2450-129">Sul lato server hello è supporta le versioni SSTP 1.0, 1.1 e 1.2.</span><span class="sxs-lookup"><span data-stu-id="e2450-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="e2450-130">client Hello decide quali toouse versione.</span><span class="sxs-lookup"><span data-stu-id="e2450-130">hello client decides which version toouse.</span></span> <span data-ttu-id="e2450-131">Per Windows 8.1 e versioni successive, SSTP usa per impostazione predefinita la versione 1.2.</span><span class="sxs-lookup"><span data-stu-id="e2450-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="e2450-132">Per ulteriori informazioni sulle connessioni Point-to-Site, vedere hello [Point-to-Site domande frequenti su](#faq) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e2450-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="e2450-133">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e2450-133">Before beginning</span></span>

* <span data-ttu-id="e2450-134">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="e2450-135">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e2450-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="e2450-136">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e2450-137">Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2450-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="e2450-138"><a name="example"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="e2450-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="e2450-139">È possibile utilizzare toocreate valori di esempio hello un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e2450-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="e2450-140">Le variabili di hello è impostata nella sezione [1](#declare) dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="e2450-141">È possibile utilizzare i passaggi di hello come una procedura dettagliata e utilizzare i valori hello senza alcuna modifica o modificarle tooreflect l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="e2450-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="e2450-142">**Nome: VNet1**</span><span class="sxs-lookup"><span data-stu-id="e2450-142">**Name: VNet1**</span></span>
* <span data-ttu-id="e2450-143">**Spazio degli indirizzi: 192.168.0.0/16** e **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="e2450-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="e2450-144">Per questo esempio, utilizziamo tooillustrate spazio di indirizzi più che il funzionamento della configurazione con più spazi degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e2450-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="e2450-145">ma per questa configurazione non sono necessari più spazi indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e2450-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="e2450-146">**Nome subnet: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="e2450-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="e2450-147">**Intervallo di indirizzi subnet: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="e2450-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="e2450-148">**Nome subnet: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="e2450-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="e2450-149">**Intervallo di indirizzi subnet: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="e2450-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="e2450-150">**Nome subnet: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="e2450-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="e2450-151">nome della Subnet Hello *GatewaySubnet* è obbligatorio per toowork gateway VPN di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="e2450-152">**Intervallo di indirizzi subnet del gateway: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="e2450-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="e2450-153">**Pool di indirizzi client VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="e2450-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="e2450-154">I client VPN che si connettono a una rete virtuale usando questa connessione Point-to-Site toohello riceveranno un indirizzo IP da pool di indirizzi del client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="e2450-155">**Sottoscrizione:** se si dispone di più di una sottoscrizione, verificare che si sta utilizzando hello corretto.</span><span class="sxs-lookup"><span data-stu-id="e2450-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="e2450-156">**Gruppo di risorse: TestRG**</span><span class="sxs-lookup"><span data-stu-id="e2450-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="e2450-157">**Località: Stati Uniti orientali**</span><span class="sxs-lookup"><span data-stu-id="e2450-157">**Location: East US**</span></span>
* <span data-ttu-id="e2450-158">**Server DNS: Indirizzo IP** del server DNS hello che si vuole toouse per la risoluzione dei nomi.</span><span class="sxs-lookup"><span data-stu-id="e2450-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="e2450-159">**Nome del gateway: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="e2450-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="e2450-160">**Nome dell'IP pubblico: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="e2450-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="e2450-161">**VpnType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="e2450-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="e2450-162"><a name="declare"></a>1. Accedere e impostare le variabili</span><span class="sxs-lookup"><span data-stu-id="e2450-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="e2450-163">In questa sezione si accedere e dichiarare i valori hello usati per questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="e2450-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="e2450-164">Hello dichiarato valori vengono utilizzati negli script di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="e2450-165">Modificare tooreflect valori hello al proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="e2450-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="e2450-166">In alternativa, è possibile utilizzare valori dichiarati hello ed eseguono passaggi hello come esercizio.</span><span class="sxs-lookup"><span data-stu-id="e2450-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="e2450-167">Aprire la console di PowerShell con privilegi elevati e Accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="e2450-168">Questo cmdlet richiede le credenziali di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="e2450-169">Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2450-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="e2450-170">Ottenere un elenco delle sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="e2450-171">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="e2450-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="e2450-172">Dichiarare le variabili di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="e2450-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="e2450-173">Utilizzare hello di esempio seguente, sostituendo i valori hello per la propria quando necessario.</span><span class="sxs-lookup"><span data-stu-id="e2450-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

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

## <span data-ttu-id="e2450-174"><a name="ConfigureVNet"></a>2. Configurare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e2450-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="e2450-175">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e2450-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="e2450-176">Creazione di configurazioni di subnet per la rete virtuale hello, denominarli hello *front-end*, *back-end*, e *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="e2450-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="e2450-177">I prefissi devono far parte di hello spazio degli indirizzi di rete virtuale che è stato dichiarato.</span><span class="sxs-lookup"><span data-stu-id="e2450-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="e2450-178">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-178">Create hello virtual network.</span></span>

  <span data-ttu-id="e2450-179">In questo esempio, i server DNS hello è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="e2450-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="e2450-180">Se si specifica un valore, non verrà creato un nuovo server DNS.</span><span class="sxs-lookup"><span data-stu-id="e2450-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="e2450-181">Hello indirizzo IP del server DNS specificato deve essere in grado di risolvere nomi hello per le risorse di hello a che ci si connette un server DNS.</span><span class="sxs-lookup"><span data-stu-id="e2450-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="e2450-182">In questo esempio è stato usato un indirizzo IP privato, ma è probabile che non si tratta di indirizzo IP di hello del server DNS.</span><span class="sxs-lookup"><span data-stu-id="e2450-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="e2450-183">Essere toouse che i valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e2450-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="e2450-184">Specificare le variabili di hello per la rete virtuale di hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e2450-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="e2450-185">Un gateway VPN deve avere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="e2450-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="e2450-186">Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="e2450-187">indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="e2450-188">Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*.</span><span class="sxs-lookup"><span data-stu-id="e2450-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="e2450-189">Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici.</span><span class="sxs-lookup"><span data-stu-id="e2450-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="e2450-190">Tuttavia, questo non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour.</span><span class="sxs-lookup"><span data-stu-id="e2450-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="e2450-191">Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="e2450-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="e2450-192">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="e2450-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="e2450-193">Richiedere un indirizzo IP pubblico assegnato dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e2450-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="e2450-194"><a name="creategateway"></a>3. Creare il gateway VPN hello</span><span class="sxs-lookup"><span data-stu-id="e2450-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="e2450-195">Configurare e creare il gateway di rete virtuale hello per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="e2450-196">Hello *- il tipo di gateway* deve essere **Vpn** hello e *- VpnType* deve essere **tipo RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="e2450-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="e2450-197">Un gateway VPN può richiedere fino a too45 minuti toocomplete, a seconda di hello [sku di gateway](vpn-gateway-about-vpn-gateway-settings.md) selezionate.</span><span class="sxs-lookup"><span data-stu-id="e2450-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="e2450-198"><a name="addresspool"></a>4. Aggiungere pool di indirizzi di client VPN hello</span><span class="sxs-lookup"><span data-stu-id="e2450-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="e2450-199">Al termine gateway VPN hello creazione, è possibile aggiungere hello client indirizzi della VPN.</span><span class="sxs-lookup"><span data-stu-id="e2450-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="e2450-200">pool di indirizzi del client VPN Hello è intervallo hello da cui i client VPN hello riceveranno un indirizzo IP durante la connessione.</span><span class="sxs-lookup"><span data-stu-id="e2450-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="e2450-201">Utilizzare un intervallo di indirizzi IP privato che non si sovrapponga con percorso locale hello che ci si connette da, o con rete virtuale che si desidera tooconnect per hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="e2450-202">In questo esempio hello pool di indirizzi del client VPN viene dichiarato come un [variabile](#declare) nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="e2450-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="e2450-203"><a name="Certificates"></a>5. Generare i certificati</span><span class="sxs-lookup"><span data-stu-id="e2450-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="e2450-204">I certificati usati dai client VPN di Azure tooauthenticate per le connessioni VPN Point-to-Site.</span><span class="sxs-lookup"><span data-stu-id="e2450-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="e2450-205">Informazioni sulla chiave pubblica hello di hello radice certificato tooAzure caricare.</span><span class="sxs-lookup"><span data-stu-id="e2450-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="e2450-206">la chiave pubblica di Hello viene quindi considerata 'trusted'.</span><span class="sxs-lookup"><span data-stu-id="e2450-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="e2450-207">I certificati client devono essere generati dal certificato radice attendibile hello e quindi installati in ogni computer client nell'archivio di certificati utente corrente di certificati/personale hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="e2450-208">certificato di Hello è client hello tooauthenticate utilizzato quando avvia toohello una connessione tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e2450-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="e2450-209">Se usati, i certificati autofirmati devono essere creati con parametri specifici.</span><span class="sxs-lookup"><span data-stu-id="e2450-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="e2450-210">È possibile creare un certificato autofirmato utilizzando le istruzioni di hello per [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), o, se non si dispone di Windows 10, è possibile utilizzare [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="e2450-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="e2450-211">È importante seguire i passaggi delle hello hello istruzioni durante la generazione di certificati radice autofirmati e certificati client.</span><span class="sxs-lookup"><span data-stu-id="e2450-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="e2450-212">In caso contrario, generare i certificati di hello non sono compatibili con le connessioni P2S e si riceverà un errore di connessione.</span><span class="sxs-lookup"><span data-stu-id="e2450-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="e2450-213"><a name="cer"></a>1. Ottenere il file con estensione cer hello per il certificato radice hello</span><span class="sxs-lookup"><span data-stu-id="e2450-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="e2450-214"><a name="generate"></a>2. Generazione di un certificato client</span><span class="sxs-lookup"><span data-stu-id="e2450-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="e2450-215"><a name="upload"></a>6. Carica informazioni sulla chiave pubblica certificato radice di hello</span><span class="sxs-lookup"><span data-stu-id="e2450-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="e2450-216">Verificare che la creazione del gateway VPN sia stata completata.</span><span class="sxs-lookup"><span data-stu-id="e2450-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="e2450-217">Una volta completata, è possibile caricare hello file con estensione cer, che contiene informazioni sulla chiave pubblica di hello, per un tooAzure certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="e2450-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="e2450-218">Una volta caricato il file a.cer, Azure può utilizzarlo tooauthenticate client che hanno installato un certificato client generato da hello certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="e2450-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="e2450-219">È possibile caricare i file di certificato radice attendibile - backup tooa totale di 20, in un secondo momento, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e2450-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="e2450-220">Dichiarare la variabile hello per il nome del certificato, sostituendo il valore di hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e2450-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="e2450-221">Sostituire il percorso di file hello con valori personalizzati e quindi eseguire i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="e2450-222">Caricare hello tooAzure di informazioni sulla chiave pubblica.</span><span class="sxs-lookup"><span data-stu-id="e2450-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="e2450-223">Una volta caricati, informazioni sul certificato hello Azure considera questa toobe un certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="e2450-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="e2450-224"><a name="clientconfig"></a>7. Scaricare il pacchetto di configurazione client VPN di hello</span><span class="sxs-lookup"><span data-stu-id="e2450-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="e2450-225">tooconnect tooa virtuale usando una VPN Point-to-Site, è necessario installare ogni client di un pacchetto di configurazione di client che consente di configurare i client VPN nativo hello con le impostazioni di hello e file di rete virtuale di toohello tooconnect necessarie.</span><span class="sxs-lookup"><span data-stu-id="e2450-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="e2450-226">pacchetto di configurazione client VPN Hello configura i client VPN di Windows nativo hello, non installa un client VPN di nuovo o diverso.</span><span class="sxs-lookup"><span data-stu-id="e2450-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="e2450-227">È possibile utilizzare hello stessa configurazione del client VPN del pacchetto in ogni computer client, come versione di hello corrisponda architettura hello per client hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="e2450-228">Per hello l'elenco dei sistemi operativi client supportati, vedere hello [connessioniPoint-to-Sitedomande frequenti su](#faq) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="e2450-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="e2450-229">Dopo aver creato il gateway di hello, è possibile generare e scaricare il pacchetto di configurazione client hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="e2450-230">In questo esempio Scarica il pacchetto di hello per i client a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="e2450-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="e2450-231">Se si desidera client a 32 bit hello toodownload, sostituire 'Amd64' con 'x86'.</span><span class="sxs-lookup"><span data-stu-id="e2450-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="e2450-232">È anche possibile scaricare client VPN hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="e2450-233">Copiare e incollare il collegamento hello restituito tooa browser toodownload hello pacchetto web, prestando attenzione virgolette hello tooremove circostanti collegamento hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="e2450-234">Scaricare e installare i pacchetti hello in computer client hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="e2450-235">Se viene visualizzato un popup SmartScreen, fare clic su **Altre informazioni** e quindi su **Esegui comunque** per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e2450-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="e2450-236">È inoltre possibile salvare tooinstall pacchetti hello in altri computer client.</span><span class="sxs-lookup"><span data-stu-id="e2450-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="e2450-237">In un computer client hello passare troppo**le impostazioni di rete** e fare clic su **VPN**.</span><span class="sxs-lookup"><span data-stu-id="e2450-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="e2450-238">connessione VPN Hello Mostra il nome di hello della rete virtuale hello che si connette a.</span><span class="sxs-lookup"><span data-stu-id="e2450-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="e2450-239"><a name="clientcertificate"></a>8. Installare un certificato client esportato</span><span class="sxs-lookup"><span data-stu-id="e2450-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="e2450-240">Se si desidera un P2S toocreate connessione da un computer client diverso hello è utilizzato i certificati di toogenerate hello client, è necessario tooinstall un certificato client.</span><span class="sxs-lookup"><span data-stu-id="e2450-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="e2450-241">Quando si installa un certificato client, è necessario password hello creata quando è stato esportato il certificato di client hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="e2450-242">In genere, è sufficiente fare doppio clic sul certificato hello e installarlo.</span><span class="sxs-lookup"><span data-stu-id="e2450-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="e2450-243">Verificare che il certificato di client hello è stato esportato come un file pfx con hello intera catena di certificati (ovvero hello (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="e2450-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="e2450-244">In caso contrario, non è presente nel computer client hello informazioni del certificato radice hello e client hello non saranno in grado di tooauthenticate correttamente.</span><span class="sxs-lookup"><span data-stu-id="e2450-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="e2450-245">Per altre informazioni, vedere [Installare un certificato client esportato](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="e2450-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="e2450-246"><a name="connect"></a>9. Connettersi tooAzure</span><span class="sxs-lookup"><span data-stu-id="e2450-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="e2450-247">tooconnect tooyour rete virtuale, computer client hello passare tooVPN connessioni e individuare la connessione VPN hello creato.</span><span class="sxs-lookup"><span data-stu-id="e2450-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="e2450-248">Il file è denominato hello stesso nome della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e2450-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="e2450-249">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="e2450-249">Click **Connect**.</span></span> <span data-ttu-id="e2450-250">Che fa riferimento il certificato di hello toousing viene visualizzato un messaggio popup.</span><span class="sxs-lookup"><span data-stu-id="e2450-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="e2450-251">Fare clic su **continua** toouse privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="e2450-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="e2450-252">In hello **connessione** pagina di stato, fare clic su **Connetti** connessione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="e2450-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="e2450-253">Se viene visualizzato un **Seleziona certificato** schermata, verificare che hello certificato client visualizzato sia hello uno che si desidera toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e2450-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="e2450-254">In caso contrario, utilizzare hello freccia tooselect hello corretto certificato e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e2450-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![I client VPN si connette tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="e2450-256">Verrà stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="e2450-256">Your connection is established.</span></span>

  ![Connessione stabilita](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="e2450-258">Risoluzione dei problemi delle connessioni P2S</span><span class="sxs-lookup"><span data-stu-id="e2450-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="e2450-259"><a name="verify"></a>10. Verificare la connessione</span><span class="sxs-lookup"><span data-stu-id="e2450-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="e2450-260">tooverify che la connessione VPN sia attiva, aprire un prompt dei comandi con privilegi elevati ed eseguire *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="e2450-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="e2450-261">Visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-261">View hello results.</span></span> <span data-ttu-id="e2450-262">Si noti che l'indirizzo IP hello che è stato ricevuto uno degli indirizzi hello all'interno di hello Point-to-Site VPN Client Pool di indirizzi specificato nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="e2450-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="e2450-263">risultati di Hello sono simili toothis esempio:</span><span class="sxs-lookup"><span data-stu-id="e2450-263">hello results are similar toothis example:</span></span>

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

## <span data-ttu-id="e2450-264"><a name="connectVM"></a>Connettere la macchina virtuale di tooa</span><span class="sxs-lookup"><span data-stu-id="e2450-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="e2450-265"><a name="addremovecert"></a>Aggiungere o rimuovere un certificato radice</span><span class="sxs-lookup"><span data-stu-id="e2450-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="e2450-266">È possibile aggiungere e rimuovere certificati radice attendibili da Azure.</span><span class="sxs-lookup"><span data-stu-id="e2450-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="e2450-267">Quando si rimuove un certificato radice, i client che dispongono di un certificato generato dal certificato radice hello non è possibile eseguire l'autenticazione e non saranno in grado di tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e2450-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="e2450-268">Se si desidera tooauthenticate un client e la connessione, è necessario tooinstall un nuovo certificato client generato da un certificato radice attendibile tooAzure (caricato).</span><span class="sxs-lookup"><span data-stu-id="e2450-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="e2450-269"><a name="addtrustedroot"></a>tooadd un certificato radice attendibile</span><span class="sxs-lookup"><span data-stu-id="e2450-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="e2450-270">È possibile aggiungere backup too20 radice certificato con estensione cer file tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2450-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="e2450-271">esempio Hello i passaggi della Guida si aggiunge un certificato radice:</span><span class="sxs-lookup"><span data-stu-id="e2450-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="e2450-272"><a name="certmethod1"></a>Metodo 1</span><span class="sxs-lookup"><span data-stu-id="e2450-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="e2450-273">Si tratta di tooupload metodo più efficiente di hello un certificato radice.</span><span class="sxs-lookup"><span data-stu-id="e2450-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="e2450-274">Preparare tooupload di file con estensione cer hello:</span><span class="sxs-lookup"><span data-stu-id="e2450-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="e2450-275">Caricare file hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-275">Upload hello file.</span></span> <span data-ttu-id="e2450-276">È possibile caricare un solo file alla volta.</span><span class="sxs-lookup"><span data-stu-id="e2450-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="e2450-277">tooverify che il file di certificato caricato hello:</span><span class="sxs-lookup"><span data-stu-id="e2450-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="e2450-278"><a name="certmethod2"></a>Metodo 2</span><span class="sxs-lookup"><span data-stu-id="e2450-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="e2450-279">Questo metodo è ha ulteriori passaggi rispetto al metodo 1, ma è hello stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="e2450-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="e2450-280">È incluso in caso di necessità di dati del certificato tooview hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="e2450-281">Creare e preparare hello nuovo certificato tooadd tooAzure radice.</span><span class="sxs-lookup"><span data-stu-id="e2450-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="e2450-282">Esportare la chiave pubblica hello come x. 509 con codifica Base 64 (. CER) e aprirlo con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e2450-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="e2450-283">Copiare i valori hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="e2450-283">Copy hello values, as shown in hello following example:</span></span>

  ![certificato](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="e2450-285">Quando si copiano i dati del certificato hello, assicurarsi di copiare testo hello come un'unica riga continua senza ritorni a capo o avanzamenti riga.</span><span class="sxs-lookup"><span data-stu-id="e2450-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="e2450-286">Potrebbe essere necessario toomodify la visualizzazione nel too'Show editor di testo hello simbolo/Mostra avanzamenti di riga e restituisce un ritorno a capo hello toosee di tutti i caratteri.</span><span class="sxs-lookup"><span data-stu-id="e2450-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="e2450-287">Specificare il nome di certificato hello e informazioni sulla chiave come una variabile.</span><span class="sxs-lookup"><span data-stu-id="e2450-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="e2450-288">Sostituire le informazioni di hello personalizzata, come illustrato in hello nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e2450-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="e2450-289">Aggiungi nuovo certificato radice di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-289">Add hello new root certificate.</span></span> <span data-ttu-id="e2450-290">È possibile aggiungere solo un certificato alla volta.</span><span class="sxs-lookup"><span data-stu-id="e2450-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="e2450-291">È possibile verificare che il nuovo certificato hello è stata aggiunta correttamente utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e2450-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="e2450-292"><a name="removerootcert"></a>tooremove un certificato radice</span><span class="sxs-lookup"><span data-stu-id="e2450-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="e2450-293">Dichiarare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="e2450-294">Rimuovere il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="e2450-295">Hello utilizzare seguente tooverify di esempio che hello certificato è stato rimosso correttamente.</span><span class="sxs-lookup"><span data-stu-id="e2450-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="e2450-296"><a name="revoke"></a>Revocare un certificato client</span><span class="sxs-lookup"><span data-stu-id="e2450-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="e2450-297">È possibile revocare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="e2450-297">You can revoke client certificates.</span></span> <span data-ttu-id="e2450-298">certificato Hello elenco di revoche di certificati consente tooselectively negare connettività Point-to-Site in base a singoli certificati client.</span><span class="sxs-lookup"><span data-stu-id="e2450-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="e2450-299">Questa operazione è diversa rispetto alla rimozione di un certificato radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="e2450-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="e2450-300">Se si rimuove un CER del certificato radice attendibile da Azure, comporta la revoca l'accesso per tutti i certificati client generato firmato dall'autorità di certificazione revocata hello hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="e2450-301">Revoca di un certificato client, anziché certificato radice hello consente hello altri certificati che sono stati generati da hello radice certificato toocontinue toobe utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e2450-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="e2450-302">pratica comune Hello è accesso toouse hello radice certificato toomanage livelli team o dell'organizzazione, durante l'utilizzo dei certificati client revocati per il controllo di accesso con granularità fine per utenti singoli.</span><span class="sxs-lookup"><span data-stu-id="e2450-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="e2450-303"><a name="revokeclientcert"></a>toorevoke un certificato client</span><span class="sxs-lookup"><span data-stu-id="e2450-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="e2450-304">Recuperare l'identificazione personale del certificato client di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="e2450-305">Per ulteriori informazioni, vedere [come tooretrieve hello identificazione personale del certificato](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2450-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="e2450-306">Copiare l'editor di testo hello informazioni tooa e rimuovere tutti gli spazi in modo che sia una stringa continua.</span><span class="sxs-lookup"><span data-stu-id="e2450-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="e2450-307">Questa stringa è dichiarata come variabile nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="e2450-308">Dichiarare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-308">Declare hello variables.</span></span> <span data-ttu-id="e2450-309">Verificare l'identificazione personale di hello toodeclare che è stato recuperato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="e2450-310">Aggiungere l'elenco di toohello hello identificazione personale dei certificati revocati.</span><span class="sxs-lookup"><span data-stu-id="e2450-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="e2450-311">Viene visualizzato "Succeeded" quando è stato aggiunto l'identificazione personale hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="e2450-312">Verificare che tale identificazione digitale hello è stato aggiunto l'elenco di revoche di certificati toohello.</span><span class="sxs-lookup"><span data-stu-id="e2450-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="e2450-313">Dopo l'aggiunta di identificazione personale hello, certificato hello non può più essere utilizzato tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e2450-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="e2450-314">I client che tentano di tooconnect usando questo certificato, ricevono un messaggio che informa che il certificato hello non è più valido.</span><span class="sxs-lookup"><span data-stu-id="e2450-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="e2450-315"><a name="reinstateclientcert"></a>tooreinstate un certificato client</span><span class="sxs-lookup"><span data-stu-id="e2450-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="e2450-316">È possibile ripristinare un certificato client rimuovendo l'identificazione personale hello dall'elenco di hello dei certificati client revocati.</span><span class="sxs-lookup"><span data-stu-id="e2450-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="e2450-317">Dichiarare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-317">Declare hello variables.</span></span> <span data-ttu-id="e2450-318">Verificare che si dichiara hello corretta identificazione digitale certificato hello che si desidera tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="e2450-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="e2450-319">Rimuovere l'identificazione personale del certificato hello dall'elenco di revoche di certificati hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="e2450-320">Controllare se identificazione personale hello viene rimosso dall'elenco di revocati hello.</span><span class="sxs-lookup"><span data-stu-id="e2450-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="e2450-321"><a name="faq"></a>Domande frequenti sulla connettività da punto a sito</span><span class="sxs-lookup"><span data-stu-id="e2450-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e2450-322">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2450-322">Next steps</span></span>
<span data-ttu-id="e2450-323">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e2450-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="e2450-324">Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="e2450-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="e2450-325">toounderstand informazioni sulle reti e macchine virtuali, vedere [Cenni preliminari sulla rete di Azure e VM Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2450-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
