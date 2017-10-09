#### <a name="toostop-and-start-a-virtual-device"></a><span data-ttu-id="e8e6e-101">toostop e avviare un dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="e8e6e-101">toostop and start a virtual device</span></span>
<span data-ttu-id="e8e6e-102">toostop un dispositivo virtuale, fare clic sul nome e quindi fare clic su **arresto**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-102">toostop a virtual device, click its name, and then click **Shutdown**.</span></span> <span data-ttu-id="e8e6e-103">Mentre il dispositivo virtuale hello è in corso l'arresto, lo stato è **arresto**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-103">While hello virtual device is shutting down, its status is **Stopping**.</span></span> <span data-ttu-id="e8e6e-104">Dopo che la periferica virtuale hello viene interrotta, il suo stato sia **arrestato**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-104">After hello virtual device is stopped, its status is **Stopped**.</span></span>

<span data-ttu-id="e8e6e-105">Utilizzare hello toostop i cmdlet seguenti e avviare un dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-105">Use hello following cmdlets toostop and start a virtual device.</span></span>

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a><span data-ttu-id="e8e6e-106">toorestart un dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="e8e6e-106">toorestart a virtual device</span></span>
<span data-ttu-id="e8e6e-107">Quando un dispositivo virtuale è in esecuzione e si desidera toorestart, fare clic sul nome e quindi fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-107">When a virtual device is running and you want toorestart it, click its name, and then click **Restart**.</span></span> <span data-ttu-id="e8e6e-108">Mentre la periferica virtuale hello viene riavviato, il suo stato sia **riavvio**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-108">While hello virtual device is restarting, its status is **Restarting**.</span></span> <span data-ttu-id="e8e6e-109">Quando la periferica virtuale hello è pronta per si toouse, lo stato è **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-109">When hello virtual device is ready for you toouse, its status is **Running**.</span></span>

<span data-ttu-id="e8e6e-110">Utilizzare hello seguente cmdlet toorestart un dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="e8e6e-110">Use hello following cmdlet toorestart a virtual device.</span></span>

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

