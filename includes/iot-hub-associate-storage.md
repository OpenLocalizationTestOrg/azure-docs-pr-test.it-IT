## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Associare un tooIoT di account di archiviazione di Azure Hub

Poiché l'applicazione dispositivo simulato hello carica un blob tooa file, è necessario disporre un [di archiviazione di Azure](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) account associati tooIoT Hub. Quando si associa un account di archiviazione di Azure con un hub IoT, hub IoT hello genera un URI SAS. Un dispositivo consente il caricamento di toosecurely URI SAS un contenitore di blob tooa file. Hello servizio IoT Hub e hello dispositivo SDK coordinare processo hello che genera l'errore hello URI SAS e lo rende tooupload toouse di dispositivo tooa disponibile un file.

Seguire le istruzioni hello [caricamenti di file di configurazione tramite il portale di Azure hello](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate un hub di IoT tooyour account di archiviazione di Azure. Assicurarsi che un contenitore BLOB venga associato all'hub IoT e che siano abilitate le notifiche file.

![Abilitazione di notifiche file nel portale](media/iot-hub-associate-storage/enable-file-notifications.png)