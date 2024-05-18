## RQ_Lib

Current version : v1.0.1

History :
- v1.0.1 : add modelVersion property
- v1.0.0 : First stable version (including all improvment to manage combat, pnj sheet, etc.)
- v0.0.0 : First unstable version

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
- if (STR+SIZ) =< 50) : newDamageModIndex=ceil((newSTR + newSIZ) 5)-1
  - if (STR+SIZ>50) : newDamageModIndex = ceil((newSTR + newSIZ)/10)+4
```
damageMod = ["-1d8","-1d6","-1d4","-1d2","0","+1d2","+1d4","+1d6","+1d8","+1d10","+1d12","+2d6","+1d8+1d6","+2d8","+1d10+1d8","+2d10","+2d10+1d12","+2d10+1d4"]
```

### Melee Weapon DB

RQ_Lib Property : *meleeWeaponDb*

```
{
	"Archer’s Blade": {
		"Type": "1H Sword",
		"Damage": "1D4",
		"Size": "M",
		"Reach": "M",
		"Enc": "1",
		"ApHp": "4/6",
		"Manoeuvre": "Bleed, Impale",
		"Special": "-5% to bow skill"
	}
}
```

### Range Weapon DB

RQ_Lib Property : *rangeWeaponDb*

```
{
	"Arbalest": {
		"Type": "Crossbow",
		"DmgMod": "N",
		"Damage": "1D12",
		"Range": "180m",
		"Load": "4",
		"StrDex": "STR/DEX",
		"Size": "E",
		"Manoeuvre": "Impale, Sunder",
		"ApHp": "AP/HP",
		"Special": ""
	}
}
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

### fatigueLevel
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

### situationMod
Json structure for malus management based on the situationMOd : Prone, Blinded, Surprised, etc.
`
{
	"none": {
		"skillGrade" : 0,
		"movement" : "no penalty",
		"strikeRank" : 0,
		"actionPoints" : 0,
		"recoveryPeriod" : "none" 
	},
	"prone": {
		"skillGrade" : -20,
		"movement" : "-4m",
		"strikeRank" : 0,
		"actionPoints" : 0,
		"recoveryPeriod" : "none" 
	},
	"blinded": {
		"skillGrade" : -80,
		"movement" : "-6m",
		"strikeRank" : -8,
		"actionPoints" : 0,
		"recoveryPeriod" : "none" 
	}
}
```
situationMod = {"none":{"skillGrade":0,"movement":"no penalty","strikeRank":0,"actionPoints":0,"recoveryPeriod":"none"},"prone":{"skillGrade":-20,"movement":"-4m","strikeRank":0,"actionPoints":0,"recoveryPeriod":"none"},"blinded":{"skillGrade":-80,"movement":"-6m","strikeRank":-8,"actionPoints":0,"recoveryPeriod":"none"}}
```

### heroicDb

* name : heroicId name (must be unique) i.e arrowCutting
  * displayname : i.e Arrow Cutting
  * requirements : i.e DEX 15 or higher, any close combat style at 90% or higher
  * type : categroy of heroic abilities - generic, magic or draconic
  * heroPoints : number to be spent to gain the ability
  * duration :
  * lnk : Link to wiki page
  * desc : info, effects

On the token, heroicID are stored in a JSON array in the propertie *heroicSkills* cf [heroib Skill Mgt](../../libRQII/sheetManagement/README.md)

```
{
	"arrowCutting": {
		"displayname" : "Arrow Cutting",
		"type" : "generic",
		"requirements" : "DEX 15 or higher, any close combat style at 90% or higher",
		"heroPoints" : 10,
		"duration" : "A number of melee rounds equal to CON",
		"lnk":"Rq/HeroicHability#HArrowCutting",
		"desc" : "Your reactions are preternatural, allowing you to parry missile attacks with melee weapons instead of being limited to a shield." 
	},
	"awesomeSmash": {
		"displayname" : "Awesome Smash",
		"type" : "generic",
		"requirements" : "STR 15 or higher, any unarmed or bludgeon weapon style at 90% or higher",
		"heroPoints" : 12,
		"duration" : "One melee attack",
		"lnk":"Rq/HeroicHability#HAwesomeSmash",
		"desc" : "Invoked whilst wielding a bludgeoning weapon or using Unarmed combat, you cause an automatic knockback of 1 metre per 2 points of rolled damage before it is reduced by parrying, armour or magic.	<br>If the victim strikes any obstacle they smash into it, fall prone and automatically receive the attacker’s Damage Bonus to a random location, ignoring any protection." 
	},
	"autocasting": {
		"displayname" : "Autocasting",
		"type" : "magic",
		"requirements" : "DEX 16 or higher, any Magic skill at 90% or higher",
		"heroPoints" : 8,
		"duration" : "",
		"lnk":"Rq/HeroicHability#HAutocasting",
		"desc" : "All of your spell casting times are considered to be one Combat Action less than the listed Casting Time, with any existing Casting Time of one actually only taking one Combat Reaction instead. Spells cast as Combat Reactions still occur on your normal Strike Rank instead of a Combat Action." 
	},
	"blurMovement": {
		"displayname" : "Graceful Blur of Movement",
		"type" : "draconic",
		"requirements" : "POW 15 or higher, Martial Arts 90% or higher",
		"heroPoints" : 8,
		"duration" : "",
		"lnk":"Rq/HeroicHability#HGracefulBlurofMovement",
		"desc" : "The chance of a Dodge critical success is doubled. In addition, the character never needs to Give Ground unless he decides to do so, representing his unfailing ability to maintain his balance and dodge at close-quarters." 
	},
	"predatorRoar": {
		"displayname" : "Predator roar",
		"type" : "draconic",
		"requirements" : "POW 15 or higher, Martial Arts 90% or higher",
		"heroPoints" : 8,
		"duration" : "",
		"lnk":"Rq/HeroicHability#HPredator2019sRoar",
		"desc" : "Each turn that an enemy opposes a roaring dragonspeaker with this Legendary Ability in close combat, the enemy increases their chance to fumble any Weapon skill test by 1%." 
	}
}
```
```
heroicDb = {"arrowCutting":{"displayname":"Arrow Cutting","type":"generic","requirements":"DEX 15 or higher, any close combat style at 90% or higher","heroPoints":10,"duration":"A number of melee rounds equal to CON","lnk":"Rq/HeroicHability#HArrowCutting","desc":"Your reactions are preternatural, allowing you to parry missile attacks with melee weapons instead of being limited to a shield."},"awesomeSmash":{"displayname":"Awesome Smash","type":"generic","requirements":"STR 15 or higher, any unarmed or bludgeon weapon style at 90% or higher","heroPoints":12,"duration":"One melee attack","lnk":"Rq/HeroicHability#HAwesomeSmash","desc":"Invoked whilst wielding a bludgeoning weapon or using Unarmed combat, you cause an automatic knockback of 1 metre per 2 points of rolled damage before it is reduced by parrying, armour or magic.		<br>If the victim strikes any obstacle they smash into it, fall prone and automatically receive the attacker’s Damage Bonus to a random location, ignoring any protection."},"autocasting":{"displayname":"Autocasting","type":"magic","requirements":"DEX 16 or higher, any Magic skill at 90% or higher","heroPoints":8,"duration":"","lnk":"Rq/HeroicHability#HAutocasting","desc":"All of your spell casting times are considered to be one Combat Action less than the listed Casting Time, with any existing Casting Time of one actually only taking one Combat Reaction instead. Spells cast as Combat Reactions still occur on your normal Strike Rank instead of a Combat Action."},"blurMovement":{"displayname":"Graceful Blur of Movement","type":"draconic","requirements":"POW 15 or higher, Martial Arts 90% or higher","heroPoints":8,"duration":"","lnk":"Rq/HeroicHability#HGracefulBlurofMovement","desc":"The chance of a Dodge critical success is doubled. In addition, the character never needs to Give Ground unless he decides to do so, representing his unfailing ability to maintain his balance and dodge at close-quarters."},"predatorRoar":{"displayname":"Predator roar","type":"draconic","requirements":"POW 15 or higher, Martial Arts 90% or higher","heroPoints":8,"duration":"","lnk":"Rq/HeroicHability#HPredator2019sRoar","desc":"Each turn that an enemy opposes a roaring dragonspeaker with this Legendary Ability in close combat, the enemy increases their chance to fumble any Weapon skill test by 1%."}}
```

### traitDb

* name : traits ID -  name (must be unique) i.e excellentSwimmer
  * displayname : i.e Excellent Swimmer
  * type : generic or chaotic
  * d100 : for chaotic traits
  * lnk : Link to wiki page
  * desc : info, effects

On the token, heroicID are stored in a JSON array in the propertie *heroicSkills* cf [heroib Skill Mgt](../../libRQII/sheetManagement/README.md)

```
{
	"darksense": {
		"displayname" : "Darksense",
		"type" : "generic",
		"d100" : 5,
		"lnk":"Rq/MonstersTraits#HDarksense",
		"desc" : "The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.			<br>Creatures with this trait function as well underground as humans function above it in broad daylight." 
	},
	"excellentSwimmer": {
		"displayname" : "Excellent Swimmer",
		"type" : "generic",
		"d100" : 7,
		"lnk":"Rq/MonstersTraits#HDarksense",
		"desc" : "The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.				<br>Creatures with this trait function as well underground as humans function above it in broad daylight." 
	},
	"absorbing": {
		"displayname" : "Absorbing",
		"type" : "chaotic",
		"d100" : 1,
		"lnk":"Rq/TraitChaotiques",
		"desc" : "The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.					<br>Creatures with this trait function as well underground as humans function above it in broad daylight." 
	},
	"accursed": {
		"displayname" : "Accursed",
		"type" : "chaotic",
		"d100" : 2,
		"lnk":"Rq/TraitChaotiques",
		"desc" : "Temporarily weakens the soul of an opponent by 1D8 POW each successful hit." 
	}
}
```
```
traitsDb = {"darksense":{"displayname":"Darksense","type":"generic","d100":5,"lnk":"Rq/MonstersTraits#HDarksense","desc":"The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.						<br>Creatures with this trait function as well underground as humans function above it in broad daylight."},"excellentSwimmer":{"displayname":"Excellent Swimmer","type":"generic","d100":7,"lnk":"Rq/MonstersTraits#HDarksense","desc":"The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.<br>Creatures with this trait function as well underground as humans function above it in broad daylight."},"absorbing":{"displayname":"Absorbing","type":"chaotic","d100":1,"lnk":"Rq/TraitChaotiques","desc":"The creature possesses a combination of Dark Sight, olfactory awareness and echolocation to achieve precise underground awareness and orientation.<br>Creatures with this trait function as well underground as humans function above it in broad daylight."},"accursed":{"displayname":"Accursed","type":"chaotic","d100":2,"lnk":"Rq/TraitChaotiques","desc":"Temporarily weakens the soul of an opponent by 1D8 POW each successful hit."}}
```

## Skills

### CommonSkills

```
{
  "Athletics": {
    "code": "STR+DEX",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Brawn": {
    "code": "STR+SIZ",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Culture (Own)": {
    "code": "INT*2",
    "subtype": "Jrusteli",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Dance": {
    "code": "DEX+CHA",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Drive": {
    "code": "DEX+POW",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Evade": {
    "code": "DEX*2",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Evaluate": {
    "code": "INT+CHA",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "First Aid": {
    "code": "INT+DEX",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Influence": {
    "code": "CHA*2",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Insight": {
    "code": "INT+POW",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Lore (Regional)": {
    "code": "INT*2",
    "subtype": "Kethaela",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Perception": {
    "code": "POW+INT",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Persistence": {
    "code": "POW*2",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Resilience": {
    "code": "CON*2",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Ride": {
    "code": "DEX+POW",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Sing": {
    "code": "CHA+POW",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Sleight": {
    "code": "DEX+CHA",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Stealth": {
    "code": "INT+DEX",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Swim": {
    "code": "STR+CON",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  },
  "Unarmed": {
    "code": "STR+DEX",
    "subtype": "0",
    "lnk": "/Rq/Skills/CommonSkills/"
  }
}
```

```
CommonSkills = {"Athletics":{"code":"STR+DEX","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Brawn":{"code":"STR+SIZ","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Culture (Own)":{"code":"INT*2","subtype":"Jrusteli","lnk":"/Rq/Skills/CommonSkills/"},"Dance":{"code":"DEX+CHA","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Drive":{"code":"DEX+POW","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Evade":{"code":"DEX*2","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Evaluate":{"code":"INT+CHA","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"First Aid":{"code":"INT+DEX","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Influence":{"code":"CHA*2","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Insight":{"code":"INT+POW","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Lore (Regional)":{"code":"INT*2","subtype":"Kethaela","lnk":"/Rq/Skills/CommonSkills/"},"Perception":{"code":"POW+INT","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Persistence":{"code":"POW*2","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Resilience":{"code":"CON*2","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Ride":{"code":"DEX+POW","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Sing":{"code":"CHA+POW","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Sleight":{"code":"DEX+CHA","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Stealth":{"code":"INT+DEX","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Swim":{"code":"STR+CON","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"},"Unarmed":{"code":"STR+DEX","subtype":"0","lnk":"/Rq/Skills/CommonSkills/"}}
```