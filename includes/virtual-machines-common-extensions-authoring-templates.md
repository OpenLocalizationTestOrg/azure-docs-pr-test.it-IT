## <a name="overview-of-azure-resource-manager-templates"></a>Panoramica dei modelli di Gestione risorse di Azure
Modelli di gestione risorse di Azure consentono di toodeclaratively specificare infrastruttura IaaS di Azure hello nel linguaggio Json definendo le dipendenze di hello tra risorse. Per una panoramica dettagliata dei modelli di gestione risorse di Azure, consultare l'articolo toohello riportato di seguito:

[Panoramica del gruppo di risorse](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Frammento di modello di esempio per le estensioni della macchina virtuale.
Distribuzione di estensioni di macchina virtuale come parte di un modello di gestione risorse di Azure richiede toodeclaratively specificare configurazione dell'estensione hello nel modello di hello.
Di seguito è formato hello per la specifica di configurazione dell'estensione hello.

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

Come si può vedere dal hello precedente, il modello di estensione hello contiene due parti principali:

1. Nome dell'estensione, editore e versione.
2. Configurazione dell'estensione.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Server di pubblicazione hello identificazione, il tipo e typeHandlerVersion per tutte le estensioni
Le estensioni VM di Azure vengono pubblicate da Microsoft e attendibili 3 parti e ogni estensione è identificato in modo univoco da typeHandlerVersion relativo server di pubblicazione, tipo e hello. Questi possono essere determinati come segue:  

