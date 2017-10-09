#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Configurazione progetto iOS hello in Studio a Xamarin
1. In Xamarin.Studio, aprire **Info. plist**e aggiornamento hello **identificatore Bundle** con hello aggregare ID creato in precedenza con il nuovo ID di app.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Scorrere verso il basso troppo**modalità di Background**. Seleziona hello **abilitare la modalità di Background** casella e hello **notifiche Remote** casella.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Fare doppio clic sul progetto in hello soluzione pannello tooopen **opzioni progetto**.
4. In **compilare**, scegliere **firma Bundle iOS**e selezionare hello identità corrispondente e profilo di provisioning è sufficiente impostare per questo progetto.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   In questo modo che il progetto hello utilizza nuovo profilo hello per la firma del codice. Per hello ufficiale Xamarin provisioning dei dispositivi documentazione, vedere [Provisioning dei dispositivi Xamarin].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Configurare il progetto di iOS hello in Visual Studio
1. In Visual Studio, fare clic sul progetto hello e quindi fare clic su **proprietà**.
2. Nelle pagine delle proprietà hello, fare clic su hello **applicazione iOS** scheda e aggiornamento hello **identificatore** con ID hello creato in precedenza.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. In hello **firma Bundle iOS** scheda identità corrispondenti selezionare hello e provisioning profilo è solo set di backup per questo progetto.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    In questo modo che il progetto hello utilizza nuovo profilo hello per la firma del codice. Per hello ufficiale Xamarin provisioning dei dispositivi documentazione, vedere [Provisioning dei dispositivi Xamarin].
4. Fare doppio clic sul file Info. plist tooopen e quindi abilitare **RemoteNotifications** in **modalità di Background**.

[Provisioning dei dispositivi Xamarin]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
