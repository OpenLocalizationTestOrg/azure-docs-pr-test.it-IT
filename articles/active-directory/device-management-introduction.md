---
title: gestione toodevice aaaIntroduction in Azure Active Directory | Documenti Microsoft
description: Informazioni su come la gestione dei dispositivi consente un controllo tooget dei dispositivi hello che accedono alle risorse nell'ambiente in uso.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Gestione toodevice introduzione in Azure Active Directory

In un ambiente mobile-first, prima di cloud, Azure Active Directory (Azure AD) consente di single sign-on toodevices, applicazioni e servizi da qualsiasi posizione. Con la proliferazione di hello di dispositivi, tra cui BYOD Bring Your Own Device (), i professionisti IT devono affrontare due obiettivi opposti:

- Consentire toobe gli utenti finali di hello produttivi ovunque e
- Proteggere le risorse aziendali hello in qualsiasi momento

Tramite i dispositivi, gli utenti ottengono accesso risorse aziendali tooyour. tooprotect risorse aziendali, come un amministratore IT, si desidera controllare toohave questi dispositivi. In questo modo toomake assicurarsi che gli utenti accede alle risorse dai dispositivi che soddisfano gli standard di sicurezza e conformità. 

Gestione dei dispositivi è inoltre foundation hello per [accesso condizionale basato su dispositivo](active-directory-conditional-access-policy-connected-applications.md). Con accesso condizionale basato su dispositivi, è possibile garantire che tooresources nell'ambiente in uso è possibile solo con accesso dispositivo attendibile.   

Questo argomento illustra il funzionamento della gestione dei dispositivi in Azure Active Directory.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Dispositivi sotto controllo hello di Azure AD

tooget un dispositivo sotto controllo hello di Azure AD, sono disponibili due opzioni:

- Registrazione 
- Aggiunta

**Registrazione** tooAzure un dispositivo AD consente si toomanage identità di un dispositivo. Quando un dispositivo viene registrato, registrazione dispositivo di Azure AD fornisce dispositivo hello con un'identità che è un dispositivo di hello tooauthenticate utilizzato quando un utente accede tooAzure Active Directory. È possibile utilizzare hello identità tooenable o disattivare un dispositivo.

Se combinato con una soluzione di management(MDM) di dispositivi mobili, ad esempio Microsoft Intune, sugli attributi del dispositivo hello in Azure AD vengono aggiornati con informazioni aggiuntive sul dispositivo di hello. Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità. Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere Registrare i dispositivi per la gestione in Intune.

**Unione di** un dispositivo è un tooregistering estensione un dispositivo. Ciò significa, esso consente di tutti i vantaggi di hello della registrazione di un dispositivo in toothis aggiunta, modifica inoltre lo stato locale di hello di un dispositivo. Modifica dello stato locale hello consente il dispositivo tooa toosign-in utenti utilizzando un organizzazione account aziendale o dell'istituto di istruzione anziché un account personale.

## <a name="azure-ad-registered-devices"></a>Dispositivi registrati in Azure AD   

obiettivo di dispositivi AD Azure registrata Hello è tooprovide è con il supporto per hello **BYOD Bring Your Own Device ()** scenario. In questo scenario un utente può accedere alle risorse dell'organizzazione controllate da Azure Active Directory usando un dispositivo personale.  

![Dispositivi registrati in Azure AD](./media/device-management-introduction/03.png)

accesso Hello è basata su un account aziendale o dell'istituto di istruzione che è stata immessa nel dispositivo hello.  
Ad esempio, Windows 10 consente tooadd agli utenti un lavoro o scuola account tooa per PC, tablet o telefono.  
Quando un utente ha aggiunto un account aziendale o dell'istituto di istruzione, il dispositivo hello è registrato con Azure AD e facoltativamente registrato nel sistema di gestione (MDM) di dispositivi mobili hello che l'organizzazione ha configurato. Aggiungere un lavoro agli utenti dell'organizzazione o dell'istituto di istruzione convenientemente dispositivo personale tooa di account:

- Quando si accede a un'applicazione di lavoro per hello prima volta
- Manualmente tramite hello **impostazioni** menu nel caso di hello di Windows 10 

È possibile configurare dispositivi registrati in Azure AD per Windows 10, iOS, Android e macOS.

## <a name="azure-ad-joined-devices"></a>Dispositivi aggiunti ad Azure AD

obiettivo di Hello dei dispositivi di Azure AD aggiunti è toosimplify:

- Distribuzioni Windows di dispositivi di proprietà dell'azienda 
- Accesso alle App tooorganizational e risorse da qualsiasi dispositivo Windows

![Dispositivi registrati in Azure AD](./media/device-management-introduction/02.png)


