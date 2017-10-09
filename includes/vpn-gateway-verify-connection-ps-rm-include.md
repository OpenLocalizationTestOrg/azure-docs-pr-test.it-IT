È possibile verificare che la connessione ha avuto esito positivo tramite i cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, con o senza '-Debug'. 

1. Hello utilizzare cmdlet di esempio seguente, la configurazione di hello toomatch di valori personalizzati. Se richiesto, selezionare 'A' in ordine toorun "All". Nell'esempio hello, '-Name' fa riferimento il nome di toohello della connessione di hello che si desidera tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Al termine di cmdlet hello, visualizzare i valori hello. Nell'esempio hello seguente, lo stato di connessione hello Mostra come "Connessi" e si possono vedere byte in ingresso e in uscita.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```