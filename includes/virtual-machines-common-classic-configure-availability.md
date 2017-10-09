


Un set di disponibilità aiuta a mantenere disponibili le macchine virtuali durante il tempo di inattività, ad esempio durante la manutenzione. Inserimento di due o più macchine virtuali configurate in modo simile in un set di disponibilità crea hello ridondanza necessita toomaintain disponibilità di applicazioni di hello o servizi che esegue la macchina virtuale. Per informazioni dettagliate sul funzionamento, vedere [gestione hello disponibilità delle macchine virtuali][Manage hello availability of virtual machines].

È una migliore toouse pratica sia set di disponibilità e bilanciamento del carico endpoint toohelp assicurarsi che l'applicazione sia sempre disponibile e in esecuzione in modo efficiente. Per informazioni dettagliate sugli endpoint con bilanciamento del carico, vedere [Bilanciamento del carico per i servizi di infrastruttura di Azure][Load balancing for Azure infrastructure services].

È possibile aggiungere le macchine virtuali in un set di disponibilità usando una di queste due opzioni:

* [Opzione 1: Creare una macchina virtuale e un gruppo di disponibilità in hello stesso tempo][Option 1: Create a virtual machine and an availability set at hello same time]. Quindi, aggiungere nuove macchine virtuali toohello, imposta quando si creano le macchine virtuali.
* [Opzione 2: Aggiungere un set di disponibilità tooan macchina virtuale esistente][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> Nel modello classico hello, macchine virtuali che si desidera tooput nei hello stesso set di disponibilità deve appartenere toohello stesso servizio cloud.
> 
> 

## <a id="createset"></a>Opzione 1: creare una macchina virtuale e un gruppo di disponibilità in hello stesso tempo
È possibile utilizzare entrambi hello portale di Azure o Azure PowerShell comandi toodo questo.

hello toouse portale di Azure:

1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com).
2. Nel menu hub hello, fare clic su **+ nuovo**, quindi fare clic su **macchina virtuale**.
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Selezionare l'immagine di macchina virtuale Marketplace hello desiderato toouse. È possibile scegliere toocreate una macchina virtuale Linux o Windows.
4. Per hello selezionato macchina virtuale, verificare che il modello di distribuzione hello sia impostato troppo**classico** e quindi fare clic su **crea**
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Immettere il nome della macchina virtuale, il nome utente e la password (per computer Windows) o la chiave pubblica SSH (per i computer Linux). 
6. Scegliere le dimensioni VM hello e quindi fare clic su **selezionare** toocontinue.
7. Scegliere **configurazione facoltativa > set di disponibilità**e selezionare il set di disponibilità hello desiderato tooadd hello della macchina virtuale.
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Verificare le impostazioni di configurazione. Al termine dell'operazione, scegliere **Crea**.
9. Mentre Azure crea la macchina virtuale, è possibile monitorare lo stato di avanzamento hello in **macchine virtuali** nel menu hub hello.

Azure PowerShell toouse comandi toocreate una macchina virtuale di Azure e aggiungerlo tooa set di disponibilità di nuovo o esistente, vedere [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Opzione 2: aggiungere un set di disponibilità tooan macchina virtuale esistente
Nel portale di Azure hello, è possibile aggiungere tooan di macchine virtuali classiche esistenti set di disponibilità esistente o crearne uno nuovo per loro. (Tenere presente che le macchine virtuali hello in hello stesso set di disponibilità deve appartenere toohello stesso servizio cloud.) passaggi di Hello sono quasi hello stesso. Con Azure PowerShell, è possibile aggiungere hello macchina virtuale tooan set di disponibilità esistente.

1. Se non è già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com).
2. Nel menu Hub hello, fare clic su **macchine virtuali (classico)**.
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Elenco di hello di macchine virtuali, selezionare il nome di hello della macchina virtuale hello che si desidera tooadd toohello set.
4. Scegliere **set di disponibilità** dalla macchina virtuale hello **impostazioni**.
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Selezionare il set di disponibilità hello desiderato tooadd hello della macchina virtuale. macchina virtuale Hello devono appartenere toohello servizio stesso cloud come set di disponibilità hello.
   
    ![Testo immagine alt](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Fare clic su **Salva**.

comandi di Azure PowerShell toouse, aprire una sessione di PowerShell di Azure a livello di amministratore ed eseguire hello comando seguente. Per i segnaposto hello (ad esempio &lt;VmCloudServiceName&gt;), sostituire tutto il contenuto all'interno di virgolette hello, inclusi i caratteri di hello < e >, con hello correggere nomi.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> macchina virtuale Hello potrebbe essere riavviato toobe toofinish aggiungerlo toohello set di disponibilità.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

