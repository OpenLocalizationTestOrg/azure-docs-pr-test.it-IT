---
title: 'Azure AD Connect: Abilitazione del writeback dei dispositivi | Documentazione Microsoft'
description: Questo documento come dettagli tooenable writeback dei dispositivi con Azure AD Connect
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: abilitazione del writeback dei dispositivi
> [!NOTE]
> TooAzure una sottoscrizione AD Premium è necessario per il writeback dei dispositivi.
> 
> 

Hello seguente documentazione vengono fornite informazioni sulla modalità di funzionalità di writeback dei dispositivi tooenable hello in Azure AD Connect. Writeback dei dispositivi viene utilizzato nei seguenti scenari hello:

* Abilitare l'accesso condizionale in base a dispositivi tooADFS (2012 R2 o versione successiva) protetti applicazioni (trust della relying party).

Questo offre sicurezza aggiuntiva e garanzia che accedono a tooapplications viene concessa solo ai dispositivi tootrusted. Per altre informazioni sull'accesso condizionale, vedere [Gestione dei rischi con l'accesso condizionale](../active-directory-conditional-access.md) e [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Dispositivi devono essere posizionati nella stessa foresta come utenti hello hello. Poiché i dispositivi devono essere riscritte tooa singola foresta, questa funzionalità non supporta attualmente una distribuzione con più foreste di utente.</li>
> <li>Oggetti di configurazione di un solo dispositivo registrazione può essere aggiunto toohello foresta di Active Directory locale. Questa funzionalità non è compatibile con una topologia in cui hello locale Active Directory è toomultiple sincronizzato Azure Active Directory.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Parte 1: Installare Azure AD Connect
1. Installare Azure AD Connect usando le impostazioni personalizzate o rapide Microsoft consiglia di toostart con tutti gli utenti e gruppi di sincronizzazione completata prima di abilitare il writeback di dispositivi.

## <a name="part-2-prepare-active-directory"></a>Parte 2: Preparare Active Directory
Utilizzare hello seguendo i passaggi tooprepare per l'utilizzo di writeback dei dispositivi.

1. Dalla macchina di hello in cui è installato Azure AD Connect, avviare PowerShell con privilegi elevati.
2. Se il modulo di Active Directory PowerShell hello non è installato, installarlo utilizzando hello comando seguente:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Se non è installato il modulo di Azure Active Directory PowerShell hello, quindi scaricare e installare da [modulo di Azure Active Directory per Windows PowerShell (versione a 64 bit)](http://go.microsoft.com/fwlink/p/?linkid=236297). Questo componente presenta una dipendenza hello Assistente per l'accesso, che viene installato con Azure AD Connect.
4. Con credenziali di amministratore dell'organizzazione, eseguire hello i comandi seguenti e quindi uscire da PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Credenziali amministratore dell'organizzazione sono necessarie perché lo spazio dei nomi di modifiche toohello configurazione sono necessari. Le autorizzazioni di un amministratore di dominio non sono sufficienti.

![PowerShell per l'abilitazione del writeback dei dispositivi](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Descrizione:

* Se non esistono già, crea e configura nuovi contenitori e oggetti in CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].
* Se non esistono già, crea e configura nuovi contenitori e oggetti in CN=RegisteredDevices,[domain-dn]. Gli oggetti dispositivo verranno creati in questo contenitore.
* Imposta le autorizzazioni necessarie su hello account Azure Active Directory Connector, dispositivi toomanage in Active Directory.
* È sufficiente toorun in una foresta, anche se Azure AD Connect viene installato su più foreste.

Parametri

* DomainName: dominio di Active Directory in cui verranno creati gli oggetti dispositivo. Nota: tutti i dispositivi per una foresta Active Directory specifica verranno creati in un singolo dominio.
* AdConnectorAccount: Account di Active Directory che verrà utilizzato da Azure AD Connect toomanage oggetti nella directory hello. Si tratta di account hello utilizzato dal tooAD tooconnect di sincronizzazione Azure AD Connect. Se è stato installato utilizzando le impostazioni express, si tratta di account di hello preceduti MSOL_.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Parte 3: Abilitare il writeback dei dispositivi in Azure AD Connect
Utilizzare hello seguendo procedure tooenable writeback dei dispositivi in Azure AD Connect.

1. Eseguire nuovamente l'installazione guidata di hello. Selezionare **personalizzare le opzioni di sincronizzazione** dall'attività aggiuntive di hello pagina e fare clic su **Avanti**.
   ![Installazione personalizzata - Personalizzazione delle opzioni di sincronizzazione](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Nella pagina di funzionalità facoltative hello writeback dei dispositivi non sono disattivati. Si noti che se hello passaggi di preparazione di Azure AD Connect non vengano completati verranno disattivate nella pagina di funzionalità facoltative di hello writeback dei dispositivi. Selezionare la casella hello per il writeback dei dispositivi e fare clic su **Avanti**. Se è ancora disabilitata hello casella di controllo, vedere hello [risoluzione dei problemi di sezione](#the-writeback-checkbox-is-still-disabled).
   ![Installazione personalizzata - Funzionalità facoltative di writeback dei dispositivi](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Nella pagina di hello writeback, si vedrà dominio hello fornito come insieme di strutture di hello predefinito dispositivo writeback.
   ![Installazione personalizzata - Foresta di destinazione del writeback dei dispositivi](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Completare l'installazione di hello di hello procedura guidata senza apportare modifiche di configurazione aggiuntive. Se necessario, fare riferimento troppo[installazione personalizzata di Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Abilitare l'accesso condizionale
Istruzioni dettagliate tooenable questo scenario sono disponibili all'interno di [configurare l'accesso condizionale locale con Azure Active Directory Device Registration](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Verificare che i dispositivi siano sincronizzati tooActive Directory
Il writeback dei dispositivi dovrebbe funzionare correttamente. Tenere presente che può richiedere ore too3 dispositivo oggetti toobe writeback tooAD.  tooverify che i dispositivi da sincronizzare correttamente, hello seguente dopo il completamento di regole di sincronizzazione hello:

1. Avviare il Centro di amministrazione di Active Directory.
2. Espandere RegisteredDevices, all'interno di hello dominio viene federato.
   ![Interfaccia di amministrazione di Active Directory - Dispositivi registrati](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. I dispositivi attualmente registrati saranno visualizzati in questo elenco.
   ![Interfaccia di amministrazione di Active Directory - Elenco dei dispositivi registrati](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="hello-writeback-checkbox-is-still-disabled"></a>Hello writeback checkbox rimane disabilitato.
Se la casella di controllo di hello per writeback dei dispositivi non è abilitato, anche se sono state eseguite operazioni hello precedente, hello alla procedura seguente consentirà di tramite installazione quali hello verifica in corso prima casella hello è abilitata.

Attività iniziali:

* Assicurarsi che almeno una foresta disponga di Windows Server 2012 R2. tipo di oggetto dispositivo Hello deve essere presente.
* Se l'installazione guidata di hello è già in esecuzione, le modifiche non venga rilevate. In questo caso, completare l'installazione guidata di hello ed eseguirlo nuovamente.
* Assicurarsi che l'account hello fornito nello script di inizializzazione hello è effettivamente hello corretto utente utilizzato da Active Directory Connector hello. tooverify, seguire questi passaggi:
  * Dal menu di avvio hello, aprire **servizio di sincronizzazione**.
  * Aprire hello **connettori** scheda.
  * Trovare hello connettore con tipo di servizi di dominio Active Directory e selezionarlo.
  * In **Azioni** selezionare **Proprietà**.
  * Andare troppo**connettersi foresta Directory tooActive**. Verificare che hello dominio e il nome utente specificato sullo schermo corrispondenza hello account fornito toohello script.
    ![Account connettore in Synchronization Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Verificare la configurazione in Active Directory:

* Verificare che hello Device Registration Service si trova nel percorso di hello seguente (CN DeviceRegistrationService, CN = = dispositivo registrazione Services, CN = Device Registration Configuration, CN = Services, CN = Configuration) nel contesto dei nomi di configurazione.

![Risoluzione dei problemi, DeviceRegistrationService nello spazio dei nomi di configurazione](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Verificare sia presente un solo oggetto di configurazione eseguendo una ricerca di spazio dei nomi di configurazione hello. Se è presente più di uno, eliminare duplicato hello.

![Risoluzione dei problemi, eseguire la ricerca di oggetti duplicati hello](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Oggetto servizio Registrazione dispositivi di hello, assicurarsi che hello attributo msDS-DeviceLocation è presente e ha un valore. Ricerca il percorso e assicurarsi che è presente con hello objectType msDS-DeviceContainer.

![Risoluzione dei problemi, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Risoluzione dei problemi, classe di oggetti RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Verificare l'account hello utilizzato da hello che Active Directory Connector dispone delle autorizzazioni necessarie per il contenitore di dispositivi registrati hello trovato dal passaggio precedente hello. Si tratta delle autorizzazioni di hello previsto per questo contenitore:

![Risoluzione dei problemi, verificare le autorizzazioni per il contenitore](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Verificare hello account Active Directory disponga delle autorizzazioni su hello CN = Device Registration Configuration, CN = Services, CN = oggetto di configurazione.

![Risoluzione dei problemi, verificare le autorizzazioni per la configurazione della registrazione dispositivo](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Informazioni aggiuntive
* [Gestione dei rischi con l'accesso condizionale](../active-directory-conditional-access.md)
* [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).

