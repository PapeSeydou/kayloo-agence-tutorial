# KAYLOO — « Je suis une agence. Comment rejoindre KAYLOO ? »

Relevé du parcours réel d'inscription d'une agence, capturé le 2026-11-05 sur l'environnement de test local (Docker) du site Kayloo.

- URL : `http://kayloo.local:8000`
- Navigateur : Chrome, viewport 1440 × 810, device scale factor 2 (2880 × 1620 par capture)
- Langue : français
- Compte de test : Agence Horizon Immobilier, contact@horizon-immo.com, Awa Diop

## Environnement utilisé

`kayloo.immo` répond en maintenance (503, page Infomaniak) et `test.kayloo.immo` est l'ancien site WordPress (thème Houzez), pas la plateforme actuelle. Le parcours exploitable est l'application FastAPI du dépôt, lancée dans Docker et accessible sur `http://kayloo.local:8000` (résolution locale définie dans le fichier hosts). C'est cet environnement qui a été utilisé.

L'envoi d'e-mails est désactivé dans `.env` (`EMAIL_ENABLED=false`) et l'envoi de SMS dépend d'un fournisseur externe. Pour capturer le parcours réel, un serveur SMTP local de capture a été branché sur le conteneur web ; les codes de vérification et l'e-mail de bienvenue ont été lus dans ce serveur. Aucun e-mail n'est parti vers une adresse réelle.

## Écart principal avec le script fourni

Le script décrit un tunnel marketing « Devenir partenaire » avec NINEA, RCCM, documents, quatre formules et une Charte Partenaire. Ce tunnel n'existe pas dans la plateforme actuelle. Le parcours réel est un parcours d'authentification unifié (`/inscription`) : choix e-mail ou téléphone, code de vérification, identité, mot de passe, type de compte, informations de l'agence, création du compte. Les documents d'identification et les formules d'abonnement se trouvent après la création du compte, dans l'espace agence (`/admin`).

Conséquence : les étapes 05 (documents), 06 (formules) et 07 (Charte Partenaire) du script ne sont pas dans l'ordre demandé et la Charte Partenaire n'existe pas. Elles ont été capturées là où elles existent réellement, et les absences sont documentées plus bas.

## Ordre réel des écrans

