---
title: aaaCustomizing i mapping degli attributi di Active Directory di Azure | Documenti Microsoft
description: "Conoscere il mapping degli attributi per le applicazioni SaaS in Azure Active Directory come è possibile modificarle tooaddress l'azienda necessita."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a>Personalizzazione dei mapping degli attributi del provisioning degli utenti per le applicazioni SaaS in Azure Active Directory
Microsoft Azure AD fornisce supporto per applicazioni SaaS di terze parti toothird come Salesforce, Google Apps e altre di provisioning dell'utente. Se si dispone di un'applicazione SaaS di terze parti abilitata il provisioning degli utenti, hello portale di gestione di Azure controlla i valori di attributo sotto forma di una configurazione denominata "mapping degli attributi".

Esiste un set preconfigurato di mapping degli attributi tra gli oggetti utente di Azure AD e gli oggetti utente di ogni app SaaS. Alcune app gestiscono altri tipi di oggetti, quali Gruppi o Contatti. <br> 
 È possibile personalizzare i mapping degli attributi predefinito hello in base alle esigenze aziendali tooyour. È infatti possibile modificare o eliminare i mapping degli attributi esistenti oppure crearne di nuovi.

Nel portale di Azure AD hello, è possibile accedere a questa funzionalità facendo clic su un **mapping** configurazione **Provisioning** in hello **Gestisci** sezione di un  **Applicazione aziendale**.


![Salesforce][5] 

Fare clic su un **mapping** configurazione, verrà aperta hello correlato **attributo Mapping** blade.  
Sono presenti i mapping degli attributi richiesti da un toofunction applicazione SaaS correttamente. Per gli attributi obbligatori, hello **eliminare** funzionalità non è disponibile.


![Salesforce][6]  

Nell'esempio hello sopra, è possibile visualizzare tale hello **Username** attributo di un oggetto gestito in Salesforce è popolato con hello **userPrincipalName** valore di hello collegato l'oggetto di Azure Active Directory.

È possibile personalizzare i **Mapping degli attributi** esistenti facendo clic su un mapping. Verrà visualizzata hello **Modifica attributo** blade.

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a>Informazioni sui tipi di mapping degli attributi
I mapping degli attributi permettono di controllare il modo in cui gli attribuiti vengono popolati in un'applicazione SaaS di terze parti. Sono supportati quattro diversi tipi di mapping:

* **Diretto** : attributo di destinazione hello viene popolato con il valore di hello di un attributo dell'oggetto collegato hello in Azure AD.
* **Costante** : attributo di destinazione hello viene popolato con una stringa specifica è stato specificato.
* **Espressione** -attributo di destinazione hello viene popolato in base al risultato di un'espressione analoga a uno script hello. 
  Per altre informazioni, vedere [Scrittura di espressioni per il mapping degli attributi in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).
* **Nessuna** -attributo di destinazione hello viene lasciato invariato. Tuttavia, se l'attributo di destinazione hello viene lasciato vuoto, viene popolata con il valore predefinito di hello specificato.

In tipi di mapping di addizione toothese quattro attributi di base, mapping di attributi personalizzati supportano il concetto di hello di facoltativa **predefinito** valore assegnazione. assegnazione di valore predefinito di Hello garantisce che un attributo di destinazione viene popolato con un valore se è presente un valore né in Azure AD, né nell'oggetto di destinazione hello. la configurazione più comune di Hello è tooleave questo vuoto.


## <a name="understanding-attribute-mapping-properties"></a>Informazioni sulle proprietà di mapping degli attributi

Nella sezione precedente hello, sono già state introdotte toohello attributo mapping tipo proprietà.
Nella proprietà toothis inoltre, i mapping degli attributi supportano anche hello gli attributi seguenti:

- **Attributo di origine** -attributo utente hello dal sistema di origine hello (ad esempio: Azure Active Directory).
- **Attributo di destinazione** : attributo utente hello nel sistema di destinazione hello (ad esempio: ServiceNow).
- **Associare gli oggetti utilizzando l'attributo** : questo mapping deve essere utilizzato o meno toouniquely identificare gli utenti tra i sistemi di origine e destinazione hello. È in genere impostato su userPrincipalName hello o attributo mail in Azure AD, che è in genere eseguito il mapping di campo del nome utente tooa in un'applicazione di destinazione.
- **Precedenza abbinamento**: è possibile impostare più attributi corrispondenti. Quando sono presenti più, essi vengono valutati in ordine di hello definito in questo campo. Quando viene rilevata una corrispondenza la valutazione degli attributi corrispondenti termina.
- **Applica questo mapping**
    - **Sempre**: applica il mapping sia all'azione di creazione che all'azione di aggiornamento dell'utente
    - **Only during creation** (Solo durante la creazione): applica il mapping solo alle azioni di creazione dell'utente


## <a name="what-you-should-know"></a>Informazioni utili

Microsoft Azure AD offre un'implementazione efficiente di un processo di sincronizzazione. In un ambiente inizializzato, durante un ciclo di sincronizzazione vengono elaborati solo gli oggetti che richiedono aggiornamenti. L'aggiornamento di mapping degli attributi ha un impatto sulle prestazioni di hello di un ciclo di sincronizzazione. Una configurazione di mapping di aggiornamento toohello attributo richiede rivalutate tutte toobe di oggetti gestiti. È un best practice tookeep hello numero consigliato di mapping degli attributi di modifiche consecutivi tooyour almeno.

## <a name="next-steps"></a>Passaggi successivi

* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Automatizzare tooSaaS utente Provisioning o Deprovisioning App](active-directory-saas-app-provisioning.md)
* [Scrittura di espressioni per i mapping degli attributi](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Ambito dei filtri per il Provisioning utente](active-directory-saas-scoping-filters.md)
* [Utilizzando SCIM tooenable il provisioning automatico degli utenti e gruppi da Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Notifiche relative al provisioning dell'account](active-directory-saas-account-provisioning-notifications.md)
* [Elenco di esercitazioni sulla tooIntegrate App SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

