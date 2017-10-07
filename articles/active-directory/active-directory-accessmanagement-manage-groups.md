---
title: aaaManaging gruppi in Azure Active Directory | Documenti Microsoft
description: Come toocreate e gestire gruppi toomanage Azure mediante Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Gestione dei gruppi in Azure Active Directory
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-groups-create-azure-portal.md)
> * [Portale di Azure classico](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Una delle funzionalità di hello di gestione di utenti di Azure Active Directory (Azure AD) è di gruppi di toocreate hello possibilità degli utenti. Usare le attività di gestione tooperform un gruppo, ad esempio l'assegnazione di licenze o autorizzazioni tooa numero di utenti in una sola volta. È inoltre possibile utilizzare gruppi le autorizzazioni di accesso tooassign per

* Risorse, ad esempio gli oggetti nella directory hello
* Directory delle risorse toohello esterno, ad esempio applicazioni SaaS, servizi di Azure, siti di SharePoint o alle risorse locali

Inoltre, un proprietario della risorsa può anche assegnare gruppo accesso tooa risorse tooan Azure AD di proprietà da un altro utente. Questa assegnazione concede ai membri di hello di tale risorsa toohello accesso di gruppo. Quindi, il proprietario di hello del gruppo di hello gestisce l'appartenenza al gruppo hello. In effetti, hello proprietario delegati toohello proprietario della risorsa di hello hello autorizzazione tooassign utenti tootheir risorsa del gruppo di.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per toomanage come i gruppi nel centro di amministrazione di hello Azure AD, vedere [creare un gruppo e aggiungere membri in Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Come si crea un gruppo?
A seconda di hello toowhich di servizi che sottoscritti dall'organizzazione, è possibile creare un gruppo utilizzando uno dei seguenti hello:

* Hello portale di Azure classico
* portale per gli account Office 365 Hello
* portale di account Windows Intune Hello

Verranno descritti attività come avviene nel portale di Azure classico hello. Per ulteriori informazioni sull'uso di directory di Azure AD toomanage portali non Azure, vedere [amministrazione della directory di Azure AD](active-directory-administer.md).

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**, quindi selezionare hello nome della directory hello per l'organizzazione.
2. Seleziona hello **gruppi** scheda.
3. Selezionare **Aggiungi gruppo**.
4. In hello **Aggiungi gruppo** finestra, specificare il nome di hello e hello descrizione di un gruppo.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Come aggiungere o rimuovere singoli utenti in un gruppo di sicurezza?
**un gruppo di singolo utente tooa tooadd**

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**, quindi selezionare hello nome della directory hello per l'organizzazione.
2. Seleziona hello **gruppi** scheda.
3. Aprire hello toowhich di gruppo che si desidera tooadd membri. Aprire hello **membri** scheda di hello selezionato gruppo se è non è già visualizzato.
4. Selezionare **Aggiungi membri**.
5. In hello **Aggiungi membri** pagina, il nome di hello selezionare dell'utente di hello o un gruppo che si vuole tooadd come un membro di questo gruppo. Assicurarsi che questo nome viene aggiunto toohello **selezionati** riquadro.

**tooremove un singolo utente da un gruppo**

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**, quindi selezionare hello nome della directory hello per l'organizzazione.
2. Seleziona hello **gruppi** scheda.
3. Aprire gruppo hello da cui si desidera consentire ai membri tooremove.
4. Seleziona hello **membri** scheda, nome selezionare hello del membro di hello che desidera tooremove da questo gruppo e quindi fare clic su **rimuovere**.
5. Confermare al prompt dei comandi hello tooremove questo membro dal gruppo hello.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Come è possibile gestire l'appartenenza di hello di un gruppo in modo dinamico?
In Azure AD, è possibile impostare in modo molto semplice toodetermine una semplice regola gli utenti che sono membri di toobe del gruppo di hello. Una regola semplice è una regola che esegue un solo confronto. Ad esempio, se tooa applicazione SaaS è assegnato a un gruppo, è possibile impostare una regola tooadd utenti che dispongono di una posizione di "Sales Rep". Questa regola concede quindi l'accesso utenti tooall di applicazioni SaaS toothis con tale titolo nella directory.

Quando gli attributi di una modifica dell'utente, sistema di hello valuta tutte le regole del gruppo dinamico in una directory di toosee se Modifica attributo hello dell'utente hello comportava l'attivazione di qualsiasi gruppo aggiunge o rimuove. Se un utente soddisfa una regola in un gruppo, vengono aggiunti come gruppo toothat membro. Se non è più soddisfano la regola hello di un gruppo che sono membri di, questi vengono rimossi come un tipo di membri dal gruppo.

> [!NOTE]
> È possibile configurare una regola per l'appartenenza dinamica nei gruppi di sicurezza o nei gruppi di Office 365. Appartenenze a gruppi nidificati non sono attualmente supportate per l'assegnazione basata su gruppo tooapplications.
>
> Appartenenza dinamica ai gruppi richiedono un toobe di licenza di Azure AD Premium assegnato a
>
> * messaggio per l'amministratore che gestisce la regola hello in un gruppo
> * Tutti i membri del gruppo di hello
>
>

**tooenable dell'appartenenza dinamica per un gruppo**

1. In hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **Active Directory**, quindi selezionare hello nome della directory hello per l'organizzazione.
2. Seleziona hello **gruppi** scheda e aprire hello gruppo tooedit.
3. Seleziona hello **configura** scheda e quindi impostare **Abilita appartenenze dinamiche** troppo**Sì**.
4. Impostare una singola regola semplice per hello gruppo toocontrol funzionamento dell'appartenenza dinamica per questo gruppo. Verificare che hello **aggiungere utenti in cui** opzione è selezionata e quindi selezionare una proprietà dell'utente dall'elenco di hello (ad esempio, department, jobTitle, ecc.)
5. Selezionare una condizione (Non uguale a, Uguale a, Non inizia con, Inizia con, Non contiene, Contiene, Non corrispondente, Corrispondente).
6. Specificare un valore di confronto per la proprietà utente hello selezionato.

toolearn sulla toocreate *avanzate* regole, che può contenere più confronti, per l'appartenenza dinamica ai gruppi, vedere [utilizzando attributi toocreate regole avanzate](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Informazioni aggiuntive
Questi articoli forniscono informazioni aggiuntive su Azure Active Directory.

* [Gestione di accesso tooresources con gruppi di Azure Active Directory](active-directory-manage-groups.md)
* [Cmdlet di Azure Active Directory per la configurazione delle impostazioni di gruppo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Informazioni su Azure Active Directory](active-directory-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
