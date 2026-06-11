# Politique de confidentialité — Maths du jour

**Date d'entrée en vigueur :** 2026-05-21
**Dernière mise à jour :** 2026-06-10

Cette politique décrit comment l'app iOS Maths du jour (« l'App ») traite vos informations. Elle s'applique à partir de la v1.0, y compris le modèle de partage CloudKit à famille unique de la v3 (qui remplace le partage par profil de la v2.0).

## Résumé en clair

- Nous n'exploitons aucun serveur. Nous ne collectons aucune information personnelle.
- Tout reste sur votre appareil, sauf si vous activez la **synchronisation iCloud**, auquel cas Apple, et non nous, la stocke dans votre compte iCloud privé.
- L'App utilise votre micro uniquement pendant que vous répondez à un problème en mode vocal. L'audio est traité par la reconnaissance vocale d'Apple (sur l'appareil, de classe Siri) et immédiatement supprimé ; nous ne le stockons, ne l'envoyons ni ne l'analysons jamais.
- Il n'y a aucun traceur tiers, aucune publicité et aucun SDK d'analyse.

## Ce que l'App stocke sur votre appareil

- **Profils.** Nom, emoji, couleur et réglages par profil.
- **État de répétition espacée.** Pour chaque carte (par ex. `7 + 8`) : date de la prochaine révision, difficulté, stabilité et nombre de révisions.
- **Activité.** Un décompte quotidien des révisions terminées par profil (utilisé pour l'étiquette de série et l'écran Statistiques).
- **Erreurs.** Une file de problèmes que vous avez récemment mal résolus, afin que l'App puisse les réafficher.
- **Préférences.** Réglages à l'échelle de l'App, comme l'activation ou non de la synchronisation iCloud.

Tout cela est écrit dans le dossier Documents isolé propre à l'App et dans `UserDefaults`. L'App ne peut pas lire les données des autres apps, et les autres apps ne peuvent pas lire les données de l'App.

## Ce que l'App stocke éventuellement dans iCloud

La synchronisation iCloud est **désactivée par défaut**. Quand vous l'activez (icône d'engrenage → **Réglages → Synchronisation → Utiliser iCloud**), l'App écrit les mêmes données décrites ci-dessus dans votre iCloud privé via l'API **CloudKit** d'Apple. C'est votre iCloud, accessible uniquement par vous sur les appareils connectés au même identifiant Apple. Nous n'y avons aucun accès.

- Les données exactement synchronisées : profils, états des cartes, activité, erreurs et (en option) les métadonnées de partage de la famille (un nom d'affichage que vous choisissez pour votre famille).
- La synchronisation iCloud **n'inclut pas** le contenu d'un enregistrement vocal ni aucune analyse.
- Quand vous vous connectez avec un autre identifiant Apple, l'App détecte le changement et désactive la synchronisation jusqu'à ce que vous la réactiviez explicitement, afin que les données ne soient pas envoyées en silence vers un autre compte.
- Supprimer un profil depuis **Gérer les profils** retire le profil de l'appareil et (lorsque iCloud est accessible sur l'identifiant Apple d'origine) de votre copie iCloud également.

## Partage de la famille

En v3, le partage se fait au niveau de la **famille** plutôt que par profil. Ouvrez l'icône d'engrenage → **Réglages → Famille → Configurer la famille**, nommez votre famille et invitez des proches via la feuille de partage standard d'iOS (Messages, Mail ou AirDrop).

- Tous les profils de l'appareil du propriétaire appartiennent à la famille. Inviter un proche les partage tous d'un coup.
- Les données résident dans l'**iCloud du propriétaire de la famille**. Les participants ne stockent pas de copie distincte dans leur propre iCloud ; leur activité d'étude est écrite directement dans le CloudKit du propriétaire via le modèle d'autorisations CKShare limité à la zone d'Apple.
- Rejoindre une famille est **destructif sur l'appareil qui rejoint** : les profils locaux existants du participant sont remplacés par ceux de la famille. Avant de rejoindre, l'App propose une option **Exporter les profils dans un fichier** pour que vous enregistriez une copie JSON de vos données actuelles et la réimportiez plus tard si vous changez d'avis.
- Si le propriétaire dissout la famille (Réglages → Famille → Dissoudre) ou se déconnecte d'iCloud, les participants perdent l'accès en direct à leur prochaine synchronisation. Le cache local des profils de la famille devient le leur (aucune suppression destructive en partant).
- Un participant peut quitter une famille à tout moment (Réglages → Famille → Quitter). En partant, il conserve les profils de la famille sur son appareil comme les siens.
- La limite `CKShare` d'Apple est de 100 participants par élément partagé. L'échelle naturelle d'une famille est d'environ 6.

## Exporter / Importer (sauvegarde JSON)

Dans **Réglages → Sauvegarde**, vous pouvez :

- **Exporter les profils dans un fichier** : enregistrer un fichier JSON contenant tous les profils de l'appareil actuel (quel que soit l'état de la famille). Utile comme sauvegarde manuelle ou avant des opérations destructives.
- **Importer les profils depuis un fichier** : restaurer un export précédent. Le mode **Fusionner** ajoute les profils manquants et met à jour les existants si la copie importée est plus récente. Le mode **Remplacer** efface les profils locaux et installe l'ensemble importé ; disponible uniquement lorsque vous n'êtes pas dans une famille.

