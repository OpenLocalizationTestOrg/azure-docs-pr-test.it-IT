---
title: Configurare il proxy Web per il dispositivo StorSimple serie 8000 | Microsoft Docs
description: Informazioni su come configurare le impostazioni del proxy Web per il dispositivo StorSimple tramite Windows PowerShell per StorSimple
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: 1109e44ed9c6aa8a0f7305b8a50410316711589c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurare il proxy web per il dispositivo StorSimple

## <a name="overview"></a>Overview

In questa esercitazione viene illustrato come utilizzare Windows PowerShell per StorSimple per configurare e visualizzare le impostazioni proxy Web per il dispositivo StorSimple. Le impostazioni proxy Web vengono utilizzate dal dispositivo StorSimple per comunicare con il cloud. Un server proxy Web viene utilizzato per aggiungere un ulteriore livello di sicurezza, contenuto per filtro e cache per semplificare i requisiti di larghezza di banda o l'analisi dei dati.

Le indicazioni fornite in questa esercitazione si applicano solo ai dispositivi fisici StorSimple serie 8000. La configurazione del proxy Web non è supportata nell'appliance cloud StorSimple (8010 e 8020).

Il proxy Web è una configurazione _facoltativa_ per il dispositivo StorSimple. È possibile configurare il proxy Web solo tramite Windows PowerShell per StorSimple. La configurazione è un processo in due passaggi come indicato di seguito:

1. È innanzitutto necessario configurare le impostazioni proxy Web tramite l'installazione guidata o i cmdlet di Windows PowerShell per StorSimple.
2. È quindi possibile abilitare le impostazioni proxy Web configurate utilizzando i cmdlet di Windows PowerShell per StorSimple.

Una volta completata la configurazione del proxy Web, è possibile visualizzare le impostazioni proxy Web configurate nel servizio Gestione dispositivi StorSimple di Microsoft Azure e in Windows PowerShell per StorSimple.

Dopo aver letto questa esercitazione, si sarà in grado di:

* Configurare il proxy Web usando i cmdlet e l'installazione guidata.
* Abilitare il proxy Web usando i cmdlet.
* Visualizzare le impostazioni proxy Web nel portale di Azure.
* Risolvere gli errori durante la configurazione del proxy Web.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurare il proxy Web tramite Windows PowerShell per StorSimple

Utilizzare uno dei seguenti metodi per configurare le impostazioni proxy Web:

* Installazione guidata per semplificare i passaggi di configurazione.
* Cmdlet di Windows PowerShell per StorSimple.

Ognuno di questi metodi è descritto nelle sezioni seguenti.

## <a name="configure-web-proxy-via-the-setup-wizard"></a>Configurare il proxy Web tramite l'installazione guidata

Usare l'installazione guidata per semplificare i passaggi per la configurazione del proxy Web. Eseguire i passaggi seguenti per configurare il proxy Web sul dispositivo.

#### <a name="to-configure-web-proxy-via-the-setup-wizard"></a>Per configurare il proxy Web tramite l'installazione guidata

1. Nel menu della console seriale scegliere l'opzione 1, **Connessione con accesso completo**, e specificare la **password di amministratore del dispositivo**. Digitare il comando seguente per avviare una sessione dell'installazione guidata:
   
    `Invoke-HcsSetupWizard`
2. Se questa è la prima volta che viene usata l'installazione guidata per la registrazione del dispositivo, è necessario configurare tutte le impostazioni di rete necessarie fino a raggiungere la configurazione del proxy Web. Se il dispositivo è già registrato, accettare tutte le impostazioni di rete configurate fino a raggiungere la configurazione del proxy Web. Nella configurazione guidata, quando viene richiesto di configurare le impostazioni proxy Web, digitare **Sì**.
3. Per l' **URL proxy Web**specificare l'indirizzo IP o il nome di dominio completo (FQDN) del server proxy Web e il numero di porta TCP che si desidera che il dispositivo utilizzi per comunicare con il cloud. Utilizzare il seguente formato:
   
    `http://<IP address or FQDN of the web proxy server>:<TCP port number>`
   
    Per impostazione predefinita, viene specificato il numero di porta TCP 8080.
4. Scegliere il tipo di autenticazione: **NTLM**, **Di base** o **Nessuno**. L'autenticazione di base è quella meno sicura per la configurazione del server proxy. NT LAN Manager (NTLM) è un protocollo di autenticazione altamente protetta e complessa che utilizza un sistema di messaggistica a tre vie (a volte quattro, se è necessaria ulteriore integrità) per autenticare un utente. L'autenticazione predefinita è NTLM. Per altre informazioni, vedere l'autenticazione [di base](http://hc.apache.org/httpclient-3.x/authentication.html) e [NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Nel servizio Gestione dispositivi StorSimple, i grafici di monitoraggio del dispositivo non funzionano quando l’autenticazione di base o NTLM è abilitata nella configurazione del server proxy per il dispositivo. Per usare i grafici di monitoraggio, è necessario assicurarsi che l'autenticazione sia impostata su NESSUNO.**
  
5. Se l'autenticazione è abilitata, fornire un **nome utente del proxy Web** e la **password del proxy Web**. È necessario anche confermare la password.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 1](./media/storsimple-configure-web-proxy/IC751830.png)

Se si sta registrando il dispositivo per la prima volta, continuare con la registrazione. Se il dispositivo è già stato registrato, la procedura guidata viene chiusa. Le impostazioni configurate vengono salvate.

Il proxy Web è ora abilitato. È possibile ignorare il passaggio [Abilitare il proxy Web](#enable-web-proxy) e passare direttamente a [Visualizzare le impostazioni proxy Web nel Portale di Azure](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configurare il proxy Web tramite i cmdlet di Windows PowerShell per StorSimple

Un modo alternativo per configurare le impostazioni proxy Web consiste nell'utilizzo dei cmdlet di Windows PowerShell per StorSimple. Eseguire i passaggi seguenti per configurare il proxy Web.

#### <a name="to-configure-web-proxy-via-cmdlets"></a>Per configurare il proxy Web tramite i cmdlet
1. Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**. Quando richiesto, fornire la **password di amministratore del dispositivo**. La password predefinita è `Password1`.
2. Al prompt dei comandi digitare:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Fornire e confermare la password quando richiesto.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 3](./media/storsimple-configure-web-proxy/IC751831.png)

Il proxy Web è ora configurato e deve essere abilitato.

## <a name="enable-web-proxy"></a>Abilitare il proxy Web

Il proxy Web è disabilitato per impostazione predefinita. Dopo aver configurato le impostazioni proxy Web sul dispositivo StorSimple, usare Windows PowerShell per StorSimple per abilitare le impostazioni proxy Web.

> [!NOTE]
> **Questo passaggio non è necessario se è stata usata l'installazione guidata per configurare il proxy Web. Il proxy Web viene abilitato automaticamente per impostazione predefinita dopo una sessione dell'installazione guidata.**


Per abilitare il proxy Web sul dispositivo in Windows PowerShell per StorSimple, procedere come segue:

