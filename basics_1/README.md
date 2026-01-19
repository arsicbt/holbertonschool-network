# Explication Tache : 1. Show attached IPs 


```

Décomposons :

### `ifconfig`
Affiche les informations de toutes les interfaces réseau. Exemple de sortie :
```
eth0: flags=4163<UP,BROADCAST,RUNNING>
        inet 172.17.0.2  netmask 255.255.0.0
lo: flags=73<UP,LOOPBACK,RUNNING>
        inet 127.0.0.1  netmask 255.0.0.0
```

### `grep -oP '(?<=inet\s)\d+(\.\d+){3}'`

**Options :**
- `-o` : affiche **seulement** la partie qui correspond (pas toute la ligne)
- `-P` : utilise les **regex Perl** (plus puissantes)

**Regex expliquée :**
- `(?<=inet\s)` : **Lookbehind positif** = cherche ce qui suit "inet" + un espace, sans inclure "inet " dans le résultat
- `\d+` : un ou plusieurs chiffres
- `(\.\d+){3}` : répète 3 fois "un point suivi de chiffres"

**Pattern complet :** `123.45.67.89` (après "inet ")

### Résultat
```
172.17.0.2
127.0.0.1

-----------------
# Explication Tache : 2. Port listening on localhost
``` 
**nc (netcat)**
Netcat est un *outil réseau puissant*, souvent appelé le "couteau suisse TCP/IP". Il peut :

* Écouter sur un port (mode serveur)
* Se connecter à un port (mode client)
* Transférer des données

**Options utilisées :**

* **-l : Listen mode (mode écoute)** - crée un serveur qui attend des connexions
* **localhost :** écoute uniquement sur l'interface locale **(127.0.0.1)**
* **98 :** numéro du port
```