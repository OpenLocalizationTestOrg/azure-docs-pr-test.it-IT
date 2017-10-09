> [!IMPORTANT]
> le notifiche Push da Mobile Engagement tooreceive, è necessario tooenable `Silent Remote Notifications` nell'applicazione. È necessario la matrice UIBackgroundModes tooadd hello remoto notifica valore toohello nel file Info. plist.
> 
> 

1. Aprire `info.plist` file nel progetto hello
2. Fare clic con il pulsante destro su hello prima voce elenco hello (`Information Property List`) e aggiungere una nuova riga
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Nella nuova riga hello immettere`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Fare clic sulla riga hello tooexpand di hello freccia sinistra
5. Aggiungere hello seguente elemento toohello valore 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Dopo aver modificato hello, Info. plist hello XML deve contenere hello seguente chiave e valore:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Se si usano **Xcode 7+** e **iOS 9+**:
   
   * Abilitare **Notifiche push** in Destinazioni > Nome destinazione > Funzionalità.

