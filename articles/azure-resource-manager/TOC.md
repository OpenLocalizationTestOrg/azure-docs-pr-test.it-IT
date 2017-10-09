# Panoramica
## [Informazioni su Resource Manager](resource-group-overview.md)
## [Provider e tipi di risorse](resource-manager-supported-services.md)
## [Distribuzione Resource Manager e classica](resource-manager-deployment-model.md)
## [Governance per le sottoscrizioni](resource-manager-subscription-governance.md)
## [Applicazioni gestite](managed-application-overview.md)

# Introduzione
## [Esportare il modello](resource-manager-export-template.md)
## [Creare e distribuire il modello](resource-manager-create-first-template.md)
## [Visual Studio con Resource Manager](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)

# Esempi
## [Esempi di codice](https://azure.microsoft.com/en-us/resources/samples/?service=azure-resource-manager)
## PowerShell
### [Distribuire un modello](resource-manager-samples-powershell-deploy.md)

## Interfaccia della riga di comando di Azure
### [Distribuire un modello](resource-manager-samples-cli-deploy.md)

# Procedure
## Creare modelli
### [Procedure consigliate per i modelli](resource-manager-template-best-practices.md)
### [Sezioni di modelli](resource-group-authoring-templates.md)
### [Collegamento tooother modelli](resource-group-linked-templates.md)
### [Definire la dipendenza tra risorse](resource-group-define-dependencies.md)
### [Creare più istanze](resource-group-create-multiple.md)
### [Impostare la posizione](resource-manager-template-location.md)
### [Assegnare i tag](resource-manager-template-tags.md)
### [Impostare il nome e il tipo della risorsa figlio](resource-manager-template-child-resource.md)
### [Aggiornare una risorsa](resource-manager-update.md)
### [Usare gli oggetti per i parametri](resource-manager-objects-as-parameters.md)
### [Condividere lo stato tra modelli collegati](best-practices-resource-manager-state.md)
### [Schemi per la progettazione di modelli](best-practices-resource-manager-design-templates.md)

## Distribuire
### PowerShell
#### [Distribuire un modello](resource-group-template-deploy.md)
#### [Distribuire un modello privato con token SAS](resource-manager-powershell-sas-token.md)
#### [Esportare il modello e ridistribuirlo](resource-manager-export-template-powershell.md)
### Interfaccia della riga di comando di Azure
#### [Distribuire un modello](resource-group-template-deploy-cli.md)
#### [Distribuire un modello privato con token SAS](resource-manager-cli-sas-token.md)
#### [Esportare il modello e ridistribuirlo](resource-manager-export-template-cli.md)
### [Portale](resource-group-template-deploy-portal.md)
### [API REST](resource-group-template-deploy-rest.md)
### [Distribuzione in più gruppi di risorse](resource-manager-cross-resource-group-deployment.md)
### [Integrazione continua con Visual Studio Team Services](../vs-azure-tools-resource-groups-ci-in-vsts.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
### [Passare valori protetti durante la distribuzione](resource-manager-keyvault-parameter.md)

## Gestire
### [PowerShell](powershell-azure-resource-manager.md)
### [Interfaccia della riga di comando di Azure](xplat-cli-azure-resource-manager.md)
### [Portale](resource-group-portal.md)
### [API REST](resource-manager-rest-api.md)
### [Utilizzare tag tooorganize risorse](resource-group-using-tags.md)
### [Spostare sottoscrizione o il gruppo di risorse toonew](resource-group-move-resources.md)
### [Esempi di governance](resource-manager-subscription-examples.md)

## Controllare l'accesso
### Creare un'entità servizio
#### [PowerShell](resource-group-authenticate-service-principal.md)
#### [Interfaccia della riga di comando di Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
#### [Interfaccia della riga di comando di Azure 1.0](resource-group-authenticate-service-principal-cli.md)
#### [Portale](resource-group-create-service-principal-portal.md)
### [Sottoscrizioni tooaccess API di autenticazione](resource-manager-api-authentication.md)
### [Bloccare le risorse](resource-group-lock-resources.md)

## Impostare i criteri delle risorse
### [Informazioni sui criteri delle risorse](resource-manager-policy.md)
### [Utilizzare i criteri di tooassign portale](resource-manager-policy-portal.md)
### [Usare gli script tooassign criteri](resource-manager-policy-create-assign.md)
### esempi
#### [Tag](resource-manager-policy-tags.md)
#### [Convenzioni di denominazione](resource-manager-policy-naming-convention.md)
#### [Rete](resource-manager-policy-network.md)
#### [Archiviazione](resource-manager-policy-storage.md)
#### [VM Linux](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)
#### [VM Windows](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)

## Usare le applicazioni gestite
### [Pubblicare un'applicazione del catalogo di servizi](managed-application-publishing.md)
### [Utilizzare un'applicazione del catalogo di servizi](managed-application-consumption.md)
### [Pubblicare un'applicazione del Marketplace](managed-application-author-marketplace.md)
### [Utilizzare un'applicazione del Marketplace](managed-application-consume-marketplace.md)
### [Creare definizioni dell'interfaccia utente](managed-application-createuidefinition-overview.md)

## Audit
### [Visualizzare log di attività](resource-group-audit.md)
### [Visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md)

## Risoluzione dei problemi
### [Errori di distribuzione comuni](resource-manager-common-deployment-errors.md)
### [Informazioni sugli errori di distribuzione](resource-manager-troubleshoot-tips.md)
### [Errore RequestDisallowedByPolicy](resource-manager-policy-requestdisallowedbypolicy-error.md)
### Errori di distribuzione delle macchine virtuali
#### [Linux](../virtual-machines/linux/troubleshoot-deploy-vm.md)
#### [Windows](../virtual-machines/windows/troubleshoot-deploy-vm.md)

# Riferimento
## [Formato del modello](/azure/templates/)
## [Funzioni di modello](resource-group-template-functions.md)
### [Matrici e funzioni oggetto](resource-group-template-functions-array.md)
### [Funzioni di confronto](resource-group-template-functions-comparison.md)
### [Funzioni di distribuzione](resource-group-template-functions-deployment.md)
### [Funzioni logiche](resource-group-template-functions-logical.md)
### [Funzioni numeriche](resource-group-template-functions-numeric.md)
### [Funzioni delle risorse](resource-group-template-functions-resource.md)
### [Funzioni stringa](resource-group-template-functions-string.md)
## [Funzioni di definizione dell'interfaccia utente](managed-application-createuidefinition-functions.md)
## [Elementi di definizione dell'interfaccia utente](managed-application-createuidefinition-elements.md)
### [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
### [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
### [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
### [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
### [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
### [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
### [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
### [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
### [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
### [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
### [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
### [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
### [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)
## [PowerShell](/powershell/module/azurerm.resources)
## [Interfaccia della riga di comando di Azure](/cli/azure/resource)
## [.NET](/dotnet/api/microsoft.azure.management.resourcemanager)
## [Java](/java/api/com.microsoft.azure.management.resources)
## [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagement.html)
## [REST](/rest/api/resources/)

# Risorse
## [Roadmap per Azure](https://azure.microsoft.com/roadmap/?category=monitoring-management)
## [Calcolatore prezzi](https://azure.microsoft.com/pricing/calculator/)
## [Aggiornamenti del servizio](https://azure.microsoft.com/updates/?product=azure-resource-manager)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-resource-manager)
## [Limitazione delle richieste](resource-manager-request-limits.md)
## [Tenere traccia delle operazioni asincrone](resource-manager-async-operations.md)
## [Video](https://azure.microsoft.com/documentation/videos/index/?services=azure-resource-manager)
