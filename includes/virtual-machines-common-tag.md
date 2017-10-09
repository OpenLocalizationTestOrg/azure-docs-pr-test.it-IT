


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="23f91-101">Assegnazione di tag a una macchina virtuale tramite modelli</span><span class="sxs-lookup"><span data-stu-id="23f91-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="23f91-102">In primo luogo, diamo un'occhiata ai tag tramite modelli.</span><span class="sxs-lookup"><span data-stu-id="23f91-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="23f91-103">[Questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) racchiude il tag su hello seguenti risorse: calcolo (macchina virtuale), di archiviazione (Account di archiviazione) e di rete (indirizzo IP pubblico, rete virtuale e l'interfaccia di rete).</span><span class="sxs-lookup"><span data-stu-id="23f91-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="23f91-104">Questo modello riguarda una VM Windows ma può essere adattato per le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="23f91-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="23f91-105">Fare clic su hello **distribuire tooAzure** pulsante hello [collegamento modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="23f91-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="23f91-106">Questo si sposterà toohello [portale di Azure](https://portal.azure.com/) in cui è possibile distribuire questo modello.</span><span class="sxs-lookup"><span data-stu-id="23f91-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Distribuzione semplice di tag](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="23f91-108">Questo modello include hello tag seguenti: *reparto*, *applicazione*, e *creato da*.</span><span class="sxs-lookup"><span data-stu-id="23f91-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="23f91-109">È possibile aggiungere o modificare i tag direttamente nel modello di hello se si desidera che i nomi di tag diverso.</span><span class="sxs-lookup"><span data-stu-id="23f91-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Tag di Azure in un modello](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="23f91-111">Come si può notare, vengono definiti i tag di hello come coppie chiave/valore, separate da due punti (:).</span><span class="sxs-lookup"><span data-stu-id="23f91-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="23f91-112">tag Hello devono essere definiti in questo formato:</span><span class="sxs-lookup"><span data-stu-id="23f91-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="23f91-113">Salvare il file di modello hello dopo aver completato la modifica con tag hello di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="23f91-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="23f91-114">Successivamente, nel hello **modifica parametri** sezione, è possibile compilare i valori hello per i tag.</span><span class="sxs-lookup"><span data-stu-id="23f91-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Modificare i tag nel portale di Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="23f91-116">Fare clic su **crea** toodeploy questo modello con i valori di tag.</span><span class="sxs-lookup"><span data-stu-id="23f91-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="23f91-117">Assegnazione di tag tramite hello portale</span><span class="sxs-lookup"><span data-stu-id="23f91-117">Tagging through hello Portal</span></span>
<span data-ttu-id="23f91-118">Dopo aver creato le risorse con i tag, è possibile visualizzare, aggiungere ed eliminare i tag nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="23f91-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="23f91-119">Seleziona hello tag tooview sull'icona del tag:</span><span class="sxs-lookup"><span data-stu-id="23f91-119">Select hello tags icon tooview your tags:</span></span>

![Icona di tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="23f91-121">Aggiungere un nuovo tag tramite il portale di hello definendo la propria coppia chiave/valore e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="23f91-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Aggiungi nuovo Tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="23f91-123">Il nuovo tag verrà ora visualizzato nell'elenco di hello di tag per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="23f91-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nuovo Tag salvato nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

