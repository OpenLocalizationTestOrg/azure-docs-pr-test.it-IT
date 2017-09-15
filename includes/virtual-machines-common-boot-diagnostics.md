<span data-ttu-id="fbb9d-101">In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="fbb9d-102">Quando si usa l'immagine personale in Azure o anche quando si avvia una delle immagini della piattaforma, una macchina virtuale può passare a uno stato non avviabile per diversi motivi.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="fbb9d-103">Queste funzionalità consentono di diagnosticare facilmente gli errori di avvio e di ripristinare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="fbb9d-104">Per le macchine virtuali Linux, è possibile visualizzare facilmente l'output del log della console dal portale:</span><span class="sxs-lookup"><span data-stu-id="fbb9d-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Portale di Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="fbb9d-106">Per le macchine virtuali sia Windows che Linux, Azure consente anche di visualizzare uno screenshot della VM dall'hypervisor:</span><span class="sxs-lookup"><span data-stu-id="fbb9d-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Errore](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="fbb9d-108">Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="fbb9d-109">Si noti che la visualizzazione degli screenshot e dell'output nell'account di archiviazione può richiedere fino a 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="fbb9d-110">Errori di avvio comuni</span><span class="sxs-lookup"><span data-stu-id="fbb9d-110">Common boot errors</span></span>

- [<span data-ttu-id="fbb9d-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="fbb9d-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="fbb9d-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="fbb9d-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="fbb9d-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="fbb9d-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="fbb9d-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="fbb9d-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="fbb9d-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="fbb9d-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="fbb9d-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="fbb9d-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="fbb9d-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="fbb9d-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="fbb9d-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="fbb9d-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="fbb9d-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="fbb9d-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="fbb9d-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="fbb9d-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="fbb9d-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="fbb9d-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="fbb9d-122">Sistema operativo non trovato</span><span class="sxs-lookup"><span data-stu-id="fbb9d-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="fbb9d-123">Errore di avvio o INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="fbb9d-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="fbb9d-124">Abilitare la diagnostica in una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fbb9d-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="fbb9d-125">Quando si crea una nuova macchina virtuale dal portale di anteprima, selezionare **Azure Resource Manager** dall'elenco a discesa del modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="fbb9d-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Gestione risorse](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="fbb9d-127">Configurare l'opzione Monitoraggio per selezionare l'account di archiviazione in cui si vogliono inserire questi file di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Creare una macchina virtuale](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="fbb9d-129">Se si esegue la distribuzione da un modello di Azure Resource Manager, passare alla risorsa macchina virtuale e aggiungere la sezione del profilo di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="fbb9d-130">Si ricordi di usare l'intestazione di versione API "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="fbb9d-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="fbb9d-131">Il profilo di diagnostica consente di selezionare l'account di archiviazione in cui si vogliono inserire questi log.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

<span data-ttu-id="fbb9d-132">Per distribuire una macchina virtuale di esempio con la diagnostica di avvio abilitata, vedere il repository qui.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="fbb9d-133">Aggiornare una macchina virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="fbb9d-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="fbb9d-134">Per abilitare la diagnostica dal portale, è anche possibile aggiornare una macchina virtuale esistente dal portale.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="fbb9d-135">Selezionare l'opzione Diagnostica di avvio e fare clic su Salva.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="fbb9d-136">Riavviare la VM per rendere effettivo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="fbb9d-136">Restart the VM to take effect.</span></span>

![Aggiornare una VM esistente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

