#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop e avviare un'applicazione cloud

1. toostop un'applicazione cloud, andare toohello macchina virtuale per l'applicazione cloud.
    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Dalla barra dei comandi di hello, fare clic su **arrestare**.

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Alla richiesta di conferma fare clic su **Sì**.

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Con l'arresto, la macchina virtuale viene deallocata. Durante l'arresto di appliance di cloud hello, lo stato è **Deallocating**. Dopo l'arresto appliance di cloud hello, lo stato è **arrestato (deallocato)**.

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Una volta che una macchina virtuale viene arrestata, fare clic su **avviare** (pulsante diventa disponibile) hello toostart macchina virtuale. Dopo che il dispositivo di cloud hello è stata avviata, il suo stato sia **Started**.

    ![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Utilizzare hello toostop i cmdlet seguenti e avviare un'applicazione cloud.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart un'applicazione cloud

toorestart un'applicazione cloud, andare toohello macchina virtuale per l'applicazione cloud. Dalla barra dei comandi di hello, fare clic su **riavviare**. Quando richiesto, confermare il riavvio di hello. Quando il dispositivo di cloud hello è pronto per si toouse, lo stato è **esecuzione**.

![Macchina virtuale appliance cloud StorSimple](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Utilizzare hello seguente cmdlet toorestart un'applicazione cloud.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

