È possibile verificare che la connessione ha avuto esito positivo tramite i cmdlet 'Get-AzureVNetConnection' hello.

1. Hello utilizzare cmdlet di esempio seguente, la configurazione di hello toomatch di valori personalizzati. nome di Hello della rete virtuale hello deve essere racchiuso tra virgolette se contiene spazi.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Al termine di cmdlet hello, visualizzare i valori hello. Nell'esempio hello seguente, lo stato di connettività hello viene visualizzato come "Connessi" ed è possibile visualizzare i byte in ingresso e in uscita.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal