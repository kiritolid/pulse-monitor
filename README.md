# Pulse Monitor

Moniteur système natif pour macOS 14 et versions ultérieures.

## Fonctions

- Interface claire, sombre ou adaptée au système, navigation par composant.
- CPU global et par cœur, RAM, GPU (si le pilote expose ses compteurs).
- Débits disque et réseau, batterie et état thermique macOS.
- Historique de dix minutes avec valeurs au survol.
- Rapport HTML autonome et interactif, avec export CSV en JavaScript.
- Menu de la barre système, pause et cadence réglable.

## Trois langages, trois responsabilités

| Langage | Rôle |
| --- | --- |
| Swift | Application SwiftUI, collecte, graphiques, export |
| C | Lecture native des informations matérielles via sysctl et uname |
| JavaScript | Exploration des rapports hors ligne et export CSV |

## Téléchargement

Le fichier `Pulse-Mac.zip` contient l’application universelle et toutes les sources Swift, C et JavaScript. Décompressez-le puis ouvrez le dossier `Pulse`.

## Compilation

Installez les outils de ligne de commande Xcode, puis lancez :

```sh
chmod +x Construire.command
./Construire.command
open Pulse.app
```

Le script compile un exécutable universel Apple Silicon / Intel. Le matériel, la mémoire, les volumes et le GPU sont détectés sur l’ordinateur qui lance l’application : aucune configuration personnelle n’est inscrite dans les sources.

```sh
Pulse.app/Contents/MacOS/Pulse --self-test
```

Le test d’intégration utilise les compteurs disponibles sur le Mac de test. L’absence de certains compteurs peut faire échouer ce diagnostic sans empêcher l’interface de fonctionner.

## Confidentialité et limites

Aucune télémétrie ni requête réseau. Les rapports sont enregistrés uniquement sur demande et contiennent les spécifications génériques et les séries CPU/RAM/GPU, sans nom d’utilisateur, adresse IP, numéro de série ou liste des processus.

Les compteurs GPU dépendent du pilote ; les valeurs absentes restent indisponibles. Les températures détaillées, fréquences CPU, FPS globaux, ANE, SMART et suivi GPU par processus ne sont pas implémentés. La mémoire des processus est RSS ; le CPU par processus est la moyenne de `ps`, avec 100 % pour un cœur. Les unités mémoire utilisent une base 1024.

La compilation Intel est fournie mais n’a pas été testée sur un Mac Intel physique. L’application est signée localement (ad hoc), sans notarisation Apple. Aucun lancement automatique ni service privilégié n’est installé.
