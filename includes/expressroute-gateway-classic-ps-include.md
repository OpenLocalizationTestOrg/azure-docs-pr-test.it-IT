È necessario creare innanzitutto una rete virtuale e una subnet del gateway prima di utilizzare hello seguenti attività. Vedere l'articolo hello [configurare una rete virtuale utilizzando portale classico hello](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) per ulteriori informazioni.   

## <a name="add-a-gateway"></a>Aggiungere un gateway
Utilizzare il comando hello sotto toocreate un gateway. Essere toosubstitute che uno qualsiasi dei valori personalizzati.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Verificare che sia stato creato il gateway hello
Comando hello Use sotto tooverify che hello gateway è stato creato. Inoltre, questo comando Recupera l'ID gateway hello, che è necessario per le altre operazioni.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Ridimensionare un gateway
Esistono diversi [SKU del gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). È possibile utilizzare hello successivo comando toochange hello SKU di Gateway in qualsiasi momento.

> [!IMPORTANT]
> Questo comando non funziona per il gateway UltraPerformance. toochange il gateway UltraPerformance tooan gateway, rimuovere innanzitutto hello gateway ExpressRoute esistente e quindi creare un nuovo gateway UltraPerformance. toodowngrade rimuovere prima il gateway da un gateway, UltraPerformance hello UltraPerformance gateway e quindi creare un nuovo gateway. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Rimuovere un gateway
Utilizzare il comando hello sotto tooremove un gateway

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>