#### <a name="toostop-and-start-a-virtual-device"></a>toostop e avviare un dispositivo virtuale
toostop un dispositivo virtuale, fare clic sul nome e quindi fare clic su **arresto**. Mentre il dispositivo virtuale hello è in corso l'arresto, lo stato è **arresto**. Dopo che la periferica virtuale hello viene interrotta, il suo stato sia **arrestato**.

Utilizzare hello toostop i cmdlet seguenti e avviare un dispositivo virtuale.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart un dispositivo virtuale
Quando un dispositivo virtuale è in esecuzione e si desidera toorestart, fare clic sul nome e quindi fare clic su **riavviare**. Mentre la periferica virtuale hello viene riavviato, il suo stato sia **riavvio**. Quando la periferica virtuale hello è pronta per si toouse, lo stato è **esecuzione**.

Utilizzare hello seguente cmdlet toorestart un dispositivo virtuale.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

