## <a name="overview"></a><span data-ttu-id="91499-101">Panoramica</span><span class="sxs-lookup"><span data-stu-id="91499-101">Overview</span></span>
<span data-ttu-id="91499-102">Quando si crea una nuova macchina virtuale (VM) in un gruppo di risorse tramite la distribuzione di un'immagine da [Azure Marketplace](https://azure.microsoft.com/marketplace/), unità di sistema operativo predefinita hello è di 127 GB.</span><span class="sxs-lookup"><span data-stu-id="91499-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="91499-103">Anche se è possibile tooadd dati dischi toohello VM (seconda quanti hello SKU scelta) e inoltre è consigliato tooinstall applicazioni e carichi di lavoro con utilizzo intensivo della CPU su tali dischi supplemento, spesso i clienti devono tooexpand hello del sistema operativo unità toosupport determinati scenari, ad esempio i seguenti:</span><span class="sxs-lookup"><span data-stu-id="91499-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="91499-104">Supporto di applicazioni legacy che installano componenti nell'unità del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="91499-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="91499-105">Migrazione di un computer fisico o di una macchina virtuale locali a un'unità del sistema operativo più grande.</span><span class="sxs-lookup"><span data-stu-id="91499-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91499-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: Gestione risorse e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="91499-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="91499-107">In questo articolo viene illustrato l'utilizzo del modello di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="91499-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="91499-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="91499-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="91499-109">Ridimensionare l'unità del sistema operativo hello</span><span class="sxs-lookup"><span data-stu-id="91499-109">Resize hello OS drive</span></span>
<span data-ttu-id="91499-110">In questo articolo si sarà attività hello di ridimensionamento di un'unità hello del sistema operativo tramite i moduli di gestione delle risorse [Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="91499-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="91499-111">Aprire Powershell ISE della finestra di Powershell in modalità amministrativa e seguire i passaggi di hello riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="91499-112">Accedi tooyour Microsoft Azure in modalità di gestione delle risorse dell'account e selezionare la sottoscrizione, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="91499-113">Impostare il nome del gruppo di risorse e il nome della VM come segue:</span><span class="sxs-lookup"><span data-stu-id="91499-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="91499-114">Ottenere un tooyour riferimento VM come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="91499-115">Arrestare VM hello prima del ridimensionamento del disco hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="91499-116">Di seguito e il momento di hello di che è stato in attesa!</span><span class="sxs-lookup"><span data-stu-id="91499-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="91499-117">Impostare dimensioni hello del valore di hello del sistema operativo del disco toohello desiderato e aggiornare hello VM come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="91499-118">nuova dimensione Hello deve essere maggiore di dimensioni del disco esistente hello.</span><span class="sxs-lookup"><span data-stu-id="91499-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="91499-119">Hello massimo consentito è 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="91499-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="91499-120">Aggiornamento hello VM potrebbe richiedere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="91499-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="91499-121">Una volta terminato il comando hello in esecuzione, riavviare hello VM come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="91499-122">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="91499-122">And that’s it!</span></span> <span data-ttu-id="91499-123">Ora RDP in hello macchina virtuale, aprire Gestione Computer (o Gestione disco) ed espandere l'unità di hello tramite hello appena allocato.</span><span class="sxs-lookup"><span data-stu-id="91499-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="91499-124">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="91499-124">Summary</span></span>
<span data-ttu-id="91499-125">In questo articolo, abbiamo utilizzato Gestione risorse di Azure i moduli di Powershell tooexpand hello unità del sistema operativo di una macchina virtuale IaaS.</span><span class="sxs-lookup"><span data-stu-id="91499-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="91499-126">Riprodotta sotto è script completo di hello riferimento:</span><span class="sxs-lookup"><span data-stu-id="91499-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="91499-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91499-127">Next Steps</span></span>
<span data-ttu-id="91499-128">Sebbene sia in questo articolo è incentrato principalmente sull'espansione disco hello del sistema operativo della macchina virtuale hello, hello sviluppato script può anche essere usato per l'espansione di hello dati dischi collegati toohello macchina virtuale tramite la modifica di una singola riga di codice.</span><span class="sxs-lookup"><span data-stu-id="91499-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="91499-129">Ad esempio, dati prima di hello tooexpand disco collegato toohello VM, sostituire hello ```OSDisk``` oggetto ```StorageProfile``` con ```DataDisks``` matrice e come utilizzare un tooobtain indice numerico, un disco dati collegato toofirst di riferimento, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="91499-130">Analogamente è possibile fare riferimento a altri dati dischi collegati toohello macchina virtuale, è necessario utilizzare un indice, come illustrato in precedenza o hello ```Name``` hello disco come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="91499-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="91499-131">Se si desidera toofind out come tooattach dischi tooan VM di Azure Resource Manager, selezionare questa opzione [articolo](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91499-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

