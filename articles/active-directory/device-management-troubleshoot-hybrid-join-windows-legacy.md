---
title: ibrida aaaTroubleshooting Azure Active Directory aggiunti dispositivi di livello inferiore | Documenti Microsoft
description: "Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory 

In questo argomento è applicabile toohello solo i dispositivi seguenti: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Per Windows 10 o Windows Server 2016, vedere [Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).

In questo argomento si presuppone che sia [Configurazione ibrida di Azure Active Directory i dispositivi appartenenti](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport seguenti scenari:

- Accesso condizionale basato su dispositivo

- [Roaming aziendale delle impostazioni](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business) 





In questo argomento fornisce informazioni aggiuntive su come tooresolve potenziali problemi di risoluzione dei problemi.  

**Informazioni utili:** 

- numero massimo di Hello di dispositivi per utente è incentrato sui dispositivi. Ad esempio, se *jdoe* e *jharnett* tooa accesso dispositivo, una registrazione separati (DeviceID) viene creata per ognuno di essi in hello **utente** scheda informazioni.  

- Hello registrazione iniziale / unione dei dispositivi è tooperform configurato un tentativo di accesso o blocco / sblocco. Potrebbero esserci 5 minuti di ritardo causati da un'attività dell'utilità di pianificazione. 

- La reinstallazione del sistema operativo hello o un manuale di annullare la registrazione e registrare nuovamente possibile creare una nuova registrazione in Azure AD e hello di risultati in più voci nella scheda informazioni utente di hello nel portale di Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Passaggio 1: Recuperare lo stato della registrazione hello 

**stato della registrazione tooverify hello:**  

1. Hello Apri prompt dei comandi come amministratore 

2. Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.

Questo comando Visualizza una finestra di dialogo che fornisce le informazioni più dettagliate sullo stato di join di hello.

![Aggiunta all'area di lavoro per Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Passaggio 2: Valutare lo stato di join hello ibrida Azure AD 

Se l'aggiunta ad Azure AD ibrido hello non ha esito positivo, la finestra di dialogo hello fornisce dettagli sul problema hello che si è verificato.

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
  
**le cause più comuni di un join di Azure AD ibrido Hello sono:** 

- Il computer non si trova nella rete interna dell'organizzazione hello o una connessione VPN senza connessione tooan locale controller di dominio Active Directory.

- Si è connessi in computer tooyour con un account computer locale. 

- Problemi di configurazione del servizio: 

  - Hello server federativo è stato configurato toosupport **WIAORMULTIAUTHN**. 

  - È presente alcun oggetto di punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello.

  - Un utente ha raggiunto il limite di hello dei dispositivi. 

## <a name="next-steps"></a>Passaggi successivi

Per domande, vedere hello [domande frequenti sulla gestione dei dispositivi](device-management-faq.md)  
