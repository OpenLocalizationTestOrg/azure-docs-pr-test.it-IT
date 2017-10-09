### <a name="troubleshoot-azure-diagnostics"></a>Risolvere i problemi relativi a Diagnostica di Azure

Se si riceve hello seguente messaggio di errore, non è registrato alcun provider di risorse Insights hello:

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

provider di risorse tooregister hello, eseguire hello in hello portale di Azure come segue:

1.  Nel riquadro di spostamento hello hello sinistra, fare clic su *sottoscrizioni*
2.  Selezionare la sottoscrizione di hello identificata nel messaggio di errore hello
3.  Fare clic su *Provider di risorse*.
4.  Trovare hello *Insights* provider
5.  Fare clic su hello *registrare* collegamento

![Registrare il provider di risorse Microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

Una volta hello *Insights* provider di risorse è registrato, nuovo tentativo di configurazione della diagnostica.


In PowerShell, se si riceve hello seguente messaggio di errore, occorre tooupdate la versione di PowerShell:

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

Aggiornare la versione di PowerShell toohello novembre 2016 (v2.3.0) o versione successiva, rilasciare seguendo le istruzioni di hello nella hello [Introduzione ai cmdlet di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) articolo.
