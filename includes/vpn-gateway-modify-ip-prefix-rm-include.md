### <span data-ttu-id="9ffbf-101"><a name="noconnection"></a>Per modificare i prefissi degli indirizzi IP del gateway di rete locale senza connessione gateway</span><span class="sxs-lookup"><span data-stu-id="9ffbf-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="9ffbf-102">Per aggiungere altri prefissi degli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="9ffbf-102">To add additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="9ffbf-103">Per rimuovere prefissi degli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="9ffbf-103">To remove address prefixes:</span></span><br>
<span data-ttu-id="9ffbf-104">Escludere i prefissi non più necessari.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-104">Leave out the prefixes that you no longer need.</span></span> <span data-ttu-id="9ffbf-105">In questo esempio non è più necessario il prefisso 20.0.0.0/24 usato nell'esempio precedente. Il gateway di rete locale verrà quindi aggiornato escludendo tale prefisso.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-105">In this example, we no longer need prefix 20.0.0.0/24 (from the previous example), so we update the local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="9ffbf-106"><a name="withconnection"></a>Per modificare i prefissi degli indirizzi IP del gateway di rete locale con connessione gateway esistente</span><span class="sxs-lookup"><span data-stu-id="9ffbf-106"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="9ffbf-107">Se è disponibile una connessione gateway e si vogliono aggiungere o rimuovere i prefissi di indirizzo IP inclusi nel gateway di rete locale, è necessario seguire questa procedura nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-107">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="9ffbf-108">Questo comporterà periodi di inattività per la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="9ffbf-109">Quando si modificano i prefissi degli indirizzi IP, non è necessario eliminare il gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-109">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="9ffbf-110">Occorre rimuovere solo la connessione.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-110">You only need to remove the connection.</span></span>


1. <span data-ttu-id="9ffbf-111">Rimuovere la connessione.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-111">Remove the connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="9ffbf-112">Modificare i prefissi di indirizzo IP per il gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-112">Modify the address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="9ffbf-113">Impostare la variabile per LocalNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-113">Set the variable for the LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="9ffbf-114">Modificare i prefissi.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-114">Modify the prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="9ffbf-115">Creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-115">Create the connection.</span></span> <span data-ttu-id="9ffbf-116">In questo esempio viene configurato un tipo di connessione IPsec.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="9ffbf-117">Quando si ricrea la connessione, usare il tipo di connessione specificato per la configurazione in uso.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-117">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="9ffbf-118">Per altri tipi di connessione, vedere la pagina dei [cmdlet di PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9ffbf-118">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="9ffbf-119">Impostare la variabile per VirtualNetworkGateway.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-119">Set the variable for the VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="9ffbf-120">Creare la connessione.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-120">Create the connection.</span></span> <span data-ttu-id="9ffbf-121">Questo esempio usa la variabile $local impostata nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="9ffbf-121">This example uses the variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```