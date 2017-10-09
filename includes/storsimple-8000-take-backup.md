<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake una copia di backup

1. Passare il servizio di gestione di dispositivi StorSimple tooyour. Nell'elenco tabulare di hello delle periferiche, selezionare e fare clic su un dispositivo e quindi fare clic su **tutte le impostazioni**. In hello **impostazioni** pannello andare troppo**Impostazioni > Gestisci > Criteri di Backup**.

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu1.png)

2. In hello **criteri di Backup** pannello, fare clic su **+ Aggiungi criteri**.

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu2.png)

3. In hello **creare criteri di backup** pannello, specificare un nome di lunghezza compresa tra 3 e 150 caratteri per i criteri di backup.

4. Selezionare toobe volumi hello sottoposti a backup. Se si seleziona più di un volume, tali volumi vengono raggruppati toocreate contemporaneamente un backup coerente con l'arresto anomalo del sistema.

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu4.png)

5. Nel pannello **Aggiungere la prima pianificazione**:

    1. Selezionare il tipo di hello di backup. Per ripristini più rapidi selezionare **Snapshot locale**. Per la resilienza dei dati, selezionare **Snapshot cloud**.
    2. Specificare la frequenza di backup hello in minuti, ore, giorni o settimane.
    3. Selezionare un periodo di conservazione. le scelte di conservazione Hello dipendono dalla frequenza di backup hello. Ad esempio, per criteri giornalieri, conservazione hello è possibile specificare in settimane, mentre per i criteri mensili in mesi.
    4. Selezionare l'ora e la data per i criteri di backup hello hello.
    5. Fare clic su **OK** toocreate dei criteri di backup hello.

        ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. Fare clic su **crea** toostart la creazione dei criteri di backup hello. Ricevere notifiche quando i criteri di backup hello viene creato correttamente. viene aggiornato anche l'elenco di Hello di criteri di backup.
      
      ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      A questo punto è disponibile un criterio di backup che creerà backup pianificati dei dati del volume.




