i passaggi di Hello per questa attività, utilizzare una rete virtuale in base ai valori hello hello seguente elenco di riferimento configurazione. In questo elenco sono indicati anche i nomi e le impostazioni aggiuntive. È non utilizzare questo elenco direttamente in uno dei passaggi di hello, anche se è aggiungere le variabili in base ai valori hello in questo elenco. È possibile copiare hello elenco toouse come riferimento, sostituendo i valori hello con valori personalizzati.

**Elenco di riferimento per la configurazione**

* Nome rete virtuale = "TestVNet"
* Spazio degli indirizzi della rete virtuale = 192.168.0.0/16
* Gruppo di risorse = "TestRG"
* Nome subnet1 = "FrontEnd" 
* Spazio indirizzi subnet1 = "192.168.1.0/24"
* Nome subnet del gateway: "GatewaySubnet" Il nome della subnet del gateway deve sempre essere *GatewaySubnet*.
* Spazio degli indirizzi della subnet gateway = "192.168.200.0/26"
* Area = "East US"
* Nome del gateway = "GW"
* Nome IP del gateway = "GWIP"
* Nome della configurazione IP del gateway = "gwipconf"
* Tipo = "ExpressRoute" Questo tipo è necessario per una configurazione ExpressRoute.
* Nome IP pubblico del gateway = "gwpip"

## <a name="add-a-gateway"></a>Aggiungere un gateway
1. Connettersi tooyour sottoscrizione Azure.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Dichiarare le variabili per questo esercizio. Essere tooedit che hello tooreflect hello le impostazioni di esempio che si desidera toouse.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Oggetto di rete virtuale archivio hello come una variabile.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Aggiungere un tooyour subnet gateway rete virtuale. subnet del gateway Hello devono essere denominati "GatewaySubnet". È consigliabile creare una subnet gateway che sia /27 o più grande (/26, /25 e così via).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Impostare la configurazione hello.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Archiviare subnet del gateway hello come una variabile.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Richiedere un indirizzo IP pubblico. indirizzo IP Hello è richiesto prima di creare il gateway hello. Non è possibile specificare l'indirizzo IP hello che si desidera toouse; viene allocata in modo dinamico. Utilizzare questo indirizzo IP nella successiva sezione di configurazione hello. Hello AllocationMethod deve essere dinamica.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Creare hello configurazione per il gateway. configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello. In questo passaggio, si specifica configurazione hello che verrà utilizzato quando si crea gateway hello. Questo passaggio non crea effettivamente l'oggetto gateway hello. Utilizzare l'esempio di hello sotto toocreate la configurazione del gateway.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Creare il gateway di hello. In questo passaggio, hello **- il tipo di gateway** è particolarmente importante. È necessario utilizzare il valore di hello **ExpressRoute**. Dopo aver eseguito questi cmdlet, gateway hello può richiedere 45 minuti o più toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Verificare che sia stato creato il gateway hello
Utilizzare hello seguenti comandi tooverify che hello gateway è stato creato:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Ridimensionare un gateway
Esistono diversi [SKU del gateway](../articles/expressroute/expressroute-about-virtual-network-gateways.md). È possibile utilizzare hello successivo comando toochange hello SKU di Gateway in qualsiasi momento.

> [!IMPORTANT]
> Questo comando non funziona per il gateway UltraPerformance. toochange il gateway UltraPerformance tooan gateway, rimuovere innanzitutto hello gateway ExpressRoute esistente e quindi creare un nuovo gateway UltraPerformance. toodowngrade rimuovere prima il gateway da un gateway, UltraPerformance hello UltraPerformance gateway e quindi creare un nuovo gateway.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Rimuovere un gateway
Utilizzare hello comando tooremove un gateway di seguito:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```