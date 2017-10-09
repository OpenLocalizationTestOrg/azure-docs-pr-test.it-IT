È possibile creare macchine virtuali in Azure usando Esplora server in Visual Studio.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>Creare una macchina virtuale di Azure in Esplora server
Sebbene sia possibile creare una macchina virtuale in hello [il portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103), è anche possibile creare una macchina virtuale in Azure usando i comandi in Esplora Server. Macchine virtuali possono essere utilizzate, ad esempio, tooprovide un front end dietro a un endpoint di pubblico comune con bilanciamento del carico.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate una nuova macchina virtuale
1. In Esplora Server, aprire hello **Azure** nodo e fare clic su **macchine virtuali**.
2. Nel menu di scelta rapida hello, fare clic su **crea macchina virtuale**.
   
    Hello **creare una nuova macchina virtuale** procedura guidata viene visualizzata.
   
    ![Hello comando Crea macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. In hello **scegliere una sottoscrizione** selezionare toouse una sottoscrizione durante la creazione di macchine virtuali hello e quindi fare clic su **Avanti**.
   
    Se non sei connesso tooAzure, fare clic su **Accedi** toosign in. Quindi, selezionare la sottoscrizione di Azure nella casella di riepilogo a discesa hello se non è già selezionata.
4. In hello **selezionare un'immagine di macchina virtuale** pagina, selezionare un tipo di immagine in hello **tipo di immagine** nella casella di riepilogo a discesa e quindi selezionare un'immagine di macchina virtuale in hello **nome immagine** casella di riepilogo. Al termine, fare clic su **Avanti**.
   
    ![Selezionare una pagina di immagini di macchine virtuali](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    È possibile scegliere i seguenti tipi di immagine hello.
   
   * **Immagini pubbliche** sono elencate le immagini di macchine virtuali dei sistemi operativi e del software di server come Windows Server ed SQL Server.
   * **Immagini MSDN** vengono elencate le immagini di macchina virtuale di sottoscrittori tooMSDN disponibili software, ad esempio Visual Studio e Microsoft Dynamics.
   * **Immagini private** sono elencate le immagini di macchine virtuali specializzate e generalizzate create dall'utente.
     
     toolearn circa specializzate e generalizzate macchine virtuali, vedere [immagine di macchina virtuale](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/). Vedere [come tooCapture tooUse una macchina virtuale di Windows come modello](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) per informazioni su come creare una macchina virtuale in un modello che è possibile utilizzare tooquickly tooturn preconfigurato macchine virtuali.
     
     È possibile scegliere un'immagine nome toosee informazioni sulla macchina virtuale sull'immagine di hello hello destra della pagina hello.
     
     > [!NOTE]
     > Non è possibile aggiungere toohello immagini di macchina virtuale **immagini pubbliche** o **immagini MSDN** Elenca in quanto sono di sola lettura. Tutte le macchine virtuali create vengono aggiunte toohello **immagini Private** elenco.
     > 
     > 
     
     Gli abbonati MSDN con una sottoscrizione di livello Visual Studio possono creare una macchina virtuale di Azure predefinita contenente Visual Studio, oltre a diverse altre immagini. Per altre informazioni, vedere come [creare una macchina virtuale in Visual Studio tramite le immagini della raccolta di Visual Studio 2013 per sottoscrittori MSDN](http://visualstudio2013msdngalleryimage.azurewebsites.net) e le [sottoscrizioni MSDN](https://www.visualstudio.com/products/msdn-subscriptions-vs).|
5. In hello **le impostazioni di base di macchina virtuale** pagina, immettere un nome di computer e quindi aggiungere le specifiche di hello per la macchina virtuale hello, tra cui dimensioni hello e un nome utente e una password. Al termine, fare clic su **Avanti**.
   
    Si utilizzerà un nuovo nome hello e password toolog macchina hello tramite desktop remoto, pertanto è toowrite una buona idea li verso il basso nel caso si dimentichi. Dopo aver creato una macchina virtuale di Azure in Visual Studio, è possibile modificare le dimensioni e altre impostazioni di hello [il portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
   
   > [!NOTE]
   > Se si scelgono di dimensioni maggiori per la macchina virtuale hello, aggiuntivi potrebbero essere addebitati. Per altre informazioni, vedere [Dettagli prezzi per le macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/) .
   > 
   > 
6. Le macchine virtuali create in Visual Studio richiedono un servizio cloud. In hello **le impostazioni del servizio Cloud** pagina, selezionare un servizio cloud per la macchina virtuale hello oppure fare clic su **< Crea nuovo … >** nell'elenco a discesa di hello se si dispone già di un cloud service o desidera toouse un nuovo uno. È inoltre necessario un account di archiviazione, quindi scegliere un account di archiviazione (o creare un nuovo account di archiviazione) in hello **account di archiviazione** elenco a discesa. Vedere [tooMicrosoft introduzione di archiviazione di Azure](../articles/storage/common/storage-introduction.md) per ulteriori informazioni.
7. Se si desidera toospecify una rete virtuale (operazione facoltativa), selezionarlo in hello rete virtuale e Subnet elenchi a discesa.
   
    Macchine virtuali che sono membri di un set di disponibilità vengono distribuite toodifferent domini di errore. Per altre informazioni, vedere [Rete virtuale di Azure](https://azure.microsoft.com/services/virtual-network/) .
8. Se si desidera che il macchina virtuale toobelong tooan set di disponibilità (operazione facoltativa), selezionare hello **specificare un set di disponibilità** casella di controllo e quindi scegliere un set nella casella di riepilogo a discesa hello di disponibilità. Al termine, scegliere hello **Avanti** pulsante.
   
    Aggiungere la macchina virtuale di tooan set di disponibilità consente di restare disponibile durante errori di rete, errori hardware del disco locale e qualsiasi tempo di inattività. È necessario hello toouse [il portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103) imposta toocreate le reti virtuali, subnet e la disponibilità. Vedere [Gestisci hello disponibilità delle macchine virtuali](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) per ulteriori informazioni.
9. In hello **endpoint** specificare endpoint pubblici di hello che si desidera toousers disponibili della macchina virtuale. Ad esempio, è possibile scegliere tooenable HTTP (porta 80) inoltre toohello Desktop remoto e PowerShell endpoint, che sono abilitati per impostazione predefinita. tooadd un endpoint, sceglierne uno nell'hello **nome porta** elenco a discesa nella casella di riepilogo e quindi scegliere hello **Aggiungi** pulsante. tooremove un endpoint, scegliere hello rosso **X** nome toohello successivo nell'elenco di endpoint hello.
   
    ![pagina endpoint Hello nella procedura guidata di hello macchine virtuali.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    endpoint Hello disponibili dipendono dal servizio cloud di hello selezionato per la macchina virtuale. Per altre informazioni, vedere [Endpoint di servizio di Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) .
   
   > [!NOTE]
   > Gli endpoint pubblici abilitando servizi su toohello di disponibile la macchina virtuale internet. Essere tooinstall verificare e configurare correttamente hello endpoint e i servizi sulla macchina virtuale, ad esempio elenchi di controllo di accesso impostazione (ACL) per gli endpoint di hello. Vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) per ulteriori informazioni.
   > 
   > 
10. Dopo la configurazione delle impostazioni hello macchina virtuale, scegliere hello **crea** macchina virtuale di hello toocreate pulsante.
    
     Quando Azure crea macchina virtuale hello, hello **Log attività Azure** Mostra hello lo stato di avanzamento dell'operazione di creazione di hello macchina virtuale.
    
     ![Log attività macchina virtuale - in corso.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     informazioni di macchina virtuale solo tooview, scegliere hello **macchine virtuali** scheda hello **Log attività Azure**.
    
     ![Log attività macchina virtuale - completato.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Se il completamento dell'operazione di hello, hello nuova macchina virtuale viene visualizzata in hello **macchine virtuali** nodo in Esplora Server. È possibile accedere al suo interno facendo hello **connessione tramite Desktop remoto** scelta rapida.
    
     ![Macchina virtuale visualizzata in Esplora server.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>Gestire le macchine virtuali
Nella pagina di configurazione macchina virtuale hello inoltre tooshutting verso il basso, la connessione, aggiornare e aggiungere checkpoint toohello selezionata macchina virtuale, è anche possibile visualizzare o modificare le impostazioni per la macchina virtuale hello. È possibile:

* Modificare la dimensione di macchina virtuale hello.
* Set di disponibilità di hello selezionare toouse con la macchina virtuale hello.
* Aggiungere, rimuovere o modificare le impostazioni per gli endpoint pubblici.
* Aggiungere, rimuovere o configurare le estensioni delle macchine virtuali.
* Visualizza informazioni sui dischi hello associata a una macchina virtuale hello.

### <a name="view-or-change-virtual-machine-settings"></a>Visualizzare o modificare impostazioni della macchina virtuale
1. In Esplora Server, scegliere la macchina virtuale in hello **macchine virtuali di Azure** nodo.
2. Scegliere dal menu di scelta rapida di hello **configura** pagina di configurazione tooview hello macchina virtuale.
   
    ![pagina di configurazione macchina virtuale di Azure Hello](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Consente di visualizzare informazioni della macchina virtuale hello o modificarlo.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>Salvare o ripristinare lo stato di hello della macchina virtuale
Come configurare la macchina virtuale e installare software su di esso, è un tooregularly opportuno salvare lo stato di avanzamento tramite la creazione di checkpoint della macchina virtuale. Un checkpoint è uno snapshot, o immagine, dello stato corrente di hello della macchina virtuale. Se si verificano problemi con la macchina virtuale hello o macchina virtuale di hello tooreconfigure, è possibile risparmiare tempo ripristinandolo tooa lo stato di checkpoint precedente anziché ripartire da zero.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>toocreate un checkpoint della macchina virtuale
1. In Esplora Server, scegliere la macchina virtuale in hello **macchine virtuali di Azure** nodo.
2. Scegliere dal menu di scelta rapida di hello **configura** pagina di configurazione tooview hello macchina virtuale.
3. Nella pagina Configurazione hello scegliere hello **Acquisisci immagine** pulsante.
   
    ![Pulsante Acquisisci della pagina di configurazione di Azure](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    Hello **Acquisisci macchina virtuale** viene visualizzata la finestra.
   
    ![Finestra di dialogo Acquisisci macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. Specificare un'etichetta di immagine e una descrizione. Vengono fornite un'etichetta e una descrizione predefinite, ma se si preferisce è possibile sovrascriverle con le proprie.
5. Se già stato eseguito Sysprep nella macchina virtuale, selezionare hello **Sysprep eseguito sulla macchina virtuale hello** casella.
   
    Sysprep è uno strumento che, tra le altre cose, rimuove i dati specifici del sistema dalla versione di hello virtuale della macchina virtuale di Windows, creando un modello che altri utenti possono usare. Vedere [come tooCapture tooUse una macchina virtuale di Windows come modello](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) per ulteriori informazioni. Eseguire il backup hello VM prima di eseguire Sysprep.
6. Dopo la configurazione delle impostazioni di acquisizione hello, scegliere hello **acquisire** checkpoint di hello toocreate pulsante.
   
    Durante la creazione del checkpoint hello, hello **Log attività Azure** Mostra hello lo stato di avanzamento dell'operazione di hello.
   
    ![Acquisizione di un checkpoint della macchina virtuale](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Al termine dell'operazione di checkpoint hello, verrà visualizzato in hello **Log attività Azure**.
   
    ![Operazione di checkpoint completata](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>Checkpoint della macchina virtuale toomanage
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>lo stato precedentemente salvato toorestore tooa una macchina virtuale
* Seguire i passaggi di hello illustrati in [procedura dettagliata: eseguire Cloud Ripristina Microsoft macchine virtuali di Azure con PowerShell - parte 2](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx).

### <a name="toodelete-a-checkpoint"></a>toodelete un checkpoint
1. Passare toohello [il portale di gestione di Azure](http://go.microsoft.com/fwlink/?LinkID=253103).
2. Nella pagina di configurazione macchina virtuale hello scegliere hello **immagini** scheda nella parte superiore di hello della pagina hello.
3. Scegliere checkpoint hello toodelete desiderato e quindi scegliere hello **eliminare** pulsante nella parte inferiore di hello della pagina hello.

## <a name="shut-down-your-virtual-machine"></a>Arrestare la macchina virtuale
1. In Esplora Server, scegliere macchina virtuale di hello da tooshut verso il basso in hello **macchine virtuali di Azure** nodo.
2. Scegliere dal menu di scelta rapida hello, hello **arresto** comando oppure scegliere **configura** tooview hello pagina di configurazione macchina virtuale e quindi scegliere hello **arresto**pulsante.

## <a name="next-steps"></a>Passaggi successivi
toolearn informazioni sulla creazione di macchine virtuali, vedere [creare una macchina virtuale che esegue Linux](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) e [creare una macchina virtuale in esecuzione Windows nel portale di anteprima di Azure hello](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

