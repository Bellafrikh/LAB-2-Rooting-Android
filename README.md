# LAB-2-Rooting-Android

## Introduction
Ce laboratoire analyse l'impact du rooting sur les mécanismes d'intégrité d'Android (Verified Boot, Sandboxing) afin d'évaluer la sécurité d'une application dans un environnement à privilèges élevés (UID 0).

## Informations Générales
* **Application testée** : DIVA (Damn Insecure and Vulnerable App)
* **Version** : 1.0 (Beta)
* **Support de test** : 
    * **AVD** : Pixel 6 (Émulateur Android Studio)
    * **Image Système** : Android 15.0 (Google APIs) | API Level 35
* **Objectif du TP** : Comprendre les mécanismes du **rooting**, l'architecture de sécurité Android et analyser les impacts d'un accès privilégié sur la confidentialité des données.

## Etape 1: Rooter l'AVD

Objectif : Obtenir les privilèges UID 0 pour accéder aux zones protégées du système.

![](https://github.com/user-attachments/assets/47113cbd-daa2-47b3-882a-85df8df3c47d)
*Figure 1 : affichage du uid*


![](https://github.com/user-attachments/assets/7ce21c4e-d160-431c-8528-0eef3d02f102)
*Figure 2 : Processus de Rooting et Remount*

![](https://github.com/user-attachments/assets/694e78f0-3bac-42eb-be0e-c86b7afb97f5)
*Figure 3 : Vérification des indicateurs d'intégrité*

![](https://github.com/user-attachments/assets/6d92bcbe-ea38-4229-a909-75740bf04ced)
*Figure 4 : Vérification des indicateurs d'intégrité*

![](https://github.com/user-attachments/assets/5a8b5dc6-218b-4ab9-b926-2afe9e23862d)
*Figure 5 : Analyse du fichier Logcat*

## Etape 3: Démarrer un AVD PROPRE

Démarrer un AVD (Android Virtual Device) vierge pour garantir l'intégrité des résultats et observer les mécanismes de sécurité modernes

![](https://github.com/user-attachments/assets/4b4943b8-0c37-4095-8574-4e506c6faea2)
*Figure 6 : État Initial et Connexion*


## Etape 4: Installer et lancer l'app de test

Installer l'application vulnérable sur l'environnement de test pour analyser ses mécanismes de sécurité en mode rooté.

![](https://github.com/user-attachments/assets/741e596f-ac02-478e-b7c7-cb11a12e64be)
*Figure 7 : l'installation réussie de l'application via ADB.*

![](https://github.com/user-attachments/assets/5004ff22-228f-42d2-813e-4a6d4ae155ea)

*Figure 8 : Interface utilisateur de l'application "DIVA"*


## Etape 5: Définir 3 scénarios simples 



##1.Ouvrir l'écran d'accueil
Lancement de l'application DIVA et vérification de l'affichage du menu principal

![](https://github.com/user-attachments/assets/c2271c0a-925c-47ca-bced-60d706a2e627)


*Figure 9 : Analyse en temps réel des journaux système pendant l'exécution de l'application DIVA.*


##2.Rechercher un item
Sélection du module "1. INSECURE LOGGING" pour tester la saisie de données.

![](https://github.com/user-attachments/assets/d647fb50-8984-487c-a288-796af9709c58)

*Figure 10 : Exploitation d'une faille de validation d'entrée dans le module "Input Validation Issues - Part 2"*


##3.Ouvrir un détail (fiche produit/profil)


![](https://github.com/user-attachments/assets/8b043136-71fd-4abe-ac9d-ebf6f5c5119e)


*Figure 11 : Saisie d'identifiants de test dans le module "Insecure Data Storage - Part 1"*

![](https://github.com/user-attachments/assets/460ca2bb-031f-482a-90bc-f2017f95a931)

*Figure 12 : Utilisation des privilèges root pour inspecter le système de fichiers privé de l'application.*


## Etape 6: Lire Android Security


La sécurité Android repose sur une architecture multicouche garantissant la confidentialité et l'intégrité des données. Le Sandboxing assure l'isolation logicielle en confinant chaque application dans un environnement étanche. Le Modèle de Permissions régule l'accès aux ressources sensibles, tandis que l'Intégrité Système prévient toute modification non autorisée de la structure globale. Le rooting compromet ces piliers en accordant des privilèges totaux sur l'ensemble de la forteresse numérique.


## Etape 7:  Verified Boot (idée générale + check AVD)

Garantir que le code exécuté au démarrage provient exclusivement d'une source officielle sans altération malveillante.

![](https://github.com/user-attachments/assets/5a52e5f1-93ff-4d67-8e2d-6be02d668541)

*Figure 13 : Vérification du Verified Boot State (Audit de clôture)*


## Etape 8:  AVB (Android Verified Boot)

L'AVB 2.0 sécurise le démarrage via une signature granulaire des partitions et intègre une protection anti-rollback empêchant le retour vers des versions vulnérables. En audit, l'état orange de mon terminal confirme que ces contrôles d'intégrité ont été levés pour autoriser l'accès root. Ce mécanisme transforme ainsi une sécurité matérielle rigide en une gestion logicielle flexible mais strictement contrôlée.



## Etape 9: Définir le rooting 

Le Rooting : Privilèges et Responsabilités
Le rooting consiste à obtenir les privilèges super-utilisateur (UID 0), offrant un contrôle total sur le système d'exploitation Android. Cette manipulation désactive les barrières de sécurité natives (comme Verified Boot et le Sandboxing), modifiant ainsi fondamentalement la confiance accordée à l'intégrité du système. En environnement de laboratoire, cet accès est indispensable pour observer des comportements de bas niveau et analyser les mécanismes de défense des applications. Cependant, en raison des risques d'exposition des données, cette pratique impose une isolation stricte du réseau, une traçabilité complète des actions et une réinitialisation systématique de l'appareil après test.



## Etape 10: Intérêt labo 

L'utilisation d'un environnement rooté en laboratoire autorisé uniquement permet d'auditer la sécurité profonde d'une application en observant des artefacts système normalement inaccessibles. Ce cadre privilégié facilite l'analyse des comportements à bas niveau et permet de tester la robustesse du stockage local face à un attaquant. Par exemple, cet accès a permis de confirmer que l'application testée stocke des données sensibles en clair, révélant une absence critique de chiffrement propre.



## Etape 11: Matrice de risques

Intégrité non garantie : Un système modifié peut donner des résultats de test faux ou biaisés.
Surface d'attaque accrue si l'appareil sort du labo : L'appareil devient très vulnérable aux virus s'il quitte le laboratoire.
Données sensibles exposées si présentes : Sans isolation (sandbox), n'importe quel intrus peut lire vos fichiers privés.
Instabilité système : Le root peut causer des bugs rendant les tests impossibles à reproduire.
Mélange comptes perso/test : Utiliser ses vrais accès risque de faire fuiter ses infos personnelles dans le labo.
Mauvais nettoyage fin de séance : Ne pas tout effacer laisse vos traces pour les prochains utilisateurs.
Réseau non isolé : Les tests pourraient toucher des systèmes extérieurs par accident.
Traçabilité insuffisante : Sans logs, on ne peut pas prouver ou refaire le test plus tard.


## Etape 12: Mesures défensives

Réseau isolé : Bloquer les connexions externes pour éviter toute communication non voulue.

Données fictives : Utiliser uniquement de fausses informations pour supprimer tout risque de fuite réelle.

Support dédié : Utiliser un AVD réservé uniquement au labo pour ne pas compromettre d'autres outils.

Nettoyage total : Effectuer un "Wipe Data" après chaque test pour effacer toute trace résiduelle.

Journal de configuration : Noter chaque réglage pour pouvoir refaire le test exactement à l'identique.

Aucun compte personnel : Ne jamais se connecter à ses mails ou réseaux sociaux sur l'appareil de test.

Contrôle des APK : Vérifier la source de chaque application installée pour limiter les risques.

Traçabilité complète : Capturer chaque étape avec l'heure pour prouver le bon déroulement de l'audit.

## Etape 13: OWASP MASVS

MASVS-STORAGE-1 : Les données sensibles (mots de passe, clés API) doivent être chiffrées avant d'être stockées localement.

MASVS-NETWORK-1 : Toutes les communications doivent être sécurisées via un protocole TLS configuré pour vérifier l'authenticité des certificats.

Application pratique : L'accès root a permis de confirmer que l'application DIVA échoue à l'exigence STORAGE-1 en stockant des secrets en clair.

## Etape 14: OWASP MASTG ( idées de tests)

Relation MASVS/MASTG : Alors que le MASVS définit les objectifs de sécurité, le MASTG fournit les procédures techniques pour les auditer.

Test de Stockage : Inspection directe du répertoire /data/data/[package_name]/shared_prefs/ via l'accès root pour identifier des données sensibles en clair.

Analyse Dynamique : Utilisation de adb logcat pour intercepter les flux de données runtime et détecter des fuites d'informations dans les journaux systèm


## Etape 15: Commandes de rooting (rappel synthèse)

adb devices
adb root
adb remount
adb shell id
adb shell getprop ro.boot.veritymode
adb shell getprop ro.boot.vbmeta.device_state
adb shell "su -c id"


## Etape 16: Traçabilité : fiche environnement 

###Informations Générales

Auteur : BELLAFRIKH ZAYNAB.

Date : 13 Février 2026.

Support : Émulateur Android (AVD) "emu64xa".

Modèle Émulé : Pixel 6 (x86_64).

Système : Android 15 (VanillaIceCream) avec API Level 35.

Application : DIVA (Damn Insecure and Vulnerable App).

###Synthèse des Observations
Accès Privilégié : Succès de l'obtention des droits root (uid=0).

État d'Intégrité : Verified Boot en état "orange" (chaîne de confiance rompue).

Vulnérabilité Majeure : Stockage d'identifiants (Secret123!) en clair dans les préférences partagées.

###Galerie des Preuves (Traçabilité)
Preuve 1 : Lancement de l'application (Image 7).

Preuve 2 : Confirmation du mode root (Image 2-3).

Preuve 3 : État du Verified Boot (Image 13).

Preuve 4 : Lecture des données sensibles (Image 9-10-12).

🧹 État de Sortie
Limites : Tests effectués uniquement sur un environnement virtualisé sans protection matérielle (TEE/StrongBox).

Reset effectué : Oui, réinitialisation complète de l'AVD effectuée pour supprimer toute trace de données fictives.


## Etape 17: Remise à zéro AVD  
Restaurer l'AVD à son état d'usine pour éliminer toute trace de l'audit et prévenir la contamination de futurs tests.

1. Réinitialisation de l'AVD :
![](https://github.com/user-attachments/assets/c9085942-9178-443b-8a58-e320848001d2)

*Figure 14 : Sélection de l'option "Wipe Data"*

2. Capture de preuve :
![](https://github.com/user-attachments/assets/521e22ae-ee39-4eba-8fb5-cd201eb77d05)


*Figure 15 : Redémarrage faisant suite à la réinitialisation.*
