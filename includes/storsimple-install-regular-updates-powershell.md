<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="f5659-101">tooinstall aggiornamenti periodici tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="f5659-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="f5659-102">Aprire console seriale del dispositivo hello e selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="f5659-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="f5659-103">Digitare la password hello.</span><span class="sxs-lookup"><span data-stu-id="f5659-103">Type hello password.</span></span> <span data-ttu-id="f5659-104">password predefinita Hello è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="f5659-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="f5659-105">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="f5659-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="f5659-106">Si riceverà la notifica se sono disponibili aggiornamenti e se gli aggiornamenti di hello siano dannose o non comportano interruzioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="f5659-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="f5659-107">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="f5659-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="f5659-108">verrà avviato il processo di aggiornamento Hello.</span><span class="sxs-lookup"><span data-stu-id="f5659-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f5659-109">Questo comando si applica solo aggiornamenti di tooregular.</span><span class="sxs-lookup"><span data-stu-id="f5659-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="f5659-110">È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="f5659-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="f5659-111">È possibile riscontrare un failover del controller durante il processo di aggiornamento hello; Tuttavia, hello failover non influiranno la disponibilità del sistema o l'operazione.</span><span class="sxs-lookup"><span data-stu-id="f5659-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

