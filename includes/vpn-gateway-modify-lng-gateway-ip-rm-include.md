### <span data-ttu-id="e207a-101"><a name="gwipnoconnection"></a>gateway di rete locale hello toomodify 'GatewayIpAddress' - Nessuna connessione gateway</span><span class="sxs-lookup"><span data-stu-id="e207a-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="e207a-102">Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare.</span><span class="sxs-lookup"><span data-stu-id="e207a-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="e207a-103">Utilizzare toomodify esempio hello un gateway di rete locale che non dispone di un gateway di connessione.</span><span class="sxs-lookup"><span data-stu-id="e207a-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="e207a-104">Quando si modifica questo valore, è inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="e207a-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="e207a-105">Essere certi toouse hello esistente nome del gateway di rete locale nelle impostazioni di ordine toooverwrite hello corrente.</span><span class="sxs-lookup"><span data-stu-id="e207a-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="e207a-106">Se si utilizza un nome diverso, si crea un nuovo gateway di rete locale, anziché sovrascrivere hello uno esistente.</span><span class="sxs-lookup"><span data-stu-id="e207a-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="e207a-107"><a name="gwipwithconnection"></a>gateway di rete locale hello toomodify 'GatewayIpAddress' - connessione gateway esistente</span><span class="sxs-lookup"><span data-stu-id="e207a-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="e207a-108">Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare.</span><span class="sxs-lookup"><span data-stu-id="e207a-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="e207a-109">Se esiste già una connessione del gateway, è necessario innanzitutto connessione hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="e207a-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="e207a-110">Dopo la rimozione di connessione hello, è possibile modificare l'indirizzo IP del gateway hello e ricreare una nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="e207a-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="e207a-111">È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="e207a-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="e207a-112">Questo comporterà periodi di inattività per la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="e207a-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="e207a-113">Quando si modifica l'indirizzo IP del gateway hello, non è necessario gateway VPN di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="e207a-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="e207a-114">È necessario solo connessione hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="e207a-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="e207a-115">Rimuovere la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-115">Remove hello connection.</span></span> <span data-ttu-id="e207a-116">È possibile trovare nome hello della connessione utilizzando i cmdlet 'Get-AzureRmVirtualNetworkGatewayConnection' hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="e207a-117">Modificare il valore di 'GatewayIpAddress' hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="e207a-118">È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="e207a-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="e207a-119">Essere certi toouse hello esistente nome di rete locale gateway toooverwrite hello impostazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="e207a-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="e207a-120">In caso contrario, si crea un nuovo gateway di rete locale, anziché sovrascrivere hello uno esistente.</span><span class="sxs-lookup"><span data-stu-id="e207a-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="e207a-121">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-121">Create hello connection.</span></span> <span data-ttu-id="e207a-122">In questo esempio viene configurato un tipo di connessione IPsec.</span><span class="sxs-lookup"><span data-stu-id="e207a-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="e207a-123">Quando si ricrea la connessione, utilizzare i tipo di connessione hello specificato per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="e207a-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="e207a-124">Per i tipi di connessione aggiuntive, vedere hello [cmdlet PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="e207a-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="e207a-125">nome del gateway di rete virtuale hello tooobtain, è possibile eseguire i cmdlet 'Get-AzureRmVirtualNetworkGateway' hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="e207a-126">Impostare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="e207a-127">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e207a-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```