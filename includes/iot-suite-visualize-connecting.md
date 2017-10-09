## <a name="view-device-telemetry-in-hello-dashboard"></a><span data-ttu-id="c06c1-101">Telemetria di dispositivo di visualizzazione nel dashboard di hello</span><span class="sxs-lookup"><span data-stu-id="c06c1-101">View device telemetry in hello dashboard</span></span>
<span data-ttu-id="c06c1-102">dashboard di Hello in hello Abilita soluzione si tooview hello telemetria tooIoT Hub di inviare i dispositivi di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="c06c1-102">hello dashboard in hello remote monitoring solution enables you tooview hello telemetry your devices send tooIoT Hub.</span></span>

1. <span data-ttu-id="c06c1-103">Nel browser, toohello restituito remoto soluzione dashboard di monitoraggio, fare clic su **dispositivi** in hello pannello sinistro toonavigate toohello **elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="c06c1-103">In your browser, return toohello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="c06c1-104">In hello **elenco dispositivi**, si dovrebbe essere stato hello del dispositivo **esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="c06c1-104">In hello **Devices list**, you should see that hello status of your device is **Running**.</span></span> <span data-ttu-id="c06c1-105">In caso contrario, fare clic su **abilitare dispositivo** in hello **dettagli dispositivo** pannello.</span><span class="sxs-lookup"><span data-stu-id="c06c1-105">If not, click **Enable Device** in hello **Device Details** panel.</span></span>
   
    ![Visualizzare lo stato dei dispositivi][18]
3. <span data-ttu-id="c06c1-107">Fare clic su **Dashboard** tooreturn toohello dashboard, selezionare il dispositivo in hello **dispositivo tooView** tooview elenco a discesa la telemetria.</span><span class="sxs-lookup"><span data-stu-id="c06c1-107">Click **Dashboard** tooreturn toohello dashboard, select your device in hello **Device tooView** drop-down tooview its telemetry.</span></span> <span data-ttu-id="c06c1-108">la telemetria Hello dall'applicazione di esempio hello è 50 unità per la temperatura, 55 unità esterne temperatura e 50 unità per umidità.</span><span class="sxs-lookup"><span data-stu-id="c06c1-108">hello telemetry from hello sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Visualizzare la telemetria dei dispositivi][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="c06c1-110">Richiamare un metodo sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="c06c1-110">Invoke a method on your device</span></span>
<span data-ttu-id="c06c1-111">dashboard Hello nella soluzione di monitoraggio remoto hello consente metodi tooinvoke nei dispositivi tramite IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c06c1-111">hello dashboard in hello remote monitoring solution enables you tooinvoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="c06c1-112">Nella soluzione di monitoraggio remoto hello, ad esempio, è possibile richiamare un metodo toosimulate il riavvio di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c06c1-112">For example, in hello remote monitoring solution you can invoke a method toosimulate rebooting a device.</span></span>

1. <span data-ttu-id="c06c1-113">In hello remoto soluzione dashboard di monitoraggio, fare clic su **dispositivi** in hello pannello sinistro toonavigate toohello **elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="c06c1-113">In hello remote monitoring solution dashboard, click **Devices** in hello left-hand panel toonavigate toohello **Devices list**.</span></span>
2. <span data-ttu-id="c06c1-114">Fare clic su **ID dispositivo** per il dispositivo in hello **elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="c06c1-114">Click **Device ID** for your device in hello **Devices list**.</span></span>
3. <span data-ttu-id="c06c1-115">In hello **dettagli dispositivo** pannello, fare clic su **metodi**.</span><span class="sxs-lookup"><span data-stu-id="c06c1-115">In hello **Device details** panel, click **Methods**.</span></span>
   
    ![Metodi per il dispositivo][13]
4. <span data-ttu-id="c06c1-117">In hello **metodo** elenco a discesa, selezionare **InitiateFirmwareUpdate**, quindi nel **FWPACKAGEURI** immettere un URL fittizio.</span><span class="sxs-lookup"><span data-stu-id="c06c1-117">In hello **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="c06c1-118">Fare clic su **Richiama metodo** metodo hello toocall sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="c06c1-118">Click **Invoke Method** toocall hello method on hello device.</span></span>
   
    ![Richiamare un metodo per il dispositivo][14]
   

5. <span data-ttu-id="c06c1-120">Viene visualizzato un messaggio nella console di hello in esecuzione il codice del dispositivo quando il dispositivo hello gestisce metodo hello.</span><span class="sxs-lookup"><span data-stu-id="c06c1-120">You see a message in hello console running your device code when hello device handles hello method.</span></span> <span data-ttu-id="c06c1-121">risultati di Hello del metodo hello vengono aggiunti toohello cronologia nel portale di soluzione hello:</span><span class="sxs-lookup"><span data-stu-id="c06c1-121">hello results of hello method are added toohello history in hello solution portal:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="c06c1-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c06c1-123">Next steps</span></span>
<span data-ttu-id="c06c1-124">articolo Hello [personalizzazione preconfigurato soluzioni] [ lnk-customize] vengono descritte alcune differenze, è possibile estendere questo esempio.</span><span class="sxs-lookup"><span data-stu-id="c06c1-124">hello article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="c06c1-125">Le estensioni possibili comprendono l'utilizzo di sensori reali e implementazione di comandi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c06c1-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="c06c1-126">È possibile approfondire hello [le autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="c06c1-126">You can learn more about hello [permissions on hello azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
