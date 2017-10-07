---
title: aaaOverview di controllo di accesso in archivio Data Lake | Documenti Microsoft
description: Informazioni sul funzionamento del controllo di accesso in Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Controllo di accesso in Azure Data Lake Store

Archivio Azure Data Lake implementa un modello di controllo di accesso che deriva da HDFS, che a sua volta deriva dal modello di controllo degli accessi di hello POSIX. Questo articolo riepiloga le nozioni di base di hello del modello di controllo di accesso di hello per archivio Data Lake. toolearn più sul modello di controllo degli accessi HDFS hello, vedere [HDFS autorizzazioni Guida](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Elenchi di controllo di accesso per file e cartelle

Esistono due tipologie di elenchi di controllo di accesso (ACL): **ACL di accesso** e **ACL predefiniti**.

* **Accesso ACL**: questi oggetti tooan di controllo accesso. Sia i file che le cartelle hanno ACL di accesso.

* **Gli ACL predefinito**: "Modello" degli ACL associato a una cartella che determinano hello accesso ACL per gli oggetti figlio che vengono creati in tale cartella. I file non hanno ACL predefiniti.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

Sia gli ACL di accesso e gli ACL predefinito hanno hello stessa struttura.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Modifica hello ACL predefinito per un elemento padre non influisce sul hello accesso o ACL predefinito degli elementi figlio che esistono già.
>
>

## <a name="users-and-identities"></a>Utenti e identità

Ogni file e cartella ha autorizzazioni distinte per le entità seguenti:

* utente del file hello proprietario Hello
* gruppo proprietario Hello
* Utenti non anonimi
* Gruppi con nome
* Tutti gli altri utenti

identità di Hello di utenti e gruppi sono le identità di Azure Active Directory (Azure AD). Se non specificato diversamente, un "user", nel contesto di hello dell'archivio Data Lake, è possibile uno: un utente di Azure Active Directory o un gruppo di sicurezza di Azure AD.

## <a name="permissions"></a>Autorizzazioni

le autorizzazioni di Hello su un oggetto file System sono **lettura**, **scrivere**, e **Execute**, e possono essere usati nei file e cartelle come illustrato nella seguente tabella hello:

|            |    File     |   Cartella |
|------------|-------------|----------|
| **Lettura (R)** | Grado di leggere il contenuto di hello di un file | Richiede **lettura** e **Execute** contenuto hello toolist della cartella hello|
| **Scrittura (W)** | Scrivere o aggiungere file tooa | Richiede **scrivere** e **Execute** toocreate di elementi figlio in una cartella |
| **Esecuzione (X)** | Non significa che qualsiasi elemento nel contesto di hello dell'archivio Data Lake | Elementi figlio di hello tootraverse obbligatorio di una cartella |

### <a name="short-forms-for-permissions"></a>Forme brevi per le autorizzazioni

**RWX** è usato tooindicate **lettura + scrivere ed eseguire**. In cui è presente un formato numerico più ridotto **lettura = 4**, **scrivere = 2**, e **Execute = 1**, hello somma che rappresenta le autorizzazioni di hello. Di seguito sono riportati alcuni esempi.

| Forma numerica | Forma breve |      Significato     |
|--------------|------------|------------------------|
| 7            | RWX        | Lettura + Scrittura + Esecuzione |
| 5            | R-X        | Lettura + Esecuzione         |
| 4            | R--        | Lettura                   |
| 0            | ---        | Nessuna autorizzazione         |


### <a name="permissions-do-not-inherit"></a>Non ereditarietà delle autorizzazioni

Nel modello di tipo POSIX hello utilizzato dall'archivio Data Lake, autorizzazioni per un elemento vengono archiviate in elemento hello stesso. In altre parole, le autorizzazioni per un elemento non possono essere ereditate dagli elementi padre hello.

## <a name="common-scenarios-related-toopermissions"></a>Toopermissions correlati a scenari comuni

Di seguito sono alcune toohelp scenari comuni comprendere quali autorizzazioni sono necessarie tooperform determinate operazioni in un account archivio Data Lake.

### <a name="permissions-needed-tooread-a-file"></a>Autorizzazioni necessarie tooread un file

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Per leggere toobe di file di hello, hello chiamante esigenze **lettura** autorizzazioni.
* Per tutti hello cartelle nella struttura di cartelle hello che contengono file hello, hello chiamante esigenze **Execute** autorizzazioni.

### <a name="permissions-needed-tooappend-tooa-file"></a>Autorizzazioni necessarie tooappend tooa file

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Per toobe file hello accodati a, hello chiamante esigenze **scrivere** autorizzazioni.
* Per tutti hello cartelle contenenti file hello, hello chiamante esigenze **Execute** autorizzazioni.

### <a name="permissions-needed-toodelete-a-file"></a>Autorizzazioni necessarie toodelete un file

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Cartella padre hello, hello chiamante esigenze **scrittura eseguire** autorizzazioni.
* Per tutti hello altre cartelle nel percorso del file hello, hello chiamante esigenze **Execute** autorizzazioni.



> [!NOTE]
> Scrivere le autorizzazioni per file hello non sono necessari toodelete purché hello precedente due condizioni sono true.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Autorizzazioni necessarie tooenumerate una cartella

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Per tooenumerate cartella hello, hello chiamante esigenze **lettura + Execute** autorizzazioni.
* Per tutti hello cartelle predecessore, hello chiamante esigenze **Execute** autorizzazioni.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Autorizzazioni di visualizzazione nel portale di Azure hello

Da hello **Esplora dati** fare clic su Pannello di hello account archivio Data Lake, **accesso** toosee hello ACL per un file o una cartella. Fare clic su **accesso** toosee hello ACL per hello **catalogo** cartella hello **mydatastore** account.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

In questo pannello, nella sezione superiore hello Mostra una panoramica delle autorizzazioni hello. (Nella schermata hello utente hello è Bob). Successivamente, vengono visualizzate le autorizzazioni di accesso hello. Dopo che da hello **accesso** pannello, fare clic su **vista semplice** toosee hello visualizzazione più semplice.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Fare clic su **vista avanzata** toosee hello più avanzate, visualizzazione in cui vengono visualizzati i concetti di hello di ACL predefinito, la maschera e utente avanzato.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>utente avanzato Hello

Un utente avanzato è hello la maggior parte dei diritti di tutti gli utenti di hello hello archivio Data Lake. Un utente con privilegi avanzati:

* Disponga delle autorizzazioni di RWX troppo**tutti** file e cartelle.
* Può modificare le autorizzazioni di hello su qualsiasi file o cartella.
* Cambiare hello utente proprietario o l'appartenenza a gruppo di qualsiasi file o cartella.

In Azure un account Data Lake Store include diversi ruoli di Azure, tra cui:

* Proprietari
* Collaboratori
* Lettori

Tutti gli utenti hello **proprietari** ruolo per un account archivio Data Lake è automaticamente un utente avanzato per l'account. vedere, più toolearn [controllo di accesso basato sui ruoli](../active-directory/role-based-access-control-configure.md).
Se si desidera toocreate un ruolo di controllo di accesso basato sui ruoli (RBAC) personalizzato che dispone delle autorizzazioni utente avanzato, è necessario hello toohave queste autorizzazioni:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>utente proprietario Hello

utente di Hello che ha creato l'elemento hello è automaticamente hello utente dell'elemento hello proprietario. Un utente proprietario può:

* Modificare le autorizzazioni di hello di un file di proprietà.
* Modificare l'appartenenza gruppo di un file di proprietà, come utente proprietario hello è anche un membro del gruppo di destinazione hello hello.

> [!NOTE]
> utente proprietario Hello *Impossibile* modificare hello proprietario l'utente di un altro file di proprietà. Solo gli utenti Super modificabili hello proprietario l'utente di un file o cartella.
>
>

## <a name="hello-owning-group"></a>gruppo proprietario Hello

Hello ACL POSIX, ogni utente è associata a un "gruppo primario". Ad esempio, l'utente "alice" potrebbe appartenere gruppo "finance" toohello. Alice potrebbe appartenere anche toomultiple gruppi, ma un gruppo viene sempre definito come suo gruppo primario. In POSIX, quando Alice crea un file, hello appartenenza gruppo di file è tooher gruppo primario, ovvero in questo caso "finance".

Quando viene creato un nuovo elemento filesystem, archivio Data Lake assegna un valore toohello proprietario gruppo.

* **Caso 1**: cartella radice hello "/". Questa cartella viene creata al momento della creazione di un account Data Lake Store. In questo caso, hello appartenenza gruppo toohello utente che ha creato l'account di hello.
* **Caso 2** (tutti gli altri casi): quando viene creato un nuovo elemento, gruppo proprietario hello viene copiato dalla cartella padre hello.

gruppo proprietario Hello può essere modificato da:
* Qualsiasi utente con privilegi avanzati.
* Hello proprietario l'utente, se l'utente proprietario hello è anche un membro del gruppo di destinazione hello.

## <a name="access-check-algorithm"></a>Algoritmo di controllo dell'accesso

Hello nella figura riportata di seguito rappresenta l'algoritmo di controllo di accesso di hello per gli account archivio Data Lake.

![Algoritmo per gli ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>maschera di Hello e "autorizzazioni"

Hello **mask** è un RWX valore che rappresenta l'accesso toolimit utilizzati per **denominato utenti**, hello **proprietario gruppo**, e **gruppi denominati** quando si è algoritmo di controllo di accesso hello in esecuzione. Ecco i concetti chiave hello per mask hello.

* maschera di Hello crea "autorizzazioni". Vale a dire, di modificare le autorizzazioni di hello in fase di hello di controllo di accesso.
* maschera di Hello può essere modificato direttamente dal proprietario del file hello e a qualsiasi utente super.
* maschera Hello è possibile rimuovere le autorizzazioni toocreate hello effettivo di autorizzazioni. maschera di Hello *Impossibile* aggiungere autorizzazioni toohello effettivo di autorizzazioni.

Verranno ora esaminati alcuni esempi. Nell'esempio seguente di hello, mask hello è troppo**RWX**, che indica che la maschera hello non rimuovere tutte le autorizzazioni. le autorizzazioni valide di Hello per hello denominato utente, denominato gruppo e appartenenza gruppo non vengono modificate durante il controllo di accesso di hello.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

Nell'esempio seguente di hello, mask hello è troppo**R-X**. Ciò significa che **disattiva le autorizzazioni di scrittura hello** per **denominato utente**, **proprietario gruppo**, e **gruppo denominato** in fase di hello di accesso controllo.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Per riferimento, ecco maschera hello per un file o una cartella in cui è presente hello portale di Azure.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Per un nuovo account archivio Data Lake, hello mask per hello accesso ACL predefinita della radice hello ("/") per impostazione predefinita cartella tooRWX.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Autorizzazioni per nuovi file e cartelle

Quando in una cartella esistente, viene creato un nuovo file o una cartella, hello ACL predefinita nella cartella padre hello determina:

- ACL predefinito e ACL di accesso di una cartella figlio.
- ACL di accesso di un file figlio (i file non hanno un ACL predefinito).

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Hello accesso di una cartella o file figlio

Quando viene creata una cartella o un file figlio, viene copiato ACL predefinito dell'elemento padre di hello come hello accesso ACL del file figlio hello o della cartella. Inoltre, se **altri** utente disponga delle autorizzazioni di RWX nell'ACL predefinito dell'elemento padre di hello, viene rimosso dalla finestra di accesso dell'elemento figlio di hello.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

Nella maggior parte degli scenari, le informazioni precedenti relative hello vengono che tutti necessarie tooknow sulla determinazione di accesso dell'elemento figlio. Tuttavia, se si ha familiarità con i sistemi POSIX e dettagliate desidera toounderstand come viene ottenuta questa trasformazione, vedere la sezione hello [ruolo dell'Umask creazione hello accesso ACL per i nuovi file e cartelle](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) più avanti in questo articolo.


### <a name="a-child-folders-default-acl"></a>ACL predefinito di una cartella figlio

Creazione di una cartella figlio in una cartella padre, ACL predefinito della cartella padre hello è copiate come ACL predefinito della cartella di toohello figlio.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Argomenti avanzati per informazioni dettagliate sugli ACL in Data Lake Store

Di seguito sono toohelp alcuni argomenti avanzati che è comprendere il modo in cui vengono determinati gli ACL per le cartelle o file di archivio Data Lake.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Ruolo dell'umask creazione hello accesso ACL per i nuovi file e cartelle

In un sistema compatibile POSIX, concetto generale hello è tale umask è un valore di bit 9 alla cartella padre hello utilizzati autorizzazione hello tootransform per **utente proprietario**, **proprietario gruppo**, e  **altri** su hello accesso di una cartella o un nuovo file figlio. bit Hello di un umask identificare quali tooturn bit accesso ACL dell'elemento figlio di hello. In questo modo viene utilizzato tooselectively impedire la propagazione di hello delle autorizzazioni per **utente proprietario**, **proprietario gruppo**, e **altri**.

In un sistema di HDFS umask hello in genere è un'opzione di configurazione in tutto il sito che viene controllata dagli amministratori. Data Lake Store usa una proprietà **umask a livello di account** non modificabile. annullare il mascheramento Hello hello illustrato nella tabella seguente per archivio Data Lake.

| Gruppo utenti  | Impostazione | Effetto sull'ACL di accesso di un nuovo elemento figlio |
|------------ |---------|---------------------------------------|
| utente proprietario | ---     | Nessun effetto                             |
| gruppo proprietario| ---     | Nessun effetto                             |
| altri       | RWX     | Rimuovere Lettura + Scrittura + Esecuzione         |

Hello nella figura seguente viene illustrata questa umask in azione. effetto Hello è tooremove **lettura + scrivere ed eseguire** per **altri** utente. Poiché umask hello non specificava bits per **utente proprietario** e **proprietario gruppo**, tali autorizzazioni non vengono trasformate.

![ACL in Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>bit permanenti Hello

bit permanenti Hello è una funzionalità più avanzata di un file System POSIX. Nel contesto di hello dell'archivio Data Lake, è improbabile che bit permanenti hello saranno necessari.

Hello nella tabella seguente viene illustrato il funzionamento di bit permanenti hello in archivio Data Lake.

| Gruppo utenti         | File    | Cartella |
|--------------------|---------|-------------------------|
| Sticky bit **OFF** | Nessun effetto   | Nessun effetto           |
| Sticky bit **ON**  | Nessun effetto   | Impedisce a chiunque tranne **utenti super** hello e **utente proprietario** di un elemento figlio da eliminazione o ridenominazione di tale elemento figlio.               |

bit permanenti Hello non è visualizzata nel portale di Azure hello.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Domande frequenti sugli ACL in Data Lake Store

Di seguito sono riportate alcune domande frequenti sugli ACL in Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>È necessario il supporto per gli elenchi ACL tooenable?

No. Il controllo di accesso tramite ACL è sempre attivo per un account Data Lake Store.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Quali autorizzazioni sono necessarie toorecursively Elimina la cartella e il relativo contenuto?

* cartella padre Hello deve avere **scrittura eseguire** autorizzazioni.
* Hello toobe cartella eliminata, e ogni cartella all'interno di esso, è necessario **lettura + scrivere ed eseguire** autorizzazioni.

> [!NOTE]
> Non è necessario scrivere le autorizzazioni toodelete file nelle cartelle. Inoltre, hello cartella radice "/" può **mai** da eliminare.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Chi è proprietario di hello di un file o cartella?

creatore Hello di un file o cartella diventa il proprietario di hello.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Il gruppo a cui è impostato come proprietario del gruppo di file o cartelle al momento della creazione di hello?

gruppo proprietario Hello viene copiato dal proprietario della cartella padre hello quali hello nuovo file o cartella viene creato in gruppo di hello.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Sto hello proprietario l'utente di un file ma non si dispone delle autorizzazioni RWX hello che è necessario. Cosa devo fare?

utente proprietario Hello possibile modificarle hello toogive file hello stessi eventuali autorizzazioni RWX che necessarie.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Quando si visualizzano gli ACL nel portale di Azure hello vedo nomi utente, ma tramite le API, viene visualizzato GUID, è possibile?

Voci ACL hello vengono archiviate come GUID corrispondenti toousers in Azure AD. Hello API restituiscono hello GUID come è. Hello portale di Azure tenta toomake ACL più facile toouse dalla conversione hello GUID in nomi descrittivi, quando possibile.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Perché viene talvolta visualizzato GUID hello ACL durante l'utilizzo di hello portale di Azure?

Un GUID viene visualizzato quando l'utente hello non esiste in più di Azure AD. In genere ciò si verifica quando l'utente hello ha lasciato l'azienda di hello o il proprio account è stato eliminato in Azure AD.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Data Lake Store supporta l'ereditarietà degli ACL?

No.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Qual è la differenza hello tra maschera e umask?

| mask | umask|
|------|------|
| Hello **mask** proprietà è disponibile in tutti i file e cartelle. | Hello **umask** è una proprietà di hello account archivio Data Lake. Pertanto, è solo un singolo umask hello archivio Data Lake.    |
| proprietà mask Hello in un file o cartella può essere modificata da hello proprietario l'utente o gruppo di un file o un utente avanzato di proprietario. | proprietà umask Hello non può essere modificato da alcun utente, anche un utente avanzato. È un valore costante non modificabile.|
| proprietà mask Hello viene utilizzato durante l'algoritmo di controllo di accesso di hello in fase di esecuzione toodetermine se un utente ha tooperform destra hello operazione su un file o cartella. ruolo di Hello della maschera hello è toocreate "autorizzazioni" in fase di hello di controllo di accesso. | umask Hello non viene usato affatto durante il controllo di accesso. umask Hello è usato toodetermine hello accesso ACL di nuovi elementi figlio di una cartella. |
| maschera di Hello è un valore di 3 bit RWX che applica toonamed utente, gruppo e utente proprietario in fase di hello di controllo di accesso.| umask Hello è un valore di bit 9 che applica toohello proprietario l'utente, proprietario, gruppo e **altri** di un nuovo elemento figlio.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>Dove è possibile reperire altre informazioni sul modello di controllo di accesso POSIX?

* [POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html) (Elenchi di controllo di accesso POSIX in Linux)

* [HDFS Permission Guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html) (Guida alle autorizzazioni HDFS)

* [Domande frequenti su POSIX](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [ACL POSIX in Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL: Using Access Control Lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/) (ACL: uso di elenchi di controllo di accesso in Linux)

## <a name="see-also"></a>Vedere anche

* [Panoramica dell’Archivio Data Lake di Azure](data-lake-store-overview.md)
