
<br>

> [!NOTE]
> Se si sono ricevuti un nome utente e una password da un amministratore, è probabile che si abbia già un ID aziendale o dell’istituto d’istruzione (a volte detto anche *ID dell’organizzazione*). In questo caso, è possibile iniziare immediatamente toouse il tooaccess account Azure, le risorse di Azure che richiedono uno. Se si ritiene che non è possibile utilizzare tali risorse, potrebbe essere tooreturn toothis articolo per la Guida. Per ulteriori informazioni, vedere [gli account che è possibile utilizzare per l'accesso](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) e [sottoscrizione di Azure è tooAzure correlati AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

passaggi di Hello sono semplici. È necessario toolocate accesso sull'identità nel portale di Azure classico hello, individuare il dominio di Azure Active Directory predefinito e aggiungere un nuovo tooit utente come co-amministratore Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Individuare la directory predefinita nel portale di Azure classico hello
Avviare accedendo toohello [portale di Azure classico](https://manage.windowsazure.com) con l'identità dell'account Microsoft personale. Dopo che sono connessi, scorrere verso il basso il pannello di hello blu sul lato sinistro hello e fare clic su **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Occorre innanzitutto trovare alcuni informazioni sulla propria identità in Azure. Dovrebbe essere simile al seguente hello seguente nel riquadro principale hello, che mostra la presenza di una directory predefinita.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

È possibile cercare altre informazioni sulla directory Fare clic sulla riga directory predefinita hello, che consente di nelle proprietà di directory predefinito hello.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

nome di dominio predefinito hello tooview, fare clic su **domini**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

In questo caso dovrebbe essere in grado di toosee quando è stato creato hello account Azure, Azure Active Directory creato un dominio personale predefinito che è un valore hash (un numero generato da una stringa di testo) dell'ID personale utilizzato come un sottodominio di c o m. Ovvero hello dominio toowhich questo punto si aggiungerà un nuovo utente.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Creazione di un nuovo utente nel dominio predefinito hello
Fare clic su **UTENTI** e cercare il proprio account personale. Dovrebbe essere in hello **originato da** colonna che si tratta di un **account Microsoft**. Vogliamo toocreate un utente nel predefinito. c o m dominio di Azure Active Directory.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Stiamo toofollow [queste istruzioni](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello passaggi successivi, ma utilizzare un esempio specifico.

Nella parte inferiore di hello della pagina hello, fare clic su **+ Aggiungi utente**. Nella pagina hello che viene visualizzato, digitare nome utente hello e apportare hello **tipo di utente** un **nuovo utente nell'organizzazione**. In questo esempio, nuovo nome utente di hello è `ahmet`. Selezionare dominio predefinito hello che è stato individuato in precedenza come dominio hello indirizzo dell'ahmet di posta elettronica. Fare clic sulla freccia avanti di hello al termine.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Aggiungere ulteriori dettagli per Ahmet, ma assicurarsi che tooselect hello appropriato **ruolo** valore. È facile toouse **amministratore globale** toomake che tutto funzioni, ma se è possibile utilizzare un ruolo inferiore, che è una buona idea. Questo esempio viene utilizzato hello **utente** ruolo. Per altre informazioni, vedere le [autorizzazioni degli amministratori in base al ruolo](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1). Non abilitare l'autenticazione a più fattori a meno che non si desidera toouse autenticazione a più fattori per ogni log nell'operazione. Al termine, fare clic sulla freccia avanti hello.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Fare clic su hello **creare** pulsante toogenerate e visualizzare una password temporanea per Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Copiare l'indirizzo di posta elettronica di nome utente hello o utilizzare **invia PASSWORD IN messaggio di posta elettronica**. Sarà necessario toolog informazioni hello in a breve.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Ora verrà visualizzato un nuovo utente hello, **Ahmet hello Developer**, origine da Azure Active Directory. Si è creato un nuovo lavoro hello o identità dell'istituto di istruzione con Azure Active Directory. Tuttavia, questa identità non dispone ancora di autorizzazioni toouse Azure le risorse.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

Se si utilizza **invia PASSWORD IN messaggio di posta elettronica**, hello seguente tipo di messaggio di posta elettronica viene inviato.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Aggiunta di diritti di co-amministratore di Azure per le sottoscrizioni
A questo punto è necessario tooadd hello nuovo utente come coamministratore della sottoscrizione in modo hello nuovo utente possa accedere toohello portale di gestione. Questa operazione, nel Pannello di hello in basso a sinistra fare clic su toodo **impostazioni**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Nell'area Impostazioni principali hello, fare clic su **amministratori** in hello superiore e si dovrebbe essere solo della tua identità di account Microsoft. Nella parte inferiore di hello della pagina hello, fare clic su **+ Aggiungi** toospecify un coamministratore. In questo caso, immettere indirizzo di posta elettronica hello del nuovo utente hello che è stato creato, inclusi il dominio predefinito. Come illustrato nella schermata successiva di hello, un segno di spunta verde viene visualizzata utente toohello successivo per la directory predefinita hello. Ricordare tooselect tutte le sottoscrizioni di hello che si desidera tooadminister in grado di toobe questo utente.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

Al termine dovrebbero essere visibili due utenti, tra cui la nuova identità di co-amministratore. Disconnettersi da portale hello.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Accesso e modifica password hello del nuovo utente
Accedere come nuovo utente creato hello.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Sarà immediatamente toocreate richiesta una nuova password.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Deve essere ricompensati con esito positivo simile hello seguente.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Passaggi successivi
È ora possibile usare il nuovo toouse identità Azure Active Directory [modelli gruppo di risorse di Azure](../articles/xplat-cli-azure-resource-manager.md).

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
