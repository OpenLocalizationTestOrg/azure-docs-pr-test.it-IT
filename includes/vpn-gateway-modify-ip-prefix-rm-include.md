### <span data-ttu-id="7d37f-101"><a name="noconnection"></a>toomodify rete locale gateway prefissi degli indirizzi IP - Nessuna connessione gateway</span><span class="sxs-lookup"><span data-stu-id="7d37f-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="7d37f-102">prefissi di indirizzo aggiuntivo tooadd:</span><span class="sxs-lookup"><span data-stu-id="7d37f-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="7d37f-103">prefissi di indirizzo tooremove:</span><span class="sxs-lookup"><span data-stu-id="7d37f-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="7d37f-104">Esclusi i prefissi hello che non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="7d37f-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="7d37f-105">In questo esempio è non è più base prefisso 20.0.0.0/24 (da hello esempio precedente), pertanto è aggiornare il gateway di rete locale hello, escludendo tale prefisso.</span><span class="sxs-lookup"><span data-stu-id="7d37f-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="7d37f-106"><a name="withconnection"></a>toomodify rete locale gateway prefissi di indirizzi IP - connessione gateway esistente</span><span class="sxs-lookup"><span data-stu-id="7d37f-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="7d37f-107">Se si dispone di una connessione gateway e tooadd o rimuovere i prefissi di indirizzi IP hello contenuti nel gateway di rete locale, è necessario hello toodo alla procedura seguente, in ordine.</span><span class="sxs-lookup"><span data-stu-id="7d37f-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="7d37f-108">Questo comporterà periodi di inattività per la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="7d37f-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="7d37f-109">Quando si modificano i prefissi di indirizzi IP, non è necessario gateway VPN di hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="7d37f-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="7d37f-110">È necessario solo connessione hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="7d37f-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="7d37f-111">Rimuovere la connessione di hello.</span><span class="sxs-lookup"><span data-stu-id="7d37f-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="7d37f-112">Modificare i prefissi di indirizzo hello per il gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="7d37f-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="7d37f-113">Impostare la variabile hello per hello gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="7d37f-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="7d37f-114">Modificare i prefissi hello.</span><span class="sxs-lookup"><span data-stu-id="7d37f-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="7d37f-115">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="7d37f-115">Create hello connection.</span></span> <span data-ttu-id="7d37f-116">In questo esempio viene configurato un tipo di connessione IPsec.</span><span class="sxs-lookup"><span data-stu-id="7d37f-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="7d37f-117">Quando si ricrea la connessione, utilizzare i tipo di connessione hello specificato per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="7d37f-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="7d37f-118">Per i tipi di connessione aggiuntive, vedere hello [cmdlet PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="7d37f-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="7d37f-119">Impostare la variabile hello per hello gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="7d37f-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="7d37f-120">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="7d37f-120">Create hello connection.</span></span> <span data-ttu-id="7d37f-121">Nell'esempio viene utilizzata la variabile hello $local impostate nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="7d37f-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```