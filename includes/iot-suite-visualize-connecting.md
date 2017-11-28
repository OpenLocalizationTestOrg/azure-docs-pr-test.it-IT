## <a name="view-device-telemetry-in-the-dashboard"></a><span data-ttu-id="32576-101">Visualizzare la telemetria del dispositivo nel dashboard</span><span class="sxs-lookup"><span data-stu-id="32576-101">View device telemetry in the dashboard</span></span>
<span data-ttu-id="32576-102">Il dashboard nella soluzione di monitoraggio remoto consente di visualizzare la telemetria che i dispositivi inviano all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="32576-102">The dashboard in the remote monitoring solution enables you to view the telemetry your devices send to IoT Hub.</span></span>

1. <span data-ttu-id="32576-103">Nel browser tornare al dashboard della soluzione di monitoraggio remoto e fare clic su **Dispositivi** nel pannello di sinistra per passare a **Elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="32576-103">In your browser, return to the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="32576-104">In **Devices list** (Elenco dispositivi) si noterà che lo stato del dispositivo è ora **In esecuzione**.</span><span class="sxs-lookup"><span data-stu-id="32576-104">In the **Devices list**, you should see that the status of your device is **Running**.</span></span> <span data-ttu-id="32576-105">Se non lo è, nel pannello **Dettagli dispositivo** fare clic su **Attiva dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="32576-105">If not, click **Enable Device** in the **Device Details** panel.</span></span>
   
    ![Visualizzare lo stato dei dispositivi][18]
3. <span data-ttu-id="32576-107">Fare clic su **Dashboard** per tornare al dashboard e selezionare il dispositivo nell'elenco a discesa **Dispositivo da visualizzare** per visualizzarne i dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="32576-107">Click **Dashboard** to return to the dashboard, select your device in the **Device to View** drop-down to view its telemetry.</span></span> <span data-ttu-id="32576-108">La telemetria dall'applicazione di esempio è di 50 unità per la temperatura interna, 55 unità per la temperatura esterna e 50 unità per l’umidità.</span><span class="sxs-lookup"><span data-stu-id="32576-108">The telemetry from the sample application is 50 units for internal temperature, 55 units for external temperature, and 50 units for humidity.</span></span>
   
    ![Visualizzare la telemetria dei dispositivi][img-telemetry]

## <a name="invoke-a-method-on-your-device"></a><span data-ttu-id="32576-110">Richiamare un metodo sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="32576-110">Invoke a method on your device</span></span>
<span data-ttu-id="32576-111">Il dashboard nella soluzione di monitoraggio remoto consente di richiamare metodi sui dispositivi tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="32576-111">The dashboard in the remote monitoring solution enables you to invoke methods on your devices through IoT Hub.</span></span> <span data-ttu-id="32576-112">Nella soluzione di monitoraggio remota, ad esempio, è possibile richiamare un metodo per simulare il riavvio di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="32576-112">For example, in the remote monitoring solution you can invoke a method to simulate rebooting a device.</span></span>

1. <span data-ttu-id="32576-113">Nel dashboard della soluzione di monitoraggio remoto fare clic su **Dispositivi** nel pannello di sinistra per passare a **Elenco dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="32576-113">In the remote monitoring solution dashboard, click **Devices** in the left-hand panel to navigate to the **Devices list**.</span></span>
2. <span data-ttu-id="32576-114">In **Elenco dispositivi** fare clic sull'**ID** del proprio dispositivo.</span><span class="sxs-lookup"><span data-stu-id="32576-114">Click **Device ID** for your device in the **Devices list**.</span></span>
3. <span data-ttu-id="32576-115">Nel pannello **Dettagli dispositivo** fare clic su **Metodi**.</span><span class="sxs-lookup"><span data-stu-id="32576-115">In the **Device details** panel, click **Methods**.</span></span>
   
    ![Metodi per il dispositivo][13]
4. <span data-ttu-id="32576-117">Nel menu a discesa **Metodi**, selezionare **InitiateFirmwareUpdate**, quindi in **FWPACKAGEURI** immettere un URL fittizio.</span><span class="sxs-lookup"><span data-stu-id="32576-117">In the **Method** drop-down, select **InitiateFirmwareUpdate**, and then in **FWPACKAGEURI** enter a dummy URL.</span></span> <span data-ttu-id="32576-118">Fare clic su **Richiama metodo** per chiamare il metodo sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="32576-118">Click **Invoke Method** to call the method on the device.</span></span>
   
    ![Richiamare un metodo per il dispositivo][14]
   

5. <span data-ttu-id="32576-120">Viene visualizzato un messaggio nella console che esegue il codice del dispositivo quando il dispositivo gestisce il metodo.</span><span class="sxs-lookup"><span data-stu-id="32576-120">You see a message in the console running your device code when the device handles the method.</span></span> <span data-ttu-id="32576-121">I risultati del metodo vengono aggiunti alla cronologia nel portale delle soluzioni:</span><span class="sxs-lookup"><span data-stu-id="32576-121">The results of the method are added to the history in the solution portal:</span></span>

    ![Visualizzare la cronologia del metodo][img-method-history]

## <a name="next-steps"></a><span data-ttu-id="32576-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32576-123">Next steps</span></span>
<span data-ttu-id="32576-124">L'articolo [Personalizzazione delle soluzioni preconfigurate][lnk-customize] descrive alcuni modi per estendere questo esempio.</span><span class="sxs-lookup"><span data-stu-id="32576-124">The article [Customizing preconfigured solutions][lnk-customize] describes some ways you can extend this sample.</span></span> <span data-ttu-id="32576-125">Le estensioni possibili comprendono l'utilizzo di sensori reali e implementazione di comandi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="32576-125">Possible extensions include using real sensors and implementing additional commands.</span></span>

<span data-ttu-id="32576-126">Per altre informazioni sulle [autorizzazioni visitare il sito azureiotsuite.com][lnk-permissions].</span><span class="sxs-lookup"><span data-stu-id="32576-126">You can learn more about the [permissions on the azureiotsuite.com site][lnk-permissions].</span></span>

[13]: ./media/iot-suite-visualize-connecting/suite4.png
[14]: ./media/iot-suite-visualize-connecting/suite7-1.png
[18]: ./media/iot-suite-visualize-connecting/suite10.png
[img-telemetry]: ./media/iot-suite-visualize-connecting/telemetry.png
[img-method-history]: ./media/iot-suite-visualize-connecting/history.png
[lnk-customize]: ../articles/iot-suite/iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-permissions]: ../articles/iot-suite/iot-suite-permissions.md
