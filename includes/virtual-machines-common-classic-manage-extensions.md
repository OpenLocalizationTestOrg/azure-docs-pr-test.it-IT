


## <a name="using-vm-extensions"></a>Uso delle estensioni di macchina virtuale
Le estensioni VM di Azure implementano comportamenti o funzionalità che consentono di altri programmi di lavorare su macchine virtuali di Azure (ad esempio, hello **WebDeployForVSDevTest** estensione consente tooWeb di Visual Studio distribuire soluzioni nella macchina virtuale di Azure) o fornire Hello possibilità per toointeract con hello VM toosupport alcuni altri comportamenti (ad esempio, è possibile utilizzare le estensioni di accesso alla VM hello da PowerShell, hello Azure CLI e tooreset client REST o modificare i valori di accesso remoto nella macchina virtuale di Azure).

> [!IMPORTANT]
> Per un elenco completo delle estensioni in base che supportano le funzionalità di hello, vedere [estensioni VM di Azure e funzionalità](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Poiché ogni estensione della macchina virtuale supporta una funzionalità specifica, esattamente ciò che è possibile e non con un'estensione dipendono estensione hello. Pertanto, prima di modificare la macchina virtuale, assicurarsi che hanno leggere hello documentazione per l'estensione della macchina virtuale si desidera toouse hello. La rimozione di alcune estensioni di macchina virtuale non è supportata, mentre altre includono proprietà che possono essere impostate e che modificano radicalmente il comportamento della macchina virtuale.
> 
> 

Hello più comuni sono:

1. Individuazione delle estensioni disponibili
2. Aggiornamento delle estensioni caricate
3. Aggiunta di estensioni
4. Rimozione di estensioni

## <a name="find-available-extensions"></a>Individuare le estensioni disponibili
È possibile trovare l'estensione, insieme a informazioni estese, usando:

* PowerShell
* Interfaccia della riga di comando multipiattaforma di Azure (interfaccia della riga di comando di Azure)
* API REST di gestione dei servizi

### <a name="azure-powershell"></a>Azure PowerShell
Alcune estensioni includono i cmdlet di PowerShell toothem specifico, che possono semplificare la configurazione da PowerShell; ma hello seguenti cmdlet funzionano per tutte le estensioni di macchina virtuale.

È possibile utilizzare i seguenti cmdlet tooobtain informazioni sulle estensioni disponibili hello:

* Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.
* Per le istanze di macchine virtuali, è possibile utilizzare hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.
  
   Ad esempio, hello seguente esempio di codice viene illustrato come le informazioni per hello toolist **IaaSDiagnostics** estensione utilizzando PowerShell.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Interfaccia della riga di comando di Azure (Azure CLI)
Alcune estensioni includono comandi CLI di Azure specifico toothem (hello estensione della macchina virtuale Docker è un esempio), che possono semplificarne la configurazione; ma seguente hello dei comandi per tutte le estensioni di macchina virtuale.

È possibile utilizzare hello **elenco di estensioni di macchina virtuale di azure** comando tooobtain informazioni sulle estensioni disponibili e utilizzare hello **–-json** opzione toodisplay tutte le informazioni disponibili su una o più estensioni. Se non si utilizza un nome di estensione, il comando hello restituisce una descrizione JSON di tutte le estensioni disponibili.

Ad esempio, hello esempio di codice seguente viene illustrato come toolist hello informazioni per hello **IaaSDiagnostics** estensione usando hello Azure CLI **elenco di estensioni di macchina virtuale di azure** comando e Usa hello **–-json** opzione tooreturn di informazioni complete.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>API REST di gestione dei servizi
È possibile utilizzare le seguenti API REST tooobtain informazioni sulle estensioni disponibili hello:

* Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello [elenco delle estensioni disponibili](https://msdn.microsoft.com/library/dn169559.aspx) operazione. versioni di hello toolist delle estensioni disponibili, è possibile utilizzare [elenco delle versioni dell'estensione](https://msdn.microsoft.com/library/dn495437.aspx).
* Per le istanze di macchine virtuali, è possibile utilizzare hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operazione. versioni di hello toolist delle estensioni disponibili, è possibile utilizzare [elenco delle versioni dell'estensione risorsa](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Aggiungere, aggiornare o disabilitare le estensioni
È possibile aggiungere estensioni quando viene creata un'istanza o possono essere aggiunti tooa esegue l'istanza. Le estensioni possono essere aggiornate, disabilitate o rimosse. È possibile eseguire queste azioni utilizzando i cmdlet PowerShell di Azure o utilizzando le operazioni API REST di gestione di hello. I parametri sono necessari tooinstall e configurare alcune estensioni. Per le estensioni sono supportati parametri pubblici e privati.

### <a name="azure-powershell"></a>Azure PowerShell
Tramite i cmdlet PowerShell di Azure è hello più semplice modo tooadd e aggiornare le estensioni. Quando si usano i cmdlet di estensione hello, viene eseguita la maggior parte della configurazione di hello dell'estensione hello. In alcuni casi, potrebbe essere necessario tooprogrammatically aggiungere un'estensione. Quando è necessario questo toodo, è necessario fornire la configurazione hello dell'estensione di hello.

È possibile utilizzare i seguenti cmdlet tooknow se un'estensione richiede una configurazione di parametri pubblici e privati hello:

* Per le istanze dei ruoli web o ruoli di lavoro, è possibile utilizzare hello **Get-AzureServiceAvailableExtension** cmdlet.
* Per le istanze di macchine virtuali, è possibile utilizzare hello **Get-AzureVMAvailableExtension** cmdlet.

### <a name="service-management-rest-apis"></a>API REST di gestione dei servizi
Quando si recupera un elenco di estensioni disponibili tramite le API REST di hello, si ottengono informazioni su come estensione hello è toobe configurato. informazioni restituite Hello potrebbero visualizzare informazioni sui parametri, rappresentati da uno schema pubblico e privato dello schema. I valori dei parametri pubblici vengono restituiti in query sulle istanze di hello. I valori dei parametri privati non vengono restituiti.

È possibile utilizzare i seguenti API REST tooknow se un'estensione richiede una configurazione di parametri pubblici e privati hello:

* Per le istanze dei ruoli web o ruoli di lavoro, hello **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementi contengono informazioni hello in risposta hello hello [elenco Le estensioni disponibili](https://msdn.microsoft.com/library/dn169559.aspx) operazione.
* Per le istanze di macchine virtuali, hello **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementi contengono informazioni hello in risposta hello hello [elenco Le estensioni di risorsa](https://msdn.microsoft.com/library/dn495441.aspx) operazione.

> [!NOTE]
> Le estensioni possono anche usare configurazioni definite con JSON. Quando vengono utilizzati questi tipi di estensioni, hello solo **SampleConfig** viene utilizzato l'elemento.
> 
> 

