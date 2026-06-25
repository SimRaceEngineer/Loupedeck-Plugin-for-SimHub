# Changelog — Loupedeck for SimHub

## 1.0.0 — Première release publique (25 juin 2026)

- **Copier une page** : sur une page, « Copier depuis : Page X » → recopie tuiles + molettes + rôles
  de la page X (pratique pour garder les mêmes molettes et ne changer que les tuiles).
- **Rôles Control Mapper sur les molettes** : chaque sens (↻ / ↺) et le clic peut déclencher un rôle
  (presse son bouton vJoy) ou une action de plugin — même liste que les tuiles.

- Chemins **génériques** (plus aucun dossier personnel en dur). Les **rôles sont lus automatiquement**
  depuis la config Control Mapper active de SimHub (`PluginsData\Common\ControlMapperPlugin.GeneralSettingsV2.json`)
  — zéro réglage ; un sélecteur `.shomapping` reste dispo pour pointer un export. Dossier d'icônes
  configurable (défaut `LoupedeckIcons` à côté de SimHub).
- Première version publique regroupant toutes les fonctions ci-dessous.

## 0.10.1 — Indexation des icônes en cache (25 juin 2026)

- **Navigateur d'icônes instantané** : la liste des 17k fichiers + les vignettes décodées sont
  **mises en cache** (statique), avec **pré-chargement en arrière-plan au démarrage** du plugin →
  fini les 4-5s d'indexation à chaque ouverture.

## 0.10.0 — Valeurs des propriétés + pages 0-7 (25 juin 2026)

- **Navigateur de propriétés avec VALEURS** : la liste affiche `nom = valeur live` → tu vois ce que
  contient chaque propriété et tu choisis la bonne pour la télémétrie d'une tuile (bouton « ↻ Valeurs »).
- Pages numérotées **0 à 7** (au lieu de 1 à 8) pour coller à la numérotation des boutons.

## 0.9.0 — Icônes des molettes (bandes latérales) (25 juin 2026)

- **Icônes des 6 molettes** dans les bandes latérales de l'écran : `DrawRegion` générique +
  `DrawDial` (zones 60×90 — gauche TL/CL/BL, droite TR/CR/BR). `IconRenderer` accepte une taille
  (icône centrée ajustée). Bouton « icône… » + ✕ par molette dans l'éditeur, propre à chaque page.
- (Sans icône, la bande affiche « M1…M6 ».)

## 0.8.0 — Miroir du Control Mapper (25 juin 2026)

