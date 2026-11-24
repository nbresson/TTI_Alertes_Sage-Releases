<p align="center">
  <img src="Logo.png" alt="TTI Alertes Sage 100" width="128">
</p>

# TTI Alertes Sage 100 — Releases

Dépôt de distribution des versions publiées de **TTI Alertes Sage 100** : notifications automatiques par email des créations et modifications dans les bases SQL Server Sage 100 (Comptabilité, Gestion commerciale, Trésorerie).

## Téléchargement

Les binaires sont disponibles dans l'onglet [**Releases**](../../releases).

Chaque version contient :

- **TTI_Alertes_Sage.App** — console d'administration (tâches d'alerte, modèles d'email, historique, paramètres SQL / SMTP) ;
- **TTI_Alertes_Sage.Worker** — service Windows qui exécute les tâches planifiées en arrière-plan.

## Prérequis

- Windows 10/11 ou Windows Server
- Runtime [.NET 10 Desktop](https://dotnet.microsoft.com/download/dotnet/10.0)
- Accès en lecture à la base SQL Server Sage 100
- Un serveur SMTP ou un tenant Microsoft 365 (OAuth 2.0 / Microsoft Graph)

## Installation

1. Décompresser l'archive de la version dans un dossier (ex. `C:\Program Files\TTI_Alertes_Sage`).
2. Lancer `TTI_Alertes_Sage.App.exe` et configurer la connexion SQL Sage 100 et le serveur de messagerie.
3. Installer le service Windows dans une console PowerShell **administrateur** :

   ```powershell
   sc.exe create TTI_Alertes_Sage_Service binPath= "C:\Program Files\TTI_Alertes_Sage\Worker\TTI_Alertes_Sage.Worker.exe" start= auto
   sc.exe start TTI_Alertes_Sage_Service
   ```

La configuration est partagée entre la console et le service dans `%ProgramData%\TTI_Alertes_Sage\tti_alertes_sage.db`.

## Sécurité

L'application interroge Sage 100 **en lecture seule** (`WITH (NOLOCK)`) et ne modifie jamais les tables Sage.
