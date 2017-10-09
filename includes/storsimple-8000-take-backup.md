<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a><span data-ttu-id="ecbf2-101">tootake una copia di backup</span><span class="sxs-lookup"><span data-stu-id="ecbf2-101">tootake a backup</span></span>

1. <span data-ttu-id="ecbf2-102">Passare il servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-102">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="ecbf2-103">Nell'elenco tabulare di hello delle periferiche, selezionare e fare clic su un dispositivo e quindi fare clic su **tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-103">From hello tabular listing of devices, select and click your device and then click **All settings**.</span></span> <span data-ttu-id="ecbf2-104">In hello **impostazioni** pannello andare troppo**Impostazioni > Gestisci > Criteri di Backup**.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-104">In hello **Settings** blade, go too**Settings > Manage > Backup policy**.</span></span>

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu1.png)

2. <span data-ttu-id="ecbf2-106">In hello **criteri di Backup** pannello, fare clic su **+ Aggiungi criteri**.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-106">In hello **Backup policy** blade, click **+ Add policy**.</span></span>

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu2.png)

3. <span data-ttu-id="ecbf2-108">In hello **creare criteri di backup** pannello, specificare un nome di lunghezza compresa tra 3 e 150 caratteri per i criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-108">In hello **Create backup policy** blade, supply a name that contains between 3 and 150 characters for your backup policy.</span></span>

4. <span data-ttu-id="ecbf2-109">Selezionare toobe volumi hello sottoposti a backup.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-109">Select hello volumes toobe backed up.</span></span> <span data-ttu-id="ecbf2-110">Se si seleziona più di un volume, tali volumi vengono raggruppati toocreate contemporaneamente un backup coerente con l'arresto anomalo del sistema.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-110">If you select more than one volume, these volumes are grouped together toocreate a crash-consistent backup.</span></span>

    ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu4.png)

5. <span data-ttu-id="ecbf2-112">Nel pannello **Aggiungere la prima pianificazione**:</span><span class="sxs-lookup"><span data-stu-id="ecbf2-112">On **Add first schedule** blade:</span></span>

    1. <span data-ttu-id="ecbf2-113">Selezionare il tipo di hello di backup.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-113">Select hello type of backup.</span></span> <span data-ttu-id="ecbf2-114">Per ripristini più rapidi selezionare **Snapshot locale**.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-114">For faster restores, select **Local** snapshot.</span></span> <span data-ttu-id="ecbf2-115">Per la resilienza dei dati, selezionare **Snapshot cloud**.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-115">For data resiliency, select **Cloud** snapshot.</span></span>
    2. <span data-ttu-id="ecbf2-116">Specificare la frequenza di backup hello in minuti, ore, giorni o settimane.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-116">Specify hello backup frequency in minutes, hours, days, or weeks.</span></span>
    3. <span data-ttu-id="ecbf2-117">Selezionare un periodo di conservazione.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-117">Select a retention time.</span></span> <span data-ttu-id="ecbf2-118">le scelte di conservazione Hello dipendono dalla frequenza di backup hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-118">hello retention choices depend on hello backup frequency.</span></span> <span data-ttu-id="ecbf2-119">Ad esempio, per criteri giornalieri, conservazione hello è possibile specificare in settimane, mentre per i criteri mensili in mesi.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-119">For example, for a daily policy, hello retention can be specified in weeks, whereas retention for a monthly policy is in months.</span></span>
    4. <span data-ttu-id="ecbf2-120">Selezionare l'ora e la data per i criteri di backup hello hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-120">Select hello starting time and date for hello backup policy.</span></span>
    5. <span data-ttu-id="ecbf2-121">Fare clic su **OK** toocreate dei criteri di backup hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-121">Click **OK** toocreate hello backup policy.</span></span>

        ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. <span data-ttu-id="ecbf2-123">Fare clic su **crea** toostart la creazione dei criteri di backup hello.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-123">Click **Create** toostart hello backup policy creation.</span></span> <span data-ttu-id="ecbf2-124">Ricevere notifiche quando i criteri di backup hello viene creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-124">You are notified when hello backup policy is successfully created.</span></span> <span data-ttu-id="ecbf2-125">viene aggiornato anche l'elenco di Hello di criteri di backup.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-125">hello list of backup policies is also updated.</span></span>
      
      ![Aggiungi criterio di backup](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      <span data-ttu-id="ecbf2-127">A questo punto è disponibile un criterio di backup che creerà backup pianificati dei dati del volume.</span><span class="sxs-lookup"><span data-stu-id="ecbf2-127">You now have a backup policy that creates scheduled backups of your volume data.</span></span>




