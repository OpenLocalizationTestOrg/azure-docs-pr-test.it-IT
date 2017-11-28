## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="52852-101">Panoramica dei modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="52852-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="52852-102">I modelli di Azure Resource Manager consentono di specificare in modo dichiarativo l'infrastruttura IaaS di Azure in linguaggio JSON, definendo le dipendenze tra risorse.</span><span class="sxs-lookup"><span data-stu-id="52852-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="52852-103">Per una panoramica dettagliata dei modelli di Azure Resource Manager, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="52852-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="52852-104">Panoramica del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="52852-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="52852-105">Frammento di modello di esempio per le estensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="52852-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="52852-106">Per la distribuzione di estensioni della macchina virtuale come parte del modello di Azure Resource Manager è necessario specificare in modo dichiarativo la configurazione dell'estensione nel modello.</span><span class="sxs-lookup"><span data-stu-id="52852-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="52852-107">Di seguito è riportato il formato per specificare la configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="52852-107">Here is the format for specifying the extension configuration.</span></span>

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

<span data-ttu-id="52852-108">Come si può notare da quanto sopra, il modello dell'estensione contiene due parti principali:</span><span class="sxs-lookup"><span data-stu-id="52852-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="52852-109">Nome dell'estensione, editore e versione.</span><span class="sxs-lookup"><span data-stu-id="52852-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="52852-110">Configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="52852-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="52852-111">Identificazione dell'editore, del tipo e del valore typeHandlerVersion per le estensioni.</span><span class="sxs-lookup"><span data-stu-id="52852-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="52852-112">Le estensioni della macchina virtuale di Azure vengono pubblicate da Microsoft ed editori di terze parti attendibili e ogni estensione è identificata in modo univoco dall'editore, dal tipo e dal valore typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="52852-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="52852-113">Questi possono essere determinati come segue:</span><span class="sxs-lookup"><span data-stu-id="52852-113">These can be determined as following:</span></span>  