| Fichier | Écran | URL | Remarque |
|---|---|---|---|
| `01_home.png` | Accueil, haut de page, héros visible | `/` | Bandeau cookies refusé avant la capture |
| `02_cta_default.png` | Bouton « Connexion / Inscription », état normal | `/` | Remplace le bouton « Devenir partenaire » du script, absent du site |
| `02_cta_hover.png` | Même bouton, souris dessus | `/` | Aucun style de survol : l'apparence est identique à l'état normal (styles calculés comparés, aucune différence) |
| `03_auth_entry.png` | Panneau de connexion ouvert | `/?connexion=1` | Première étape réelle après le bouton |
| `03_auth_start.png` | Début d'inscription, numéro de téléphone | `/inscription` | Lien « S'inscrire avec une adresse e-mail » utilisé |
| `03_auth_email.png` | Saisie de l'e-mail | `/inscription` | |
| `03_auth_code.png` | Code à 6 chiffres reçu par e-mail | `/inscription` | |
| `03_auth_identity.png` | Prénom, nom, téléphone | `/inscription` | Étape absente du script |
| `03_auth_password.png` | Création du mot de passe | `/inscription` | Étape absente du script |
| `04_role_none.png` | Choix du type de compte, rien de sélectionné | `/inscription` | Trois cartes : Chercher un bien / Vendre ou louer mon bien / Agence ou promoteur |
| `04_role_agency.png` | « Agence ou promoteur » sélectionné | `/inscription` | Remplace « Agence immobilière » |
| `05_form_empty.png` | Formulaire agence vide | `/inscription` | |
| `05_form_b-name.png` | Champ « Nom de l'agence » rempli et focalisé | `/inscription` | |
| `05_form_b-email.png` | Champ « E-mail » rempli et focalisé | `/inscription` | |
| `05_form_b-phone.png` | Champ « Téléphone » rempli et focalisé | `/inscription` | |
| `05_form_b-website.png` | Champ « Site web » rempli et focalisé | `/inscription` | |
| `05_form_b-country.png` | Champ « Pays » focalisé | `/inscription` | |
| `05_form_filled.png` | Formulaire entièrement rempli, sans erreur | `/inscription` | CGU cochées |
| `05_form_filled.png` | Formulaire rempli, case CGU cochée | `/inscription` | Seule case à cocher du parcours ; la Charte Partenaire n'existe pas |
| `05_form_submit_hover.png` | Bouton « Créer mon compte » survolé | `/inscription` | Remplace le bouton « Valider » du script |
| `05_form_error-email.png` | Erreur de validation, e-mail `awa.diop@` | `/inscription` | Message exact : « Adresse e-mail invalide. » |
| `06_success.png` | Confirmation « Bienvenue, Awa ! » | `/inscription` | Correspond à l'écran de confirmation du script |
| `07_dashboard_modal.png` | Premier accès à l'espace agence, modale d'attente de validation | `/admin/dashboard` | |
| `07_dashboard.png` | Tableau de bord agence | `/admin/dashboard` | |
| `08_docs_empty.png` | Validation de compte, formulaire masqué | `/admin/profile?tab=validation` | |
| `08_docs_form_empty.png` | Formulaire de dépôt de documents vide | `/admin/profile?tab=validation` | |
| `08_docs_empty_scrolled.png` | Formulaire vide, vue défilée | `/admin/profile?tab=validation` | |
| `08_docs_filled.png` | Trois documents chargés, noms de fichiers visibles | `/admin/profile?tab=validation` | NINEA.pdf, RCCM.pdf, CNI.pdf |
| `08_docs_submit_success.png` | Message de succès après envoi | `/admin/profile?tab=validation` | Une seconde avant le basculement d'onglet |
| `08_docs_submitted.png` | Statut « EN ATTENTE », trois documents listés | `/admin/profile?tab=validation` | |
| `09_plans_all.png` | Les trois formules visibles avec prix et avantages | `/admin/credits-shop` | Découverte, Standard, Business |
| `09_plans_selected.png` | Formule Standard sélectionnée | `/admin/credits-shop` | |
| `11_dashboard_*.png` | Sections de l'espace agence | `/admin/...` | Activités, statistiques, annonces, CRM, crédits, profil, agence, notifications |
| `12_email_confirmation.png` | E-mail de bienvenue, contenu seul, 2x | — | Objet : « Bienvenue sur Kayloo — Compte agence créé » |

## Correspondance avec la numérotation du script

| Script | Réalité |
|---|---|
| 01 Accueil | `01_home.png` |
| 02 « Devenir partenaire » | Bouton réel « Connexion / Inscription » : `02_cta_default.png`, `02_cta_hover.png` |
| 03 Type de partenaire | `04_role_none.png`, `04_role_agency.png` (libellé « Agence ou promoteur ») |
| 04 Formulaire agence | `05_form_*.png` (pas de NINEA ni RCCM à cette étape) |
| 05 Documents | `08_docs_*.png`, après création du compte, dans l'espace agence |
| 06 Formules | `09_plans_*.png`, trois formules au lieu de quatre |
| 07 Charte Partenaire | Absente. Case CGU aux couleurs du site, cochée dans `05_form_filled.png` |
| 08 Confirmation | `06_success.png` |
| 09 E-mail de confirmation | `12_email_confirmation.png` |
| 10 Offre et paiement | Non exécuté : la boutique crédits affiche les moyens de paiement (Wave, Orange Money, YAS). Aucun paiement réel n'a été lancé. |
| 11 Tableau de bord | `07_dashboard*.png` et `11_dashboard_*.png` |

## Formulaire agence : champs réels

Nom de l'agence (obligatoire), E-mail (facultatif, format e-mail contrôlé), Téléphone (facultatif), Site web (facultatif, URL), Pays (liste, Sénégal par défaut). Case « J'accepte les CGU et la politique de confidentialité de Kayloo. » obligatoire. Message d'information : « Votre compte professionnel sera activé après vérification par nos équipes. »

Champs du script absents : NINEA, RCCM, nom du contact, pièces jointes, formules, Charte Partenaire.

## Documents d'identification

L'écran de validation accepte un ou plusieurs documents, avec un type par document : N.I.N.E.A., Registre du Commerce, Carte Nationale d'Identité, Passeport, Autre document. Formats acceptés : JPG, PNG ou PDF, 10 Mo maximum. Après envoi, le statut passe à « EN ATTENTE » et les documents sont listés avec leur date.

