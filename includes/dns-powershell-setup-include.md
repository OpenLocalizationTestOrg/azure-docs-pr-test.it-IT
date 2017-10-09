## <a name="set-up-azure-powershell-for-azure-dns"></a>Configurare Azure PowerShell per DNS di Azure

### <a name="before-you-begin"></a>Prima di iniziare

Verificare di aver hello seguenti prima di iniziare la configurazione.

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* È necessario tooinstall hello più recente di hello cmdlet PowerShell di gestione risorse di Azure. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Accedi tooyour account Azure

Aprire la console di PowerShell e tooyour account di connessione. Per altre informazioni, vedere [Uso di PowerShell con Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Selezionare la sottoscrizione hello
 
Controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

Scegliere quali di toouse le sottoscrizioni di Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Tuttavia, poiché tutte le risorse DNS sono globali, non è regionale, scelta hello del percorso del gruppo di risorse ha alcun impatto su DNS di Azure.

Se si usa un gruppo di risorse esistente, è possibile ignorare questo passaggio.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Registrare il provider di risorse

Hello servizio DNS di Azure viene gestita dal provider di risorse Microsoft. Network hello. La sottoscrizione di Azure deve essere registrato toouse questo provider di risorse prima di poter usare DNS di Azure. Questa operazione viene eseguita una sola volta per ogni sottoscrizione.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```