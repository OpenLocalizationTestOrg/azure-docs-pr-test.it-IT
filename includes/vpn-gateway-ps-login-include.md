<span data-ttu-id="f4e32-101">Prima di iniziare questa configurazione, è necessario accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e32-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="f4e32-102">cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e32-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="f4e32-103">Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4e32-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="f4e32-104">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f4e32-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="f4e32-105">toolog, aprire la console di PowerShell con privilegi elevati e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="f4e32-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="f4e32-106">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="f4e32-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f4e32-107">Se si dispone di più sottoscrizioni di Azure, controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="f4e32-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f4e32-108">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="f4e32-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```