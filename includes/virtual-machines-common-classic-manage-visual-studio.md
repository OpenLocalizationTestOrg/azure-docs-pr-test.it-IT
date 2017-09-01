È possibile creare macchine virtuali in Azure usando Esplora server in Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Creare una macchina virtuale di Azure in Esplora server
Anche se è possibile creare una macchina virtuale nel [portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103)è possibile creare una macchina virtuale anche in Azure usando i comandi in Esplora server. È possibile usare le macchine virtuali, ad esempio, per fornire un front-end dietro un comune endpoint pubblico con carico bilanciato.

### <a name="to-create-a-new-virtual-machine"></a>Per creare una nuova macchina virtuale
1. In Esplora Server, aprire il nodo **Azure** e fare clic su **Macchine virtuali**.
2. Nel menu di scelta rapida fare clic su **Crea macchina virtuale**.
   
    Viene visualizzata la procedura guidata **Creare una nuova macchina virtuale** .
   
    ![Comando Crea macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Nella pagina **Scegliere una sottoscrizione** selezionare una sottoscrizione da usare durante la creazione della macchina virtuale e quindi fare clic su **Avanti**.
   
    Se non si è connessi ad Azure, fare clic su **Accedi** per effettuare l'accesso. Quindi, se non è già selezionata, selezionare la propria sottoscrizione di Azure nell'elenco a discesa.
4. Nella pagina **Selezionare un'immagine di macchina virtuale** selezionare un tipo di immagine nell'elenco a discesa **Tipo immagine** e quindi selezionare le immagini di una macchina virtuale nell'elenco a discesa **Nome immagine**. Al termine, fare clic su **Avanti**.
   
    ![Selezionare una pagina di immagini di macchine virtuali](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    È possibile scegliere tra i seguenti tipi di immagine.
   
   * **Immagini pubbliche** sono elencate le immagini di macchine virtuali dei sistemi operativi e del software di server come Windows Server ed SQL Server.
   * **Immagini MSDN** sono elencate le immagini di macchine virtuali del software disponibile agli abbonati MSDN, ad esempio Visual Studio e Microsoft Dynamics.
   * **Immagini private** sono elencate le immagini di macchine virtuali specializzate e generalizzate create dall'utente.
     
     Per altre informazioni sulle macchine virtuali specializzate e generalizzate, vedere il post di blog sull' [immagine della macchina virtuale](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Per informazioni su come trasformare una macchina virtuale in un modello da usare per creare rapidamente nuove macchine virtuali preconfigurate, vedere [Come acquisire una macchina virtuale Windows da usare come modello](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) .
     
     È possibile fare clic sul nome di un'immagine di macchina virtuale per visualizzare informazioni sull'immagine nel lato destro della pagina.
     
     > [!NOTE]
     > Non è possibile aggiungere immagini di macchine virtuali agli elenchi **Immagini pubbliche** o **Immagini MSDN** perché sono di sola lettura. Tutte le macchine virtuali create vengono aggiunte all'elenco **Immagini private** .
     > 
     > 
     
     Gli abbonati MSDN con una sottoscrizione di livello Visual Studio possono creare una macchina virtuale di Azure predefinita contenente Visual Studio, oltre a diverse altre immagini. Per altre informazioni, vedere come [creare una macchina virtuale in Visual Studio tramite le immagini della raccolta di Visual Studio 2013 per sottoscrittori MSDN](http://visualstudio2013msdngalleryimage.azurewebsites.net) e le [sottoscrizioni MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs).|
5. Nella pagina **Impostazioni di base della macchina virtuale** immettere il nome di una macchina, quindi aggiungere le specifiche della macchina virtuale, inclusi dimensione, nome utente e password. Al termine, fare clic su **Avanti**.
   
    Il nuovo nome e la password verranno usati per accedere alla macchina con il desktop remoto, quindi è consigliabile prenderne nota. Dopo aver creato una macchina virtuale di Azure in Visual Studio, è possibile modificarne le dimensioni e le altre impostazioni nel [portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Se si scelgono dimensioni maggiori per la macchina virtuale potrebbero essere applicati costi aggiuntivi. Per altre informazioni, vedere [Dettagli prezzi per le macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/) .
   > 
   > 
6. Le macchine virtuali create in Visual Studio richiedono un servizio cloud. Nella pagina **Impostazioni servizio cloud** selezionare un servizio cloud per la macchina virtuale oppure fare clic su **<Crea nuovo>** nell'elenco a discesa se non si ha già un servizio cloud oppure si vuole usarne uno nuovo. È anche necessario un account di archiviazione, quindi sceglierne uno (o crearne uno nuovo) nell'elenco a discesa **Account di archiviazione** . Per altre informazioni, vedere [Introduzione ad Archiviazione di Microsoft Azure](../articles/storage/common/storage-introduction.md) .
7. Per specificare una rete virtuale (facoltativa) selezionarla negli elenchi a discesa Rete virtuale e Subnet.
   
    Le macchine virtuali che fanno parte di un set di disponibilità vengono distribuite in diversi domini di errore. Per altre informazioni, vedere [Rete virtuale di Azure](https://azure.microsoft.com/services/virtual-network/) .
8. Se la macchina virtuale deve appartenere a un set di disponibilità (facoltativo), selezionare la casella di controllo **Specificare un set di disponibilità** e quindi scegliere un set di disponibilità nell'elenco a discesa. Al termine, scegliere il pulsante **Avanti** .
   
    L'aggiunta della macchina virtuale a un set di disponibilità garantisce la disponibilità dell'applicazione in caso di errori della rete, guasti hardware di un disco locale ed eventuali tempi di inattività pianificati. Per creare reti virtuali, subnet e set di disponibilità è necessario usare il [portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103) . Per altre informazioni, vedere [Gestione della disponibilità delle macchine virtuali](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) .
9. Nella pagina **Endpoint** specificare gli endpoint pubblici che dovranno essere disponibili per gli utenti della macchina virtuale. Ad esempio, è possibile scegliere di abilitare il protocollo HTTP (porta 80) oltre agli endpoint Desktop remoto e PowerShell, che sono abilitati per impostazione predefinita. Per aggiungere un endpoint, sceglierne uno nell'elenco a discesa **Nome porta** e quindi fare clic su **Aggiungi**. Per rimuovere un endpoint, scegliere la **X** rossa accanto al nome nell'elenco di endpoint.
   
    ![Pagina Endpoint nella procedura guidata delle macchine virtuali.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    Gli endpoint disponibili dipendono dal servizio cloud selezionato per la macchina virtuale. Per altre informazioni, vedere [Endpoint di servizio di Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) .
   
   > [!NOTE]
   > L'abilitazione degli endpoint pubblici rende i servizi presenti sulla macchina virtuale disponibili in Internet. Assicurarsi di installare e configurare correttamente gli endpoint e i servizi sulla macchina virtuale, ad esempio impostando gli elenchi di controllo di accesso (ACL) per gli endpoint. Per altre informazioni, vedere la pagina [Come configurare gli endpoint a una macchina virtuale](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) .
   > 
   > 
10. Dopo aver terminato di configurare le impostazioni della macchina virtuale, scegliere **Crea** per creare la macchina virtuale.
    
     Durante la creazione della macchina virtuale, la finestra **Log attività di Azure** mostra l'avanzamento dell'operazione di creazione della macchina virtuale.
    
     ![Log attività macchina virtuale - in corso.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     Per visualizzare solo le informazioni sulla macchina virtuale, scegliere la scheda **Macchine virtuali** nella finestra **Log attività di Microsoft Azure**.
    
     ![Log attività macchina virtuale - completato.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Se l'operazione viene completata correttamente, la nuova macchina virtuale viene visualizzata sotto il nodo **Macchine virtuali** in Esplora Server. È possibile accedervi facendo clic con il tasto destro del mouse e scegliendo **Connessione tramite desktop remoto** .
    
     ![Macchina virtuale visualizzata in Esplora server.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Gestire le macchine virtuali
Nella pagina di configurazione della macchina virtuale, oltre a eseguire le operazioni di arresto, connessione, aggiornamento e di aggiunta di checkpoint alla macchina virtuale selezionata, è anche possibile visualizzare o modificare le impostazioni per la macchina virtuale. È possibile:

* Modificare le dimensioni della macchina virtuale.
* Selezionare il set di disponibilità da usare con la macchina virtuale.
* Aggiungere, rimuovere o modificare le impostazioni per gli endpoint pubblici.
* Aggiungere, rimuovere o configurare le estensioni delle macchine virtuali.
* Visualizzare informazioni relative ai dischi associati alla macchina virtuale.

### <a name="view-or-change-virtual-machine-settings"></a>Visualizzare o modificare impostazioni della macchina virtuale
1. In Esplora Server, scegliere la macchina virtuale nel nodo **Macchine virtuali di Azure** .
2. Nel menu di scelta rapida, scegliere **Configura** per visualizzare la pagina di configurazione della macchina virtuale.
   
    ![Pagina di configurazione della macchina virtuale di Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Visualizzare oppure modificare le informazioni relative alla macchina virtuale.

### <a name="save-or-restore-the-status-of-your-virtual-machine"></a>Salvare o ripristinare lo stato della macchina virtuale
Quando si configura la macchina virtuale e vi si installa del software, è consigliabile salvare regolarmente lo stato di avanzamento creando dei checkpoint della macchina virtuale. Un checkpoint è una snapshot (o immagine) dello stato corrente della macchina virtuale. Se si verificano problemi con la macchina virtuale oppure si vuole riconfigurarla, è possibile risparmiare tempo ripristinandone lo stato a un checkpoint precedente anziché ricominciare da zero.

### <a name="to-create-a-virtual-machine-checkpoint"></a>Per creare un checkpoint della macchina virtuale
1. In Esplora Server, scegliere la macchina virtuale nel nodo **Macchine virtuali di Azure** .
2. Nel menu di scelta rapida, scegliere **Configura** per visualizzare la pagina di configurazione della macchina virtuale.
3. Nella pagina di configurazione, scegliere **Capture Image** .
   
    ![Pulsante Acquisisci della pagina di configurazione di Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Verrà visualizzata la finestra di dialogo **Capture Virtual Machine** .
   
    ![Finestra di dialogo Acquisisci macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Specificare un'etichetta di immagine e una descrizione. Vengono fornite un'etichetta e una descrizione predefinite, ma se si preferisce è possibile sovrascriverle con le proprie.
5. Se è già stato eseguito Sysprep in questa macchina virtuale, selezionare la casella **Sysprep eseguito sulla macchina virtuale** .
   
    Sysprep è uno strumento che, tra le altre cose, rimuove i dati specifici del sistema dalla versione della macchina virtuale di Windows, rendendola un modello utilizzabile dagli altri utenti. Per altre informazioni, vedere [Come acquisire una macchina virtuale Windows da usare come modello](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) . Eseguire il backup della VM prima di eseguire Sysprep.
6. Dopo aver terminato di configurare le impostazioni di acquisizione, scegliere **Acquisisci** per creare il checkpoint.
   
    Durante la creazione del checkpoint, la finestra **Log attività di Azure** mostra l'avanzamento dell'operazione.
   
    ![Acquisizione di un checkpoint della macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Il completamento dell'operazione di checkpoint sarà indicato nella finestra **Log attività di Azure**.
   
    ![Operazione di checkpoint completata](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="to-manage-virtual-machine-checkpoints"></a>Per gestire i checkpoint delle macchine virtuali
### <a name="to-restore-a-virtual-machine-to-a-previously-saved-state"></a>Per ripristinare uno stato precedentemente salvato di una macchina virtuale
* Seguire la procedura dettagliata descritta nella seconda parte del post di blog su come [eseguire ripristini nel cloud delle macchine virtuali di Microsoft Azure con PowerShell](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="to-delete-a-checkpoint"></a>Per eliminare un checkpoint
1. Accedere al [portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Nella parte superiore della pagina di configurazione della macchina virtuale scegliere la scheda **Immagini** .
3. Scegliere il checkpoint che si vuole eliminare e quindi fare clic su **Elimina** nella parte inferiore della pagina.

## <a name="shut-down-your-virtual-machine"></a>Arrestare la macchina virtuale
1. In Esplora Server, scegliere la macchina virtuale che si vuole arrestare nel nodo **Macchine virtuali di Azure** .
2. Nel menu di scelta rapida scegliere il comando **Arresta** oppure **Configura** per visualizzare la pagina di configurazione della macchina virtuale, quindi fare clic su **Arresta**.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sulla creazione di macchine virtuali, vedere [Creare una macchina virtuale che esegue Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [Creare una macchina virtuale che esegue Windows nel portale di anteprima di Azure](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

