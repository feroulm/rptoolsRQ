## RQ_Lib

### combat

Keep track of MR & Cycle
```
combat = {"mr":1,"cycle":1,"initRoll":1}
```

* **mr** : current MR nb
* **cycle** : current Cycle nb within an MR
* **initRoll** : nb of initiatvie roll done during the combat

### damageMod
JSON Array to define damage modifier. Base on range of size 5 of (STR+SIZ).
Index is based on the formula : 
- if (STR+SIZ) =< 50) : newDamageModIndex = ceil((newSTR + newSIZ)/5)-1
- if (STR+SIZ > 50) : newDamageModIndex = ceil((newSTR + newSIZ)/10)+4
```
damageMod = ["-1d8","-1d6","-1d4","-1d2","0","+1d2","+1d4","+1d6","+1d8","+1d10","+1d12","+2d6","+1d8+1d6","+2d8","+1d10+1d8","+2d10","+2d10+1d12","+2d10+1d4"]
```