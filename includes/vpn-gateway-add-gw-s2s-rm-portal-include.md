1. Scegliere hello il lato sinistro di pagina del portale hello,  **+**  e digitare 'Gateway della rete virtuale' nella ricerca. In **Risultati** individuare e selezionare **Gateway di rete virtuale**.
2. Nella parte inferiore di hello del pannello "Gateway di rete virtuale" hello, fare clic su **crea**. Verrà visualizzata hello **gateway di rete virtuale crea** blade.

    ![Campi del pannello Crea gateway di rete virtuale](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "Nuovo gateway")

3. In hello **gateway di rete virtuale crea** pannello, specificare i valori hello per il gateway di rete virtuale.

  - **Nome**: assegnare un nome al gateway. Questo non è hello uguale a una subnet del gateway di denominazione. Nome di hello dell'oggetto gateway hello che si sta creando del.
  - **Tipo di gateway**: selezionare **VPN**. Tipo di gateway di rete virtuale hello di usare i gateway VPN **VPN**. 
  - **Tipo di VPN**: Seleziona tipo VPN hello specificato per la configurazione. La maggior parte delle configurazioni richiede un tipo di VPN basato su route.
  - **SKU**: lo SKU del gateway hello selezionare dall'elenco a discesa hello. SKU Hello elencati nell'elenco a discesa hello dipendono dal hello tipo VPN selezionato. Per informazioni sugli SKU del gateway, vedere [SKU del gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).
  - **Percorso**: tooscroll toosee percorso potrebbe essere necessario. Regolare hello **percorso** campo toopoint toohello percorso in cui si trova la rete virtuale. Se il percorso di hello non punta toohello area in cui risiede la rete virtuale, rete virtuale hello non verrà visualizzati nel passaggio successivo hello 'Scegliere una rete virtuale' elenco a discesa.
  - **Rete virtuale**: scegliere toowhich di rete virtuale hello desiderato tooadd questo gateway. Fare clic su **rete virtuale** pannello ', scegliere una rete virtuale' hello di tooopen. Selezionare hello rete virtuale. Se non viene visualizzata la rete virtuale, assicurarsi che il campo di percorso hello stia puntando toohello area in cui si trova la rete virtuale.
  - **Indirizzo IP pubblico**: pannello 'Crea indirizzo IP pubblico' hello crea un oggetto di indirizzo IP pubblico. indirizzo IP pubblico Hello viene assegnata dinamicamente quando viene creato gateway VPN hello. Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*. Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour. Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato. Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.

    - In primo luogo, fare clic su **indirizzo IP pubblico** tooopen hello pannello 'Scegliere l'indirizzo IP pubblico', quindi fare clic su **+ creare nuovi** pannello 'Crea indirizzo IP pubblico' hello di tooopen.
    - Successivamente, di input un **nome** per l'indirizzo IP pubblico, quindi fare clic su **OK** in hello fondo toosave questo pannello le modifiche.

      ![Crea indirizzo IP pubblico](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "Crea indirizzo IP pubblico")

4. Verificare le impostazioni di hello. È possibile selezionare **toodashboard Pin** nella parte inferiore di hello del pannello hello se si desidera che il gateway tooappear nel dashboard di hello. 
5. Fare clic su **crea** toobegin creazione gateway VPN hello. Hello impostazioni verranno convalidate, si noterà hello "Gateway di rete virtuale di distribuzione" riquadro nel dashboard di hello. Creazione di un gateway può richiedere too45 minuti. Potrebbe essere necessario toorefresh lo stato di completamento hello toosee pagina del portale.

Dopo aver creato il gateway di hello, visualizzare l'indirizzo IP hello assegnato tooit esaminando rete virtuale di hello nel portale di hello. gateway Hello verrà visualizzato come un dispositivo connesso. È possibile fare clic hello connesso dispositivo (il gateway di rete virtuale) tooview ulteriori informazioni.
