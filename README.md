# 📦 Base de Données de Gestion d’Inventaire – Microsoft Access

## ✨ Aperçu

Ce dépôt contient une **base de données complète de gestion d’inventaire** développée sous **Microsoft Access**.  
Elle combine :

- **SQL** pour les requêtes  
- **VBA** pour les automatisations *(alertes, validations, mises à jour automatiques)*  

💡 **Objectif :** tester la pertinence d’Access aujourd’hui et explorer les améliorations possibles *(rapports, alertes, synchronisation, etc.)*.

---

## 🌟 Fonctionnalités

- 🗂️ **Catégories de Produits** : classification claire et hiérarchisée  
- 📦 **Suivi des Lots** : dates d’achat, d’expiration, fournisseur  
- 📉 **Gestion des Stocks** : suivi en temps réel + alertes pour stock minimum  
- 🕓 **Historique complet** : suivi des achats et retraits *(qui, quand, pourquoi)*  
- 👥 **Gestion des Utilisateurs** : contrôle des droits et traçabilité  
- ⚙️ **Automatisations VBA** : alertes, validations et mises à jour automatiques  

---

## 🔧 Prérequis

- 💻 Microsoft Access **2016 ou version plus récente**  
- 🧠 Connaissances de base en **SQL** et **VBA** *(optionnel mais recommandé)*  
- 🚫 Aucune dépendance externe – **tout est contenu dans Access**

---

## 📥 Installation

1. **Télécharger ou cloner le dépôt :**
   ```bash
   git clone https://github.com/tonprojet/inventory-access.git
   ```
2. **Ouvrir le fichier** `.accdb` dans Microsoft Access  
3. **Activer le contenu** (macros/VBA) si demandé  
4. Aller dans : `Outils > Base de données > Compacter et Réparer`

---

## 👩‍💻 Utilisation

- 📝 **Saisie de données** : via formulaires ou édition directe des tables  
- 🔍 **Requêtes SQL et rapports personnalisés** :
   ```sql
   SELECT * 
   FROM tbl_Inventory 
   WHERE CurrentQuantity < MinimumStock;
   ```
- 🤖 **Automatisations VBA** : mise à jour automatique du stock après un retrait  
- 🚀 **Évolutivité** : migration possible vers **SQL Server** pour gestion multi-utilisateurs  

---

## 📋 Structure de la Base

### 🧱 Tables Principales

| Table | Description |
|--------|--------------|
| `tbl_Categories` | ID, Nom, Description |
| `tbl_Products` | ID, Code, Nom, Catégorie, StockMin, Description |
| `tbl_Lots` | ID, NumLot, Produit, DateAchat, Expiration, QtéInitiale, Fournisseur |
| `tbl_Inventory` | ID, Produit, Lot, QuantitéActuelle |
| `tbl_PurchaseHistory` | ID, Produit, Lot, Quantité, Date, Fournisseur, Notes |
| `tbl_WithdrawalHistory` | ID, Produit, Lot, ParQui, PourQui, Quantité, Date, Notes |
| `tbl_Users` | ID, Nom, Département, Rôle |

---

## 🔗 Relations entre Tables

```text
tbl_Categories ──< tbl_Products ──< tbl_Lots ──< tbl_Inventory
                       │                   │
                       ├──< tbl_PurchaseHistory
                       └──< tbl_WithdrawalHistory
tbl_Users ─────────────┘
```

💬 *Commentaire :* Ces relations doivent être créées dans `Outils > Relations` avec intégrité référentielle activée.

---

## 🛠️ Guide Rapide

### Étape 1️⃣ : Création des Tables

- Crée les tables listées ci-dessus  
- Définit les types de données (`Texte court`, `Numérique`, `Date/Heure`, etc.)  
- Attribue les clés primaires (`ID` auto-incrément)  

### Étape 2️⃣ : Définir les Relations

- Ouvre `Outils de base de données > Relations`  
- Relie les champs de clé étrangère (ex. `CategoryID` → `tbl_Categories.ID`)

### Étape 3️⃣ : Créer les Formulaires

- Crée un formulaire par entité (`Produits`, `Lots`, `Retraits`, etc.)  
- Ajoute des boutons de navigation et d’action  

### Étape 4️⃣ : Automatiser avec VBA

#### Exemple VBA simple

```vba
' ============================================
' Mise à jour automatique du stock après retrait
' ============================================
Private Sub Quantity_AfterUpdate()
    On Error GoTo Err_Handler
    DoCmd.RunSQL "UPDATE tbl_Inventory " & _
                 "SET CurrentQuantity = CurrentQuantity - " & Me.Quantity & _
                 " WHERE ProductID = " & Me.ProductID
Exit Sub

Err_Handler:
    MsgBox "Erreur lors de la mise à jour du stock : " & Err.Description, vbCritical
End Sub
```

💬 *Commentaire :* Ce script soustrait automatiquement la quantité retirée du stock dès que le champ `Quantity` est modifié.

---

## 💡 Améliorations Futures

- 🔔 Alertes automatiques pour stock minimum  
- 📈 Tableaux de bord Power BI / Access  
- 🧾 Rapports PDF pour les achats et retraits  
- 🔐 Rôles utilisateurs (Admin, Logisticien, Lecteur)  
- 🔄 Intégration Excel / SharePoint  

---

## 🤝 Contributions

Les contributions sont **ouvertes à tous** 💪  
Fork, modifie et crée une **pull request**  

Focus suggéré :
- Automatisations VBA  
- Tests multi-utilisateurs  
- Optimisation SQL  
- Design de formulaires Access  

---
