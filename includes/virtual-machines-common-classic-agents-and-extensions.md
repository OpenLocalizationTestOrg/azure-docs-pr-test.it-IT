

Con le estensioni VM è possibile:

* Modificare le funzionalità di sicurezza e identità, ad esempio la reimpostazione dei valori dell'account e l'uso di soluzioni antimalware.
* Avviare, arrestare o configurare il monitoraggio e la diagnostica.
* Reimpostare o installare funzionalità di connettività, ad esempio RDP e SSH.
* Eseguire la diagnosi, il monitoraggio e la gestione delle macchine virtuali.

Sono disponibili anche molte altre funzionalità. Periodicamente vengono rilasciate nuove funzionalità delle estensioni VM. Questo articolo descrive hello Azure VM agenti per Windows e Linux e modalità con cui supportano funzionalità di estensione della macchina virtuale. Per un elenco di estensioni VM raggruppate per categoria di funzionalità, vedere [Estensioni e funzionalità delle macchine virtuali](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agenti VM di Azure per Windows e Linux
Hello agente di macchine virtuali di Azure (agente VM) è un processo protetto e leggero che installa, configura e rimuove estensioni VM su istanze di macchine virtuali di Azure. Agente VM Hello funge da servizio di controllo locale sicuro hello per la macchina virtuale di Azure. estensioni Hello hello agente carica forniscono funzionalità specifiche tooincrease la produttività istanza hello.

Esistono due agenti VM di Azure, rispettivamente per le macchine virtuali Windows e Linux.

Se si desidera un toouse di istanza di macchina virtuale di una o più estensioni di macchina virtuale, istanza di hello deve essere un agente VM installato. Un'immagine di macchina virtuale creata utilizzando hello portale di Azure e un'immagine da hello **Marketplace** installa automaticamente un agente di macchine Virtuali nel processo di creazione hello. Se un'istanza di macchina virtuale non dispone di un agente di macchine Virtuali, è possibile installare hello agente VM dopo la creazione di istanza di macchina virtuale hello. In alternativa, è possibile installare l'agente di hello in un'immagine di macchina virtuale personalizzata da caricare.

> [!IMPORTANT]
> Gli agenti VM sono servizi con requisiti di risorse limitati che consentono l'amministrazione protetta delle istanze di macchine virtuali. Ci sono casi in cui si desidera hello agente della macchina virtuale. In tal caso, in macchine virtuali di toocreate assicurarsi che non dispongono di hello agente VM installato con hello CLI di Azure o PowerShell. Sebbene hello agente della macchina virtuale può essere rimosso fisicamente, comportamento di hello delle estensioni VM nell'istanza di hello è definito. Di conseguenza, la rimozione di un agente VM installato non è supportata.
>

Hello agente della macchina virtuale è abilitata nella hello seguenti situazioni:

* Quando si crea un'istanza di una macchina virtuale utilizzando hello portale di Azure e selezionando un'immagine hello **Marketplace**,
* Quando si crea un'istanza di una macchina virtuale utilizzando hello [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) o hello [New-AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) cmdlet. È possibile creare una macchina virtuale senza un agente di macchine Virtuali tramite l'aggiunta di hello **– DisableGuestAgent** parametro toohello [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) cmdlet,

* Quando si manualmente scaricare e installare hello agente della macchina virtuale in un'istanza di macchina virtuale esistente e impostare hello **ProvisionGuestAgent** valore troppo**true**. È possibile usare questa tecnica per gli agenti Windows e Linux tramite un comando di PowerShell o una chiamata REST. (Se non si imposta hello **ProvisionGuestAgent** valore dopo l'installazione manuale agente VM, aggiunta di hello di hello agente della macchina virtuale non viene rilevata correttamente hello.) hello seguente esempio di codice viene illustrato come toodo questo utilizzo di PowerShell in cui hello `$svc` e `$name` sono già stati determinati argomenti:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Quando si crea un'immagine di macchina virtuale che include un agente VM installato. Una volta reso disponibile immagine hello con hello agente della macchina virtuale, è possibile caricare tale tooAzure immagine. Per una macchina virtuale di Windows, scaricare hello [file con estensione msi dell'agente VM di Windows](http://go.microsoft.com/fwlink/?LinkID=394789) e installare l'agente VM hello. Per una VM Linux, installare hello all'agente della macchina virtuale dal repository GitHub hello <https://github.com/Azure/WALinuxAgent>. Per ulteriori informazioni su come tooinstall hello agente VM in Linux, vedere hello [Guida dell'utente dell'agente VM Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Nelle soluzioni PaaS hello agente VM è denominato **WindowsAzureGuestAgent**ed è sempre disponibile sul Web e macchine virtuali di ruolo di lavoro. (Per ulteriori informazioni, vedere [Azure Role Architecture](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) hello agente della macchina virtuale per le macchine virtuali ruolo può ora aggiungere estensioni toohello cloud servizio macchine virtuali nel hello stesso modo in cui avviene per le macchine virtuali persistenti. Hello differenza principale tra le estensioni di macchina virtuale nel ruolo di macchine virtuali e macchine virtuali persistenti è quando vengono aggiunti le estensioni VM hello. Con ruolo di macchine virtuali, le estensioni vengono aggiunte primo servizio cloud toohello, quindi toohello distribuzioni all'interno di tale servizio cloud.
>
> Utilizzare il [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) toolist cmdlet tutte le estensioni VM di ruolo disponibili.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Trovare, aggiungere, aggiornare e rimuovere estensioni VM
Per informazioni dettagliate sulle attività, vedere come [aggiungere, trovare, aggiornare e rimuovere estensioni di VM di Azure](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
