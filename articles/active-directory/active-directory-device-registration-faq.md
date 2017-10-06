---
title: domande frequenti sulla registrazione automatica dei dispositivi di Active Directory aaaAzure | Documenti Microsoft
description: Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory.
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
ms.openlocfilehash: ba7f113fd3bc310def001a1f44d938b0be71dba8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a>Domande frequenti sulla registrazione automatica dei dispositivi con Azure Active Directory

**D: registrazione dispositivo di hello recentemente. Impossibile visualizzare dispositivo hello in mie info di utente nel portale di Azure hello?**

**R:** i dispositivi Windows 10 che appartengono a un dominio con la registrazione automatica del dispositivo non vengono visualizzati nelle informazioni utente hello.
È necessario toouse PowerShell toosee tutti i dispositivi. 

Solo hello dispositivi seguenti sono elencati sotto informazioni utente hello:

- Tutti i dispositivi personali non aggiunti a un dominio aziendale 
- Tutti i dispositivi non Windows 10/Windows Server 2016 
- Tutti i dispositivi non Windows 

---

**D: perché non visualizzare tutti i dispositivi di hello registrati in Azure Active Directory nel portale di Azure hello?** 

**R:** attualmente non è disponibile alcun toosee modo tutti i dispositivi registrati in hello portale di Azure. È possibile usare Azure PowerShell toofind tutti i dispositivi. Per ulteriori informazioni, vedere hello [Get MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.

--- 

**D: come si capisce quali lo stato di registrazione dispositivo hello del client hello è?**

**R:** varia a seconda dello stato di registrazione dispositivo hello:

- Il dispositivo hello è
- Modalità di registrazione 
- I dettagli correlati tooit. 
 

---

**D: perché è un dispositivo eliminato in hello Azure portal o con Windows PowerShell ancora elencati come registrato?**

**A:** Si tratta di un comportamento previsto da progettazione. dispositivo Hello non avranno accesso tooresources nel cloud hello. Se si desidera tooremove hello dispositivo e ripetere la registrazione, un'azione manuale deve essere eseguita sul dispositivo hello toobe. 

Per i dispositivi Windows 10 e Windows Server 2016 aggiunti a un dominio AD locale:

1.  Aprire il prompt dei comandi di hello come amministratore.

2.  Digitare `dsregcmd.exe /debug /leave`.

3.  Disconnetti e Accedi tootrigger hello attività pianificata che registra il dispositivo hello nuovamente. 

Per altre piattaforme Windows aggiunte a un dominio AD locale:

1.  Aprire il prompt dei comandi di hello come amministratore.
2.  Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.
3.  Digitare `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.

---

**D: Perché vengono visualizzate voci di dispositivo duplicate nel portale di Azure?**

**R:**

-   Per Windows 10 e Windows Server 2016, se vengono ripetuti tentativi toounjoin e aggiungere nuovamente hello stesso dispositivo, potrebbero essere presenti voci duplicate. 

-   Se si utilizza Aggiungi Account aziendale o dell'istituto di istruzione, ogni utente di windows che utilizza Aggiungi Account aziendale o dell'istituto di istruzione verrà creato un nuovo record di dispositivo con hello dello stesso nome dispositivo.

-   Altre piattaforme di Windows che sono locali AD appartenenti a un dominio utilizzando la registrazione automatica verrà creato un nuovo record di dispositivo con hello dello stesso nome di dispositivo per ogni utente di dominio che accede al dispositivo hello. 

-   Una macchina AADJ che è stata cancellata, reinstallato e nuovamente aggiunti con hello stesso nome, verrà visualizzato come un altro record con hello dello stesso nome dispositivo.

---

**D: perché è un utente ancora accedere alle risorse da un dispositivo che è stato disabilitato in hello portale di Azure?**

**R:** può richiedere fino a ora tooan per un toobe revoke applicato.

>[!Note] 
>Per i dispositivi persi, è consigliabile cancellazione hello dispositivo tooensure che gli utenti non possono accedere dispositivo hello. Per altre informazioni, vedere , vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune). 


---

**D: Perché viene visualizzato un messaggio che avvisa dell'impossibilità di raggiungere un determinato dispositivo?**

**R:** se è stato configurato determinati toorequire di regole di accesso condizionale uno stato di dispositivi specifici e hello dispositivo non soddisfa i criteri di hello, gli utenti vengono bloccati e visualizzare questo messaggio. Valutazione delle regole di hello e verificare che il dispositivo hello è in grado di toomeet hello criteri tooavoid questo messaggio.

---


**D: Vedere record del dispositivo hello nelle informazioni utente hello in hello portale di Azure e visualizzare lo stato di hello registrate nel client hello. La configurazione è corretta per l'uso dell'accesso condizionale?**

**R:** record del dispositivo hello (deviceID) e stato nel portale di Azure hello deve corrispondere client hello e soddisfare i criteri di valutazione per l'accesso condizionale. Per altre informazioni, vedere [Introduzione a Registrazione dispositivo Azure Active Directory](active-directory-device-registration.md).

---

**D: perché viene visualizzato un messaggio "nome utente o password non corretta" per un dispositivo è stato appena entrato tooAzure AD?**

**R:** Di seguito vengono elencati alcuni motivi comuni per questo scenario:

- Le credenziali dell'utente non sono più valide.

- Il computer è Impossibile toocommunicate con Azure Active Directory. Verificare la presenza di eventuali problemi di connettività di rete.

- non sono stati soddisfatti i prerequisiti aggiunta ad Azure AD Hello. Verificare di aver eseguito i passaggi di hello per [estensione cloud dispositivi tooWindows 10 funzionalità tramite Azure Active Directory Join](active-directory-azureadjoin-overview.md).  

- Gli account di accesso federato richiede il toosupport server federativo un endpoint attivo WS-Trust. 

---

**D: perché vedere hello "... si è verificato un errore!" finestra di dialogo quando si tenta di aggiungere il PC?**

**R:** La finestra viene visualizzata quando si registra Azure Active Directory con Intune. Per altri dettagli, vedere [Configurare la gestione dei dispositivi Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).  

---

**D: perché non è stato toojoin il tentativo di un PC non riuscire anche se non ho ricevuto le informazioni di errore?**

**R:** una causa probabile è che l'utente hello viene registrato nel dispositivo toohello utilizzando l'account predefinito administrator hello. Creare un account locale diverso prima di usare Azure Active Directory Join toocomplete hello il programma di installazione. 

---

**D: dove è possibile trovare istruzioni per l'installazione di hello di registrazione automatica dei dispositivi?**

**R:** per istruzioni dettagliate, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

---

**D: dove posso trovare la risoluzione dei problemi informazioni sulla registrazione automatica dei dispositivi hello?**

**R:** Per informazioni sulla risoluzione dei problemi, vedere:

- [Risoluzione dei problemi di registrazione automatica del dominio aggiunti a un computer tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)

- [Risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

