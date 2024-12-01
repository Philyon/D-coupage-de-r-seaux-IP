# Découpage de réseaux IP

## Découpage symétrique :

Avec le réseau `172.16.1.0/24` on a 254 adresses disponibles (256 - 2)
On est sur un découpage pour 4 pôles, dont le plus gros compte 50 équipements. Le 2^n >= à 50 le plus proche est 2^6 (64), soit une CIDR de 32 - 6 = 26 soit /26.
Avec le découpage symétrique dans ces conditions on est sur un nombre d'adresses totales par pôle de 256 / 4 = 64. 
64 - 2 = 62 adresses disponibles par pôles.

Pour le réseau `172.16.1.0/24` on peut faire le découpage symétrique suivant :

#### Sous réseau 1 : Pôle informatique
Adresse de réseau : `172.16.1.0/26`
Déblut de plage IP disponible : `172.16.1.1`
Fin de plage IP disponible : `172.16.1.62`
Adresse de broadcoast : `172.16.1.63`

#### Sous réseau 2 : Pôle développement
Adresse de réseau : `172.16.1.64/26`
Déblut de plage IP disponible : `172.16.1.65`
Fin de plage IP disponible : `172.16.1.126`
Adresse de broadcoast : `172.16.1.127`

#### Sous réseau 3 : Pôle administratif
Adresse de réseau : `172.16.1.128/26`
Déblut de plage IP disponible : `172.16.1.129`
Fin de plage IP disponible : `172.16.1.190`
Adresse de broadcoast : `172.16.1.191`

#### Sous réseau 4 : Pôle technicien
Adresse de réseau : `172.16.1.192/26`
Déblut de plage IP disponible : `172.16.1.193`
Fin de plage IP disponible : `172.16.1.254`
Adresse de broadcoast : `172.16.1.255`

Voici ce que ça donne résumé dans un tableau :

##### Découpage symétrique
| Pôle              | Adresse réseau | Adresse broadcoast | Adresse  début plage | Adresse fin plage |
|------------------|---------------|---------------------|------------------------|----------------|
| Informatique     | 172.16.1.0/26| 172.16.1.63|      172.16.1.1      |     172.16.1.62    |
| Développement   | 172.16.1.64/26| 172.16.1.127|       172.16.1.65      |     172.16.1.126    |
| Administratif   | 172.16.1.128/26| 172.16.1.191|       172.16.1.129      |    172.16.1.190     |
| Technicien       | 172.16.1.192/26| 172.16.1.255|      172.16.1.193       |    172.16.1.254     |


## Découpage asymétrique :

Avec le réseau `172.16.1.0/24` on a 254 adresses disponibles (256 - 2)
On est sur un découpage pour 4 pôles, répartis ainsi par ordre décroissant de nombre d'équipements :
- Le Pôle informatique de 50 équipements
- Le Pôle administratif de 20 équipements
- Le Pôle technicien de 15 équipements
- Le Pôle développement de 12 équipements

Calcul du nombre d'adresses disponibles requis et du CIDR

- Pôle informatique : le 2^n >= à 50 le plus proche est 2^6 (64), soit 2^6 -2 = 62 adresses disponibles et un CIDR de 32 - 6 = 26 soit /26
- Pôle administratif : le 2^n >= à 20 le plus proche est 2^5 (32), soit 2^5 -2 = 30 adresses disponibles et  un CIDR de 32 - 5 = 27 soit /27
- Pôle technicien : le 2^n >= à 15 le plus proche est 2^4 (16), sauf que le nombre d'adresse disponible est dans ce cas de 14 (2^4 - 2), il manque donc une adresse pour pouvoir raccorder les 15 équipements. Cela nécessite donc de passer sur le 2^n supérieur, soit 2^5 (32), pour un CIDR de 32 - 5 = 27 soit /27
- Pôle développement : le 2^n >= à 12 le plus proche est 2^4 (16), soit 2^4 -2 = 14 adresses disponibles et  un CIDR de 32 - 4 = 28 soit /28


Pour le réseau `172.16.1.0/24` on peut faire le découpage asymétrique suivant :

#### Sous réseau 1 : Pôle informatique
Adresse de réseau : `172.16.1.0/26`
Déblut de plage IP disponible : `172.16.1.1`
Fin de plage IP disponible : `172.16.1.62`
Adresse de broadcoast : `172.16.1.63`

#### Sous réseau 2 : Pôle administratif
Adresse de réseau : `172.16.1.64/27`
Déblut de plage IP disponible : `172.16.1.65`
Fin de plage IP disponible : `172.16.1.94`
Adresse de broadcoast : `172.16.1.95`

#### Sous réseau 3 : Pôle technicien
Adresse de réseau : `172.16.1.96/27`
Déblut de plage IP disponible : `172.16.1.97`
Fin de plage IP disponible : `172.16.1.126`
Adresse de broadcoast : `172.16.1.127`

#### Sous réseau 4 : Pôle développement
Adresse de réseau : `172.16.1.128/28`
Déblut de plage IP disponible : `172.16.1.129`
Fin de plage IP disponible : `172.16.1.142`
Adresse de broadcoast : `172.16.1.143`

Voici ce que ça donne résumé dans un tableau :

##### Découpage asymétrique
| Pôle              | Adresse réseau | Adresse broadcoast | Adresse  début plage | Adresse fin plage |
|------------------|---------------|---------------------|------------------------|----------------|
| Informatique     | 172.16.1.0/26| 172.16.1.63         |      172.16.1.1      |     172.16.1.62    |
| Administratif    | 172.16.1.64/27| 172.16.1.95       |      172.16.1.65    |     172.16.1.94    |
| Technicien       | 172.16.1.96/27 | 172.16.1.127     |       172.16.1.97      |    172.16.1.126     |
| Développement    | 172.16.1.128/28|  172.16.1.143 |      172.16.1.129       |    172.16.1.142     |
