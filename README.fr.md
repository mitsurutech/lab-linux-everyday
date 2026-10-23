# Lab des commandes Linux du quotidien : ls, grep, tail -f, ssh, scp et kill dans une VM Ubuntu

[English](README.md) | [Français](README.fr.md) | [日本語](README.ja.md) | [Español](README.es.md)

[![check](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml/badge.svg)](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml)

Un **lab de commandes Linux** prêt à l’emploi pour la classe, issu de la [plateforme d’apprentissage MitsuruTech](https://mitsurutech.co.uk/fr/learning), où les écoles et les établissements donnent à chaque élève sa propre machine Ubuntu et un terminal dans le navigateur. Il contient de quoi s’exercer sur chaque commande qu’un ingénieur logiciel tape sans avoir à la chercher : **parcourir et chercher des fichiers** (`ls`, `cd`, `find`, `grep`), **lire un journal encore en cours d’écriture** (`tail -f`), **trouver et arrêter un processus** (`ps | grep`, `kill`, `kill -9`), **télécharger et décompresser des fichiers** (`curl`, `wget`, `zip`, `gzip`) et **se connecter à un autre compte et lui copier des fichiers** (`ssh`, `scp`). Rien n’est installé sur l’ordinateur de l’élève.

## Ce que contient la machine

| Quoi | Où | Pour |
| --- | --- | --- |
| Un journal d’une heure de lignes, qui grandit toutes les deux secondes | `/var/log/test.log` | `tail`, `grep`, compter les erreurs |
| Une archive et un fichier à compresser | `~/test.zip`, `~/test` | `unzip`, `gzip` |
| Une petite arborescence à parcourir et un dossier où l’on peut supprimer sans risque | `~/projects`, `~/scratch` | `ls`, `cd`, `find`, `cp`, `mv`, `rm -rf` |
| Un serveur web sur le port 8000 avec deux petits fichiers | `localhost:8000` | `curl`, `wget` |
| Deux processus, dont un ignore un simple `kill` | `lab-worker`, `lab-stubborn` | `ps`, `kill`, `kill -9` |
| Un second compte, `dev`, atteint par clé sous le nom `devbox` | `ssh devbox` | `ssh`, `scp` |

Le second compte est sur la **même machine**, pas sur une seconde : les commandes sont les mêmes et une seconde VM ne ferait qu’ajouter de l’attente. Le lab n’a ni vérification ni tâche. Les cinq leçons de la plateforme sont l’activité, et un enseignant qui veut une note prépare lui-même un rendu.

## Ce que contient le fichier

`linux-everyday.lab.yaml` est une **définition de lab VM** complète, exactement ce que la plateforme exécute :

| Clé | Rôle |
| --- | --- |
| `cpus`, `memory`, `disk` | la taille de la VM de chaque élève : 1 processeur, 1024 Mo et 10 Go |
| `open` | les ports ouverts dans le navigateur : aucun, le lab est le terminal |
| `setup` | un script exécuté une fois, en root, au premier démarrage de la VM de chaque élève : il installe quelques paquets depuis l’archive d’Ubuntu, crée le journal, les fichiers, les deux processus, le serveur web et le second compte, et écrit un README dans le dossier personnel |

## L’utiliser sur la plateforme

1. Dans votre module, ajoutez une tâche et choisissez la carte **Lab VM Ubuntu**.
2. Appuyez sur l’exemple, ou collez le contenu de `linux-everyday.lab.yaml`. Utiliser un exemple remplace le texte, et Annuler rend le vôtre.
3. Publiez et essayez d’abord votre propre copie. Chaque élève reçoit sa propre VM, conservée entre les séances.
4. Attribuez-la comme n’importe quelle tâche, ou ouvrez les leçons de la bibliothèque et appuyez sur Exécuter à côté d’une commande.

La [page du manuel pour ce lab](https://mitsurutech.co.uk/fr/help/lab-linux-everyday), son [guide des labs VM Ubuntu](https://mitsurutech.co.uk/fr/help/labs) et sa [page des labs d’exemple](https://mitsurutech.co.uk/fr/help/sample-labs) disent le reste. Pas encore de compte d’établissement ? [Votre première année est gratuite](https://mitsurutech.co.uk/fr/pricing) jusqu’à 50 élèves, et l’[inscription](https://mitsurutech.co.uk/fr/signup) demande une adresse e-mail.

## Vérifier le fichier

À chaque push, `.github/workflows/check.yml` vérifie que le fichier est du YAML valide avec les clés ci-dessus et que `setup` tient dans la limite de 16 Ko de la plateforme. Il ne démarre pas de VM : cela se fait sur les machines de la plateforme.

## Ce qui ne marche pas dans un lab

La VM atteint l’archive de paquets d’Ubuntu, PyPI, npm et GitHub, et rien d’autre : on ne peut donc pas viser un hôte d’Internet. C’est pourquoi le serveur web est dans le lab.

## À propos

Réalisé par [Mitsuru Technologies](https://mitsurutech.co.uk) pour la [plateforme d’apprentissage MitsuruTech](https://mitsurutech.co.uk/fr/learning) : Python, Java, Go, Node, SQL et Linux dans le navigateur pour les écoles et les établissements, avec labs de conteneurs, labs de VM, applications web déployées depuis GitHub et quiz qui se corrigent seuls. Essayez du code sans compte dans le [bac à sable](https://mitsurutech.co.uk/fr/playground).

D’autres labs du même endroit : [lab-linux-admin](https://github.com/mitsurutech/lab-linux-admin), [lab-linux-privesc](https://github.com/mitsurutech/lab-linux-privesc), [lab-incident-response](https://github.com/mitsurutech/lab-incident-response), [lab-netlab](https://github.com/mitsurutech/lab-netlab), [lab-git-gitea](https://github.com/mitsurutech/lab-git-gitea) et [lab-sample](https://github.com/mitsurutech/lab-sample).

## Licence

Cette œuvre est sous licence [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). Vous pouvez la partager et l’adapter pour l’apprentissage et l’enseignement, à condition de citer Mitsuru Technologies Ltd, de ne pas l’utiliser commercialement et de partager ce que vous en tirez sous la même licence. Le texte complet est dans le fichier `LICENSE`.

`zip`, `unzip`, `curl`, `wget`, `openssh-server`, `vim` et `python3` sont installés depuis l’archive d’Ubuntu au démarrage d’une VM ; rien n’en est distribué ici.
