---
title: aaaTroubleshooting hello-registrazione automatica del dominio di Azure AD aggiunti a un computer per i client legacy di Windows | Documenti Microsoft
description: Risoluzione dei problemi di registrazione automatica hello del dominio di Azure AD aggiunti a un computer per i client legacy di Windows.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows 

In questo argomento è applicabile toohello solo i client seguenti: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Per Windows 10 o Windows Server 2016, vedere [risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure Active Directory-i computer Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Questo argomento si presuppone di aver configurato la registrazione automatica dei dispositivi appartenenti a un dominio come descritto in descritto in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-device-registration-get-started.md).
 
In questo argomento fornisce informazioni aggiuntive su come tooresolve potenziali problemi di risoluzione dei problemi.  
Toonote alcune operazioni per i risultati positivi: 

- La registrazione di questi client su Azure AD è per utente/dispositivo. Ad esempio: se jdoe e jharnett Accedi toothis dispositivo, una registrazione separati (DeviceID) viene creata per ciascuno di questi utenti nella scheda informazioni utente di hello.  

- Registrazione di questi client non viene fornita hello è configurato tootry all'accesso o bloccare/sbloccare e si può verificare che questa azione viene attivata utilizzando un'utilità di pianificazione attività ritardo di 5 minuti. 

- La reinstallazione del sistema operativo hello o annullare la registrazione manuale e ripetere la registrazione potrebbe creare una nuova registrazione in Azure AD e determinerà più voci nella scheda informazioni utente di hello in hello portale di Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Passaggio 1: Recuperare lo stato della registrazione hello 

**stato della registrazione tooverify hello:**  

1. Hello Apri prompt dei comandi come amministratore 

2. Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.

Questo comando Visualizza una finestra di dialogo che fornisce le informazioni più dettagliate sullo stato di join di hello.

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Passaggio 2: Valutare lo stato della registrazione hello 

Se il join di hello non ha esito positivo, la finestra di dialogo hello fornisce dettagli sul problema hello che si è verificato.

**Hello i problemi più comuni sono:**

- Una configurazione errata di AD FS o Azure AD

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Non si è connessi come utente di dominio

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- È stata raggiunta una quota

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- servizio Hello non risponde 

    ![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

È inoltre possibile trovare informazioni sullo stato hello nel registro eventi di hello in **all'area di lavoro di Log\Microsoft servizi e applicazioni**.
  
**le cause più comuni per una registrazione non riuscita Hello sono:** 

- Il computer non si trova nella rete interna dell'organizzazione hello o una connessione VPN senza connessione tooan locale controller di dominio Active Directory.

- Si è connessi in computer tooyour con un account computer locale. 

- Problemi di configurazione del servizio: 

  - Hello server federativo è stato configurato toosupport **WIAORMULTIAUTHN**. 

  - È presente alcun oggetto di punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello.

  - Un utente ha raggiunto il limite di hello dei dispositivi. Vedere Introduzione a Registrazione dispositivo Azure Active Directory.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni, vedere hello [domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md) 
