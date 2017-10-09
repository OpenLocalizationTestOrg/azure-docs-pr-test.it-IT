## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Preparare Gestione risorse di Azure richiede tooauthenticate
È necessario autenticare tutte le operazioni eseguite sulle risorse con hello hello [Azure Resource Manager] [ lnk-authenticate-arm] con Azure Active Directory (AD). Hello tooconfigure modo più semplice è toouse PowerShell o CLI di Azure.

Installare hello [cmdlet di Azure PowerShell] [ lnk-powershell-install] prima di continuare.

Hello seguente procedura mostra come tooset autenticazione tramite password per un'applicazione di Active Directory tramite PowerShell. È possibile eseguire questi comandi in una sessione standard di PowerShell.

1. Accedi tooyour sottoscrizione di Azure utilizzando hello comando seguente:

    ```powershell
    Login-AzureRmAccount
    ```

1. Se si dispone di più sottoscrizioni di Azure, consente l'accesso tooall accesso tooAzure hello le sottoscrizioni di Azure associate con le credenziali. Utilizzare hello toolist hello Azure sottoscrizioni disponibili per l'utente toouse comando seguente:

    ```powershell
    Get-AzureRMSubscription
    ```

    Utilizzare hello seguente sottoscrizione tooselect comando che si desidera toouse toorun hello comandi toomanage l'hub IoT. È possibile utilizzare il nome di sottoscrizione hello o ID dall'output di hello del comando precedente hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Prendere nota dei valori di **TenantId** e **SubscriptionId**. Saranno necessari più avanti.
3. Creare una nuova applicazione di Azure Active Directory utilizzando hello comando seguente, sostituendo i segnaposto hello:
   
   * **{Display name}:** un nome visualizzato per l'applicazione, ad esempio **MySampleApp**.
   * **{URL della Home page}:** hello URL della home page di hello dell'app, ad esempio **http://mysampleapp/home**. Questo URL non è necessario toopoint tooa reali dell'applicazione.
   * **{Application identifier}:** un identificatore univoco, ad esempio **http://mysampleapp**. Questo URL non è necessario toopoint tooa reali dell'applicazione.
   * **{Password}:** una password usata tooauthenticate con l'app.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Prendere nota di hello **ApplicationId** dell'applicazione hello è stato creato. Sarà necessario più avanti.
5. Creare una nuova entità servizio utilizzando hello comando seguente, sostituendo **{MyApplicationId}** con hello **ApplicationId** dal passaggio precedente hello:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Impostare un'assegnazione di ruolo utilizzando hello comando seguente, sostituendo **{MyApplicationId}** con il **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Completata Creazione hello Azure AD è un'applicazione tooauthenticate dall'applicazione c# personalizzata. È necessario hello seguente i valori più avanti in questa esercitazione:

* TenantId
* SubscriptionId
* ApplicationId
* Password

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
