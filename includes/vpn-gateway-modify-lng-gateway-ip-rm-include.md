### <span data-ttu-id="524a0-101"><a name="gwipnoconnection"></a> Per modificare il gateway di rete locale 'GatewayIpAddress' senza connessione gateway</span><span class="sxs-lookup"><span data-stu-id="524a0-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="524a0-102">Se l'indirizzo IP pubblico del dispositivo VPN a cui ci si vuole connettere è stato modificato, è necessario modificare il gateway di rete locale per riflettere tale modifica.</span><span class="sxs-lookup"><span data-stu-id="524a0-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="524a0-103">Usare l'esempio per modificare un gateway di rete locale privo di connessione gateway.</span><span class="sxs-lookup"><span data-stu-id="524a0-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="524a0-104">Quando si modifica questo valore, è anche possibile modificare contemporaneamente i prefissi degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="524a0-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="524a0-105">Assicurarsi di usare il nome del gateway di rete locale esistente per sovrascrivere le impostazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="524a0-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="524a0-106">Se si usa un nome diverso, creare un nuovo gateway di rete locale, invece di sovrascrivere il valore esistente.</span><span class="sxs-lookup"><span data-stu-id="524a0-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="524a0-107"><a name="gwipwithconnection"></a> Per modificare il gateway di rete locale 'GatewayIpAddress' con una connessione gateway esistente</span><span class="sxs-lookup"><span data-stu-id="524a0-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="524a0-108">Se l'indirizzo IP pubblico del dispositivo VPN a cui ci si vuole connettere è stato modificato, è necessario modificare il gateway di rete locale per riflettere tale modifica.</span><span class="sxs-lookup"><span data-stu-id="524a0-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="524a0-109">Se esiste già una connessione gateway è prima necessario rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="524a0-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="524a0-110">Dopo aver rimosso la connessione sarà possibile modificare l'indirizzo IP del gateway e ricreare una nuova connessione.</span><span class="sxs-lookup"><span data-stu-id="524a0-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="524a0-111">È anche possibile modificare contemporaneamente i prefissi di indirizzo.</span><span class="sxs-lookup"><span data-stu-id="524a0-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="524a0-112">Questo comporterà periodi di inattività per la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="524a0-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="524a0-113">Quando si modifica l'indirizzo IP del gateway, non è necessario eliminare il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="524a0-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="524a0-114">Occorre rimuovere solo la connessione.</span><span class="sxs-lookup"><span data-stu-id="524a0-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="524a0-115">Rimuovere la connessione.</span><span class="sxs-lookup"><span data-stu-id="524a0-115">Remove the connection.</span></span> <span data-ttu-id="524a0-116">Il nome della connessione può essere trovato usando il cmdlet 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="524a0-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="524a0-117">Modificare il valore 'GatewayIpAddress'.</span><span class="sxs-lookup"><span data-stu-id="524a0-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="524a0-118">È anche possibile modificare contemporaneamente i prefissi di indirizzo.</span><span class="sxs-lookup"><span data-stu-id="524a0-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="524a0-119">Assicurarsi di usare il nome del gateway di rete locale esistente per sovrascrivere le impostazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="524a0-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="524a0-120">In caso contrario si creerà un nuovo gateway di rete locale, invece di sovrascrivere quello esistente.</span><span class="sxs-lookup"><span data-stu-id="524a0-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="524a0-121">Creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="524a0-121">Create the connection.</span></span> <span data-ttu-id="524a0-122">In questo esempio viene configurato un tipo di connessione IPsec.</span><span class="sxs-lookup"><span data-stu-id="524a0-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="524a0-123">Quando si ricrea la connessione, usare il tipo di connessione specificato per la configurazione in uso.</span><span class="sxs-lookup"><span data-stu-id="524a0-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="524a0-124">Per altri tipi di connessione, vedere la pagina dei [cmdlet di PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .</span><span class="sxs-lookup"><span data-stu-id="524a0-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="524a0-125">Per ottenere il nome VirtualNetworkGateway è possibile eseguire il cmdlet 'Get-AzureRmVirtualNetworkGateway'.</span><span class="sxs-lookup"><span data-stu-id="524a0-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="524a0-126">Impostare le variabili.</span><span class="sxs-lookup"><span data-stu-id="524a0-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="524a0-127">Creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="524a0-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```