Textes exacts : `screens/08_docs_*.txt`.

## Formules d'abonnement

Trois formules, pas quatre. Les noms et prix affichés :

- Découverte Kayloo — 0 crédit — 0 FCFA TTC — 5 annonces actives, 1 utilisateur, leads correspondant aux annonces, CRM intégré, statistiques.
- Standard Kayloo — 5 crédits — 75 000 FCFA TTC — 30 annonces actives, 2 utilisateurs, mise en avant des annonces, 5 leads qualifiés / mois, CRM intégré, statistiques.
- Business Kayloo — 10 crédits — 100 000 FCFA TTC — 50 annonces actives, 3 utilisateurs, mise en avant des annonces, leads qualifiés illimités, CRM intégré, statistiques.

Aucune formule « Premium ». Textes exacts : `screens/09_plans_*.txt`.

## Données de test

- Nom de l'agence : Agence Horizon Immobilier
- E-mail : contact@horizon-immo.com
- Téléphone de l'agence (champ libre) : +221 77 123 45 67
- Site web : www.horizon-immo.com
- Contact : Awa Diop
- Pays : Sénégal
- Téléphone personnel du compte : +221 78 456 78 90. Le numéro +221 77 123 45 67 du script était déjà rattaché à un compte de test existant ; l'inscription l'a refusé (conflit). Le numéro affiché dans le formulaire agence reste celui du script.
- Mot de passe du compte de test : Horizon2026! (non fourni par le script, nécessaire à l'inscription par e-mail)
- Aucun NINEA ni RCCM n'a pu être saisi : ces champs n'existent pas dans le parcours.

## Messages de validation observés

- E-mail invalide : « Adresse e-mail invalide. » (bordure rouge sous le champ).
- Téléphone personnel invalide : contrôle de longueur (9 chiffres pour +221), message « Numéro de téléphone invalide » via l'API.
- Conflit de numéro à la création : renvoi vers l'étape identité avec le champ téléphone en erreur (observé pendant la préparation, non capturé).
- Dépôt de documents : message de succès « ✓ 3 document(s) envoyé(s) avec succès ! Notre équipe vous contactera sous 48h. » puis statut « EN ATTENTE ».

## Ce qui n'existe pas ou n'a pas été capturé

- Bouton « Devenir partenaire » sur l'accueil : absent.
- Type « Agence immobilière » : libellé réel « Agence ou promoteur ».
- NINEA et RCCM dans le formulaire d'inscription : absents.
- Quatre formules DÉCOUVERTE / STANDARD / PREMIUM / BUSINESS : trois formules seulement, sans Premium.
- Charte Partenaire : aucune charte, aucun texte de charte dans le code ou sur les écrans.
- Écran de paiement et confirmation de paiement : non exécutés, pour ne pas déclencher de paiement. Les moyens de paiement sont visibles dans la boutique crédits.
- Parcours par SMS : non utilisé, le fournisseur SMS externe n'est pas configuré en local. Le parcours e-mail a été utilisé à la place.
- Notification dans l'application : la cloche « Mes notifications » existe mais aucune notification n'a été générée pour ce compte.

## Fichiers produits

- `screens/` : 42 captures 2880 × 1620, un JSON de positions par capture, fichiers texte pour les documents, les formules et l'e-mail.
- `fullpage/` : captures pleine page (largeur 2880) et JSON de positions page complète.
- `elements/` : 69 crops serrés (2x, 16 px de marge) des champs, boutons, cartes de formule, lignes de documents et case CGU.
- `assets/` : logo Kayloo (SVG), 10 icônes SVG, documents PDF fictifs, HTML de l'e-mail de bienvenue.
- `flow-recording.mp4` : enregistrement du parcours, 1440 × 810, converti à 60 fps.

## Méthode

Playwright avec Chrome, viewport 1440 × 810, device scale factor 2. Avant chaque capture : attente du chargement réseau, des polices et des animations, refus du bandeau cookies, fermeture des modales non pertinentes. Aucune capture ne contient de barre de navigateur, de curseur ni de survol parasite. Les coordonnées des JSON sont en pixels de l'image 2880 × 1620, avec `tap: true` sur les éléments réellement cliqués.
