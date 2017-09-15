<!--author=SharS last changed: 11/18/16-->

#### <a name="to-install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="fd9e5-101">Per installare aggiornamenti regolari tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="fd9e5-101">To install regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="fd9e5-102">Aprire la console seriale del dispositivo e scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-102">Open the device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="fd9e5-103">Digitare la password.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-103">Type the password.</span></span> <span data-ttu-id="fd9e5-104">La password predefinita è *Password1*.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-104">The default password is *Password1*.</span></span> 
2. <span data-ttu-id="fd9e5-105">Al prompt dei comandi digitare:</span><span class="sxs-lookup"><span data-stu-id="fd9e5-105">At the command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="fd9e5-106">Verrà notificato se sono disponibili aggiornamenti e se gli aggiornamenti sono problematici o meno.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-106">You will be notified if updates are available and whether the updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="fd9e5-107">Al prompt dei comandi digitare:</span><span class="sxs-lookup"><span data-stu-id="fd9e5-107">At the command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="fd9e5-108">Il processo di aggiornamento verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-108">The update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="fd9e5-109">Questo comando si applica solo agli aggiornamenti regolari.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-109">This command applies only to regular updates.</span></span> <span data-ttu-id="fd9e5-110">È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="fd9e5-111">Durante il processo di aggiornamento è possibile che venga eseguito il failover di un controller. Tale failover, tuttavia, non avrà effetti sulla disponibilità o sul funzionamento del sistema.</span><span class="sxs-lookup"><span data-stu-id="fd9e5-111">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>
> 
> 

