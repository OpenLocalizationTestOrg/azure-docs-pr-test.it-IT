---
title: hello aaaModify DATA 0 impostazioni in un dispositivo StorSimple | Documenti Microsoft
description: Informazioni su come toouse Windows PowerShell per StorSimple tooreconfigure hello dati interfaccia di rete 0 nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Modificare le impostazioni dell'interfaccia di rete 0 di hello dati nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
Il dispositivo StorSimple di Microsoft Azure ha sei interfacce di rete, da DATA 0 tooDATA 5. Hello DATA 0 è sempre configurata tramite l'interfaccia di Windows PowerShell hello o la console seriale hello interfaccia ed è automaticamente abilitata per il cloud. Si noti che non è possibile configurare l'interfaccia di rete 0 dati tramite hello portale di Azure classico. 

DATA 0 interfaccia viene prima configurata mediante Installazione guidata di hello durante la distribuzione iniziale del dispositivo StorSimple hello Hello. Quando il dispositivo di hello è in modalità operativa, potrebbe essere necessario tooreconfigure DATA 0 impostazioni. In questa esercitazione sono disponibili due metodi toomodify dati 0 le impostazioni di rete, sia tramite Windows PowerShell per StorSimple.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Modificare i dati 0 impostazione tramite installazione guidata di hello di rete
* Modificare le impostazioni di rete 0 dati tramite hello `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Modificare le impostazioni di rete di DATI 0 tramite la configurazione guidata
È possibile riconfigurare le impostazioni di rete 0 dati collegando toohello interfaccia di Windows PowerShell del dispositivo StorSimple e avviare una sessione della procedura guidata configurazione. Eseguire i seguenti passaggi toomodify DATA 0 hello impostazioni:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>impostazioni di rete 0 toomodify dati tramite installazione guidata
1. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Quando richiesto specificare hello **password amministratore del dispositivo**. password predefinita Hello è `Password1`.
2. Al prompt dei comandi di hello, digitare:
   
    `Invoke-HcsSetupWizard`
3. Una procedura guidata verrà visualizzato toohelp configuri hello DATA 0 interfaccia del dispositivo. Fornire nuovi valori per la subnet mask, gateway e l'indirizzo IP hello.

> [!NOTE]
> Hello fissato controller gli indirizzi IP saranno necessario riconfigurare tramite hello toobe **configura** pagina del dispositivo StorSimple hello in hello portale di Azure classico. Per ulteriori informazioni, visitare troppo[modificare interfacce di rete](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Modificare le impostazioni di rete di DATI 0 tramite il cmdlet Set-HcsNetInterface
Un tooreconfigure alternativa DATA 0 è l'interfaccia di rete tramite l'utilizzo di hello di hello `Set-HcsNetInterface` cmdlet. esecuzione del cmdlet Hello dall'interfaccia di Windows PowerShell hello del dispositivo StorSimple. Quando si utilizza questa procedura, IP fissato dei controller hello inoltre è possibile configurare. Eseguire i seguenti passaggi toomodify hello DATA 0 hello impostazioni: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>impostazioni di rete 0 toomodify dati tramite il cmdlet Set-HcsNetInterface hello
1. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Quando richiesto specificare password amministratore del dispositivo hello. password predefinita Hello è `Password1`.
2. Al prompt dei comandi di hello, digitare:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Tra parentesi quadre hello con angolata, digitare hello seguenti valori per DATA 0:
   
   * Indirizzo IPv4
   * Gateway IPv4
   * Subnet mask IPv4
   * Indirizzo IPv4 fisso per controller 0
   * Indirizzo IPv4 fisso per controller 1
     
     Per ulteriori informazioni sull'utilizzo di hello di questo cmdlet, vedere troppo[di Windows PowerShell per StorSimple cmdlet riferimento](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Passaggi successivi
* interfacce di rete tooconfigure diverse da DATA 0, è possibile utilizzare hello [pagina di configurazione nel portale di Azure classico hello](storsimple-modify-device-config.md). 
* Se si verificano problemi durante la configurazione delle interfacce di rete, fare riferimento troppo[risolvere i problemi di distribuzione](storsimple-troubleshoot-deployment.md).

