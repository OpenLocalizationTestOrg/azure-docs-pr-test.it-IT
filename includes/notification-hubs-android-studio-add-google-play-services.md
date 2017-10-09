1. Hello Open Android SDK Manager facendo clic sull'icona di hello sulla barra degli strumenti hello di Android Studio o facendo clic **strumenti** -> **Android** -> **SDK Manager**menu hello. Individuare la versione di destinazione hello di hello Android SDK utilizzato nel progetto, aprirla facendo **Mostra i dettagli del pacchetto**e scegliere **Google APIs**, se non è già installato.
2. Fare clic su hello **strumenti SDK** scheda. Se Google Play Service non è già installato, fare clic su **Google Play Services** come mostrato di seguito. Quindi fare clic su **applica** tooinstall. 
   
    Si noti percorso SDK hello, per l'utilizzo in un passaggio successivo. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Aprire hello **gradle** file nella directory dell'applicazione hello.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. In *dependencies*aggiungere questa riga: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Fare clic su hello **di progetto di sincronizzazione con i file Gradle** icona nella barra degli strumenti hello.
6. Aprire **AndroidManifest.xml** e aggiungere questo toohello tag *applicazione* tag.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

