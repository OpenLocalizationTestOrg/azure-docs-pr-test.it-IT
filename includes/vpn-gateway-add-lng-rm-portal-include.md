1. Nel portale di hello da **tutte le risorse**, fare clic su **+ Aggiungi**. In hello **tutto** nella casella di ricerca pannello **gateway di rete locale**, quindi fare clic su tooreturn un elenco di risorse. Fare clic su **gateway di rete locale** tooopen hello pannello, quindi fare clic su **crea** tooopen hello **gateway di rete locale crea** blade.
   
    ![Creare il gateway di rete locale](./media/vpn-gateway-add-lng-rm-portal-include/lng.png)

2. In hello **pannello gateway di rete locale crea**, specificare un **nome** per l'oggetto di gateway di rete locale. Se possibile, usare un nome intuitivo come **ClassicVNetLocal** o **TestVNet1Local**. Questo rende più semplice per è tooidentify hello gateway di rete locale nel portale di hello.
3. Specificare un pubblico valido **indirizzo IP** del dispositivo VPN hello o toowhich gateway di rete virtuale si desidera tooconnect.<br>**Se la rete locale rappresenta un percorso locale:** specificare l'indirizzo IP pubblico hello del dispositivo VPN hello che si desidera tooconnect per. Non può essere protetto da NAT è toobe raggiungibile da Azure.<br>**Se la rete locale rappresenta un'altra rete virtuale:** specificare l'indirizzo IP pubblico hello assegnati toohello gateway di rete virtuale per tale rete virtuale.<br>**Se non hai ancora l'indirizzo IP hello:** è possibile costituiscono un indirizzo IP segnaposto valido, quindi tornare e modificare questa impostazione prima della connessione.
4. **Lo spazio degli indirizzi** fa riferimento a intervalli di indirizzi toohello per rete hello che rappresenta la rete locale. È possibile aggiungere più intervalli di spazi indirizzi. Assicurarsi che è possibile specificare gli intervalli di hello non si sovrappongono con intervalli di toowhich altre reti che ci si connette.
5. Per **sottoscrizione**, verificare che hello sottoscrizione risulta corretto.
6. Per **gruppo di risorse**, selezionare il gruppo di risorse hello che si desidera toouse. È possibile creare un nuovo gruppo di risorse o selezionarne uno già creato.
7. Per **percorso**, selezionare il percorso di hello in cui verrà creata questa risorsa. È opportuno tooselect hello la rete virtuale si trova nella stessa posizione, ma non è necessario toodo così.
8. Fare clic su **crea** gateway di rete locale toocreate hello.

