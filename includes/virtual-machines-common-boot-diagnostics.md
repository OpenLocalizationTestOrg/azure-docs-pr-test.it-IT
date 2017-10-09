<span data-ttu-id="ab9f1-101">In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="ab9f1-102">Quando si attiva la propria immagine tooAzure o anche l'avvio delle immagini della piattaforma hello, possono esistere molti motivi per cui una macchina virtuale ottiene in uno stato non avviabile.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="ab9f1-103">Questi consentono di funzionalità si tooeasily diagnosticare e ripristinare le macchine virtuali da errori di avvio.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="ab9f1-104">Per macchine virtuali Linux, è possibile visualizzare facilmente output di hello del log dal portale hello console:</span><span class="sxs-lookup"><span data-stu-id="ab9f1-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portale di Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="ab9f1-106">Tuttavia, per Windows e macchine virtuali Linux, Azure consente inoltre di toosee una schermata di hello VM dall'hypervisor hello:</span><span class="sxs-lookup"><span data-stu-id="ab9f1-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Errore](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="ab9f1-108">Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="ab9f1-109">Si noti, schermate e l'output può richiedere fino a too10 minuti tooappear nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="ab9f1-110">Errori di avvio comuni</span><span class="sxs-lookup"><span data-stu-id="ab9f1-110">Common boot errors</span></span>

- [<span data-ttu-id="ab9f1-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="ab9f1-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="ab9f1-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="ab9f1-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="ab9f1-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="ab9f1-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="ab9f1-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="ab9f1-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="ab9f1-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="ab9f1-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="ab9f1-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="ab9f1-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="ab9f1-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="ab9f1-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="ab9f1-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="ab9f1-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="ab9f1-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="ab9f1-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="ab9f1-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="ab9f1-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="ab9f1-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="ab9f1-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="ab9f1-122">Sistema operativo non trovato</span><span class="sxs-lookup"><span data-stu-id="ab9f1-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="ab9f1-123">Errore di avvio o INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="ab9f1-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="ab9f1-124">Abilitare la diagnostica in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ab9f1-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="ab9f1-125">Quando si crea una nuova macchina virtuale dal portale di anteprima di hello, selezionare hello **Azure Resource Manager** dall'elenco a discesa modello di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="ab9f1-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gestione risorse](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="ab9f1-127">Configurare monitoraggio opzione tooselect hello account di archiviazione in cui si desidera tooplace hello questi file di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Creare una macchina virtuale](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="ab9f1-129">Se si distribuisce un modello di gestione risorse di Azure, passare la risorsa di macchina virtuale tooyour e aggiungere una sezione del profilo di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="ab9f1-130">Ricordare di intestazione della versione API toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="ab9f1-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="ab9f1-131">profilo di diagnostica Hello consente tooselect hello account di archiviazione in cui tooput questi registri.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="ab9f1-132">toodeploy un macchina virtuale di esempio con la diagnostica di avvio abilitata, qui il repository di estrazione.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="ab9f1-133">Aggiornare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="ab9f1-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="ab9f1-134">diagnostica di avvio tooenable tramite hello portale, è possibile aggiornare una macchina virtuale esistente tramite hello portale.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="ab9f1-135">La diagnostica di avvio hello seleziona l'opzione e salvare.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="ab9f1-136">Riavviare l'effetto di tootake hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab9f1-136">Restart hello VM tootake effect.</span></span>

![Aggiornare una VM esistente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

