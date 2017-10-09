## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo

In questa sezione utilizzare hello [portale di Azure] [ lnk-azure-portal] toocreate un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT. Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità. Per ulteriori informazioni, vedere sezione "Registro di sistema di identità" hello hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity]. Hello **Esplora dispositivo** in hello portale consente di generare un ID univoco del dispositivo e una chiave che il dispositivo può usare tooidentify stesso quando si connette tooIoT Hub. Gli ID dispositivo fanno distinzione tra maiuscole e minuscole.

1. Assicurarsi che si è connessi toohello [portale di Azure][lnk-azure-portal].

1. In hello Jumpbar, fare clic su **tutte le risorse** e trovare la risorsa di hub IoT.

    ![Passare l'hub Iot tooyour][img-find-iothub]

1. Quando la risorsa di hub IoT è aperto, fare clic su hello **Esplora dispositivo** strumento e quindi fare clic su **Aggiungi** nella parte superiore di hello. Specificare il nome di hello per il nuovo dispositivo, ad esempio **myDeviceId**, fare clic su **salvare**.

    ![Creare l'identità del dispositivo nel portale][img-create-device]

   In questo modo viene creata una nuova identità del dispositivo per l'hub IoT.

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. In hello **Esplora dispositivo**dell'elenco dei dispositivi, fare clic su dispositivo hello appena creato e prendere nota della hello **stringa di connessione---chiave primaria**. 

    ![Stringa di connessione del dispositivo][img-connection-string]

> [!NOTE]
> Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso. Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo. Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione. Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].

<!-- Images. -->
[img-find-iothub]: ./media/iot-hub-get-started-create-device-identity-portal/find-iothub.png
[img-create-device]: ./media/iot-hub-get-started-create-device-identity-portal/create-identity-portal.png
[img-connection-string]: ./media/iot-hub-get-started-create-device-identity-portal/device-connection-string.png


<!-- Links -->
[lnk-azure-portal]: https://portal.azure.com
[lnk-devguide-identity]: ../articles/iot-hub/iot-hub-devguide-identity-registry.md

