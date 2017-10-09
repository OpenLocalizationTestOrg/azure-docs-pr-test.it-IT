## <a name="prepare-for-akv-integration"></a>Preparare l'integrazione di AKV
toouse tooconfigure di integrazione dell'insieme di credenziali chiave di Azure la macchina virtuale di SQL Server, esistono diversi prerequisiti: 

1. [Installare Azure PowerShell](#install-azure-powershell)
2. [Creare un'istanza di Azure Active Directory](#create-an-azure-active-directory)
3. [Creare un insieme di credenziali delle chiavi](#create-a-key-vault)

Hello nelle sezioni seguenti vengono descritti i prerequisiti e le informazioni di hello necessarie i cmdlet di PowerShell toocollect toolater eseguire hello.

### <a name="install-azure-powershell"></a>Installare Azure PowerShell
Assicurarsi di aver installato hello Azure PowerShell SDK più recente. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Creare un'istanza di Azure Active Directory
È innanzitutto necessario toohave un [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) nella sottoscrizione. Tra i molti vantaggi, in questo modo toogrant autorizzazione tooyour chiave dell'insieme di credenziali per alcuni utenti e applicazioni.

Successivamente, registrare un'applicazione con AAD. Questa query fornirà un account dell'entità servizio che ha accesso tooyour insieme di credenziali chiave che sarà necessario la macchina virtuale. Nell'articolo insieme credenziali chiavi Azure hello, è possibile trovare questi passaggi in hello [registrare un'applicazione con Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) sezione, oppure è possibile vedere i passaggi di hello con nelle schermate hello **ottenere un'identità per un'applicazione hello sezione** di [questo post di blog](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Prima di completare questi passaggi, si noti che è necessario hello toocollect le seguenti informazioni durante la registrazione che è necessario in seguito quando si abilita l'integrazione dell'insieme di credenziali chiave di Azure nella VM SQL.

* Dopo l'aggiunta di un'applicazione hello, trovare hello **ID CLIENT** su hello **configura** scheda.   ![ID client di Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    ID client Hello viene assegnato successive toohello **$spName** parametro (Service Principal name) in hello PowerShell script tooenable integrazione dell'insieme di credenziali chiave di Azure. 
* Inoltre, durante questa procedura quando si crea la chiave, copiare la hello chiave privata per la chiave come illustrato nella seguente schermata hello. Questa chiave segreta viene assegnato successive toohello **$spSecret** parametro (entità servizio secret) nello script di PowerShell hello.  
    ![Segreto di Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* È necessario autorizzare il nuovo ID toohave messaggi hello del client dopo le autorizzazioni di accesso: **crittografare**, **decrittografare**, **wrapKey**, **unwrapKey**, **sign**, e **verificare**. Questa operazione viene eseguita con hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) cmdlet. Per ulteriori informazioni vedere [Authorize hello applicazione toouse hello chiave o il segreto](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Creare un insieme di credenziali delle chiavi
In ordine toouse insieme credenziali chiavi Azure toostore hello chiavi da utilizzare per la crittografia nella macchina virtuale, è necessario l'insieme di credenziali chiave di accesso tooa. Se non è già impostata la chiave dell'insieme di credenziali, crearne una seguendo i passaggi hello hello [introduzione insieme credenziali chiavi Azure](../articles/key-vault/key-vault-get-started.md) argomento. Prima di completare questi passaggi, si noti che alcune informazioni necessarie toocollect durante questo set di backup che sono necessario in seguito quando si abilita l'integrazione dell'insieme di credenziali chiave di Azure nella VM SQL.

Quando si ottengono toohello creare un passaggio di insieme di credenziali delle chiavi, hello nota restituito **vaultUri** proprietà, che è l'URL dell'insieme di credenziali chiave hello. Nell'esempio hello fornita in questo passaggio, illustrato di seguito, nome dell'insieme di credenziali chiave hello è ContosoKeyVault, pertanto URL dell'insieme di credenziali chiave hello sarebbe https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

URL dell'insieme di credenziali chiave Hello viene assegnato successive toohello **$akvURL** parametro hello PowerShell script tooenable integrazione dell'insieme di credenziali chiave di Azure.

