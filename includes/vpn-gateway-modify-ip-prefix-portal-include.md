### <a name="noconnection"></a>toomodify rete locale gateway prefissi degli indirizzi IP - Nessuna connessione gateway

#### <a name="tooadd-additional-address-prefixes"></a>prefissi di indirizzo aggiuntivo tooadd:

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.
2. Aggiungere spazio di indirizzi IP hello in hello *Aggiungi intervallo di indirizzi* casella.
3. Fare clic su **salvare** toosave le impostazioni.

#### <a name="tooremove-address-prefixes"></a>prefissi di indirizzo tooremove:

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.
2. Fare clic su hello **'...'** sulla riga hello contenente hello prefisso desiderato tooremove.
3. Fare clic su **Rimuovi**.
4. Fare clic su **salvare** toosave le impostazioni.

### <a name="withconnection"></a>toomodify rete locale gateway prefissi di indirizzi IP - connessione gateway esistente

Se si dispone di una connessione gateway e tooadd o rimuovere i prefissi di indirizzi IP hello contenuti nel gateway di rete locale, è necessario hello toodo alla procedura seguente, in ordine. Questo comporterà periodi di inattività per la connessione VPN. Quando si modificano i prefissi di indirizzi IP, non è necessario gateway VPN di hello toodelete. È necessario solo connessione hello tooremove.

#### <a name="1-remove-hello-connection"></a>1. Rimuovere la connessione di hello.

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **connessioni**.
2. Fare clic su hello **...**  hello per ogni connessione, quindi fare clic sulla riga **eliminare**.
3. Fare clic su **salvare** toosave le impostazioni.

#### <a name="2-modify-hello-address-prefixes"></a>2. Modificare i prefissi di indirizzo hello.

prefissi di indirizzo aggiuntivo tooadd:

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.
2. Aggiungere spazio di indirizzi IP hello.
3. Fare clic su **salvare** toosave le impostazioni.

prefissi di indirizzo tooremove:

1. Nella risorsa di Gateway di rete locale, in hello hello **impostazioni** fare clic su **configurazione**.
2. Fare clic su hello **...**  sulla riga hello contenente hello prefisso desiderato tooremove.
3. Fare clic su **Rimuovi**.
4. Fare clic su **salvare** toosave le impostazioni.

#### <a name="3-recreate-hello-connection"></a>3. Ricreare la connessione hello.

1. Passare toohello Gateway della rete virtuale per la rete virtuale. (Non hello Gateway di rete locale.)
2. Nel Gateway di rete virtuale Ciao hello **impostazioni** fare clic su **connessioni**.
3. Fare clic su hello **+ Aggiungi** tooopen hello **Aggiungi connessione** blade.
4. Ricreare la connessione.
5. Fare clic su **OK** connessione hello toocreate.
