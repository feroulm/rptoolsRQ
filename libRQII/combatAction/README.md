# Combat Action (CA) Management

CA is managed using the property *combatStatus* 
- baseCa depends on DEX & INT charac
- Total CA is composed of baseCA + bonusCA + weaponCA + magicCA
- cf [RQ_Human Data model](../../dataModel/RQ_Human.md).

CA is modified
- When a PNJ is created / updated (i.e following an improvement session)
- During a combat

## Combat Status
When this structure evolves it must be patched on all token, to do this use the macro :
- cf [resetPropCombatJson](../tokenPropertyManagement/resetPropCombatJson.rqm)
Process is described inside the macro.

Don't forget also to change the macro [updateGlobalCombat](./updateGlobalCombat.rqm) that reset the Combat Status.

## CA creation / update
The following macro are involved
- *initToken* : it define a default value (set to 0) for all. These values are wrong (a.k.a not calculated based on DEX & INT) but will be updated when charac will be modified later.
- *sheetManagement/updateCharac* : recompute baseCA (following a charc update) and recompute ccCA by calling the function macro combatAction/computeCcCA
- *combatAction/computeCcCA* : function to recompute ccCA,
- *editSheet* : 
  - change button call updateCharac
  - Update magic CA button call computeCcCA function

For the moment improvement forms doesn't update CA since it enable only skill improvement not charac.

editSheet
## CA Management during a Combat

### lostProCA principle

If lostProCA>0 the player can't take any proactive action : 
 - this condition is evaluated in *editCombatAction* , it sets the flag *showNoProactiveAction*, which results in enabling the player to only choose the *Delay* (cf proactive action desc in xwiki).
 
 Logic with *Delay* + *lostProcCA*
 - If the player try to interrupt, the *editComabtAction* will still only show the delay action when lostProCA > 0
 - At the end of a cycle, if turn status = *Delay*, the *resetDelayTurn* function is called and will decrement *lostProCA*
	- cf *updateGlobalCombat* for this implementation.
- Note : after choosing *delay*, the token may still use reactive ation which will also decrement "lostProCA*. If he use all its CA its status will became *out* instead of *delay*, so *resetDelayTuen* will no be triggered (otherwise it would have created an issue by removing an extra *lostProCA* without having any Ca left !)


## openCombat.rqm
- open the combat window and put all the token that are in the initiative list / window in a table
- provide global button to manage the comabt phase (next cycle & mr, reste,...)
- enable to open the combat action window on a specific token
  - only one action combat window at a time for a specific token, does not support to open two windows in parrallel

```
Logic - Mermaid Diagram
graph LR
    A[openCombat] -->|tokens - from getInitiativeList | B(editCombat)
    B -->B1(refresh lnk)
    B1 -->A
    B -->B2[/Roll Init Btn/]
    B2 -->|tokens,rollinit|C1(updateGlobalCombat)
	B -->B3[/Next Cycle Btn/]
    B3 -->|tokens,nxtcycle|C1(updateGlobalCombat)
	B -->B4[/Next MR Btn/]
    B4 -->|tokens,nxtmr|C1(updateGlobalCombat)
	B -->B5[/Start Reset Btn/]
    B5 -->|tokens,reset|C1(updateGlobalCombat)
	B -->B6[/Act Btn/]
    B6 -->|tokenId,msg|C2[openCombatAction]
	C1 -->A
	C1 -->C2
```
![openCombat Mgt flow](../../assets/doc/openCombat.png?raw=true)

## openCombatAction.rqm

* they are described in https://www.inyanga.me/xwiki/bin/view/Rq/MapTool/MaptoolCombat/#HTableaudesactions
```
Logic - Mermaid Diagram
graph LR
    A[openCombatAction] -->|tokenId| B(editCombatAction)
	B -->B1[/Active action buttons/]
	B1 -->|tokenId,action|C1(updateCombatProactive)
	B -->B2[/Reactive action buttons/]
	B2 -->|tokenId,action|C2(updateCombatReactive)
	B -->B3[/Status buttons/]
	B3 -->|tokenId,action|C4(updateCombat)
	B -->B4[/Damage heal button/]
	B4 -->|tokenId|C3(openAPHP)
	B -->B5[/Change carac button/]
	B5 -->|tokenId|C5(openHumCombatAttr)
	B -->B6[/Edit combat status/]
	B6 -->|tokenId|C5(setTokenCombatStatus)
```
![openCombatAction Mgt flow](../../assets/doc/openCombatAction.png?raw=true)

## UDF for this module

| Function | Desc |
| ---- | ---- |
| processReactiveCA | UDF : decrease remaining CA and increase nb of reactive CA spent.<br> Update the state & turnStatus if token is out of CA.|
| another UDF | |