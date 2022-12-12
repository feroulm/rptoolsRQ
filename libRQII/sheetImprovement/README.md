# Manage Improvement for a token

Called from :
- viewSheet -Y menu Improve
```
Logic - Mermaid Diagram
graph TD
    A[openSheetImprovement] -->|tokenId| B1(editSheetImprovement)
    B1 --> C1[/skills forms/]
    C1 -->|tokenId, skType| D1(subEditImproveSkill)
    D1 -->|tokenId, params| E1(improveSkills)
    E1 --> Z1(openSheetImprovement - callback)
    B1 --> C2[/improvement pts,validate improvement/]
    C2 --> |tokenId| D2(updateImprovement)
    D2 --> |tokenId| E2[[resetSkillsExperienceTmp]]
    C2 --> Z1
    C2 --> Z2(openImprovementLogs - callback)
    B1--> C3>Show Logs]
    C3 -->|tokenId| D3[openImprovementLogs]
    D3 -->|tokenId| E3(viewImprovementLogs)
    E3 --> Z2
```


![other Attribute Mgt flow](../../assets/doc/improvementMgtFlow.png?raw=true)

improvementPool
* currTmp : nb de pts restant tant que l'improvement n'est pas validé
* origTmp : valeur de depart au debut de la session d'improvment , c.a.d après ajout d'un roll. 
* currPts : Point restants une fois l'improvement validé
* prevPts : précedente valeur de currPts avant la session d'improvement
* status : running, done

```
improvementPool = {"prevPts": 0,"currPts": 0,"origTmp": 0,"currTmp" : 0, "status": "done"}       
```

improvementLog
* "improveLog1":
	* nbRoll
	* prevPts : remaining pts before the roll or after validation
	* currPts : nbe pts pool after rolls or after validation
	* des : ctx of the improvment i.e after scenar 1
	
```
improvementLog= {"improveLog1":{"nbRoll": 0,"prevPts": 0,"currPts": 0,"desc" : "Init"}}
```
	
```
improvementLog= {"improveLog1":{"nbRoll": 3,"prevPts": 0,"currPts": 0,"desc" : "after scenar 1"},"improveLog1":{"nbRoll": 2,"prevPts": 10,"currPts": 20,"desc" : "after scenar 2"}}      
```
	
Rules / Gestion du status done / running
- Si on update un skill sans ajouter un roll on créer quand meme un nouveau log 

- on ne peut pas ajouter de roll tant que le status est running (on masque le form)
- on ne peut pas valider un improvement tant le status est done (on masque le form)
- Des qu'on udpate une valeur, on remet le statut de l'improvment à running, dans ce cas le log ne précise pas de scenar - il mentionne "use remaining improvement pts"
- Des qu'on add un roll on remet le statut a running

prevPts - currPts omntre combien on a depensé lors de la dernère session d'improvement.

Cinématique Sample

1) Première session d'improvement : 
- prevPts = 0
- currPts = 0
- origTmp = 0
- currTmp = 0

2) on ajoute 15pts -> logImprovment
- prevPts = 0
- currPts = 0
- origTmp = 15
- currTmp = 15

3)Ajout de 5 pts dans un comp
- prevPts = 0
- currPts = 0
- origTmp = 15
- currTmp = 10

Quand on valide une session d'improvement:
- prevPts : nb de pt disponibles avant la dernière séance d'improvment (15)
- currPts : deviens ce qui reste dans currTmp ( le non comsommé) et origTmp et currTmp ont également la même valeur (en fait on met à jour le pool origTmp)
5)Le tableau deviens :
- prevPts = 15
- currPts = 10
- origTmp = 10
- currTmp = 10

6) Deuxieme session d'improvment, on ajoute 2 roll (10pts)
- prevPts = 15
- currPts = 10
- origTmp = 20
- currTmp = 20
*currPts sert à voir , lorsque la session n'est pas validée, combien il restait avant d'ajouter des pts*

7)Ajout de 5 pts dans un comp
- prevPts = 15
- currPts = 10
- origTmp = 20
- currTmp = 15

8)On valide
- prevPts = 20
- currPts = 15
- origTmp = 15
- currTmp = 15


