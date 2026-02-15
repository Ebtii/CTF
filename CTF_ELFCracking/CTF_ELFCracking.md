# CTF : ELF Cracking 1 (Challenge x86)

### Avant-propos 
Conformément aux bonnes pratiques des CTF, le flag final est masqué. 

### Description 

**Objectif :** Retrouver le mot de passe contenu dans un binaire ELF 32 bits fourni (`ch1.bin`). 

**Auteur :** g0uZ  
**Source :** Root Me

**Type :** Reverse engineering / Cracking

### Résolution 

Premièrement, nous identifions le type de fichier. 

```bash 
file ch1.bin
```

**Résultat :** 

```bash 
ELF 32-bi LSB executable, Intel 80386, dynamically linked, not stripped
```

**Observation :** Il s'agit d'un binaire qui utilise des registres 32 bits avec les bibliothèques associées, ici la `lib`. Le fichier utilise des fonctions externes au moment de l'exécution (`dynamic linking`).

Ensuite, nous inspectons les chaînes. 

```bash 
strings ch1.bin
```
Nous trouvons notamment : 


```bash 
Allocating memory
Reallocating memory
XXXXXXXXX
############################################################
##        Bienvennue dans ce challenge de cracking        ##
############################################################
Veuillez entrer le mot de passe : 
Bien joue, vous pouvez valider l'epreuve avec le pass : %s!
```
![Capture du terminal](CTF/CTF_ELFCracking/affichage_strings.png)

Or la seule chaîne qui ressemble à un mot de passe probable est `XXXXXXXXX` (le flag est volontairement masqué par respect des règles). 

[Capture du terminal](CTF/CTF_ELFCracking/inputFlag.png)

# Résultat 

En essayant le flag `XXXXXXXXX` qui apparaissait en clair, le CTF est bien validé. 