
1. In hello **connessioni ibride** pannello, fare clic su connessione ibrida hello appena creato, quindi fare clic su **Listener installazione**.
   
    ![Click Listener Setup](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. Hello **le proprietà di connessione ibrida** apre blade. In **locale di Hybrid Connection Manager**, scegliere **scaricare e configurare manualmente**, salvare il pacchetto di HybridConnectionManager.msi hello scaricato e copiare una stringa di connessione del gateway hello.
   
    ![Fare clic qui tooinstall](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. Da un prompt dei comandi di amministratore, digitare quanto segue di hello comandi installer hello toostart:
   
        start HybridConnectionManager.msi
4. Dopo hello esegue l'installazione, fare clic su **non ora**, quindi cartella %ProgramFiles%\Microsoft\HybridConnectionManager toohello, eseguire HCMConfigWizard.exe e fare clic su **Sì** in hello **utente Controllo dell'account** finestra di dialogo.
5. Incollare una stringa di connessione ibrida hello copiato in precedenza e fare clic su **OK**. 
   
    ![Installazione](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. Al termine dell'installazione di hello, fare clic su **Chiudi**.
   
    ![Fare clic su Chiudi](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    In hello **connessioni ibride** blade, hello **stato** colonna Mostra ora **connesso**. 
   
    ![Stato connesso](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

