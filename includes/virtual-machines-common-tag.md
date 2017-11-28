


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="d5751-101">Assegnazione di tag a una macchina virtuale tramite modelli</span><span class="sxs-lookup"><span data-stu-id="d5751-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="d5751-102">In primo luogo, diamo un'occhiata ai tag tramite modelli.</span><span class="sxs-lookup"><span data-stu-id="d5751-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="d5751-103">[Questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) inserisce i tag per le risorse seguenti: calcolo (macchina virtuale), archiviazione (Account di archiviazione) e rete (indirizzo IP pubblico, rete virtuale e interfaccia di rete).</span><span class="sxs-lookup"><span data-stu-id="d5751-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="d5751-104">Questo modello riguarda una VM Windows ma può essere adattato per le VM Linux.</span><span class="sxs-lookup"><span data-stu-id="d5751-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="d5751-105">Fare clic sul pulsante **Distribuisci in Azure** dal [collegamento modello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="d5751-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="d5751-106">Verrà visualizzato il [portale di Azure](https://portal.azure.com/) in cui è possibile distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="d5751-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Distribuzione semplice di tag](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="d5751-108">Questo modello include i tag seguenti: *Reparto*, *Applicazione* e *Creato da*.</span><span class="sxs-lookup"><span data-stu-id="d5751-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="d5751-109">È possibile aggiungere o modificare questi tag direttamente nel modello se si desiderano diversi nomi di tag.</span><span class="sxs-lookup"><span data-stu-id="d5751-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Tag di Azure in un modello](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="d5751-111">Come si può vedere, i tag vengono definiti come coppie chiave/valore, separate da due punti (:).</span><span class="sxs-lookup"><span data-stu-id="d5751-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="d5751-112">I tag devono essere definiti in questo formato:</span><span class="sxs-lookup"><span data-stu-id="d5751-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="d5751-113">Salvare il file di modello al termine della modifica, con i tag di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="d5751-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="d5751-114">Successivamente, nella sezione **Modifica parametri** , è possibile compilare i valori per i tag.</span><span class="sxs-lookup"><span data-stu-id="d5751-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Modificare i tag nel portale di Azure](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="d5751-116">Fare clic su **Crea** per distribuire il modello con i valori dei tag.</span><span class="sxs-lookup"><span data-stu-id="d5751-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="d5751-117">Assegnazione di tag tramite il portale</span><span class="sxs-lookup"><span data-stu-id="d5751-117">Tagging through the Portal</span></span>
<span data-ttu-id="d5751-118">Dopo aver creato le risorse con i tag, è possibile visualizzare, aggiungere ed eliminare i tag nel portale.</span><span class="sxs-lookup"><span data-stu-id="d5751-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="d5751-119">Selezionare l'icona di tag per visualizzare i tag:</span><span class="sxs-lookup"><span data-stu-id="d5751-119">Select the tags icon to view your tags:</span></span>

![Icona di tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="d5751-121">Aggiungere un nuovo tag tramite il portale definendo la propria coppia chiave/valore e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="d5751-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Aggiungi nuovo Tag nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="d5751-123">Il nuovo tag verrà visualizzato nell'elenco dei tag per la risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5751-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Nuovo Tag salvato nel portale di Azure](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

