## 1. Création et configuration de la GPO

1. **Ouvrir la Gestion de stratégie de groupe (Group Policy Management)** depuis votre contrôleur de domaine.

2. Dans le domaine **Wilder.lan**, créez une nouvelle GPO :
   - Faites un clic droit sur le dossier **Wilders_Students** et sélectionnez **Créer un objet GPO dans ce domaine et le lier ici**.
   - Nommez cette GPO : **Bloquer_Panneau_Configuration**.

3. **Configurer les paramètres de restriction** :
   - Faites un clic droit sur la GPO nouvellement créée et cliquez sur **Modifier**.
   - Allez dans **Configuration utilisateur > Stratégies > Modèles d'administration > Panneau de configuration**.
   - Double-cliquez sur l'option **Interdire l'accès au panneau de configuration et aux paramètres PC**.
   - Activez cette politique en sélectionnant **Activé**, puis cliquez sur **OK**.

### Filtrage de la GPO :

1. Revenez à la console de gestion des stratégies de groupe.
2. Sélectionnez la GPO créée et, dans le panneau **Étendue**, sous **Filtrage de sécurité**, cliquez sur **Ajouter**.
3. Ajoutez le groupe **Wilders_Students**.
4. Supprimez l’entrée **Authenticated Users** pour éviter que la GPO s'applique à tous les utilisateurs.

---

## 2. Vérification et tests

### Forcer la mise à jour des stratégies sur les postes clients :

1. Sur un poste client, ouvrez une invite de commande en tant qu'administrateur et tapez :

   ```bash
   gpupdate /force
   ```

2. Redémarrez si nécessaire pour appliquer complètement la GPO.

### Test avec un utilisateur du groupe **Wilders_Students** :

1. Connectez-vous avec un compte utilisateur appartenant au groupe **Wilders_Students**.
2. Essayez d'accéder au panneau de configuration. Vous devriez recevoir une erreur ou une restriction.

### Test avec un utilisateur hors du groupe **Wilders_Students** :

1. Connectez-vous avec un compte utilisateur qui **n'est pas membre** de **Wilders_Students**.
2. Vérifiez que cet utilisateur peut toujours accéder au panneau de configuration.

---

## 3. Dépannage et validation

### Si la GPO ne s'applique pas :

1. Vérifiez les permissions dans l'onglet **Délégation** de la GPO :
   - Assurez-vous que le groupe **Wilders_Students** a **Lecture** et **Appliquer la stratégie de groupe**.

2. Lancez la commande suivante sur un poste client concerné pour vérifier les GPO appliquées :

   ```bash
   gpresult /r
   ```

   Cela permettra de voir si la GPO est appliquée au compte utilisateur.

 <img src="https://github.com/Duhlan-16/ad/blob/main/Capture%20d'%C3%A9cran%202024-12-11%20112626.png?raw=true" width="400" height="200">


### Si d'autres utilisateurs sont impactés par la GPO :

- Assurez-vous que le filtrage de sécurité est correctement configuré pour cibler uniquement le groupe **Wilders_Students**.
