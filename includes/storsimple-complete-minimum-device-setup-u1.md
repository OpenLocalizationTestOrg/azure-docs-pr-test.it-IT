<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>installazione di dispositivi di toocomplete hello minimo StorSimple
1. Selezionare il dispositivo di hello e fare clic su **avvio rapido**. Fare clic su **completare l'installazione di dispositivo** toostart hello Configurazione dispositivo guidata.
2. Nella procedura guidata di hello Configura dispositivo **le impostazioni di base** finestra di dialogo casella, hello seguenti:
   
   1. Fornire un **nome descrittivo** per il dispositivo. nome del dispositivo predefinito Hello riflette informazioni quali il modello di dispositivo hello e il numero di serie. È possibile assegnare un nome descrittivo del backup too64 caratteri toomanage il dispositivo.
   2. Set hello **fuso orario** basati su hello posizione geografica in cui hello dispositivo viene distribuito. Il dispositivo utilizzerà questo fuso orario per tutte le operazioni pianificate.
   3. In **Impostazioni DNS** specificare un indirizzo per **Server DNS secondario**. Se si utilizza IPv6, il campo hello verrà popolato in base al prefisso IPv6 hello fornito nell'interfaccia di Windows PowerShell hello. 
      Se non è stato configurato alcun server DNS secondario hello, non sarà consentito toosave la configurazione del dispositivo.
   4. Nelle interfacce iSCSI abilitate, abilitare almeno una rete per iSCSI. Almeno un'interfaccia di rete deve toobe abilitata per il cloud e uno toobe abilitata per iSCSI. DATA 0 è abilitata automaticamente per il cloud.
      
      ![Impostazioni di base della configurazione minima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Fare clic sull'icona di freccia di hello. ![Icona di freccia di StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. In hello **interfacce di rete** finestra di dialogo, fornire hello fissa di indirizzi IP per il Controller 0 e Controller 1. **controller Hello indirizzi IP fissato necessario toobe liberare gli indirizzi IP in subnet hello accessibile dall'indirizzo IP del dispositivo hello.** Se hello DATA 0 interfaccia è stata configurata per IPv4, hello fissa toobe necessità di indirizzi IP forniti in hello formato IPv4. Se è stato specificato un prefisso per la configurazione IPv6, hello indirizzi IP fissato verrà popolato automaticamente in questi campi.

    ![Interfacce di rete della configurazione minima del dispositivo StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Hello indirizzi IP per il controller hello fissi vengono usati per gestire dispositivi toohello gli aggiornamenti di hello e pertanto hello indirizzi IP fissato deve essere instradabili e in grado di tooconnect toohello Internet. È possibile verificare che il controller fisso gli indirizzi IP siano instradabili utilizzando hello [Test-HcsmConnection] [ Test] cmdlet. Hello seguente esempio mostra gli indirizzi IP controller fissato è indirizzato toohello Internet e accessibile hello server Microsoft Update. 

     ![Test-HcsmConnection con indirizzi IP instradabili](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Fare clic sull'icona di controllo hello ![StorSimple controllo icona](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Verrà visualizzata di nuovo dispositivo toohello **avvio rapido** pagina.
   
   > [!NOTE]
   > È possibile modificare hello tutte le altre impostazioni del dispositivo in qualsiasi momento accedendo hello **configura** pagina.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx