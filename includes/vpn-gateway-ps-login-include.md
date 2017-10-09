Prima di iniziare questa configurazione, è necessario accedere tooyour account Azure. cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure. Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell. Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../articles/powershell-azure-resource-manager.md).

toolog, aprire la console di PowerShell con privilegi elevati e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
```

Se si dispone di più sottoscrizioni di Azure, controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

Specificare una sottoscrizione di hello che si desidera toouse.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```