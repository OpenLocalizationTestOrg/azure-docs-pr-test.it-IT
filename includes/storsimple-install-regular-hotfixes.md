<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="2773d-101">tooinstall hotfix periodici tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="2773d-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="2773d-102">Connettersi toohello console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2773d-102">Connect toohello device serial console.</span></span> <span data-ttu-id="2773d-103">Per ulteriori informazioni, vedere [passaggio 1: connessione alla console seriale toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="2773d-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="2773d-104">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="2773d-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="2773d-105">Digitare la password hello.</span><span class="sxs-lookup"><span data-stu-id="2773d-105">Type hello password.</span></span> <span data-ttu-id="2773d-106">password predefinita Hello è **Password1**.</span><span class="sxs-lookup"><span data-stu-id="2773d-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="2773d-107">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="2773d-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="2773d-108">Questo comando si applica solo aggiornamenti rapidi tooregular.</span><span class="sxs-lookup"><span data-stu-id="2773d-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="2773d-109">È possibile eseguire questo comando in un solo controller, ma verranno aggiornati entrambi i controller.</span><span class="sxs-lookup"><span data-stu-id="2773d-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="2773d-110">È possibile riscontrare un failover del controller durante il processo di aggiornamento hello; Tuttavia, hello failover non influiranno la disponibilità del sistema o l'operazione.</span><span class="sxs-lookup"><span data-stu-id="2773d-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="2773d-111">Quando richiesto, fornire hello percorso toohello cartella di rete condivisa che contiene i file dell'hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="2773d-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="2773d-112">Verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="2773d-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="2773d-113">Tipo **Y** tooproceed con l'installazione dell'hotfix hello.</span><span class="sxs-lookup"><span data-stu-id="2773d-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

