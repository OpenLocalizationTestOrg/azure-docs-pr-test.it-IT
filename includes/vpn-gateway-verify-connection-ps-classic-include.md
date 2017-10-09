<span data-ttu-id="f6440-101">È possibile verificare che la connessione ha avuto esito positivo tramite i cmdlet 'Get-AzureVNetConnection' hello.</span><span class="sxs-lookup"><span data-stu-id="f6440-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="f6440-102">Hello utilizzare cmdlet di esempio seguente, la configurazione di hello toomatch di valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="f6440-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="f6440-103">nome di Hello della rete virtuale hello deve essere racchiuso tra virgolette se contiene spazi.</span><span class="sxs-lookup"><span data-stu-id="f6440-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="f6440-104">Al termine di cmdlet hello, visualizzare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="f6440-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="f6440-105">Nell'esempio hello seguente, lo stato di connettività hello viene visualizzato come "Connessi" ed è possibile visualizzare i byte in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="f6440-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal