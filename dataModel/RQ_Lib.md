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

### Spell DB

- Simplification : All spell use the same data model. Not needed attribute are left empty.
- When added to a token, they keep the same structure. On a token. magnitude can be different from default value

```
{
    "heal": {
	    "displayname": "Heal",
        "type": "common",
        "grimoire": "",
		"cult" : "",
        "magnitude": 1,
        "lnk": "Rq/SpellBook#HHeal"
    },
	"protection": {
	    "displayname": "Protection",
        "type": "common",
        "grimoire": "",
		"cult" : "",
        "magnitude": 1,
		"lnk": "Rq/SpellBook#HProtection"
    }
}
```
####Divine
```
{
    "absorption": {
	    "displayname": "Absorption",
        "type": "divine",
        "grimoire": "",
		"cult" : "",
        "magnitude": 1,
        "lnk": "Rq/SpellBookDivine#HAbsorption"
    },
	"animateUndead": {
	    "displayname": "Animate Undead",
        "type": "divine",
        "grimoire": "",
		"cult" : "",
        "magnitude": 1,
		"lnk": "Rq/SpellBookDivine#HAnimateUndead"
    }
}
```
* name : spell name (must be unique) i.e detectWater
  * displayname : i.e detect (water)
  * type : common, divine, sorcery, draconic, spirit
  * grimoire : grimoire id, cult id
  * cult :
  * magnitude :
  * lnk : spell lnk in wiki
  
```  
commonSpellDb =
```

#### fatigueLevel
we use a Json structure in case we want to add malus management
`
{
	"Fresh": {
		"skillGrade" : 0,
		"movement" : "no penalty",
		"strikeRank" : 0,
		"actionPoints" : 0,
		"recoveryPeriod" : "none" 
	},
	"Winded": {
		"skillGrade" : -20,
		"movement" : "no penalty",
		"strikeRank" : 0,
		"actionPoints" : 0,
		"recoveryPeriod" : "15mn" 
	},
	"Tired": {
		"skillGrade" : -20,
		"movement" : "-1m",
		"strikeRank" : 0,
		"actionPoints" : 0,
		"recoveryPeriod" : "3h" 
	},
	"Wearied": {
		"skillGrade" : -40,
		"movement" : "-2m",
		"strikeRank" : -2,
		"actionPoints" : 0,
		"recoveryPeriod" : "6h" 
	},
	"Exhausted": {
		"skillGrade" : -40,
		"movement" : "halved",
		"strikeRank" : -4,
		"actionPoints" : -1,
		"recoveryPeriod" : "12h" 
	},
	"Debilitated": {
		"skillGrade" : -80,
		"movement" : "halved",
		"strikeRank" : -6,
		"actionPoints" : -2,
		"recoveryPeriod" : "18h" 
	},
	"Incapacitated": {
		"skillGrade" : -80,
		"movement" : "immobile",
		"strikeRank" : -8,
		"actionPoints" : -3,
		"recoveryPeriod" : "24h" 
	},
	"SemiConscious": {
		"skillGrade" : -200,
		"movement" : "no activities",
		"strikeRank" : -100,
		"actionPoints" : -10,
		"recoveryPeriod" : "36h" 
	},
	"Comatose": {
		"skillGrade" : -200,
		"movement" : "no activities",
		"strikeRank" : -100,
		"actionPoints" : -10,
		"recoveryPeriod" : "48h" 
	}
}
```
fatigueLevel = {"Fresh":{"skillGrade":0,"movement":"no penalty","strikeRank":0,"actionPoints":0,"recoveryPeriod":"none"},"Winded":{"skillGrade":-20,"movement":"no penalty","strikeRank":0,"actionPoints":0,"recoveryPeriod":"15mn"},"Tired":{"skillGrade":-20,"movement":"-1m","strikeRank":0,"actionPoints":0,"recoveryPeriod":"3h"},"Wearied":{"skillGrade":-40,"movement":"-2m","strikeRank":-2,"actionPoints":0,"recoveryPeriod":"6h"},"Exhausted":{"skillGrade":-40,"movement":"halved","strikeRank":-4,"actionPoints":-1,"recoveryPeriod":"12h"},"Debilitated":{"skillGrade":-80,"movement":"halved","strikeRank":-6,"actionPoints":-2,"recoveryPeriod":"18h"},"Incapacitated":{"skillGrade":-80,"movement":"immobile","strikeRank":-8,"actionPoints":-3,"recoveryPeriod":"24h"},"SemiConscious":{"skillGrade":-200,"movement":"no activities","strikeRank":-100,"actionPoints":-10,"recoveryPeriod":"36h"},"Comatose":{"skillGrade":-200,"movement":"no activities","strikeRank":-100,"actionPoints":-10,"recoveryPeriod":"48h"}}
```
