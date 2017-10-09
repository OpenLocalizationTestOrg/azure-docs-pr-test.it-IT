#### <a name="toostop-and-start-a-cloud-appliance"></a><span data-ttu-id="7454f-101">toostop e avviare un'applicazione cloud</span><span class="sxs-lookup"><span data-stu-id="7454f-101">toostop and start a cloud appliance</span></span>

1. <span data-ttu-id="7454f-102">toostop un'applicazione cloud, andare toohello macchina virtuale per l'applicazione cloud.</span><span class="sxs-lookup"><span data-stu-id="7454f-102">toostop a cloud appliance, go toohello VM for your cloud appliance.</span></span>
    <span data-ttu-id="7454f-103">![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span><span class="sxs-lookup"><span data-stu-id="7454f-103">![StorSimple Cloud Appliance Virtual Machine](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)</span></span>

2. <span data-ttu-id="7454f-104">Dalla barra dei comandi di hello, fare clic su **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="7454f-104">From hello command bar, click **Stop**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. <span data-ttu-id="7454f-106">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="7454f-106">When prompted for confirmation, click **Yes**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. <span data-ttu-id="7454f-108">Con l'arresto, la macchina virtuale viene deallocata.</span><span class="sxs-lookup"><span data-stu-id="7454f-108">When you stop a VM, it gets deallocated.</span></span> <span data-ttu-id="7454f-109">Durante l'arresto di appliance di cloud hello, lo stato è **Deallocating**.</span><span class="sxs-lookup"><span data-stu-id="7454f-109">While hello cloud appliance is stopping, its status is **Deallocating**.</span></span> <span data-ttu-id="7454f-110">Dopo l'arresto appliance di cloud hello, lo stato è **arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="7454f-110">After hello cloud appliance is stopped, its status is **Stopped (deallocated)**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. <span data-ttu-id="7454f-112">Una volta che una macchina virtuale viene arrestata, fare clic su **avviare** (pulsante diventa disponibile) hello toostart macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7454f-112">Once a VM is stopped, click **Start** (button becomes available) toostart hello VM.</span></span> <span data-ttu-id="7454f-113">Dopo che il dispositivo di cloud hello è stata avviata, il suo stato sia **Started**.</span><span class="sxs-lookup"><span data-stu-id="7454f-113">After hello cloud appliance has started up, its status is **Started**.</span></span>

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

<span data-ttu-id="7454f-115">Utilizzare hello toostop i cmdlet seguenti e avviare un'applicazione cloud.</span><span class="sxs-lookup"><span data-stu-id="7454f-115">Use hello following cmdlets toostop and start a cloud appliance.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a><span data-ttu-id="7454f-116">toorestart un'applicazione cloud</span><span class="sxs-lookup"><span data-stu-id="7454f-116">toorestart a cloud appliance</span></span>

<span data-ttu-id="7454f-117">toorestart un'applicazione cloud, andare toohello macchina virtuale per l'applicazione cloud.</span><span class="sxs-lookup"><span data-stu-id="7454f-117">toorestart a cloud appliance, go toohello VM for your cloud appliance.</span></span> <span data-ttu-id="7454f-118">Dalla barra dei comandi di hello, fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="7454f-118">From hello command bar, click **Restart**.</span></span> <span data-ttu-id="7454f-119">Quando richiesto, confermare il riavvio di hello.</span><span class="sxs-lookup"><span data-stu-id="7454f-119">When prompted, confirm hello restart.</span></span> <span data-ttu-id="7454f-120">Quando il dispositivo di cloud hello è pronto per si toouse, lo stato è **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="7454f-120">When hello cloud appliance is ready for you toouse, its status is **Running**.</span></span>

![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

<span data-ttu-id="7454f-122">Utilizzare hello seguente cmdlet toorestart un'applicazione cloud.</span><span class="sxs-lookup"><span data-stu-id="7454f-122">Use hello following cmdlet toorestart a cloud appliance.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

