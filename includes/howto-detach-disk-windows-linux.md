<span data-ttu-id="8283d-101">Quando non è più necessario un disco dati è una macchina virtuale tooa collegato, è possibile scollegarlo facilmente.</span><span class="sxs-lookup"><span data-stu-id="8283d-101">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="8283d-102">Scollegare un disco rimuove il disco hello dalla macchina virtuale hello, ma non Elimina disco hello dall'account di archiviazione Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8283d-102">Detaching a disk removes hello disk from hello virtual machine, but doesn't delete hello disk from hello Azure storage account.</span></span>

<span data-ttu-id="8283d-103">Se si desiderano nuovamente toouse hello esistente dati hello disco, è possibile ricollegarlo toohello stessa macchina virtuale o un altro.</span><span class="sxs-lookup"><span data-stu-id="8283d-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="8283d-104">toodetach un disco del sistema operativo, è necessario prima macchina virtuale di toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="8283d-104">toodetach an operating system disk, you first need toodelete hello virtual machine.</span></span>
>

## <a name="find-hello-disk"></a><span data-ttu-id="8283d-105">Trovare il disco hello</span><span class="sxs-lookup"><span data-stu-id="8283d-105">Find hello disk</span></span>
<span data-ttu-id="8283d-106">Se non si conosce il nome di hello di hello disco oppure da tooverify, prima rimuoverlo, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="8283d-106">If you don't know hello name of hello disk or want tooverify it before you detach it, follow these steps.</span></span>

1. <span data-ttu-id="8283d-107">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8283d-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="8283d-108">Fare clic su **macchine virtuali**, e quindi selezionare hello VM appropriato.</span><span class="sxs-lookup"><span data-stu-id="8283d-108">Click **Virtual Machines**, and then select hello appropriate VM.</span></span>

3. <span data-ttu-id="8283d-109">Fare clic su **dischi** lungo hello bordo sinistro del dashboard di hello macchina virtuale, in **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="8283d-109">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

 <span data-ttu-id="8283d-110">dashboard macchina virtuale Hello Elenca hello nome e tipo di tutti i dischi collegati.</span><span class="sxs-lookup"><span data-stu-id="8283d-110">hello virtual machine dashboard lists hello name and type of all attached disks.</span></span> <span data-ttu-id="8283d-111">Ad esempio, in questa schermata è visualizzata una macchina virtuale con un solo disco del sistema operativo e un unico disco dati:</span><span class="sxs-lookup"><span data-stu-id="8283d-111">For example, this screen shows a virtual machine with one operating system (OS) disk and one data disk:</span></span>

    ![Ricerca di un disco dati](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a><span data-ttu-id="8283d-113">Scollegare il disco hello</span><span class="sxs-lookup"><span data-stu-id="8283d-113">Detach hello disk</span></span>
1. <span data-ttu-id="8283d-114">Dal portale di Azure hello, fare clic su **macchine virtuali**, quindi fare clic su nome hello della macchina virtuale hello che ha un disco dati hello desiderato toodetach.</span><span class="sxs-lookup"><span data-stu-id="8283d-114">From hello Azure portal, click **Virtual Machines**, and then click hello name of hello virtual machine that has hello data disk you want toodetach.</span></span>

2. <span data-ttu-id="8283d-115">Fare clic su **dischi** lungo hello bordo sinistro del dashboard di hello macchina virtuale, in **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="8283d-115">Click **Disks** along hello left edge of hello virtual machine dashboard, under **Settings**.</span></span>

3. <span data-ttu-id="8283d-116">Fare clic hello disco toodetach.</span><span class="sxs-lookup"><span data-stu-id="8283d-116">Click hello disk you want toodetach.</span></span>

  ![Identificare hello disco toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. <span data-ttu-id="8283d-118">Dalla barra dei comandi di hello, fare clic su **scollegamento**.</span><span class="sxs-lookup"><span data-stu-id="8283d-118">From hello command bar, click **Detach**.</span></span>

  ![Individuare hello detach-comando](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. <span data-ttu-id="8283d-120">Nella finestra di conferma hello, fare clic su **Sì** disco hello toodetach.</span><span class="sxs-lookup"><span data-stu-id="8283d-120">In hello confirmation window, click **Yes** toodetach hello disk.</span></span>

  ![Confermare di scollegamento del disco hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

<span data-ttu-id="8283d-122">Hello disco rimane nel servizio di archiviazione, ma non è più macchine virtuali tooa associata.</span><span class="sxs-lookup"><span data-stu-id="8283d-122">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>
