## <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure
1. Selezionare hello macchina virtuale si desidera tooredeploy, quindi seleziona hello *ridistribuire* pulsante hello *impostazioni* blade. Potrebbe essere necessario tooscroll verso il basso hello toosee **supporto e risoluzione dei problemi** sezione contenente pulsante 'Ridistribuire' hello come hello di esempio seguente:
   
    ![Pannello VM di Azure](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. operazione select hello hello tooconfirm *ridistribuire* pulsante:
   
    ![Pannello Ridistribuire una VM](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. Hello **stato** di hello VM cambia troppo*aggiornamento* come hello VM Prepara tooredeploy, come illustrato nell'esempio seguente hello:
   
    ![Aggiornamento di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. Hello **stato** viene quindi modificato troppo*iniziale* come hello macchina virtuale viene avviato un nuovo host di Azure, come illustrato nell'esempio seguente hello:
   
    ![Avvio di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. Al termine di processo di avvio hello, hello VM hello **stato** restituisce quindi troppo*esecuzione*, che indica di hello macchina virtuale è stata ridistribuita correttamente:
   
    ![Esecuzione di una VM](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)

