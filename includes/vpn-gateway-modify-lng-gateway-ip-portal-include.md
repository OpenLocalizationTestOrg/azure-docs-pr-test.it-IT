### <a name="gwipnoconnection"></a>indirizzo IP gateway di rete locale di hello di toomodify - alcuna connessione gateway

Utilizzare toomodify esempio hello un gateway di rete locale che non dispone di un gateway di connessione. Quando si modifica questo valore, è inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente.

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.
2. In hello **indirizzo IP** modificare l'indirizzo IP hello.
3. Fare clic su **salvare** impostazioni hello toosave.

### <a name="gwipwithconnection"></a>toomodify hello locale gateway gateway indirizzo IP di rete - connessione gateway esistente

toomodify un gateway di rete locale che dispone di una connessione, è necessario toofirst rimuove la connessione di hello. Dopo la rimozione di connessione hello, è possibile modificare l'indirizzo IP del gateway hello e ricreare una nuova connessione. È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente. Questo comporterà periodi di inattività per la connessione VPN. Quando si modifica l'indirizzo IP del gateway hello, non è necessario gateway VPN di hello toodelete. È necessario solo connessione hello tooremove.
 
#### <a name="1-remove-hello-connection"></a>1. Rimuovere la connessione di hello.

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **connessioni**.
2. Fare clic su hello **...**  hello per connessione hello, quindi fare clic sulla riga **eliminare**.
3. Fare clic su **salvare** toosave le impostazioni.

#### <a name="2-modify-hello-ip-address"></a>2. Modificare l'indirizzo IP hello.

È inoltre possibile modificare i prefissi di indirizzo hello in hello contemporaneamente.

1. In hello **indirizzo IP** modificare l'indirizzo IP hello.
2. Fare clic su **salvare** impostazioni hello toosave.

#### <a name="3-recreate-hello-connection"></a>3. Ricreare la connessione hello.

1. Passare toohello Gateway della rete virtuale per la rete virtuale. (Non hello Gateway di rete locale.)
2. Nel Gateway di rete virtuale Ciao hello **impostazioni** fare clic su **connessioni**.
3. Fare clic su hello **+ Aggiungi** tooopen hello **Aggiungi connessione** blade.
4. Ricreare la connessione.
5. Fare clic su **OK** connessione hello toocreate.
