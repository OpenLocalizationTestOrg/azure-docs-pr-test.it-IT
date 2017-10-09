



A seconda di ambiente e le scelte, script di hello può creare tutta l'infrastruttura cluster hello, tra cui hello rete virtuale di Azure, gli account di archiviazione, servizi cloud, controller di dominio, i database SQL locali o remoti, il nodo head e cluster aggiuntivo nodi. In alternativa, utilizzare infrastruttura di Azure preesistente e creare solo nodi del cluster HPC hello script hello.

Per informazioni generali sulla pianificazione di un cluster HPC Pack, vedere hello [valutazione del prodotto e alla pianificazione](https://technet.microsoft.com/library/jj899596.aspx) e [Introduzione](https://technet.microsoft.com/library/jj899590.aspx) contenuto nella libreria TechNet di HPC Pack 2012 R2 hello.

## <a name="prerequisites"></a>Prerequisiti
* **Sottoscrizione di Azure**: È possibile utilizzare una sottoscrizione in un servizio Azure globale o Azure China hello. Ai termini della sottoscrizione influiscono sul numero di hello e tipo dei nodi del cluster che è possibile distribuire. Per informazioni, vedere [Limiti, quote e vincoli delle sottoscrizioni e dei servizi di Microsoft Azure](../articles/azure-subscription-service-limits.md).
* **Computer client Windows con Azure PowerShell 0.8.10 o versione successiva installato e configurato**: vedere [Guida introduttiva di Azure PowerShell](/powershell/azureps-cmdlets-docs) per installazione istruzioni e i passaggi tooconnect tooyour sottoscrizione di Azure.
* **Script di distribuzione IaaS di HPC Pack**: scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Controllare la versione di hello dello script di hello eseguendo `New-HPCIaaSCluster.ps1 –Version`. In questo articolo si basa sulla versione 4.5.2 dello script hello.
* **File di configurazione script**: creare un file XML che script hello utilizza un cluster HPC tooconfigure hello. Per informazioni ed esempi, vedere le sezioni più avanti in questo articolo e hello file Manual.rtf che accompagna script di distribuzione hello.

## <a name="syntax"></a>Sintassi
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Eseguire script hello come amministratore.
> 
> 

### <a name="parameters"></a>parameters
* **ConfigFile**: Specifica il percorso file hello hello configurazione toodescribe hello HPC del cluster di file. Vedere informazioni sui file di configurazione hello in questo argomento, o nel file hello Manual.rtf nella cartella hello contenente script hello.
* **AdminUserName**: Specifica il nome utente hello. Se la foresta di domini hello creata dallo script hello, questa diventa nome utente dell'amministratore locale hello per tutte le macchine virtuali e il nome di amministratore di dominio hello. Se esiste già una foresta di domini hello, si specifica utente di dominio hello hello tooinstall di nome utente amministratore locale HPC Pack.
* **AdminPassword**: specifica la password dell'amministratore di hello. Se non specificato nella riga di comando hello, script hello richiede password hello tooinput.
* **HPCImageName** (facoltativo): specifica un cluster HPC hello toodeploy nome immagine di macchina virtuale di HPC Pack hello. Deve essere un'immagine fornita da Microsoft HPC Pack da hello Azure Marketplace. Se non viene specificato hello (consigliato in genere), script sceglie hello più recente pubblicata [HPC Pack 2012 R2 immagine](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). immagine più recente di Hello è basata su Windows Server 2012 R2 Datacenter con HPC Pack 2012 R2 Update 3.
  
  > [!NOTE]
  > Se non si specifica un'immagine HPC Pack valida, la distribuzione avrà esito negativo.
  > 
  > 
* **File di registro** (facoltativo): percorso del file di registro distribuzione hello specifica. Se non specificato, script hello crea un file di log nella directory temp di hello del hello che esegue script hello.
* **Force** (facoltativo): Elimina tutte le richieste di conferma hello.
* **NoCleanOnFailure** (facoltativo): Specifica che le macchine virtuali di Azure che non vengono distribuiti hello non vengono rimossi. Rimuovere manualmente queste macchine virtuali prima di eseguire nuovamente la distribuzione di hello script toocontinue hello o hello distribuzione potrebbe non riuscire.
* **PSSessionSkipCACheck** (facoltativo): per ogni servizio cloud con macchine virtuali distribuite da questo script, un certificato autofirmato viene generato automaticamente da Azure e hello tutte le macchine virtuali nel servizio cloud hello Usa questo certificato, come impostazione predefinita Windows hello Certificato di gestione (WinRM) remoto. funzionalità di toodeploy HPC in queste macchine virtuali di Azure, per impostazione predefinita script hello installa temporaneamente questi certificati nel Computer locale hello\\archivio Autorità di certificazione radice attendibili di hello client computer toosuppress hello sicurezza "CA non attendibile" Errore durante l'esecuzione dello script. i certificati di Hello vengono rimossi al termine dello script hello. Se viene specificato questo parametro, i certificati di hello non sono installati nel computer client hello e hello sicurezza l'avviso.
  
  > [!IMPORTANT]
  > Questo parametro non è consigliato per distribuzioni di produzione.
  > 
  > 

### <a name="example"></a>Esempio
esempio Hello crea un cluster HPC Pack utilizzando il file di configurazione *MyConfigFile.xml*e specifica le credenziali di amministratore per l'installazione cluster hello.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Considerazioni aggiuntive
* script Hello possibile consentire l'invio di processi tramite portale web di HPC Pack hello o hello API REST di HPC Pack.
* script Hello può facoltativamente eseguire script di pre e post-configurazione personalizzati nel nodo head hello se si desidera software aggiuntivo tooinstall o configurare altre impostazioni.

## <a name="configuration-file"></a>File di configurazione
file di configurazione Hello per lo script di distribuzione hello è un file XML. file di schema Hello hpciaasclusterconfig.xsd si trova nella cartella script di distribuzione IaaS di HPC Pack hello. **IaaSClusterConfig** hello di elemento radice del file di configurazione hello, che contiene gli elementi figlio di hello descritti in dettaglio nel file hello Manual.rtf nella cartella script di distribuzione hello.

