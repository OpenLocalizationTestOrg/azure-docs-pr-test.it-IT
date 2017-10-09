### <a name="noconnection"></a>toomodify rete locale gateway prefissi degli indirizzi IP - Nessuna connessione gateway

prefissi di indirizzo aggiuntivo tooadd:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

prefissi di indirizzo tooremove:<br>
Esclusi i prefissi hello che non è più necessario. In questo esempio è non è più base prefisso 20.0.0.0/24 (da hello esempio precedente), pertanto è aggiornare il gateway di rete locale hello, escludendo tale prefisso.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify rete locale gateway prefissi di indirizzi IP - connessione gateway esistente

Se si dispone di una connessione gateway e tooadd o rimuovere i prefissi di indirizzi IP hello contenuti nel gateway di rete locale, è necessario hello toodo alla procedura seguente, in ordine. Questo comporterà periodi di inattività per la connessione VPN. Quando si modificano i prefissi di indirizzi IP, non è necessario gateway VPN di hello toodelete. È necessario solo connessione hello tooremove.


1. Rimuovere la connessione di hello.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Modificare i prefissi di indirizzo hello per il gateway di rete locale.
   
  Impostare la variabile hello per hello gateway di rete locale.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Modificare i prefissi hello.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Creare la connessione hello. In questo esempio viene configurato un tipo di connessione IPsec. Quando si ricrea la connessione, utilizzare i tipo di connessione hello specificato per la configurazione. Per i tipi di connessione aggiuntive, vedere hello [cmdlet PowerShell](https://msdn.microsoft.com/library/mt603611.aspx) pagina.
   
  Impostare la variabile hello per hello gateway di rete virtuale.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Creare la connessione hello. Nell'esempio viene utilizzata la variabile hello $local impostate nel passaggio 2.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```