## <a name="defining-a-backup-policy"></a>Definizione di un criterio di backup
Un criterio di backup definisce una matrice di caso hello dati di snapshot e il periodo di conservazione questi snapshot. Quando si definisce un criterio per il backup di una VM è possibile attivare un processo di backup *una volta al giorno*. Quando si crea un nuovo criterio, è applicato toohello insieme di credenziali. interfaccia di criteri di backup Hello è simile al seguente:

![Criterio di backup](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate un criterio:

1. Immettere un nome per hello **nome criterio**.
2. Gli snapshot dei dati possono essere acquisiti a intervalli giornalieri o settimanali. Hello utilizzare **frequenza di Backup** toochoose dal menu a discesa se dati di snapshot giornaliera o settimanale.
   
   * Se si sceglie un intervallo giornaliero, utilizzare hello evidenziato controllo tooselect hello ora hello per snapshot hello. ora di hello toochange, deselezionare ora hello e selezionare nuova ora di hello.
     
     ![Criterio di backup giornaliero](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Se si sceglie un intervallo settimana, utilizzare hello controlli evidenziato tooselect hello giorni della settimana hello e hello ora dello snapshot di hello tootake giorno. Nel menu di giorno di hello, selezionare uno o più giorni. Nel menu di ora hello, selezionare un'ora. ora hello toochange, deselezionare ora selezionato hello e selezionare nuova ora di hello.
     
     ![Criterio di backup settimanale](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Per impostazione predefinita, tutte le opzioni di **Intervallo conservazione** sono selezionate. Deselezionare qualsiasi limite dell'intervallo di conservazione non si desidera toouse. Specificare quindi hello interval(s) toouse.
   
    Mensili e annuali periodi di mantenimento dati consentono di snapshot di hello toospecify in base a un incremento settimana o giornaliero.
   
   > [!NOTE]
   > Quando si protegge una VM, una volta al giorno viene eseguito un processo di backup. ora di Hello quando cui viene eseguito backup hello è hello uguale per ogni periodo di mantenimento.
   > 
   > 
4. Dopo aver impostato tutte le opzioni per i criteri di hello, nella parte superiore di hello del pannello hello fare clic su **salvare**.
   
    nuovo criterio di Hello viene applicata immediatamente toohello insieme di credenziali.

