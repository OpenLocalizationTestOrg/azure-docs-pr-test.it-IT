<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>installazione di dispositivi di toocomplete hello minimo StorSimple

   > [!NOTE]
   > È possibile modificare il nome di dispositivo hello una volta completata l'installazione minima del dispositivo hello.
   
1. Dall'elenco dei dispositivi in hello in formato tabulare hello **dispositivi** pannello selezionare e fare clic sul dispositivo. Hello dispositivo è in un **pronto tooset backup** stato. Hello **Configura dispositivo** apre blade.

     ![Interfacce di rete della configurazione minima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. In hello **Configura dispositivo** pannello:
   
   1. Fornire un **nome descrittivo** per il dispositivo. nome del dispositivo predefinito Hello riflette informazioni quali il modello di dispositivo hello e il numero di serie. È possibile assegnare un nome descrittivo del backup too64 caratteri toomanage il dispositivo.
   2. Set hello **fuso orario** basati su hello posizione geografica in cui hello dispositivo viene distribuito. Il dispositivo usa questo fuso orario per tutte le operazioni pianificate.
   3. In hello **DATA 0 impostazioni**:

       1. I dati di interfaccia di rete viene illustrato come abilitare con hello 0 rete impostazioni (IP, subnet, gateway) configurate tramite installazione guidata di hello. DATA 0 viene abilitata automaticamente anche per il cloud e iSCSI.

       2. Fornire hello fissa di indirizzi IP per il Controller 0 e Controller 1. **controller Hello indirizzi IP fissato necessario toobe liberare gli indirizzi IP in subnet hello accessibile dall'indirizzo IP del dispositivo hello.** Se hello DATA 0 interfaccia è stata configurata per IPv4, hello fissa toobe necessità di indirizzi IP forniti in hello formato IPv4. Se è stato specificato un prefisso per la configurazione IPv6, indirizzi IP fissi hello vengono popolati automaticamente in questi campi.

            ![Interfacce di rete della configurazione minima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Hello indirizzi IP per il controller hello fissi vengono usati per gestire dispositivi toohello gli aggiornamenti di hello. Pertanto, hello indirizzi IP fissato deve essere instradabile e in grado di tooconnect toohello Internet. È possibile verificare che il controller fisso gli indirizzi IP siano instradabili utilizzando hello [Test-HcsmConnection] [ Test] cmdlet. Hello seguente esempio mostra gli indirizzi IP controller fissato è indirizzato toohello Internet e accessibile hello server Microsoft Update.

            ![Test-HcsmConnection con indirizzi IP instradabili](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Fare clic su **OK**. avvio della configurazione di dispositivo Hello. Una volta completata la configurazione dei dispositivi hello, ricevono la notifica. Hello modifiche allo stato dispositivo troppo**Online** in hello **dispositivi** blade.

    ![Interfacce di rete della configurazione minima del dispositivo StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
