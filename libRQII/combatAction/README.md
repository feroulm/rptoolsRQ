# Combat Action (CA) Management

CA is managed using the property *combatStatus* 
- baseCa depends on DEX & INT charac
- Total CA is composed of baseCA + bonusCA + weaponCA + magicCA
- cf [RQ_Human Data model](../../dataModel/RQ_Human.md).

CA is modified
- When a PNJ is created / updated (i.e following an improvement session)
- During a combat

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