
1. In Esplora soluzioni di Visual Studio, fare doppio clic su progetto di applicazione Windows Store hello e fare clic su **archivio** > **Associa applicazione a Store hello**.

    ![Associa l’app con Windows Store](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. Nella procedura guidata hello, fare clic su **Avanti**e accedere con l'account Microsoft. Immettere un nome per l'app in **Riserva un nuovo nome dell'app**, fare clic su **Riserva**.
3. Dopo la registrazione di app hello è nuovo nome di applicazione hello è stata creata, selezionare, fare clic su **Avanti**, quindi fare clic su **associare**. Consente di aggiungere il manifesto di applicazione toohello hello richiesto Windows Store registrazione informazioni.
4. Ripetere i passaggi 1 e 3 per il progetto di app Windows Phone Store hello utilizzando hello stessa registrazione creato in precedenza per app di Windows Store hello.  
5. Sfoglia toohello [Windows Dev Center](https://dev.windows.com/en-us/overview)e accedere con l'account Microsoft. Fare clic su nuova registrazione app hello in **le mie app**, quindi espandere **servizi** > **notifiche Push**.
6. In hello **notifiche Push** pagina, fare clic su **sito Services Live** in **notifica Push Windows Services (WNS) e delle App mobili di Microsoft Azure**. Prendere nota dei valori hello di hello **SID pacchetto** hello e *corrente* valore **segreto dell'applicazione**. 

    ![Impostazione dell'app nel centro per sviluppatori hello](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > segreto dell'applicazione Hello e il SID pacchetto sono credenziali di sicurezza importanti. Non condividere questi valori con altri utenti né distribuirli con l'app.
   >
   >
