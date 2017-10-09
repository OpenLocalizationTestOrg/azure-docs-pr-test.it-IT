1. Nel portale di hello da **tutte le risorse**, fare clic su **+ Aggiungi**. 
2. In hello **tutto** nella casella di ricerca pannello **gateway di rete locale**, quindi fare clic su toosearch. Viene restituito un elenco. Fare clic su **gateway di rete locale** tooopen hello pannello, quindi fare clic su **crea** tooopen hello **gateway di rete locale crea** blade.

  ![Creare il gateway di rete locale](./media/vpn-gateway-add-lng-s2s-rm-portal-include/createlng.png)

3. In hello **pannello gateway di rete locale crea**, specificare i valori hello per il gateway di rete locale.

  - **Nome:** specificare un nome per l'oggetto gateway di rete locale.
  - **Indirizzo IP:** si tratta di indirizzo IP pubblico hello del dispositivo VPN hello da Azure tooconnect per. Specificare un indirizzo IP pubblico valido: indirizzo IP di Hello non può essere dietro un NAT e ha toobe raggiungibile da Azure. Se l'indirizzo IP hello non è al momento, è possibile utilizzare valori hello illustrati nella cattura di schermata hello, ma si sarà necessario toogo nuovamente e sostituire l'indirizzo IP segnaposto con indirizzo IP pubblico hello del dispositivo VPN. In caso contrario, Azure non sarà in grado di tooconnect.
  - **Lo spazio degli indirizzi** fa riferimento a intervalli di indirizzi toohello per rete hello che rappresenta la rete locale. È possibile aggiungere più intervalli di spazi indirizzi. Assicurarsi che è possibile specificare gli intervalli di hello non si sovrappongono con intervalli di altre reti che si desidera tooconnect per. Azure indirizza l'intervallo di indirizzi hello specificare l'indirizzo IP del dispositivo VPN locale toohello. *Utilizzare i valori in questo caso, non hello sui valori indicati nella schermata di hello*.
  - **Sottoscrizione:** verificare tale hello sottoscrizione risulta corretto.
  - **Gruppo di risorse:** gruppo di risorse selezionare hello che si desidera toouse. È possibile creare un nuovo gruppo di risorse o selezionarne uno già creato.
  - **Percorso:** selezionare il percorso di hello creati in questo oggetto. È opportuno tooselect hello la rete virtuale si trova nella stessa posizione, ma non è necessario toodo così.

4. Dopo aver specificato i valori hello, fare clic su **crea** nella parte inferiore di hello hello pannello toocreate hello locale del gateway di rete.