## Micro et reconnaissance vocale

Quand le mode vocal est activé, pendant que vous répondez à un problème, l'App :

1. Capture l'audio en direct du micro avec `AVAudioEngine`.
2. Le transmet à `SFSpeechRecognizer` (le framework d'Apple). Sur les appareils iOS récents, la reconnaissance s'exécute sur l'appareil par défaut ; certaines configurations peuvent utiliser les serveurs de reconnaissance vocale d'Apple.
3. Lit les chiffres transcrits et note la réponse.
4. Arrête la capture dès qu'une réponse finale est obtenue.

Nous ne conservons ni audio, ni transcriptions, ni signal dérivé. Nous ne transmettons l'audio à aucune partie autre que le `SFSpeechRecognizer` d'Apple. L'App demande `NSMicrophoneUsageDescription` et `NSSpeechRecognitionUsageDescription` à la première utilisation ; si l'une des autorisations est refusée, le mode vocal est automatiquement désactivé et le pavé numérique à l'écran est utilisé.

## Journaux de diagnostic

L'App émet des événements de diagnostic non structurés via le framework standard `OSLog` d'Apple (par ex. « session d'étude terminée, correctes=12 incorrectes=3 »). Ces journaux :

- Restent sur l'appareil.
- Ne sont visibles que par vous, dans Console.app lorsque l'appareil est connecté à un Mac.
- Utilisent la classification de confidentialité `.private` d'Apple pour toute valeur potentiellement identifiante (id de profil, nom de profil), de sorte que ces valeurs sont masquées dans les versions publiées.

Nous ne collectons, ne récupérons ni ne transmettons le contenu d'`OSLog`.

## Données que nous NE collectons PAS

- Votre nom, e-mail ou coordonnées.
- Votre position.
- Tout identifiant d'appareil (IDFA, IDFV, identifiant publicitaire).
- Les rapports de plantage au-delà de ce qu'Apple peut collecter via vos réglages iOS.
- Toute analyse ou télémétrie comportementale.
- Les informations de paiement ou de facturation (les achats sont entièrement gérés par Apple).

## Confidentialité des enfants

Maths du jour est conçue pour être sûre pour les enfants. Comme l'App ne collecte aucune information personnelle et ne contacte aucun tiers, elle respecte la définition « aucune information personnelle » de la COPPA. Nous n'affichons pas de publicité, et il n'y a ni comptes ni fonctionnalités sociales. Maths du jour comprend un seul achat intégré (un déblocage de l'app complète) ; comme l'app est conçue pour les enfants, une barrière parentale s'affiche avant tout achat, comme l'exigent les règles de la catégorie Enfants d'Apple. Tous les paiements et toute utilisation de code sont gérés par Apple via l'App Store. L'App ne voit ni ne stocke jamais vos informations de paiement.

## Vos choix

- **Désactiver le mode vocal** à tout moment par profil (Réglages → Mode vocal), ou globalement en refusant l'autorisation du micro dans les Réglages iOS.
- **Désactiver la synchronisation iCloud** à tout moment (icône d'engrenage → Réglages → Synchronisation → Utiliser iCloud → désactivé). La désactiver ne supprime pas les copies iCloud ; supprimez chaque profil individuellement si vous voulez les retirer.
- **Dissoudre ou quitter une famille** (Réglages → Famille → Dissoudre / Quitter) pour cesser le partage. Dissoudre révoque l'accès des participants à votre famille ; quitter conserve les profils de la famille sur votre appareil comme les vôtres.
- **Exporter les profils dans un fichier** (Réglages → Sauvegarde → Exporter) et le conserver localement : une sauvegarde manuelle qui ne touche jamais iCloud.
- **Réinitialiser la progression d'un profil** sans supprimer le profil (Réglages du profil → Réinitialiser).
- **Supprimer un profil** (Gérer les profils → balayez ou touchez pour supprimer) : retire aussi la copie iCloud quand la synchronisation est activée. Répétez par profil pour tout retirer.

## Modifications de cette politique

Si nous modifions cette politique, la nouvelle version sera disponible à la même URL avec une date de **Dernière mise à jour** actualisée. Les changements importants seront aussi indiqués dans les notes de version de l'App.

## Contact

Des questions sur cette politique ou vos données ? E-mail **spacedmath@gmail.com**.
