<span data-ttu-id="bdbd3-101">i passaggi di Hello per questa attività, utilizzare una rete virtuale in base ai valori hello hello seguente elenco di riferimento configurazione.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="bdbd3-102">In questo elenco sono indicati anche i nomi e le impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="bdbd3-103">È non utilizzare questo elenco direttamente in uno dei passaggi di hello, anche se è aggiungere le variabili in base ai valori hello in questo elenco.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="bdbd3-104">È possibile copiare hello elenco toouse come riferimento, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="bdbd3-105">**Elenco di riferimento per la configurazione**</span><span class="sxs-lookup"><span data-stu-id="bdbd3-105">**Configuration reference list**</span></span>

* <span data-ttu-id="bdbd3-106">Nome rete virtuale = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="bdbd3-107">Spazio degli indirizzi della rete virtuale = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="bdbd3-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="bdbd3-108">Gruppo di risorse = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="bdbd3-109">Nome subnet1 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="bdbd3-110">Spazio indirizzi subnet1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="bdbd3-111">Nome subnet del gateway: "GatewaySubnet" Il nome della subnet del gateway deve sempre essere *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="bdbd3-112">Spazio degli indirizzi della subnet gateway = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="bdbd3-113">Area = "East US"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-113">Region = "East US"</span></span>
* <span data-ttu-id="bdbd3-114">Nome del gateway = "GW"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="bdbd3-115">Nome IP del gateway = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="bdbd3-116">Nome della configurazione IP del gateway = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="bdbd3-117">Tipo = "ExpressRoute" Questo tipo è necessario per una configurazione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="bdbd3-118">Nome IP pubblico del gateway = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="bdbd3-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="bdbd3-119">Aggiungere un gateway</span><span class="sxs-lookup"><span data-stu-id="bdbd3-119">Add a gateway</span></span>
1. <span data-ttu-id="bdbd3-120">Connettersi tooyour sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="bdbd3-121">Dichiarare le variabili per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="bdbd3-122">Essere tooedit che hello tooreflect hello le impostazioni di esempio che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="bdbd3-123">Oggetto di rete virtuale archivio hello come una variabile.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="bdbd3-124">Aggiungere un tooyour subnet gateway rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="bdbd3-125">subnet del gateway Hello devono essere denominati "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="bdbd3-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="bdbd3-126">È consigliabile creare una subnet gateway che sia /27 o più grande (/26, /25 e così via).</span><span class="sxs-lookup"><span data-stu-id="bdbd3-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="bdbd3-127">Impostare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="bdbd3-128">Archiviare subnet del gateway hello come una variabile.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="bdbd3-129">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-129">Request a public IP address.</span></span> <span data-ttu-id="bdbd3-130">indirizzo IP Hello è richiesto prima di creare il gateway hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="bdbd3-131">Non è possibile specificare l'indirizzo IP hello che si desidera toouse; viene allocata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="bdbd3-132">Utilizzare questo indirizzo IP nella successiva sezione di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="bdbd3-133">Hello AllocationMethod deve essere dinamica.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="bdbd3-134">Creare hello configurazione per il gateway.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="bdbd3-135">configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="bdbd3-136">In questo passaggio, si specifica configurazione hello che verrà utilizzato quando si crea gateway hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="bdbd3-137">Questo passaggio non crea effettivamente l'oggetto gateway hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="bdbd3-138">Utilizzare l'esempio di hello sotto toocreate la configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="bdbd3-139">Creare il gateway di hello.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-139">Create hello gateway.</span></span> <span data-ttu-id="bdbd3-140">In questo passaggio, hello **- il tipo di gateway** è particolarmente importante.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="bdbd3-141">È necessario utilizzare il valore di hello **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="bdbd3-142">Dopo aver eseguito questi cmdlet, gateway hello può richiedere 45 minuti o più toocreate.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="bdbd3-143">Verificare che sia stato creato il gateway hello</span><span class="sxs-lookup"><span data-stu-id="bdbd3-143">Verify hello gateway was created</span></span>
<span data-ttu-id="bdbd3-144">Utilizzare hello seguenti comandi tooverify che hello gateway è stato creato:</span><span class="sxs-lookup"><span data-stu-id="bdbd3-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="bdbd3-145">Ridimensionare un gateway</span><span class="sxs-lookup"><span data-stu-id="bdbd3-145">Resize a gateway</span></span>
<span data-ttu-id="bdbd3-146">Esistono diversi [SKU del gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="bdbd3-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="bdbd3-147">È possibile utilizzare hello successivo comando toochange hello SKU di Gateway in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdbd3-148">Questo comando non funziona per il gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="bdbd3-149">toochange il gateway UltraPerformance tooan gateway, rimuovere innanzitutto hello gateway ExpressRoute esistente e quindi creare un nuovo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="bdbd3-150">toodowngrade rimuovere prima il gateway da un gateway, UltraPerformance hello UltraPerformance gateway e quindi creare un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="bdbd3-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="bdbd3-151">Rimuovere un gateway</span><span class="sxs-lookup"><span data-stu-id="bdbd3-151">Remove a gateway</span></span>
<span data-ttu-id="bdbd3-152">Utilizzare hello comando tooremove un gateway di seguito:</span><span class="sxs-lookup"><span data-stu-id="bdbd3-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```