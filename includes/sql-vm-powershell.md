
## <a name="start-your-powershell-session"></a>Avviare la sessione di PowerShell
È necessario innanzitutto hello toohave più recente [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installato e in esecuzione. Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Hello esempi in questo argomento usano [il modello di distribuzione Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), pertanto esempi usano hello [i cmdlet di Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Eseguire hello [ **Aggiungi AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) cmdlet e verrà visualizzata una schermata tooenter di accesso le credenziali. Utilizzare hello stesso credenziali utilizzare toosign toohello portale di Azure.

    Add-AzureRmAccount

Se dispone di più sottoscrizioni utilizzano hello [ **Set AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect cmdlet la sottoscrizione deve utilizzare la sessione di PowerShell. toosee quale sottoscrizione hello PowerShell corrente utilizza sessione, eseguire [ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). eseguire tutte le sottoscrizioni, toosee [ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

