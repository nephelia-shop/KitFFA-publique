<div align="center">
    <h1>Nephelia KitFFA</h1>
    <p>Créez le meilleur KitFFA à partir de Nephelia Shop</p>
</div>

--------------------

# Installation
1. Vous devez mettre le plugin en .phar [.phar](https://pmt.mcpe.fun/create/)/en dossier avec le plugin [devtools](https://poggit.pmmp.io/p/DevTools/) dans le dossier **plugins**.
2. Installez le [pack](https://github.com/tedo0627/InventoryUIResourcePack/releases/) pour les inventaires, et mettez-le dans le dossier `resource_packs`.
3. Ouvrez le fichier `resource_packs.yml` et mettez `force_resources: true` et ajoutez dans `resource_stack`: `InventoryUIResourcePack.mcpack`

# Configurations:
| **Type**         | **Configuration**          | **Informations**                                                                                       |
|------------------|----------------------------|--------------------------------------------------------------------------------------------------------|
| Commandes        | `resources\commands.yml`   | Toute les commandes sont entièrement **configurables**, vous pouvez aussi les **activer/désactiver**   |
| League/Elos      | `resources\leagues.yml`    | Vous avez la possibilité de créer des ligues et leur elos, et modifier leur paramètres.                |
| Messages         | `resources\messages.yml`   | Chaque message envoyé, ainsi que son type est configurable                                             |
| **__Config__**   | `resources\config.yml`     | Ce fichier de configuration contrôle l'entierté de votre serveur, chaque système y est.                |

## Leagues :
### Config
*Vous pouvez les désactiver/activer `enabled: true` dans son fichier de configuration*
Voici **le format** d'une league
```yaml
leagues:
  Unranked:
    color: "§7"
    required-elo: 0
    elo-per-kill: 50
    elo-per-death: 8
  Bronze I:
    color: "§n"
    required-elo: 50
    elo-per-kill: 40
    elo-per-death: 10
```
*Unranked sera la première league, les leagues sont d'ordre croissant*

Celle-ci nécessite :
- Le nom -> `Unreanked`
- La couleur pour le [format](https://github.com/PocketMine/PocketMine-MP/blob/master/src/pocketmine/utils/TextFormat.php) dans le chat -> `color: §7`
- Elo-requis pour passer d'une ligue à la prochaine -> `required-elo: 50`
- Elo gagné par kill -> `elo-per-kill: 40`
- Elo perdu par mort -> `elo-per-death: 10`

### Commandes : Configurables
| Commande        | Description                                                          | Permission                                 |
|-----------------|----------------------------------------------------------------------|--------------------------------------------|
| `/elo`          | Afficher votre elo ou l'elo d'un joueur ainsi que sa league          | `kitffa.permissions.commands.elo`          |
| `/addelo`       | Ajouter des elos à un joueur                                         | `kitffa.permissions.commands.addelo `      |
| `/reduceelo`    | Réduire l'elo d'un joueur                                            | `kitffa.permissions.commands.reduceelo`    |
| `/setelo`       | Modifier les elos d'un joueur                                        | `kitffa.permissions.commands.setelo`       |
| `/topelo `      | Afficher le top                                                      | `kitffa.permissions.commands.topelo`       |
| `/topeloentity` | Modifier l'entité qui affiche le top                                 | `kitffa.permissions.commands.topeloentity` |
| `/ffa`          | Se téléporter au ffa (position configurable dans le `commands.yml`   | `kitffa.permissions.commands.ffa`          |
| `/spawn`        | Se téléporter au spawn (position configurable dans le `commands.yml` | `kitffa.permissions.commands.spawn`        |
| `/mute`         | Permet de mute un joueur                                             | `kitffa.permissions.commands.mute`         |
| `/unmute`       | Permet d'unmute un joueur                                            | `kitffa.permissions.commands.unmute`       |
| `/mutelist`     | Affiche la liste des joueurs mute                                    | `kitffa.permissions.commands.mutelist`     |
| `/ban`          | Bannir un joueur avec une durée                                      | `kitffa.permissions.commands.ban`          |
| `/banperm`      | Bannir un joueur définitivement                                      | `kitffa.permissions.commands.banperm`      |
| `/bablist`      | Affiche la liste des joueurs bannis                                  | `kitffa.permissions.commands.banlist`      |
| `/unban`        | Débannir un joueur                                                   | `kitffa.permissions.commands.unban`        |
| `/kitmodify`    | Modifier le kit                                                      | `kitffa.permissions.commands.kitmodify`    |
| `/kit`          | Permet au joueur d'équiper le kit                                    | `kitffa.permissions.commands.kit`          |
| `/setffazone`   | Permet de modifier la zone protégée ( /setffazone (a / b / center) ) | `kitffa.permissions.commands.setffazone`   |

Vous pouvez aussi supprimer des commands dans le `config.yml`, en suivant cette liste :
```yaml
unregister-commands:
  - "suicide"
  - "me"
  - "about"
```

## Systèmes :
### Zone : 
La zone protégée du kitffa est modifiable avec une commande /setffazone a | b | center, afin qu'elle marche vous devez mettre :
- Position A : `/setffazone a`
- Position B : `/setffazone b`
- Centre de la zone : `/setffazone center`
Chaque élement est requis afin de créer la zone, une fois tous les élements fournis, la zone sera opérative.
Vous pouvez aussi choisir d'activer ou de désactiver les protections du monde ffa dans `config.yml`, permission pour bypass `kitffa.permissions.bypass-protections`
```yaml
kit-ffa-protections:
  damage: true
  hunger: true
  place: true
  break: true
```
### Combat-Logger:
Totalement configurables, paramètres sur `config.yml` et messages sur `messages.yml`
#### Paramètres :
```yaml
combatlogger:
  combat-time: 10
  updatePlayerCombat: true
  killOnDisconnectCombat: true
  #permission pour bypass : kitffa.permissions.combatlogger.bypass
  banned-commands:
    - "tp"
    - "refill"
    - "warp"
    - "tpa"
    - "spawn"
    - "spawntp"
    - "hub"
    - "f"
    - "hubtp"
    - "spawntp"
    - "shop"
    - "lobby"
    - "lobbytp"
    - "rekit"
```
- `combat-time` : Durée du combat logger
- `updatePlayerCombat` : Option à activer pour afficher le temps du combat logger au joueur constamment **configurable sur `messages.yml`**
- `killOnDisconnectCombat` : Option pour tuer le joueur s'il se déconnecte en plein combat
- `banned-commands` : Commandes interdites à éxecuter en plein combat

*Il est possible de bypass le combat logger avec la permission `kitffa.permissions.combatlogger.bypass` trouvable sur `plugin.yml`*
### Modération :
#### Mute:
Les commandes **(mute, unmute, mutelist)** sont disponibles et sont **configurables** dans le fichier `commands.yml` ainsi que les **messages** dans `message.yml`
#### Ban:
Les commandes **(ban, banperm, banlist, unban)** sont disponibles et sont **configurables** dans le fichier `commands.yml` ainsi que les **messages** dans `message.yml`
### Kits :
- Vous pouvez modifier le kit avec la commande `/kitmodify`, qui prendra votre inventaire actuel et le mettra au kit.
- Le kit sera automatiquement donné au joueur quand on sort de la zone protégée du ffa ou lorsque le joueur éxecute la commande en dehors de la zone protégée du ffa.
- Vous avez le choix d'activer/désactiver le cooldown du kit dans la config ainsi que le temps du cooldown :
```yaml
kit:
  cooldown:
    enabled: true
    time: 5
```
### Heal : 
`config.yml`
#### Potions : 
Vous pouvez l'activer/désactiver, modifier le nombre de cœurs à ajouter ainsi que le rayon de la potion 
```yaml
  potions:
    enabled: true
    # 3 cœurs
    heal: 6
    size:
      x: 4.125
      y: 2.125
      z: 4.125
      #4 blocs
      max: 16
```
#### Soupes :
Vous pouvez l'activer/désactiver, modifier le nomrbe de cœurs et l'item 
```yaml
  soup:
    item: "beetroot_soup"
    enabled: true
    # 2 cœurs
    heal: 4
```
