---
title: un pacchetto di supporto StorSimple aaaCreate | Documenti Microsoft
description: Informazioni su come decrittografare, toocreate e modificare un pacchetto di supporto per il dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Creare e gestire un pacchetto di supporto StorSimple
## <a name="overview"></a>Panoramica
Un pacchetto di supporto StorSimple è un meccanismo di facile utilizzo che raccoglie tutti i log rilevanti tooassist supporto alla risoluzione dei problemi del dispositivo StorSimple. Hello registri raccolti vengono crittografati e compressi.

In questa esercitazione include istruzioni dettagliate toocreate e gestire il pacchetto di supporto di hello.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Creare e caricare un pacchetto di supporto nel portale di Azure classico hello
È possibile creare e caricare un sito del supporto Microsoft di supporto pacchetto toohello tramite hello **manutenzione** pagina del servizio hello hello portale di Azure classico.

> [!NOTE]
> caricamento di Hello richiede una passkey per il supporto. Il tecnico del supporto deve fornire questo tooyou tramite posta elettronica.
> 
> 

Un pacchetto di supporto crittografati e compressi (CAB) viene creato e caricato toohello sito del supporto tecnico. quindi è stato possibile recuperare il pacchetto dal sito del supporto tecnico di hello per risolvere il problema di hello con tecnico Hello.

