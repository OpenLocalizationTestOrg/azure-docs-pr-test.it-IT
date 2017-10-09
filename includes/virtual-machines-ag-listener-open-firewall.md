In questo passaggio si crea una porta probe di hello tooopen di regola firewall per endpoint con carico bilanciato hello (59999, come specificato in precedenza) e un'altra regola di porta di listener gruppo di disponibilità di tooopen hello. Poiché è stato creato endpoint con bilanciamento del carico hello in hello macchine virtuali che contengono repliche del gruppo di disponibilità, è necessario tooopen hello probe porta e la porta di listener hello in hello rispettive macchine virtuali.

1. Nelle macchine virtuali che ospitano le repliche, avviare **Windows Firewall con sicurezza avanzata**.

2. Fare clic con il pulsante destro del mouse su **Regole connessioni in entrata** e quindi scegliere **Nuova regola**.

3. In hello **tipo di regola** selezionare **porta**, quindi fare clic su **Avanti**.

4. In hello **protocollo e porte** selezionare **TCP**, tipo **59999** in hello **porte locali specifiche** casella e quindi fare clic su **Avanti**.

5. In hello **azione** pagina, mantenere **Consenti connessione hello** selezionata e quindi fare clic su **Avanti**.

6. In hello **profilo** pagina, accettare le impostazioni predefinite di hello e quindi fare clic su **Avanti**.

7. In hello **nome** hello della pagina **nome** testo, specificare un nome di regola, ad esempio **sempre nella porta del Listener Probe**, quindi fare clic su **fine**.

8. Ripetere i passaggi per la porta del listener gruppo di disponibilità hello (come specificato nel parametro hello $EndpointPort dello script hello) precedenti, hello e quindi specificare un nome di regola appropriata, ad esempio **sempre nella porta del Listener**.

