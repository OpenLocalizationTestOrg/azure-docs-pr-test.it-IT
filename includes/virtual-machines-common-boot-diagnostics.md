In Azure ora è disponibile il supporto per due funzionalità di debug: il supporto per l'output della console e per gli screenshot per il modello di distribuzione Resource Manager di Macchine virtuali di Azure. 

Quando si attiva la propria immagine tooAzure o anche l'avvio delle immagini della piattaforma hello, possono esistere molti motivi per cui una macchina virtuale ottiene in uno stato non avviabile. Questi consentono di funzionalità si tooeasily diagnosticare e ripristinare le macchine virtuali da errori di avvio.

Per macchine virtuali Linux, è possibile visualizzare facilmente output di hello del log dal portale hello console:

![Portale di Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Tuttavia, per Windows e macchine virtuali Linux, Azure consente inoltre di toosee una schermata di hello VM dall'hypervisor hello:

![Errore](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Entrambe le funzionalità sono supportate per Macchine virtuali di Azure in tutte le aree. Si noti, schermate e l'output può richiedere fino a too10 minuti tooappear nell'account di archiviazione.

## <a name="common-boot-errors"></a>Errori di avvio comuni

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Sistema operativo non trovato](https://support.microsoft.com/help/4010142)
- [Errore di avvio o INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Abilitare la diagnostica in una nuova macchina virtuale
1. Quando si crea una nuova macchina virtuale dal portale di anteprima di hello, selezionare hello **Azure Resource Manager** dall'elenco a discesa modello di distribuzione hello:
 
    ![Gestione risorse](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Configurare monitoraggio opzione tooselect hello account di archiviazione in cui si desidera tooplace hello questi file di diagnostica.
 
    ![Creare una macchina virtuale](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Se si distribuisce un modello di gestione risorse di Azure, passare la risorsa di macchina virtuale tooyour e aggiungere una sezione del profilo di diagnostica hello. Ricordare di intestazione della versione API toouse hello "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profilo di diagnostica Hello consente tooselect hello account di archiviazione in cui tooput questi registri.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy un macchina virtuale di esempio con la diagnostica di avvio abilitata, qui il repository di estrazione.

## <a name="update-an-existing-virtual-machine"></a>Aggiornare una macchina virtuale esistente ##

diagnostica di avvio tooenable tramite hello portale, è possibile aggiornare una macchina virtuale esistente tramite hello portale. La diagnostica di avvio hello seleziona l'opzione e salvare. Riavviare l'effetto di tootake hello macchina virtuale.

![Aggiornare una VM esistente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

