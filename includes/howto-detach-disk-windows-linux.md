<span data-ttu-id="0c289-101">Quando un disco dati collegato a una macchina virtuale non è più necessario, è possibile scollegarlo con facilità.</span><span class="sxs-lookup"><span data-stu-id="0c289-101">When you no longer need a data disk that's attached to a virtual machine, you can easily detach it.</span></span> <span data-ttu-id="0c289-102">Quando si scollega un disco, viene rimosso il disco dalla macchina virtuale, ma non viene eliminato dall'account di Archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="0c289-102">Detaching a disk removes the disk from the virtual machine, but doesn't delete the disk from the Azure storage account.</span></span>

<span data-ttu-id="0c289-103">Se si vogliono riusare i dati presenti nel disco, è possibile ricollegarlo alla stessa macchina virtuale o collegarlo a una nuova.</span><span class="sxs-lookup"><span data-stu-id="0c289-103">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="0c289-104">Per scollegare un disco del sistema operativo è prima necessario eliminare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c289-104">To detach an operating system disk, you first need to delete the virtual machine.</span></span>
>

## <a name="find-the-disk"></a><span data-ttu-id="0c289-105">Trovare il disco</span><span class="sxs-lookup"><span data-stu-id="0c289-105">Find the disk</span></span>
<span data-ttu-id="0c289-106">Se non si conosce il nome del disco o si vuole verificarlo prima di averlo scollegato, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="0c289-106">If you don't know the name of the disk or want to verify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="0c289-107">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c289-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0c289-108">Fare clic su **Macchine virtuali**, quindi selezionare la VM appropriata.</span><span class="sxs-lookup"><span data-stu-id="0c289-108">Click **Virtual Machines**, and then select the appropriate VM.</span></span>

3. <span data-ttu-id="0c289-109">Fare clic su **Dischi** sul bordo sinistro del dashboard della macchina dashboard, in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c289-109">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="0c289-110">Il dashboard della macchina virtuale elenca il nome e il tipo di tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="0c289-110">The virtual machine dashboard lists the name and type of all attached disks.</span></span> <span data-ttu-id="0c289-111">Ad esempio, in questa schermata è visualizzata una macchina virtuale con un solo disco del sistema operativo e un unico disco dati:</span><span class="sxs-lookup"><span data-stu-id="0c289-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Ricerca di un disco dati](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-the-disk"></a><span data-ttu-id="0c289-113">Rimuovere il disco</span><span class="sxs-lookup"><span data-stu-id="0c289-113">Detach the disk</span></span>
1. <span data-ttu-id="0c289-114">Nel Portale di Azure fare clic su **Macchine virtuali**, quindi sul nome della macchina virtuale con il disco dati che si vuole scollegare.</span><span class="sxs-lookup"><span data-stu-id="0c289-114">From the Azure portal, click **Virtual Machines**, and then click the name of the virtual machine that has the data disk you want to detach.</span></span>

2. <span data-ttu-id="0c289-115">Fare clic su **Dischi** sul bordo sinistro del dashboard della macchina dashboard, in **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="0c289-115">Click **Disks** along the left edge of the virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="0c289-116">Fare clic sul disco che si desidera scollegare.</span><span class="sxs-lookup"><span data-stu-id="0c289-116">Click the disk you want to detach.</span></span>

  ![Identificare il disco da scollegare](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="0c289-118">Sulla barra dei comandi fare clic su **Disconnetti**.</span><span class="sxs-lookup"><span data-stu-id="0c289-118">From the command bar, click **Detach**.</span></span>

  ![Individuare il comando di disconnessione](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="0c289-120">Nella finestra di conferma, fare clic su **Sì** per scollegare il disco.</span><span class="sxs-lookup"><span data-stu-id="0c289-120">In the confirmation window, click **Yes** to detach the disk.</span></span>

  ![Confermare la disconnessione del disco](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="0c289-122">Il disco rimane nello spazio di archiviazione ma non è più collegato a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c289-122">The disk remains in storage but is no longer attached to a virtual machine.</span></span>
