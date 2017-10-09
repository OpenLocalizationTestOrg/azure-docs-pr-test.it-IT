## <a name="create-an-iot-hub"></a>Creare un hub IoT
Creare un hub IoT per tooconnect di app del dispositivo simulato per. Hello passaggi seguenti viene illustrato come toocomplete questa attività dal utilizzando hello portale di Azure.

1. Accedi toohello [portale di Azure][lnk-portal].
1. In hello Jumpbar, fare clic su **New** > **Internet of Things** > **IoT Hub**.
   
    ![Indice del portale di Azure][1]
1. In hello **hub IoT** pannello, scegliere configurazione hello per l'hub IoT.
   
    ![Pannello Hub IoT][2]
   
   1. In hello **nome** , immettere un nome per l'hub IoT. Se hello **nome** è valido e disponibile, viene visualizzato un segno di spunta verde in hello **nome** casella.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Selezionare un [piano tariffario e un livello di scalabilità][lnk-pricing]. Per questa esercitazione non è necessario un livello specifico. Per questa esercitazione, usare il livello F1 gratuito di hello.
   1. In **Gruppo di risorse** creare un gruppo di risorse o selezionarne uno esistente. Per ulteriori informazioni, vedere [utilizzando risorse gruppi di risorse di Azure toomanage][lnk-resource-groups].
   1. In **percorso**, selezionare hello percorso toohost l'hub IoT. Per questa esercitazione, scegliere la località più vicina.
1. Dopo aver scelto le opzioni di configurazione dell'hub IoT, fare clic su **Crea**.  Può richiedere alcuni minuti per Azure toocreate l'hub IoT. stato hello toocheck, è possibile monitorare lo stato di avanzamento hello hello schermata iniziale o nel Pannello di notifiche di hello.
   
    ![Stato del nuovo hub IoT][3]
1. Hub IoT hello è stata creata, fare clic su nuovo riquadro di hello per l'hub IoT nel Pannello di hello hello tooopen portale Azure per l'hub IoT nuovo hello. Prendere nota di hello **Hostname**, quindi fare clic su **criteri di accesso condiviso**.
   
    ![Pannello del nuovo hub IoT][4]
1. In hello **criteri di accesso condiviso** pannello, fare clic su hello **iothubowner** criteri, quindi copiare e prendere nota della stringa di connessione IoT Hub hello in hello **iothubowner** blade. Per ulteriori informazioni, vedere [il controllo degli accessi] [ lnk-access-control] in hello "Guida per sviluppatori di IoT Hub".
   
    ![Pannello Criteri di accesso condivisi][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