- **Miroir du Control Mapper** (comme SmartMacro) : `ControlMapperReader` lit l'export
  `.shomapping` (role → ButtonId) ; par tuile, on choisit un **rôle par son nom** et le plugin
  presse le bouton vJoy de sortie = `ButtonId+1` sur la **cible** (#1). Plus besoin d'ajouter
  le Loupedeck comme source ni de calculer des numéros.
- Combos FN et rôles > 128 ignorés du miroir (vJoy plafonne à 128) → passer par l'« Action »
  (ex. SmartMacro `Macro.Fire`).
- Sélecteur du fichier `.shomapping` + bouton « Recharger » + compteur de rôles.
- vJoy par défaut = la cible du Control Mapper (#1).

## 0.7.0 — Pages (8 boutons = 8 pages) (25 juin 2026)

- **Multi-pages** : les **8 boutons ronds** sélectionnent 8 pages, chacune avec ses **12 tuiles**
  (icône + action/télémétrie) **+ 6 encodeurs** → jusqu'à **8 × (12 + 18) = 240 slots**.
- **Config restructurée** en `Pages[8]` (migration auto de l'ancienne config single-page → page 1).
- **vJoy page-aware** pour les rôles : page P × tuile T → bouton vJoy (P-1)×12 + T (jusqu'à 96).
- Bascule de page : rendu de l'écran + déclencheurs + télémétrie de la page active. Sélecteur de
  page dans le panneau (reconstruit tuiles + encodeurs de la page).

## 0.6.0 — Navigateur de propriétés + police télémétrie (25 juin 2026)

- **Police télémétrie adaptative** : taille selon le nombre de chiffres (RPM 5, Speed 3… tiennent enfin).
- **Navigateur de propriétés SimHub** (`PropertyBrowserWindow`) : bouton « Parcourir… » sur la donnée
  télémétrie → liste **toutes** les propriétés (`PluginManager.GetAllPropertiesNames()`) avec recherche
  → tu choisis n'importe quelle donnée, y compris tes `simrace.*`.

## 0.5.1 — Sélecteur de device vJoy (25 juin 2026)

- **Fix conflit vJoy** : l'auto-sélection **évite #1** (souvent la SORTIE du Control Mapper) et prend
  un device libre #2..#16. Le Loupedeck ne squatte plus le vJoy de sortie du remapper.
- **Sélecteur « Device vJoy »** dans le panneau (Auto / #1..#16) → tu forces lequel le Loupedeck
  alimente, et tu ajoutes ce **même numéro** comme source dans le Control Mapper. Plus d'ambiguïté.
  Avertissement affiché si le device a < 38 boutons.

## 0.5.0 — Télémétrie sur tuiles + éditeur des 6 encodeurs (25 juin 2026)

- **Télémétrie live sur les touches** : `IDataPlugin` + `DataUpdate` (throttle ~5 Hz, redraw seulement
  si la valeur change). Par tuile, mode « Télémétrie » : on choisit une propriété SimHub
  (`DataCorePlugin.GameData.Rpms`, `…SpeedKmh`, `…Gear`, conso, T° eau/huile, pression pneu…) +
  un titre → la valeur s'affiche en direct sur l'écran de la touche (`IconRenderer.RenderTelemetry`).
- **Éditeur des 6 encodeurs** : par molette, une action de plugin pour ↻ / ↺ / clic
  (`DialConfig`, déclenchées via `TriggerAction`). Liste d'actions partagée (ItemsSource).
- Section « Boutons ronds » documentée (bind natif ou vJoy 31-38).

## 0.4.1 — Visibilité vJoy (25 juin 2026)

- Le panneau et la ligne de statut affichent **quel device vJoy** le Loupedeck alimente
  (ou l'erreur si aucun vJoy libre ≥38 boutons) → on sait quels boutons mapper dans le Control Mapper.

## 0.4.0 — Haptique + rôles de jeu via vJoy (25 juin 2026)

- **Retour haptique** restauré : `SET_VIBRATION` (0x1b) à chaque appui (tuile / clic molette / bouton)
  → le Loupedeck « vibre » de nouveau.
- **Rôles de jeu (Control Mapper)** : le plugin réalimente un **vJoy** en parallèle des entrées
  natives (touches→1-12, clic molette→13-18, molette ±→19-30, boutons→31-38). Les rôles de jeu
  (Pit Request, ABS+, F1 DRY ENTRY…) sont des cibles DirectInput → on mappe ces boutons vJoy vers
  les rôles dans *Contrôles* (les entrées natives nommées ne touchent que les actions de plugin).

## 0.3.1 — Fix écran noir + navigation dossiers (25 juin 2026)

- **Fix écran noir** : toutes les écritures série passent par une **file unique drainée par
  l'unique thread d'I/O** (plus de lecture/écriture concurrentes sur le `SerialPort`, qui
  corrompaient le flux et blankaient l'écran). Rendu **d'une seule tuile** à l'édition (au lieu
  des 12), changement d'action = sauvegarde sans redraw.
- **Navigateur d'icônes** : **arbre de dossiers** (parcours des packs de styles : *bw border flat*,
  *color glow*, etc.) au lieu d'une liste aplatie ; recherche par nom dans le dossier choisi.

## 0.3.0 — Icônes + actions par tuile (25 juin 2026)

- **Rendu sur les écrans des touches** : moteur C# `IconRenderer` (PNG → 90×90 RGB565 LE via GDI+)
  + `LoupedeckDevice.DrawTile` (FRAMEBUFF/DRAW, id `\x00M`, tuiles à x=60+col*90).
- **Configurateur dans le plugin** : grille 4×3 cliquable ; par tuile = **icône** (navigateur de la
  bibliothèque Stream_Deck_Icons_v2.2 : catégories + recherche) + **action** déclenchée à l'appui
  (`PluginManager.TriggerAction`, liste des actions auto-remplie par réflexion).
- Réglages **persistés** (`ReadCommonSettings/SaveCommonSettings`). Tuile sans icône = numéro affiché.
- Molettes/boutons toujours bindables dans Contrôles / Évènements.

## 0.2.0 — Entrées natives nommées (25 juin 2026)

- **Plus de vJoy** : les contrôles sont exposés via l'API native SimHub
  (`PluginManager.AddInput` + `TriggerInputPress/Release`) → ils apparaissent **nommés**
  dans *Controls & events* : « Loupedeck Tile 1…12 », « Loupedeck Dial 1…6 Click / CW / CCW »,
  « Loupedeck Button 1…8 ». Nom propre, zéro dépendance vJoy, zéro collision avec SmartMacro.
- Géométrie écran confirmée live : décalage bande gauche **60 px** (écran 480 = 60 + 4×90 + 60).
- Statut rafraîchi quand la version firmware arrive (plus de « fw ? »).

## 0.1.0 — Input bridge (25 juin 2026)

Première version : le Loupedeck **Live / Razer Stream Controller** (VID_1532/PID_0D06)
devient un périphérique d'entrée SimHub via vJoy.

- **Protocole** reverse-engineeré et validé en Python (`tools/probe_loupedeck.py`) sur le
  device réel (firmware 0.2.14) : handshake WebSocket-sur-série @256000, trames WS, opcodes
  BUTTON/KNOB/TOUCH.
- **Disposition mesurée** (pas supposée) : 6 molettes (ids 0x01–0x06, tournent + cliquent),
  8 boutons ronds (0x07–0x0e), écran tactile 480×270 en grille **4×3 = 12 touches** (90 px,
  bande molettes gauche 60 px). → c'est une Loupedeck **Live** (pas Live S).
- **`LoupedeckDevice`** : auto-détection du port COM via le registre, handshake, thread de
  lecture, parsing des events, reconnexion auto si le port se libère.
- **`VJoyFeeder`** : P/Invoke vJoy x86 (repris de SmartMacro), auto-sélection d'un device
  vJoy libre avec ≥ 38 boutons, hold + impulsion.
- **Mapping vJoy** : 12 touches → 1–12 ; clics molette → 13–18 ; molette + → 19–24 ;
  molette − → 25–30 ; boutons ronds → 31–38.
- **UI settings** : statut live (connexion device + vJoy), dernier event, plan des boutons,
  étapes de mise en route.

### À suivre
- Rendu sur les écrans des touches (labels statiques → télémétrie live : T° freins, conso, pressions).
- Page de mapping configurable + choix du device vJoy dans l'UI.
- Couplage molettes ↔ réglages (impulsions multiples / accélération).