Questi obiettivi, vengono eseguiti da fornire agli utenti un'esperienza self-service per ottenere i dispositivi di proprietà lavoro sotto controllo hello di Azure AD.  
L'**aggiunta ad Azure AD** è destinata alle organizzazioni basate prima di tutto o esclusivamente sul cloud. Si tratta in genere piccole e medie imprese che non hanno un'infrastruttura Active Directory di Windows Server locale. 

Implementazione di dispositivi AD Azure unita in join vengono hello seguenti vantaggi:

- **Single Sign-On (SSO)** tooyour Azure gestito App SaaS e servizi. Gli utenti non visualizzano richieste di autenticazione aggiuntive quando accedono alle risorse. Hello funzionalità SSO è anche quando non sono connessi toohello rete di dominio disponibili.

- **Roaming conforme ai criteri dell'organizzazione** per le impostazioni utente tra dispositivi aggiunti. Gli utenti non devono tooconnect le impostazioni di toosee un Microsoft account (ad esempio Hotmail) tra i dispositivi.

- **Accesso tooWindows Store per le aziende** utilizzando l'account di Active Directory. Gli utenti possono scegliere da un inventario delle applicazioni pre-selezionata dall'organizzazione hello.

- **Windows Hello** supporto per le risorse toowork accesso sicuro e pratico.

- **Limitazione dell'accesso** tooapps da solo i dispositivi che soddisfano i criteri di conformità.

Anche se l'aggiunta ad Azure AD è destinata soprattutto alle organizzazioni prive di un'infrastruttura Active Directory di Windows Server locale, è ovviamente possibile usarla anche in scenari in cui:

- È possibile utilizzare un'aggiunta al dominio locale, ad esempio, se è necessario tooget di dispositivi mobili come Tablet e telefoni nel controllo.

- Gli utenti devono principalmente tooaccess Office 365 o altre applicazioni SaaS integrate con Azure AD.

- Si desidera toomanage un gruppo di utenti in Azure Active Directory anziché in Active Directory. Questo è applicabile, ad esempio, lavoratori tooseasonal, collaboratori o studenti.

- Si desidera tooprovide tooworkers funzionalità di unione nelle succursali remote con l'infrastruttura locale limitato.

È possibile configurare dispositivi aggiunti ad Azure AD per dispositivi Windows 10.


## <a name="hybrid-azure-ad-joined-devices"></a>Dispositivi aggiunti all'identità ibrida di Azure AD

Per più di dieci anni, molte organizzazioni hanno utilizzato hello dominio join tootheir locale Active Directory tooenable:

- IT reparti toomanage lavoro dispositivi di proprietà da una posizione centrale.

- Gli utenti toosign nei dispositivi tootheir con Active Directory di lavoro o scuola account. 

In genere, le organizzazioni con un footprint locale si basano su metodi tooprovision periferiche e utilizzano spesso **System Center Configuration Manager (SCCM)** o **(GP) di criteri di gruppo** toomanage essi.

Se l'ambiente comprende una locale footprint di Active Directory e si desiderano anche vantaggi offerti dalla funzionalità hello fornite da Azure Active Directory, è possibile implementare i dispositivi di Azure AD unita in join ibrido. Si tratta di dispositivi che sono entrambi, unita in join tooyour Active Directory locale e Azure Active Directory.

![Dispositivi registrati in Azure AD](./media/device-management-introduction/01.png)


È consigliabile usare dispositivi aggiunti all'identità ibrida di Azure AD se:

- Si dispone Win32 App distribuito toothese dispositivi che utilizzano l'autenticazione NTLM o Kerberos.

- È necessario criteri di gruppo o SCCM / dispositivi toomanage DCM.

- Si desidera toocontinue toouse imaging soluzioni tooconfigure dispositivi per i dipendenti.

È possibile configurare dispositivi aggiunti all'identità ibrida di Azure AD per Windows 10 e dispositivi di livello inferiore, ad esempio Windows 8 e Windows 7.

## <a name="summary"></a>Riepilogo

Con la gestione dei dispositivi in Azure AD, è possibile: 

- Semplificare il processo di hello di riportare i dispositivi sotto controllo hello di Azure AD

- Fornire agli utenti con le risorse basate su cloud toouse facile accesso tooyour di un'organizzazione

Come regola generale, è consigliabile usare:

- Dispositivi registrati in Azure AD per i dispositivi personali

- Azure AD unita in join i dispositivi per i dispositivi non aggiunti a un tooan AD locale 

- Azure AD ibrido unita in join i dispositivi per i dispositivi che vengono aggiunti a un tooan AD locale     




## <a name="next-steps"></a>Passaggi successivi

- una panoramica delle modalità dispositivo toomanage in hello Azure portale, vedere tooget [gestendo i dispositivi con hello portale di Azure](device-management-azure-portal.md)

- toolearn ulteriori informazioni sull'accesso condizionale basato su dispositivi, vedere [configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

- dispositivi di Azure AD aggiunti toosetup ibride, vedere [modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi](device-management-hybrid-azuread-joined-devices-setup.md).


