## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="577de-101">Panoramica dei modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="577de-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="577de-102">Modelli di gestione risorse di Azure consentono di toodeclaratively specificare infrastruttura IaaS di Azure hello nel linguaggio Json definendo le dipendenze di hello tra risorse.</span><span class="sxs-lookup"><span data-stu-id="577de-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="577de-103">Per una panoramica dettagliata dei modelli di gestione risorse di Azure, consultare l'articolo toohello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="577de-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="577de-104">Panoramica del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="577de-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="577de-105">Frammento di modello di esempio per le estensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="577de-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="577de-106">Distribuzione di estensioni di macchina virtuale come parte di un modello di gestione risorse di Azure richiede toodeclaratively specificare configurazione dell'estensione hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="577de-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="577de-107">Di seguito è formato hello per la specifica di configurazione dell'estensione hello.</span><span class="sxs-lookup"><span data-stu-id="577de-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="577de-108">Come si può vedere dal hello precedente, il modello di estensione hello contiene due parti principali:</span><span class="sxs-lookup"><span data-stu-id="577de-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="577de-109">Nome dell'estensione, editore e versione.</span><span class="sxs-lookup"><span data-stu-id="577de-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="577de-110">Configurazione dell'estensione.</span><span class="sxs-lookup"><span data-stu-id="577de-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="577de-111">Server di pubblicazione hello identificazione, il tipo e typeHandlerVersion per tutte le estensioni</span><span class="sxs-lookup"><span data-stu-id="577de-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="577de-112">Le estensioni VM di Azure vengono pubblicate da Microsoft e attendibili 3 parti e ogni estensione è identificato in modo univoco da typeHandlerVersion relativo server di pubblicazione, tipo e hello.</span><span class="sxs-lookup"><span data-stu-id="577de-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="577de-113">Questi possono essere determinati come segue:</span><span class="sxs-lookup"><span data-stu-id="577de-113">These can be determined as following:</span></span>  

