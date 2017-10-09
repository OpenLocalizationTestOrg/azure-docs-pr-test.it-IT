<span data-ttu-id="a64ae-101">È necessario creare innanzitutto una rete virtuale e una subnet del gateway prima di utilizzare hello seguenti attività.</span><span class="sxs-lookup"><span data-stu-id="a64ae-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="a64ae-102">Vedere l'articolo hello [configurare una rete virtuale utilizzando portale classico hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a64ae-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="a64ae-103">Aggiungere un gateway</span><span class="sxs-lookup"><span data-stu-id="a64ae-103">Add a gateway</span></span>
<span data-ttu-id="a64ae-104">Utilizzare il comando hello sotto toocreate un gateway.</span><span class="sxs-lookup"><span data-stu-id="a64ae-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="a64ae-105">Essere toosubstitute che uno qualsiasi dei valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a64ae-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="a64ae-106">Verificare che sia stato creato il gateway hello</span><span class="sxs-lookup"><span data-stu-id="a64ae-106">Verify hello gateway was created</span></span>
<span data-ttu-id="a64ae-107">Comando hello Use sotto tooverify che hello gateway è stato creato.</span><span class="sxs-lookup"><span data-stu-id="a64ae-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="a64ae-108">Inoltre, questo comando Recupera l'ID gateway hello, che è necessario per le altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="a64ae-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="a64ae-109">Ridimensionare un gateway</span><span class="sxs-lookup"><span data-stu-id="a64ae-109">Resize a gateway</span></span>
<span data-ttu-id="a64ae-110">Esistono diversi [SKU del gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="a64ae-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="a64ae-111">È possibile utilizzare hello successivo comando toochange hello SKU di Gateway in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a64ae-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a64ae-112">Questo comando non funziona per il gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="a64ae-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="a64ae-113">toochange il gateway UltraPerformance tooan gateway, rimuovere innanzitutto hello gateway ExpressRoute esistente e quindi creare un nuovo gateway UltraPerformance.</span><span class="sxs-lookup"><span data-stu-id="a64ae-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="a64ae-114">toodowngrade rimuovere prima il gateway da un gateway, UltraPerformance hello UltraPerformance gateway e quindi creare un nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="a64ae-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="a64ae-115">Rimuovere un gateway</span><span class="sxs-lookup"><span data-stu-id="a64ae-115">Remove a gateway</span></span>
<span data-ttu-id="a64ae-116">Utilizzare il comando hello sotto tooremove un gateway</span><span class="sxs-lookup"><span data-stu-id="a64ae-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>