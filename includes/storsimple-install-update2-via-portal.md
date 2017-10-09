<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>un aggiornamento dal portale di Azure hello tooinstall

1. Nella pagina del servizio StorSimple hello, selezionare il dispositivo. Passare troppo**dispositivi** > **manutenzione**.
2. Nella parte inferiore di hello della pagina hello, fare clic su **analisi aggiornamenti**. Tooscan la disponibilità di aggiornamenti viene creato un processo. Ricevere notifiche quando hello viene completato correttamente.
3. In hello **gli aggiornamenti Software** sezione hello stessa pagina, sono disponibili nuovi aggiornamenti software di hello. Che è consigliabile consultare le note sulla versione di hello prima di applicare un aggiornamento sul dispositivo.
4. Nella parte inferiore di hello della pagina hello, fare clic su **Installa aggiornamenti**e quindi **OK**.
5. In hello **installare gli aggiornamenti** la finestra di dialogo, assicurarsi di aver seguito indicazioni hello, quindi selezionare **mprendo hello sopra requisito e sono pronti tooupgrade dispositivo** e fare clic su verifica hello pulsante.
   
    ![Messaggio di conferma](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Viene avviato un set di controlli dei prerequisiti. I controlli includono quanto segue:
   
   * **Controlli di integrità controller** tooverify che hello entrambi i controller del dispositivo sono integri e online.
   * **Controlli di integrità componente hardware** tooverify che hello tutti i componenti hardware del dispositivo StorSimple siano integri.
   * **DATA 0 controlla** tooverify che DATA 0 è abilitata nel dispositivo. Se questa interfaccia non è abilitata, è necessario abilitarla e riprovare.
   * **DATA 2 e DATA 3 controlli** tooverify che le interfacce di rete DATA 2 e DATA 3 non sono abilitate. Se queste interfacce sono abilitate, è necessario disattivare queste e quindi provare tooupdate il dispositivo. Questo controllo viene eseguito solo se si sta aggiornando un dispositivo che esegue GA. Dispositivi che eseguono versioni 0,3, 0,2 o 0,1 questo controllo non è necessario.
   * **Controllo gateway** su qualsiasi dispositivo che esegue un tooUpdate precedente versione 1. Questa verifica viene eseguita su tutti i dispositivi di hello in esecuzione il software di pre-aggiornamento 1, ma non sui dispositivi hello con un gateway configurato per un'interfaccia di rete diverse da DATA 0.
     
     Se tutti i controlli vengono completati correttamente, viene applicato l'aggiornamento di Hello. Essere informati quando sono in corso controlli hello.
     
     ![Notifica sul controllo preliminare](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Hello Ecco un esempio in cui i controlli di hello non riusciti. È necessario verificare che entrambi i controller dei dispositivi hello sono integri e online. È inoltre necessario integrità hello toocheck dei componenti hardware hello. In questo esempio, il controller 0 e il controller 1 richiedono l'attenzione dell'utente. Se è possibile risolvere questi problemi personalmente, potrebbe essere necessario toocontact supporto Microsoft.
     
       ![Controlli non riusciti](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Dopo che i controlli di hello vengono completati correttamente, viene creato un processo di aggiornamento. Ricevere notifiche quando il processo di aggiornamento hello viene creato correttamente.
   
    ![Creazione del processo di aggiornamento](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    aggiornamento di Hello viene quindi applicato nel dispositivo.
    
8. stato di avanzamento hello toomonitor hello del processo di aggiornamento, fare clic su **Visualizza processo**. In hello **processi** pagina, è possibile visualizzare hello aggiornare lo stato di avanzamento.
9. Hello aggiornamento diverrà effettivo dopo alcune ore toocomplete. Selezionare il processo di aggiornamento hello e fare clic su **dettagli** dettagli hello tooview del processo di hello in qualsiasi momento.
10. Dopo aver completato il processo di hello, passare toohello **manutenzione** pagina e scorrere verso il basso troppo**gli aggiornamenti Software**.

