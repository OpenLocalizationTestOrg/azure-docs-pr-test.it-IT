
## <a name="start-your-powershell-session"></a>Avviare la sessione di PowerShell
In primo luogo, si deve avere hello più recente di Azure PowerShell installato e in esecuzione. Per informazioni dettagliate, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Numerose nuove funzionalità di Database SQL sono supportate solo quando si utilizza hello [il modello di distribuzione Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), pertanto esempi usano hello [i cmdlet di PowerShell per Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) per Gestione risorse . modello di distribuzione di gestione (classico) servizio Hello [i cmdlet di gestione del servizio di Database SQL di Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) sono supportate per compatibilità con le versioni precedenti, ma si consiglia di usare hello cmdlet di gestione risorse.
> 
> 

Eseguire hello [ **Aggiungi AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) cmdlet e verrà visualizzata una schermata di accesso di tooenter le credenziali. Utilizzare hello stesso credenziali utilizzare toosign toohello portale di Azure.

```PowerShell
Add-AzureRmAccount
```

Se si dispone di più sottoscrizioni, usare hello [ **Set AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect cmdlet la sottoscrizione deve utilizzare la sessione di PowerShell. toosee quale sottoscrizione hello PowerShell corrente utilizza sessione, eseguire [ **Get AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). eseguire tutte le sottoscrizioni, toosee [ **Get AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
