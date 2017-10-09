<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="05f72-101">tooconnect tramite la console seriale hello</span><span class="sxs-lookup"><span data-stu-id="05f72-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="05f72-102">Connettere il dispositivo di toohello cavo seriale (direttamente o tramite un adapter seriale USB).</span><span class="sxs-lookup"><span data-stu-id="05f72-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="05f72-103">Aprire hello **Pannello di controllo**e quindi aprire hello **Gestione dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="05f72-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="05f72-104">Identificare la porta COM hello come illustrato nella seguente figura hello.</span><span class="sxs-lookup"><span data-stu-id="05f72-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Connessione tramite console seriale](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="05f72-106">Avviare PuTTY.</span><span class="sxs-lookup"><span data-stu-id="05f72-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="05f72-107">Nel riquadro di destra hello, modificare hello **tipo di connessione** troppo**seriale**.</span><span class="sxs-lookup"><span data-stu-id="05f72-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="05f72-108">Nel riquadro di destra hello, digitare la porta COM appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="05f72-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="05f72-109">Assicurarsi che i parametri di configurazione seriale hello siano impostati come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="05f72-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="05f72-110">Velocità: 115.200</span><span class="sxs-lookup"><span data-stu-id="05f72-110">Speed: 115,200</span></span>
   * <span data-ttu-id="05f72-111">Bit di dati: 8</span><span class="sxs-lookup"><span data-stu-id="05f72-111">Data bits: 8</span></span>
   * <span data-ttu-id="05f72-112">Bit di stop: 1</span><span class="sxs-lookup"><span data-stu-id="05f72-112">Stop bits: 1</span></span>
   * <span data-ttu-id="05f72-113">Parità: nessuno</span><span class="sxs-lookup"><span data-stu-id="05f72-113">Parity: None</span></span>
   * <span data-ttu-id="05f72-114">Controllo di flusso: nessuno</span><span class="sxs-lookup"><span data-stu-id="05f72-114">Flow control: None</span></span>
     
     <span data-ttu-id="05f72-115">Queste impostazioni vengono visualizzate nella seguente figura hello.</span><span class="sxs-lookup"><span data-stu-id="05f72-115">These settings are shown in hello following illustration.</span></span>
     
     ![Impostazioni puTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="05f72-117">Se il controllo di flusso predefinito hello impostazione non funziona, provare a impostare controllo di flusso hello tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="05f72-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="05f72-118">Fare clic su **aprire** toostart una sessione seriale.</span><span class="sxs-lookup"><span data-stu-id="05f72-118">Click **Open** toostart a serial session.</span></span>

