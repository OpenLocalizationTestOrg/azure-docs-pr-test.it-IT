

1. In Mac avviare **Keychain Access**. Nella hello sinistra la barra di spostamento, in **categoria**aprire **certificati personali**. Trovare il certificato SSL hello che è stato scaricato nella sezione precedente hello e divulgare il relativo contenuto. Selezionare solo hello certificato (non si seleziona la chiave privata di hello), e [esportarlo](https://support.apple.com/kb/PH20122?locale=en_US).
2. In hello [portale di Azure](https://portal.azure.com/), fare clic su **Esplora tutto** > **servizi App**, scegliere il back-end App per dispositivi mobili. In **Impostazioni** fare clic su **App Service Push** (Push servizio app), quindi fare clic sul nome dell'hub di notifica. Andare troppo**servizi notifica Push di Apple** > **carica certificato**. Caricare il file hello. p12 selezionando hello corretto **modalità** (a seconda se del certificato client SSL precedenti è produzione o sandbox). Salvare le modifiche.

Il servizio è ora configurato toowork alle notifiche push in iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
