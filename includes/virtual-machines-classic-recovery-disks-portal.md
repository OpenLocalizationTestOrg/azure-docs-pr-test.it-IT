Se la macchina virtuale (VM) in Azure rileva un errore di avvio o un disco, potrebbe essere tooperform risoluzione dei problemi in disco rigido virtuale hello stesso. Un esempio comune sarebbe un aggiornamento di applicazione non riuscita che impedisce l'avvio correttamente hello macchina virtuale. Questo articolo viene descritto come toouse tooconnect portale Azure toofix VM tooanother il disco rigido virtuale gli eventuali errori e quindi ricreare la macchina virtuale originale.

## <a name="recovery-process-overview"></a>Panoramica del processo di ripristino
processo di risoluzione dei problemi di Hello è indicato di seguito:

1. Eliminare hello macchina virtuale che si è verificati problemi, ma Mantieni i dischi rigidi virtuali hello.
2. Collegare e montare hello tooanother di disco rigido virtuale a macchina virtuale per la risoluzione dei problemi.
3. Connettersi toohello risoluzione dei problemi di macchina virtuale. Modificare i file o eseguire gli strumenti toofix errori nel disco rigido virtuale originale di hello.
4. Smontare e scollegare hello disco rigido virtuale da hello risoluzione dei problemi di macchina virtuale.
5. Creare una macchina virtuale con disco rigido virtuale originale di hello.

## <a name="delete-hello-original-vm"></a>Eliminare hello macchina virtuale originale
In Azure, i dischi rigidi virtuali e le macchine virtuali sono due risorse distinte. Un disco rigido virtuale è in cui sono archiviate hello del sistema operativo, applicazioni e le configurazioni. Hello VM è esclusivamente i metadati che definisce dimensioni hello o il percorso e che fa riferimento a risorse, ad esempio un disco rigido virtuale o di una scheda di interfaccia di rete virtuale (NIC). Ogni disco rigido virtuale Ottiene un lease assegnato quando tale disco è collegato tooa macchina virtuale. Anche se è possano collegare e scollegare anche durante l'esecuzione di hello VM dischi dati, non è possibile scollegare disco del sistema operativo hello, a meno che non viene eliminato hello risorsa macchina virtuale. lease Hello continua tooassociate hello del sistema operativo disco tooa macchina virtuale, anche quando tale macchina virtuale è in uno stato arrestato e deallocato.

primo passaggio toorecovering Hello la macchina virtuale è una risorsa di macchina virtuale hello toodelete stesso. L'eliminazione hello VM lascia i dischi rigidi virtuali hello nell'account di archiviazione. Dopo aver hello che macchina virtuale viene eliminata, è possibile collegare hello disco rigido virtuale tooanother VM tootroubleshoot e risolvere gli errori di hello. 

1. Accedi toohello [portale di Azure](https://portal.azure.com). 
2. Scegliere dal menu hello sul lato sinistro hello **macchine virtuali (classico)**.
3. Fare clic su macchina virtuale che presenta il problema di hello, seleziona hello **dischi**e quindi identificare il nome di hello del disco rigido virtuale hello. 
4. Selezionare il disco rigido virtuale di hello del sistema operativo e controllare hello **percorso** account di archiviazione hello tooidentify contenente tale disco rigido virtuale. Nell'esempio seguente di hello, hello immediatamente prima stringa ". n e t" hello nome di account di archiviazione.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![immagine di Hello sulla posizione della macchina virtuale](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Hello macchina virtuale e quindi scegliere **eliminare**. Assicurarsi che i dischi di hello non selezionati quando si elimina hello macchina virtuale.
6. Creare una nuova VM di ripristino. Questa macchina virtuale deve essere in hello stessa regione e risorse gruppo (servizio Cloud) come problema hello macchina virtuale.
7. Selezionare il ripristino di hello macchina virtuale, quindi **dischi** > **collegare esistente**.
8. tooselect il disco rigido virtuale esistente, fare clic su **File VHD**:

    ![Cercare il disco rigido virtuale esistente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Selezionare l'account di archiviazione hello > contenitore di disco rigido virtuale > hello disco rigido virtuale, fare clic su hello **selezionare** pulsante tooconfirm prescelto.

    ![Selezionare il disco rigido virtuale esistente](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Con il disco rigido virtuale ora selezionato, selezionare **OK** tooattach hello disco rigido virtuale esistente.
11. Dopo alcuni secondi, hello **dischi** riquadro per la macchina virtuale verrà visualizzato il disco rigido virtuale esistente collegato come disco dati:

    ![Disco rigido virtuale esistente collegato come disco dati](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Risolvere i problemi del disco rigido virtuale originale di hello
Quando si monta hello disco rigido virtuale esistente, è ora possibile eseguire operazioni di manutenzione e risoluzione dei problemi in base alle esigenze. Dopo avere risolto i problemi di hello, continuare con hello alla procedura seguente.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Smontare e scollegare il disco rigido virtuale originale di hello
Dopo aver risolti eventuali errori, smontare e scollegare hello disco rigido virtuale esistente dalla VM sulla risoluzione dei problemi. È possibile utilizzare il disco rigido virtuale insieme a qualsiasi altra macchina virtuale finché non viene rilasciato il lease hello che collega hello disco rigido virtuale toohello risoluzione dei problemi di macchina virtuale.  

1. Accedi toohello [portale di Azure](https://portal.azure.com). 
2. Scegliere dal menu hello sul lato sinistro hello **macchine virtuali (classico)**.
3. Individuare il ripristino di hello macchina virtuale. Selezionare i dischi, disco hello pulsante destro del mouse, quindi **scollegamento**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Creare una macchina virtuale dal disco rigido originale hello

utilizzare una macchina virtuale dal disco rigido virtuale originale, toocreate [portale di Azure classico](https://manage.windowsazure.com).

1. Accedere al [portale di Azure classico](https://manage.windowsazure.com).
2. Nella parte inferiore di hello del portale hello, selezionare **New** > **calcolo** > **macchina virtuale** > **dalla raccolta** .
3. In hello **scegliere un'immagine** selezionare **dischi personali**, e quindi selezionare hello disco rigido virtuale originale. Controllare le informazioni sul percorso hello. Questo è l'area di hello in cui deve essere distribuito hello macchina virtuale. Selezionare il pulsante Avanti hello.
4. In hello **configurazione della macchina virtuale** sezione, digitare il nome di macchina virtuale hello e selezionare una dimensione per hello macchina virtuale.
