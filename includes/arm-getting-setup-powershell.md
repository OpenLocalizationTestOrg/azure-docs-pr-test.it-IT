## <a name="setting-up-powershell-for-resource-manager-templates"></a>Configurazione di PowerShell per i modelli di Gestione risorse
Prima di poter usare Azure PowerShell con Gestione risorse, è necessario verificare di disporre delle versioni corrette di Windows PowerShell e Azure PowerShell.

### <a name="verify-powershell-versions"></a>Verificare le versioni di PowerShell
Verificare che la versione di Windows PowerShell in uso sia 3.0 o 4.0. Per individuare la versione di Windows PowerShell, digitare il comando seguente al prompt dei comandi di Windows PowerShell.

    $PSVersionTable

Verrà visualizzato il tipo di informazioni seguente:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Verificare che il valore di **PSVersion** sia 3.0 o 4.0. In caso contrario, vedere [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) o [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Impostare l'account e la sottoscrizione di Azure
Se non si ha già una sottoscrizione di Azure, è possibile attivare i [benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).

Aprire un prompt dei comandi di Azure PowerShell e usare il comando seguente per accedere ad Azure.

    Login-AzureRmAccount

Se si dispone di più sottoscrizioni di Azure, è possibile usare il comando seguente per visualizzarne l'elenco.

    Get-AzureRmSubscription

Verrà visualizzato il tipo di informazioni seguente:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Per impostare la sottoscrizione di Azure corrente, eseguire i comandi seguenti al prompt dei comandi di Azure PowerShell. Sostituire tutti gli elementi all'interno delle virgolette, inclusi i caratteri < e >, con il nome corretto.

    $subscr="<SubscriptionName from the display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Per altre informazioni su sottoscrizioni e account di Azure, vedere [Procedura: Connettersi alla sottoscrizione](/powershell/azureps-cmdlets-docs#step-3-connect).