Eseguire i passaggi toocreate portale classico hello un pacchetto di supporto hello.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>un pacchetto di supporto nel portale di Azure classico hello toocreate
1. Selezionare **Dispositivi** > **Manutenzione**.
2. In hello **pacchetto di supporto** selezionare **pacchetto per creare e caricare il supporto**.
3. In hello **pacchetto per creare e caricare il supporto** finestra di dialogo casella, hello seguenti:
   
    ![Creare un pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * In hello **passkey per il supporto** testo immettere passkey hello. Il tecnico del supporto Microsoft deve inviare questo tooyou passkey tramite posta elettronica.
   * Selezionare hello casella di controllo tooprovide consenso tooautomatically caricamento hello supporto pacchetto toohello sito del supporto Microsoft.
   * Fare clic sull'icona di controllo hello ![Icona del segno di spunta](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Creare manualmente un pacchetto per il supporto
In alcuni casi, è necessario toomanually creare pacchetto di supporto hello tramite Windows PowerShell per StorSimple. ad esempio:

* Se è necessario tooremove le informazioni riservate dal log file toosharing precedente con il supporto Microsoft.
* Se si verificano problemi di caricamento hello pacchetto a causa di problemi di tooconnectivity.

È possibile condividere il pacchetto per il supporto generato manualmente con il supporto tecnico Microsoft tramite posta elettronica. Eseguire hello seguendo i passaggi toocreate un pacchetto di supporto in Windows PowerShell per StorSimple.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate un pacchetto di supporto in Windows PowerShell per StorSimple
1. toostart una sessione di Windows PowerShell come amministratore nel computer remoto hello utilizzati dispositivo di StorSimple tooyour tooconnect, immettere hello comando seguente:
   
    `Start PowerShell`
2. Nella sessione di Windows PowerShell hello, connettersi toohello SSAdmin Console del dispositivo:
   
   * Al prompt dei comandi di hello, immettere:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * Nella finestra di dialogo di hello visualizzata, immettere la password amministratore del dispositivo. password predefinita Hello è:
     
      `Password1`
     
      ![Finestra di dialogo Credenziali PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Selezionare **OK**.
   * Al prompt dei comandi di hello, immettere:
     
      `Enter-PSSession $MS`
3. Nella sessione hello visualizzata, immettere comando appropriato hello.
   
   * Per le condivisioni di rete protette da password, immettere:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Verrà richiesto per una password, una cartella condivisa di rete toohello percorso e una passphrase di crittografia (perché è crittografato il pacchetto di supporto hello). Un pacchetto di supporto viene quindi creato nella cartella specificata hello.
   * Per le condivisioni che non sono protette da password, non è necessario hello `-Credential` parametro. Immettere hello seguente:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       pacchetto di supporto Hello viene creato per entrambi i controller nella cartella condivisa di rete specificata hello. È un file compresso crittografato che può essere inviato tooMicrosoft supporto per la risoluzione dei problemi. Per ulteriori informazioni, vedere [Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>parametri del cmdlet Export-HcsSupportPackage Hello
È possibile utilizzare i seguenti parametri con il cmdlet Export-HcsSupportPackage hello hello.

| . | Obbligatorio/Facoltativo | Description |
| --- | --- | --- |
| `-Path` |Obbligatorio |Utilizzare il percorso hello tooprovide hello cartella di rete condivisa in cui hello è inserito il pacchetto di supporto. |
| `-EncryptionPassphrase` |Obbligatorio |Utilizzare tooprovide toohelp una passphrase crittografare il pacchetto di supporto di hello. |
| `-Credential` |Facoltativo |Utilizzare le credenziali di accesso toosupply per la cartella di rete condivisa hello. |
| `-Force` |Facoltativo |Utilizzare passaggio di conferma passphrase di crittografia di tooskip hello. |
| `-PackageTag` |Facoltativo |Utilizzare una directory nella directory di toospecify *percorso* che non supporta hello è inserito il pacchetto. valore predefinito di Hello è [nome dispositivo]-[data corrente e data]. |
| `-Scope` |Facoltativo |Specificare come **Cluster** toocreate (impostazione predefinita) un pacchetto di supporto per entrambi i controller. Se si desidera toocreate un pacchetto solo per il controller corrente hello, specificare **Controller**. |

## <a name="edit-a-support-package"></a>Modificare un pacchetto per il supporto
Dopo aver generato un pacchetto di supporto, è necessario tooedit hello pacchetto tooremove le informazioni riservate. Ciò può includere i nomi dei volumi, gli indirizzi IP del dispositivo e i nomi di backup dai file di log hello.

> [!IMPORTANT]
> È possibile solo modificare un pacchetto per il supporto che è stato generato tramite Windows PowerShell per StorSimple. È possibile modificare un pacchetto creato nel portale di Azure classico con il servizio StorSimple Manager hello.
> 
> 

tooedit un pacchetto di supporto prima di caricarlo sul sito del supporto Microsoft hello, innanzitutto di decrittografare il pacchetto di supporto di hello, modificare i file hello e quindi crittografarlo nuovamente. Eseguire hello alla procedura seguente.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit un pacchetto di supporto in Windows PowerShell per StorSimple
1. Generare un pacchetto di supporto come descritto in precedenza, in [toocreate un pacchetto di supporto in Windows PowerShell per StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Scaricare script hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente nel client.
3. Importare il modulo di Windows PowerShell hello. Specificare hello percorso toohello cartella locale in cui è stato scaricato script hello. modulo hello tooimport, immettere:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Tutti i file hello *AES* i file vengono compressi e crittografati. toodecompress e decrittografare i file, immettere:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Si noti che le estensioni di file effettivo hello sono ora visualizzate per tutti i file hello.
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750706.png)
5. Quando viene richiesta la passphrase di crittografia hello, immettere la passphrase hello utilizzato per la creazione del pacchetto di supporto hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Sfoglia cartella toohello che contiene i file di log hello. Poiché il file di log di hello sono ora decompressi e decrittografato, sono estensioni di file originale. Modificare questi tooremove file le informazioni specifiche del cliente, ad esempio i nomi dei volumi e gli indirizzi IP del dispositivo e salvare file hello.
7. Chiude hello file toocompress con gzip e crittografati con AES-256. Si tratta di velocità e la sicurezza in trasferimento pacchetto di supporto hello attraverso una rete. toocompress e crittografare i file, immettere hello seguenti:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Modificare il pacchetto per il supporto](./media/storsimple-create-manage-support-package/IC750707.png)
8. Quando richiesto, fornire una passphrase di crittografia per pacchetto di supporto modificato hello.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Annotare hello nuova passphrase, in modo che è possibile condividerla con il supporto Microsoft, quando richiesto.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Esempio: modifica dei file in un pacchetto per il supporto in una condivisione protetta da password
Hello di esempio seguente viene illustrato come toodecrypt, modificare e crittografare nuovamente un pacchetto di supporto.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[usare pacchetti di supporto e dispositivo registra tootroubleshoot distribuzione dispositivo](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

