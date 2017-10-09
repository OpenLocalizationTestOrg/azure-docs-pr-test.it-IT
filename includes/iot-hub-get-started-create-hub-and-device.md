## <a name="create-an-iot-hub"></a>Creare un hub IoT

1. In hello [portale di Azure](https://portal.azure.com/), fare clic su **New** > **Internet of Things** > **IoT Hub**.

   ![Creare un hub IoT in hello portale di Azure](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. In hello **hub IoT** riquadro, immettere le seguenti informazioni per l'hub IoT hello:

     **Nome**: immettere il nome di hello dell'hub IoT. Se specifica un nome hello è valido, viene visualizzato un segno di spunta verde.

     **Livello di prezzi e scalabilità**: hello seleziona **F1 - libero** livello. Questa opzione è sufficiente per questa demo. Per ulteriori informazioni, vedere hello [prezzi e livello di scalabilità](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Gruppo di risorse**: creazione di un hub IoT di hello toohost di gruppo di risorse o utilizzarne uno esistente. Per ulteriori informazioni, vedere [gruppi di risorse di utilizzare toomanage le risorse di Azure](../articles/azure-resource-manager/resource-group-portal.md).

     **Percorso**: selezionare hello più vicino tooyou percorso in cui è stato creato l'hub IoT hello.

     **PIN toodashboard**: selezionare questa opzione per l'hub IoT tooyour di facile accesso dal dashboard hello.

   ![Immettere informazioni toocreate l'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Fare clic su **Crea**. L'hub IoT potrebbe richiedere alcuni minuti toocreate. È possibile visualizzare lo stato di avanzamento in hello **notifiche** riquadro.

   ![Vedere le notifiche relative allo stato dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Dopo aver creato l'hub IoT, selezionarla nel dashboard di hello. Prendere nota di hello **Hostname**, quindi fare clic su **criteri di accesso condiviso**.

   ![Ottieni nome host hello dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. In hello **criteri di accesso condiviso** riquadro, fare clic su hello **iothubowner** criteri, quindi copia e prendere nota del hello **stringa di connessione** dell'hub IoT. Per ulteriori informazioni, vedere [tooIoT accesso controllo Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
Per questa esercitazione di configurazione non è necessaria la stringa di connessione iothubowner. Tuttavia, potrebbe essere necessario per alcune delle esercitazioni di hello in diversi scenari IoT dopo aver completato l'installazione.

   ![Ottenere la stringa di connessione dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Registrare un dispositivo nell'hub IoT hello per il dispositivo

1. In hello [portale di Azure](https://portal.azure.com/), aprire l'hub IoT.

2. Fare clic su **Esplora dispositivi**.
3. Nel riquadro di esplorazione di dispositivo hello, fare clic su **Aggiungi** tooadd un hub IoT tooyour di dispositivo. Quindi hello seguenti:

   **ID dispositivo**: immettere l'ID hello del nuovo dispositivo hello. Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.

   **Tipo di autenticazione**: selezionare **Chiave simmetrica**.

   **Genera chiavi automaticamente**: selezionare questa casella di controllo.

   **Connessione dispositivo tooIoT Hub**: fare clic su **abilitare**.

   ![Aggiungere un dispositivo in hello Esplora dispositivo dell'hub IoT](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Fare clic su **Salva**.
5. Dopo aver creato il dispositivo di hello, aprire la periferica hello in hello **Esplora dispositivo** riquadro.
6. Prendere nota della chiave primaria di hello hello della stringa di connessione.

   ![Ottenere la stringa di connessione dispositivo hello](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
