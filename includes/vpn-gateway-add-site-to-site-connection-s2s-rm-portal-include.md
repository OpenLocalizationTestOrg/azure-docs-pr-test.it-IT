1. Passare a pannello hello aprire tooand per il gateway di rete virtuale. Esistono più modi toonavigate. In questo esempio, si ci si sposta gateway toohello 'VNet1GW' passando troppo**TestVNet1 -> Panoramica -> connesso dispositivi -> VNet1GW**.
2. Nel Pannello di hello per VNet1GW, fare clic su **connessioni**. Nella parte superiore di hello del Pannello di hello connessioni, fare clic su **+ Aggiungi** tooopen hello **Aggiungi connessione** blade.

    ![Configurare una connessione da sito a sito](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. In hello **Aggiungi connessione** pannello, compilare hello valori toocreate la connessione.

  - **Nome:** assegnare un nome alla connessione. In questo esempio verrà usato il nome **VNet1toSite2**.
  - **Tipo di connessione**: selezionare **Da sito a sito (IPSec)**.
  - **Gateway di rete virtuale:** hello rappresenta un valore fisso perché ci si connette da questo gateway.
  - **Gateway di rete locale:** fare clic su **Scegli un gateway di rete locale** e selezionare hello gateway di rete locale che si desidera toouse. In questo esempio verrà usato il gateway **Site2**.
  - **Chiave condivisa:** valore hello qui deve corrispondere il valore hello che si sta utilizzando per il dispositivo VPN locale. Nell'esempio hello utilizzassimo "abc123", ma è possibile (e consigliabile) utilizzare un nome più complesse. Hello importante cosa è il valore di hello specificato qui deve essere hello che stesso valore specificato quando si configura il dispositivo VPN.
  - Hello rimanenti valori per **sottoscrizione**, **gruppo di risorse**, e **percorso** sono fisse.

4. Fare clic su **OK** toocreate la connessione. Si noterà *creazione connessione* flash nella schermata di hello.
5. È possibile visualizzare connessione hello in hello **connessioni** pannello hello virtuali del gateway di rete. Hello stato passa da *sconosciuto* troppo*connessione*e quindi troppo*Succeeded*.
