### <a name="gwipnoconnection"></a>gateway di rete locale hello toomodify 'GatewayIpAddress' - Nessuna connessione gateway

Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare. Utilizzare toomodify esempio hello un gateway di rete locale che non dispone di un gateway di connessione.

Quando si modifica questo valore, è inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente. Essere certi toouse hello esistente nome del gateway di rete locale nelle impostazioni di ordine toooverwrite hello corrente. Se si utilizza un nome diverso, si crea un nuovo gateway di rete locale, anziché sovrascrivere hello uno esistente.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>gateway di rete locale hello toomodify 'GatewayIpAddress' - connessione gateway esistente

Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare. Se esiste già una connessione del gateway, è necessario innanzitutto connessione hello tooremove. Dopo la rimozione di connessione hello, è possibile modificare l'indirizzo IP del gateway hello e ricreare una nuova connessione. È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente. Questo comporterà periodi di inattività per la connessione VPN. Quando si modifica l'indirizzo IP del gateway hello, non è necessario gateway VPN di hello toodelete. È necessario solo connessione hello tooremove.
 

1. Rimuovere la connessione di hello. È possibile trovare nome hello della connessione utilizzando i cmdlet 'Get-AzureRmVirtualNetworkGatewayConnection' hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. Modificare il valore di 'GatewayIpAddress' hello. È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente. Essere certi toouse hello esistente nome di rete locale gateway toooverwrite hello impostazioni correnti. In caso contrario, si crea un nuovo gateway di rete locale, anziché sovrascrivere hello uno esistente.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Creare la connessione hello. In questo esempio viene configurato un tipo di connessione IPsec. Quando si ricrea la connessione, utilizzare i tipo di connessione hello specificato per la configurazione. Per i tipi di connessione aggiuntive, vedere hello [cmdlet PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) pagina.  nome del gateway di rete virtuale hello tooobtain, è possibile eseguire i cmdlet 'Get-AzureRmVirtualNetworkGateway' hello.
   
    Impostare le variabili di hello.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Creare la connessione hello.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```