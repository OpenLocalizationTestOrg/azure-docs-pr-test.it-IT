


## <a name="attach-an-empty-disk"></a>Collegare un disco vuoto
Collegare un disco vuoto è tooadd un modo semplice un tipo di dati su disco, poiché Azure crea file con estensione vhd hello automaticamente e lo archivia nell'account di archiviazione hello.

1. Fare clic su **macchine virtuali (classico)**, e quindi selezionare hello VM appropriato.

2. Nel menu Impostazioni hello, fare clic su **dischi**.

   ![Collegare un nuovo disco vuoto](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Nella barra dei comandi di hello, fare clic su **nuovo collegamento**.  
    Hello **Collega nuovo disco** viene visualizzata la finestra di dialogo.

    ![Collegare un nuovo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Compilare hello le seguenti informazioni:
    - In **nome File**, accettare il nome di predefinito hello o digitare un altro per i file con estensione vhd hello. disco dati Hello utilizza un nome generato automaticamente, anche se si digita un nome diverso per i file con estensione vhd hello.
    - Seleziona hello **tipo** del disco dati hello. Tutte le macchine virtuali supportano dischi Standard. Molte macchine virtuali supportano anche dischi Premium.
    - Seleziona hello **dimensioni (GB)** del disco dati hello.
    - Per **Memorizzazione nella cache dell'host** scegliere Nessuna o Sola lettura.
    - Fare clic su OK toofinish.

4. Dopo il disco dati hello viene creato e collegato, è elencata nella sezione di dischi hello di hello VM.

   ![Disco dati nuovo e vuoto collegato correttamente](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Dopo aver aggiunto un disco dati, è necessario toolog in toohello VM e inizializzare il disco hello in modo che può essere utilizzato.

## <a name="how-to-attach-an-existing-disk"></a>Procedura: Collegare un disco esistente
Per collegare un disco esistente, è necessario che in un account di archiviazione sia disponibile un file con estensione vhd. Hello utilizzare [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) account di archiviazione di cmdlet tooupload hello VHD file toohello. Dopo aver creato e caricato i file con estensione vhd hello, è possibile collegare tooa macchina virtuale.

1. Fare clic su **macchine virtuali (classico)**, e quindi selezionare hello macchina virtuale appropriata.

2. Nel menu Impostazioni hello, fare clic su **dischi**.

3. Nella barra dei comandi di hello, fare clic su **collegamento esistente**.

    ![Collegare il disco dati](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Fare clic su **Percorso**. visualizzare gli account di archiviazione disponibile Hello. Selezionare quindi un account di archiviazione appropriato tra quelli elencati.

    ![Selezionare un account di archiviazione per il disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. Un **account di archiviazione** ha uno o più contenitori con unità disco (dischi rigidi virtuali). Selezionare il contenitore appropriato di hello da quelli elencati.

    ![Finestra di selezione del contenitore delle macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Hello **dischi rigidi virtuali** pannello elenca le unità disco hello contenute nel contenitore hello. Fare clic su uno dei dischi hello e quindi fare clic su Seleziona.

    ![Finestra di selezione dell'immagine del disco per le macchine virtuali](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Hello **collegare un disco esistente** pannello visualizzato nuovamente, con percorso hello contenente l'account di archiviazione hello, contenitore e macchina virtuale toohello tooadd di disco rigido selezionato (vhd).

  Impostare **ospitare la memorizzazione nella cache** toonone o lettura, quindi fare clic su OK.

    ![Disco dati correttamente collegato](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
