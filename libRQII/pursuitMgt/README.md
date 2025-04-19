#Pursuit Manager

Gestionnaire de poursuite

## Principe

Une poursuite se gère en mode round de mélée et sans CA.
- A chaque MR une seule action est possible _Sprint_ ou _Run_
- Le _Sprint_ est plus rapide mais il fatigue : il est généralement utilisé au démarrage.
- le mode _Run_ est utilisé si la poursuite "dure" ... elle est moins faitguante.

Cf règles RQ : https://www.inyanga.me/xwiki/bin/view/Rq/Skills/SkillRolls/Pursuit/

Principaux composants du module :
- [ ] pursuitToken :   Chaque poursuite possède un token spécifique (même principe que pour le combatLog), 
- [ ] pursuitList : structure comme une initiativeList dans laquelle on gere les membre de la poursuite. Ils sont réordonné non pas par rapport à l'initi mais à leur abscisse currX.
- [ ] pursuitView : fenetre de gestion de la poursuite. comme combatView avec un tab "principal" et une tab Log


###  token de poursuite
Chaque poursuite possède un token spécifique (même principe que pour le combatLog), ce qui permet de gérer plusieurs poursuites sur une même map.
Ce token a pour propriétés : 
- pursuitList
- pursuitLog

### pursuitList
Structure comme une initiativeList dans laquelle on gère les membres de la poursuite. Ils sont réordonnés par rapport à leur abscisse _currX_.

JSON structure : 
* mr : le MR en cours
* desc : description de la poursuite
* tokens : un tableau ordonné (JSON Array) des tokens (JSON Object) qui participent à la poursuite.
*
JSON structure pour chaque token : 
* tokenID : l'id du token
* startX : sa position ou moment il rejoint la poursuite pour la première fois
* prevX : sa position lors du MR précédent
* currX : sa position dans le MR en cours (après avoir effectué son sprint)

=== Exemple
_sur map  :   \_Main_AE_
- TST_THUG1: tokenId  : 457D6AE642AC4C2386067D1B4729204C
- TST_ShadowLizard1: tokenId : B2C6803A77C04871A989E38CAF377DDE
- TST_WARRIOR1: tokenId : 050FF7DD7FEE4D1994AD53D44589AA52
- TST_WIZARD1_PJ: tokenId : D1DDA762D82144C6845C4AEEDDBBEDB7

La course commence avec TST_THUG1, TST_ShadowLizard1 & TST_WARRIOR1
TST_WIZARD1_PJ

```
{
  "mr": 1,
  "desc": "TST_WARRIOR1 & TST_WIZARD1_PJ chassent TST_THUG1 & TST_ShadowLizard1 ",
  "tokens":   [
        {
      "startX": "4",
      "prevX": "4",
      "currX": "",
      "tokenId": "457D6AE642AC4C2386067D1B4729204C"
    },
        {
       startX": "4",
      "prevX": "4",
      "currX": "",
      "tokenId": "B2C6803A77C04871A989E38CAF377DDE"
    },
        {
       startX": "0",
      "prevX": "0",
      "currX": "",
      "tokenId": "050FF7DD7FEE4D1994AD53D44589AA52"
    }
  ]
}
```
### openPursuit
Ouvre la fenêtre de globale de gestion elle est composée de deux tabs : 
- viewPursuit : la fenetre de gestion de la poursuite
- viewPursuitLog : les logs de la poursuite. Différent des combats logs.

Principe que le poursuite se gère à part , car uniquement en MR et pas de gestion de CA.

### viewPursuit

La fenetre de globale de gestion elle permet : 

- [ ] d'ajouter / retirer des token dans la poursuite ( avec definition du startX / currX / prevX )
- [ ] d'initialiser une poursuite (remet a jour le startX
- [ ] d'afficher le MR courant par rapport au début de la course
- [ ] d'effectuer une action de SPRINT dans le MR courant (si elle n'est pas encore réaliser)
- [ ] de passer au MR suivant ce qui à pour effet de recalculer les positions de chacun.

### viewPursuitLog