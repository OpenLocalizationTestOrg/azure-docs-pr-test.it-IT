---
title: "aaaYou non è possibile accedervi da qui in hello portale di Azure da un dispositivo Windows | Documenti Microsoft"
description: "Informazioni su dove non è possibile da qui arriva da get e ciò che è possibile controllare tooavoid in esecuzione in questa finestra di dialogo."
services: active-directory
keywords: accesso condizionale basato su dispositivo, registrazione dispositivo, abilitare registrazione dispositivo, registrazione dispositivo e software MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Messaggio "Non è possibile accedervi da qui" in un dispositivo Windows

Durante un tentativo di accedere ad esempio alla Intranet SharePoint Online dell'organizzazione può essere visualizzata una pagina con il messaggio *Non è possibile accedervi da qui*. Viene visualizzata questa pagina perché l'amministratore ha configurato un criterio di accesso condizionale che impedisce l'accesso tooyour risorse aziendali in determinate condizioni. Anche se potrebbe essere necessario toocontact helpdesk o l'amministratore tooget risolto questo problema, esistono alcuni aspetti, che è possibile provare manualmente, prima di tutto.

Se si utilizza un **Windows** dispositivo, è consigliabile controllare hello seguenti:

- Il browser usato è supportato?

- Viene eseguita una versione supportata di Windows nel dispositivo?

- Il dispositivo è conforme?






## <a name="supported-browser"></a>Browser supportati

Se l'amministratore ha configurato un criterio di accesso condizionale, è possibile accedere alle risorse dell'organizzazione solo usando un browser supportato. In un dispositivo Windows sono supportati solo **Internet Explorer** ed **Microsoft Edge**.

È possibile identificare facilmente se è Impossibile accedere a una risorsa a causa del browser non supportata tooan osservando hello dettagli sezione della pagina di errore hello:

![Messaggi "Non è possibile accedervi da qui" per browser non supportati](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")

monitoraggio e aggiornamento solo di Hello è toouse un browser che supporta l'applicazione hello per la piattaforma del dispositivo. Per un elenco completo dei browser supportati, vedere [Browser supportati](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).  


## <a name="supported-versions-of-windows"></a>Versioni di Windows supportate

esempio Hello deve essere soddisfatte sul sistema operativo di Windows hello nel dispositivo: 

- Se si esegue un sistema operativo desktop di Windows sul dispositivo, è necessario toobe Windows 7 o versioni successive.
- Se si esegue un sistema operativo Windows server nel dispositivo, è necessario toobe Windows Server 2008 R2 o versioni successive. 


## <a name="compliant-device"></a>Dispositivo conforme

L'amministratore potrebbe aver configurato un criterio di accesso condizionale che consente accesso tooyour risorse aziendali solo da dispositivi conformi. Active Directory locale toobe conforme, che il dispositivo deve essere uno tooyour unita in join o aggiunto tooyour Azure Active Directory.

È possibile identificare facilmente se è possibile accedere a una risorsa a causa di dispositivo tooa che non è conforme con la ricerca nella sezione dettagli hello hello della pagina di errore:
 
![Messaggi "Non è possibile accedervi da qui" per dispositivi non registrati](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>È tooan i dispositivi aggiunti a un Active Directory locale?

**Se si aggiunge il dispositivo tooan locale di Active Directory dell'organizzazione:**

1. Assicurarsi di eseguire l'accesso tooWindows utilizzando l'account aziendale (l'account di Active Directory).
2. Connettersi alla rete aziendale tramite una rete privata virtuale (VPN) o DirectAccess tooyour.
3. Dopo essersi connessi, premere il tasto logo Windows hello + toolock chiave hello L la sessione di Windows.
4. Sbloccare la sessione di Windows immettendo le credenziali dell'account aziendale.
5. Attendere alcuni minuti e riprovare in seguito tooaccess hello applicazione o servizio.
6. Se viene visualizzato hello stessa pagina, fare clic su hello **ulteriori dettagli** collegamento e quindi contattare l'amministratore con i dettagli di hello.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>È tooan il dispositivo non unito in join Active Directory locale?

Se non è stato aggiunto il dispositivo tooan Active Directory locale e viene eseguito Windows 10, sono disponibili due opzioni:

* Eseguire l'aggiunta ad Azure AD
* Aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account

Per informazioni sulle differenze tra queste opzioni, vedere [Uso di dispositivi Windows 10 in azienda](active-directory-azureadjoin-windows10-devices.md).  
Se il dispositivo:

- Appartiene tooyour organizzazione, è consigliabile eseguire l'aggiunta di Azure AD.
- È un dispositivo personale o un dispositivo Windows phone, è necessario aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account 



#### <a name="azure-ad-join-on-windows-10"></a>Aggiunta ad Azure AD in Windows 10

Hello toojoin passaggi sono i tooAzure dispositivo AD legati versione hello di Windows 10 in esecuzione su di esso. versione di hello toodetermine del sistema operativo Windows 10, eseguire hello **winver** comando: 

![Versione di Windows](./media/active-directory-conditional-access-device-remediation/03.png )


**Windows 10 Anniversary Update (versione 1607):**

1. Aprire hello **impostazioni** app.
2. Fare clic su **Account** > **Accedi all'azienda o all'istituto di istruzione**.
3. Fare clic su **Connetti**.
4. Fare clic su **Join questa tooAzure dispositivo AD**.
5. Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.
6. Disconnettersi e quindi eseguire l'accesso con l'account aziendale.
7. Provare di nuovo un'applicazione hello tooaccess.

**Aggiornamento di novembre 2015 di Windows 10 (versione 1511):**

1. Aprire hello **impostazioni** app.
2. Fare clic su **Sistema** > **Informazioni**.
3. Fare clic su **Aggiungi ad Azure AD**.
4. Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.
5. Disconnettersi e quindi eseguire l'accesso con l'account aziendale (l'account Azure AD).
6. Provare di nuovo un'applicazione hello tooaccess.


#### <a name="workplace-join-on-windows-81"></a>Workplace Join in Windows 8.1

Se il dispositivo non è aggiunto al dominio e viene eseguito Windows 8.1, toodo un'area di lavoro e registrarsi in Microsoft Intune, hello i passaggi seguenti:

1. Aprire **Impostazioni PC**.
2. Fare clic su **Rete** > **Rete aziendale**.
3. Fare clic su **Accedi**.
4. Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.
5. Fare clic su **Attiva**.
6. Provare di nuovo un'applicazione hello tooaccess.



#### <a name="add-your-work-or-school-account-toowindows"></a>Aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account 


**Windows 10 Anniversary Update (versione 1607):**

1. Aprire hello **impostazioni** app.
2. Fare clic su **Account** > **Accedi all'azienda o all'istituto di istruzione**.
3. Fare clic su **Connetti**.
4. Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.
5. Provare di nuovo un'applicazione hello tooaccess.


**Aggiornamento di novembre 2015 di Windows 10 (versione 1511):**

1. Aprire hello **impostazioni** app.
2. Fare clic su **Account** > **Your accounts** (Account personali).
3. Fare clic su **Aggiungi account aziendale o dell'istituto di istruzione**.
4. Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.
5. Provare di nuovo un'applicazione hello tooaccess.





## <a name="next-steps"></a>Passaggi successivi
[Accesso condizionale di Azure Active Directory](active-directory-conditional-access.md)

