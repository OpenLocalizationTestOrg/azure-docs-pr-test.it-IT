<span data-ttu-id="a4c57-101">È possibile verificare che la connessione ha avuto esito positivo tramite i cmdlet "Get-AzureRmVirtualNetworkGatewayConnection" hello, con o senza '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="a4c57-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="a4c57-102">Hello utilizzare cmdlet di esempio seguente, la configurazione di hello toomatch di valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="a4c57-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="a4c57-103">Se richiesto, selezionare 'A' in ordine toorun "All".</span><span class="sxs-lookup"><span data-stu-id="a4c57-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="a4c57-104">Nell'esempio hello, '-Name' fa riferimento il nome di toohello della connessione di hello che si desidera tootest.</span><span class="sxs-lookup"><span data-stu-id="a4c57-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="a4c57-105">Al termine di cmdlet hello, visualizzare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="a4c57-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="a4c57-106">Nell'esempio hello seguente, lo stato di connessione hello Mostra come "Connessi" e si possono vedere byte in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="a4c57-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```