#### <a name="to-enable-web-proxy"></a>Per abilitare il proxy Web
1. Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**. Quando richiesto, fornire la **password di amministratore del dispositivo**. La password predefinita è `Password1`.
2. Al prompt dei comandi digitare:
   
    `Enable-HcsWebProxy`
   
    A questo punto, è stata abilitata la configurazione del proxy Web sul dispositivo StorSimple.
   
    ![Configurare il proxy Web nel dispositivo StorSimple 4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-the-azure-portal"></a>Visualizzare le impostazioni proxy Web nel portale di Azure

Le impostazioni proxy Web sono configurate tramite l'interfaccia di Windows PowerShell e non possono essere modificate nel portale. È possibile, tuttavia, visualizzare le impostazioni configurate nel portale. Eseguire i passaggi seguenti per visualizzare le impostazioni proxy Web.

#### <a name="to-view-web-proxy-settings"></a>Per visualizzare le impostazioni proxy Web
1. Passare al **servizio Gestione dispositivi StorSimple > Dispositivi**. Selezionare e fare clic su un dispositivo e quindi passare a **Impostazioni dispositivo > Rete**.

    ![Fare clic su Rete](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. Nel pannello **Impostazioni di rete** fare clic sul riquadro **Proxy Web**.

    ![Fare clic su Proxy Web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. Nel pannello **Proxy Web**, verificare le impostazioni proxy Web configurate sul dispositivo StorSimple.
   
    ![Visualizzare le impostazioni del proxy web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Errori durante la configurazione del proxy Web

Se le impostazioni proxy Web sono configurate in modo errato, verranno visualizzati messaggi di errore in Windows PowerShell per StorSimple. Nella tabella seguente sono descritti alcuni di questi messaggi di errore, le possibili cause e le azioni consigliate.

| N. di serie | Codice di errore HRESULT | Possibile causa principale | Azione consigliata |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Il comando viene eseguito dal controller passivo e non è in grado di comunicare con il controller attivo. |Eseguire il comando dal controller attivo. Per eseguire il comando dal controller passivo, sarà necessario correggere la connettività da controller passivo a controller attivo. È necessario contattare il supporto tecnico Microsoft se la connettività viene interrotta. |
| 2. |0x800710dd - L'identificatore di operazione non è valido |Le impostazioni proxy non sono supportate dall'appliance cloud StorSimple. |Le impostazioni proxy non sono supportate dall'appliance cloud StorSimple. Possono essere configurate solo in un dispositivo fisico StorSimple. |
| 3. |0x80070057 - Parametro non valido |Uno dei parametri forniti per le impostazioni proxy non è valido. |L'URI non è fornito nel formato corretto. Utilizzare il seguente formato: `http://<IP address or FQDN of the web proxy server>:<TCP port number>` |
| 4. |0x800706ba - Server RPC non disponibile |La causa principale è una delle seguenti:</br></br>Il cluster non è attivo. </br></br>Il servizio Datapath non è in esecuzione.</br></br>Il comando viene eseguito dal controller passivo e non è in grado di comunicare con il controller attivo. |Contattare il supporto tecnico Microsoft per assicurarsi che il cluster sia attivo e il servizio di percorso dati sia in esecuzione.</br></br>Eseguire il comando dal controller attivo. Se si desidera eseguire il comando dal controller passivo, è necessario verificare che il controller passivo sia in grado di comunicare con il controller attivo. È necessario contattare il supporto tecnico Microsoft se la connettività viene interrotta. |
| 5. |0X800706be - Chiamata RPC non riuscita |Cluster non attivo. |Contattare il supporto tecnico Microsoft per assicurarsi che il cluster sia attivo. |
| 6. |0x8007138f - Risorsa cluster non trovata |La risorsa cluster del servizio di piattaforma non è stata trovata. Questa situazione può verificarsi in caso di installazione non corretta. |Potrebbe essere necessario eseguire il ripristino delle impostazioni predefinite sul dispositivo. Potrebbe essere necessario creare una risorsa di piattaforma. Contattare il supporto tecnico Microsoft per i passaggi successivi. |
| 7. |0x8007138c - Risorsa cluster non online |Le risorse cluster del servizio di percorso dati o piattaforma non sono online. |Contattare il supporto tecnico Microsoft per garantire che la risorsa servizio di percorso dati e piattaforma sia online. |

> [!NOTE]
> * L'elenco dei messaggi di errore riportato sopra non è esaustivo.
> * Gli errori correlati alle impostazioni del proxy Web non vengono visualizzati nel portale di Azure del servizio Gestione dispositivi StorSimple. Se si verifica un problema con il proxy Web dopo il completamento della configurazione, lo stato del dispositivo verrà modificato in **Offline** nel portale classico.|

## <a name="next-steps"></a>Passaggi successivi
* Se si riscontrano problemi durante la distribuzione del dispositivo o la configurazione delle impostazioni proxy Web, fare riferimento a [Risoluzione dei problemi relativi alla distribuzione del dispositivo StorSimple](storsimple-troubleshoot-deployment.md).
* Per altre informazioni sull'uso del servizio Gestione dispositivi StorSimple, passare a [Uso del servizio Gestione dispositivi StorSimple per gestire il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

