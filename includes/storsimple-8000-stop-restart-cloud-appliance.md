#### <a name="to-stop-and-start-a-cloud-appliance"></a><span data-ttu-id="6fc28-101">Per arrestare e avviare un'appliance cloud</span><span class="sxs-lookup"><span data-stu-id="6fc28-101">To stop and start a cloud appliance</span></span>

1. <span data-ttu-id="6fc28-102">Per arrestare un'appliance cloud, passare alla relativa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6fc28-102">To stop a cloud appliance, go to the VM for your cloud appliance.</span></span>
    <span data-ttu-id="6fc28-103">![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="6fc28-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="6fc28-104">Nella barra dei comandi fare clic su **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-104">From the command bar, click **Stop**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="6fc28-106">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="6fc28-108">Con l'arresto, la macchina virtuale viene deallocata.</span><span class="sxs-lookup"><span data-stu-id="6fc28-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="6fc28-109">Durante l'arresto dell'appliance cloud, il suo stato è **Deallocazione**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-109">While the cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="6fc28-110">Dopo l'arresto dell'appliance cloud, il suo stato è **Arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-110">After the cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="6fc28-112">Dopo l'arresto della macchina virtuale, fare clic su **Avvia** (il pulsante diventa disponibile) per avviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6fc28-112">Once a VM is stopped, click **Start** (button becomes available) to start the VM.</span></span> <span data-ttu-id="6fc28-113">Dopo l'avvio dell'appliance cloud, il suo stato è **Avviato**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-113">After the cloud appliance has started up, its status is **Started**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="6fc28-115">Usare i cmdlet seguenti per arrestare e avviare un'appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="6fc28-115">Use the following cmdlets to stop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="to-restart-a-cloud-appliance"></a><span data-ttu-id="6fc28-116">Per riavviare un'appliance cloud</span><span class="sxs-lookup"><span data-stu-id="6fc28-116">To restart a cloud appliance</span></span>

<span data-ttu-id="6fc28-117">Per riavviare un'appliance cloud, passare alla relativa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6fc28-117">To restart a cloud appliance, go to the VM for your cloud appliance.</span></span> <span data-ttu-id="6fc28-118">Nella barra dei comandi fare clic su **Riavvia**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-118">From the command bar, click **Restart**.</span></span> <span data-ttu-id="6fc28-119">Quando richiesto, confermare il riavvio.</span><span class="sxs-lookup"><span data-stu-id="6fc28-119">When prompted, confirm the restart.</span></span> <span data-ttu-id="6fc28-120">Quando l'appliance cloud è pronta per l'uso, lo stato viene indicato come **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="6fc28-120">When the cloud appliance is ready for you to use, its status is **Running**.</span></span>

![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="6fc28-122">Usare il cmdlet seguente per riavviare un'appliance cloud.</span><span class="sxs-lookup"><span data-stu-id="6fc28-122">Use the following cmdlet to restart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

