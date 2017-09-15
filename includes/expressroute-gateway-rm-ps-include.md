<span data-ttu-id="2dd85-101">Nei passaggi di questa attività viene usata una rete virtuale basata sui valori indicati nell'elenco di riferimento per la configurazione riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2dd85-101">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="2dd85-102">In questo elenco sono indicati anche i nomi e le impostazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="2dd85-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="2dd85-103">Questo elenco non verrà utilizzato direttamente nella procedura, ma si aggiungeranno variabili basate sui valori nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2dd85-103">We don't use this list directly in any of the steps, although we do add variables based on the values in this list.</span></span> <span data-ttu-id="2dd85-104">È possibile copiare l'elenco per usarlo come riferimento, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2dd85-104">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="2dd85-105">**Elenco di riferimento per la configurazione**</span><span class="sxs-lookup"><span data-stu-id="2dd85-105">**Configuration reference list**</span></span>

* <span data-ttu-id="2dd85-106">Nome rete virtuale = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="2dd85-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="2dd85-107">Spazio degli indirizzi della rete virtuale = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2dd85-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="2dd85-108">Gruppo di risorse = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="2dd85-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="2dd85-109">Nome subnet1 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="2dd85-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="2dd85-110">Spazio indirizzi subnet1 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="2dd85-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="2dd85-111">Nome subnet del gateway: "GatewaySubnet" Il nome della subnet del gateway deve sempre essere *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="2dd85-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="2dd85-112">Spazio degli indirizzi della subnet gateway = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="2dd85-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="2dd85-113">Area = "East US"</span><span class="sxs-lookup"><span data-stu-id="2dd85-113">Region = "East US"</span></span>
* <span data-ttu-id="2dd85-114">Nome del gateway = "GW"</span><span class="sxs-lookup"><span data-stu-id="2dd85-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="2dd85-115">Nome IP del gateway = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="2dd85-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="2dd85-116">Nome della configurazione IP del gateway = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="2dd85-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="2dd85-117">Tipo = "ExpressRoute" Questo tipo è necessario per una configurazione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2dd85-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="2dd85-118">Nome IP pubblico del gateway = "gwpip"</span><span class="sxs-lookup"><span data-stu-id="2dd85-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="2dd85-119">Aggiungere un gateway</span><span class="sxs-lookup"><span data-stu-id="2dd85-119">Add a gateway</span></span>
1. <span data-ttu-id="2dd85-120">Connettersi alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd85-120">Connect to your Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="2dd85-121">Dichiarare le variabili per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="2dd85-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="2dd85-122">Assicurarsi di modificare l'esempio in base alle impostazioni da usare.</span><span class="sxs-lookup"><span data-stu-id="2dd85-122">Be sure to edit the sample to reflect the settings that you want to use.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="2dd85-123">Archiviare l'oggetto rete virtuale come variabile.</span><span class="sxs-lookup"><span data-stu-id="2dd85-123">Store the virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="2dd85-124">Aggiungere una subnet gateway alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2dd85-124">Add a gateway subnet to your Virtual Network.</span></span> <span data-ttu-id="2dd85-125">La subnet gateway deve esistere già e deve essere denominata "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="2dd85-125">The gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="2dd85-126">È consigliabile creare una subnet gateway che sia /27 o più grande (/26, /25 e così via).</span><span class="sxs-lookup"><span data-stu-id="2dd85-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="2dd85-127">Impostare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="2dd85-127">Set the configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="2dd85-128">Archiviare la subnet gateway come variabile.</span><span class="sxs-lookup"><span data-stu-id="2dd85-128">Store the gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="2dd85-129">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2dd85-129">Request a public IP address.</span></span> <span data-ttu-id="2dd85-130">L'indirizzo IP viene richiesto prima della creazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-130">The IP address is requested before creating the gateway.</span></span> <span data-ttu-id="2dd85-131">Non è possibile specificare l'indirizzo IP che si desidera utilizzare. Viene allocato in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="2dd85-131">You cannot specify the IP address that you want to use; it’s dynamically allocated.</span></span> <span data-ttu-id="2dd85-132">Questo indirizzo IP sarà utilizzato nella prossima sezione di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2dd85-132">You'll use this IP address in the next configuration section.</span></span> <span data-ttu-id="2dd85-133">AllocationMethod deve essere Dynamic.</span><span class="sxs-lookup"><span data-stu-id="2dd85-133">The AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="2dd85-134">Creare la configurazione per il gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-134">Create the configuration for your gateway.</span></span> <span data-ttu-id="2dd85-135">La configurazione del gateway definisce la subnet e l'indirizzo IP pubblico da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="2dd85-135">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="2dd85-136">In questo passaggio si specifica la configurazione che si userà per creare il gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-136">In this step, you are specifying the configuration that will be used when you create the gateway.</span></span> <span data-ttu-id="2dd85-137">Questo passaggio non crea effettivamente l'oggetto gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-137">This step does not actually create the gateway object.</span></span> <span data-ttu-id="2dd85-138">Per creare la configurazione del gateway, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="2dd85-138">Use the sample below to create your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="2dd85-139">Creare il gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-139">Create the gateway.</span></span> <span data-ttu-id="2dd85-140">In questo passaggio **-GatewayType** è particolarmente importante.</span><span class="sxs-lookup"><span data-stu-id="2dd85-140">In this step, the **-GatewayType** is especially important.</span></span> <span data-ttu-id="2dd85-141">È necessario usare il valore **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="2dd85-141">You must use the value **ExpressRoute**.</span></span> <span data-ttu-id="2dd85-142">Dopo aver eseguito questi cmdlet, la creazione del gateway può richiedere anche oltre 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="2dd85-142">After running these cmdlets, the gateway can take 45 minutes or more to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="2dd85-143">Verificare che il gateway sia stato creato</span><span class="sxs-lookup"><span data-stu-id="2dd85-143">Verify the gateway was created</span></span>
<span data-ttu-id="2dd85-144">Per verificare che il gateway sia stato creato, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dd85-144">Use the following commands to verify that the gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="2dd85-145">Ridimensionare un gateway</span><span class="sxs-lookup"><span data-stu-id="2dd85-145">Resize a gateway</span></span>
<span data-ttu-id="2dd85-146">Esistono diversi [SKU del gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="2dd85-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="2dd85-147">È possibile usare il comando seguente per modificare la SKU del gateway in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="2dd85-147">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dd85-148">Questo comando non funziona per il gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="2dd85-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="2dd85-149">Per modificare il gateway in un gateway UltraPerformance, innanzitutto rimuovere il gateway ExpressRoute esistente, quindi creare un nuovo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="2dd85-149">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="2dd85-150">Per effettuare il downgrade del gateway da un gateway UltraPerformance, innanzitutto rimuovere il gateway UltraPerformance, quindi creare un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="2dd85-150">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="2dd85-151">Rimuovere un gateway</span><span class="sxs-lookup"><span data-stu-id="2dd85-151">Remove a gateway</span></span>
<span data-ttu-id="2dd85-152">Per rimuovere un gateway, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2dd85-152">Use the following command to remove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```