<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect tramite la console seriale hello
1. Connettere il dispositivo di toohello cavo seriale (direttamente o tramite un adapter seriale USB).
2. Aprire hello **Pannello di controllo**e quindi aprire hello **Gestione dispositivi**.
3. Identificare la porta COM hello come illustrato nella seguente figura hello.
   
     ![Connessione tramite console seriale](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Avviare PuTTY. 
5. Nel riquadro di destra hello, modificare hello **tipo di connessione** troppo**seriale**.
6. Nel riquadro di destra hello, digitare la porta COM appropriata hello. Assicurarsi che i parametri di configurazione seriale hello siano impostati come indicato di seguito:
   
   * Velocità: 115.200
   * Bit di dati: 8
   * Bit di stop: 1
   * Parità: nessuno
   * Controllo di flusso: nessuno
     
     Queste impostazioni vengono visualizzate nella seguente figura hello.
     
     ![Impostazioni puTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Se il controllo di flusso predefinito hello impostazione non funziona, provare a impostare controllo di flusso hello tooXON/XOFF.
     > 
     > 
7. Fare clic su **aprire** toostart una sessione seriale.

