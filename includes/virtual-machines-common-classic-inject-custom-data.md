


<span data-ttu-id="2bf01-101">In questo argomento viene spiegato come:</span><span class="sxs-lookup"><span data-stu-id="2bf01-101">This topic describes how to:</span></span>

* <span data-ttu-id="2bf01-102">Inserire dati in una macchina virtuale (VM) di Azure durante il provisioning.</span><span class="sxs-lookup"><span data-stu-id="2bf01-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="2bf01-103">Recuperare i dati sia in Windows che in Linux.</span><span class="sxs-lookup"><span data-stu-id="2bf01-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="2bf01-104">Utilizzare strumenti speciali su alcuni sistemi toodetect e gestisce automaticamente i dati personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2bf01-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf01-105">Questo articolo descrive i dati come personalizzati possono essere inserite utilizzando una macchina virtuale creata con hello API di gestione del servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf01-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="2bf01-106">toosee toouse hello API di gestione risorse di Azure, vedere [il modello di esempio hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="2bf01-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="2bf01-107">Inserimento di dati personalizzati nella macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="2bf01-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="2bf01-108">Questa funzionalità è attualmente supportata solo in hello [interfaccia della riga di comando di Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="2bf01-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="2bf01-109">Verrà creato un `custom-data.txt` file che contiene i dati, quindi inserire che in toohello VM durante il provisioning.</span><span class="sxs-lookup"><span data-stu-id="2bf01-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="2bf01-110">Anche se è possibile utilizzare una delle opzioni di hello per hello `azure vm create` comando seguente hello viene illustrato un approccio molto semplice:</span><span class="sxs-lookup"><span data-stu-id="2bf01-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="2bf01-111">Utilizza dati personalizzata nella macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="2bf01-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="2bf01-112">Se la macchina virtuale di Azure è una macchina virtuale basata su Windows, quindi hello dati personalizzato viene salvato troppo`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="2bf01-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="2bf01-113">Sebbene sia con codifica base64 tootransfer da hello computer locale toohello nuova macchina virtuale, viene automaticamente decodificati e può essere aperta o utilizzati immediatamente.</span><span class="sxs-lookup"><span data-stu-id="2bf01-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2bf01-114">Se il file hello esiste, viene sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="2bf01-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="2bf01-115">protezione Hello hello directory è stata impostata troppo**System: Full Control** e **Administrators: Full Control**.</span><span class="sxs-lookup"><span data-stu-id="2bf01-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="2bf01-116">Se la macchina virtuale di Azure è una macchina virtuale basata su Linux, il file di dati personalizzati hello si troverà uno dei seguenti hello inserisce a seconda del tipo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2bf01-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="2bf01-117">dati Hello potrebbero essere con codifica base64, potrebbe essere necessario innanzitutto dati hello toodecode:</span><span class="sxs-lookup"><span data-stu-id="2bf01-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="2bf01-118">Inizializzazione cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="2bf01-118">Cloud-init on Azure</span></span>
<span data-ttu-id="2bf01-119">Se la macchina virtuale di Azure da un'immagine Ubuntu o CoreOS, è possibile utilizzare CustomData toosend una configurazione cloud toocloud-init.</span><span class="sxs-lookup"><span data-stu-id="2bf01-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="2bf01-120">Se il file di dati personalizzato è uno script, cloud-init può semplicemente eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="2bf01-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="2bf01-121">Immagini di Ubuntu Cloud</span><span class="sxs-lookup"><span data-stu-id="2bf01-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="2bf01-122">Nella maggior parte delle immagini Linux di Azure, è necessario modificare "/ etc/waagent.conf" tooconfigure hello temporaneo su disco e lo scambio file di risorse.</span><span class="sxs-lookup"><span data-stu-id="2bf01-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="2bf01-123">Per altre informazioni, vedere [Guida dell'utente dell'agente Linux di Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2bf01-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="2bf01-124">Le immagini di Cloud Ubuntu hello, tuttavia, è necessario utilizzare cloud init tooconfigure hello risorsa disco (vale a dire hello "temporaneo") e spazio di swapping partizione.</span><span class="sxs-lookup"><span data-stu-id="2bf01-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="2bf01-125">Vedere hello seguente pagina nel sito wiki Ubuntu hello per altri dettagli: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="2bf01-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="2bf01-126">Passaggi successivi: Utilizzo cloud-init</span><span class="sxs-lookup"><span data-stu-id="2bf01-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="2bf01-127">Per ulteriori informazioni, vedere hello [cloud init documentazione per Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="2bf01-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="2bf01-128">Aggiungere il riferimento all'API REST di gestione del servizio ruolo</span><span class="sxs-lookup"><span data-stu-id="2bf01-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="2bf01-129">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2bf01-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

