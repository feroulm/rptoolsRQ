## RQ_Human

### Localisation HP & App

* Structure for human :

```
locName = loc1=Tête;loc2=Br. G.;loc3=Br. D.;loc4=Poit-;loc5=Abd.;loc6=Jb. G.;loc7=Jb D.
```

```
locD20 = loc1=19-20;loc2=16-18;loc3=13-15;loc4=10-12;loc5=7-9;loc6=4-6;loc7=1-3
```
```
locNb = 7
```

* value are computed based on SIZ+CON & hpInit var
* to manage monster and human which do not respect this rule we use locMod to increase/decrease a specific loc Value

### Charac

bas<Charac> : used to keep the native / permanent value (defined during character creation and incresde / decreased during improvment)
tmp<Charc> : used to keep the temproary value because of an magical artefect that can be removed, a spell etc.

<charac> :  represent the current situation (usally equat to tmp<Charac>, but it can be rested to default value using the baseCharac. It Used to compute the skills.
```
Charac = {"basSTR":11,"basCON":14,"basSIZ":12,"basINT":10,"basPOW":11,"basDEX":15,"basCHA":9,"tmpSTR":11,"tmpCON":14,"tmpSIZ":12,"tmpINT":10,"tmpPOW":11,"tmpDEX":15,"tmpCHA":9}
```

### ArmorPenalty
```
ArmorPenalty = {"base":2,"current":2}
```

### StrikeRank
```
StrikeRank = {"base":2,"current":2}
```
### DamageMod
```
DamageMod = {"base":"+0+,"current":"+0"}
```

### MagicPoint

MagicPoint is the sum POW - dedicatedPOW + other magicSrc (like cristal etc.)
Number is managed staticaly using a counter powerSrcNb
```
MagicPoint = {"MP":{"base":18,"current":15},"dedPOW":1}

{
    "MP": {
        "base": 18,
        "current": 17
    },
    "dedPOW": 1
}
```

### combatStatus
Used on each token during a combat to track various status

```
{
    "turnStatus": "disabled",
    "activeTurn": 0,
    "chargeStatus": "none",
    "situationMod": "none",
    "activeCA": 0,
    "ccCA": 0,
    "proactiveCA": 0,
    "reactiveCA": 0,
    "baseCA": 0,
    "bonusCA": 0,
    "weaponCA": 0,
    "magicCA": 0,
    "castCA": 0,
    "reloadCA": 0,
    "lostProCA": 0,
    "lostCA": 0,
    "firstEvade": 0,
    "weaponReach": "ok",
    "currWeaponNb": 1,
    "defWeaponNb": 1
}
```


TST_WARRIOR1 (two weapon + magCA + bon CA + activeTur = 1) : 
```
 {"activeCA":5,"ccCA":5,"baseCA":2,"bonusCA":1,"weaponCA":1,"magicCA":1,"proactiveCA":0,"reactiveCA":0,"castCA":0,"reloadCA":0,"lostProCA":0,"lostCA":0,"turnStatus":"on","activeTurn":1,"weaponReach":"ok","currWeaponNb":2,"defWeaponNb":2}
```
TST_WARRIOR2 (one weapon + magCA) :
```
{"activeCA":3,"ccCA":3,"baseCA":2,"bonusCA":0,"weaponCA":0,"magicCA":1,"proactiveCA":0,"reactiveCA":0,"castCA":0,"reloadCA":0,,"lostProCA":0,"lostCA":0,"turnStatus":"on","activeTurn":0,"weaponReach":"ok","currWeaponNb":1,"defWeaponNb":1}
```

* **activeCA** : current remaining CA
* **ccCA** : compute using (baseCA + bonusCA + weaponCA + magicCA)
* **baseCA** : comupte using (curDEX+curINT/2)
* **bonusCA** : permanent CA added because of gift , heroic power etc... (not changed during a combat)
* **magicCA** : temporary CA added because of a spell
* **weaponCA** : usually +1 with two weapon but a monster with multiple limb can have more. Loose when weapon is lost.
* **proactiveCA** : CA used as proactive Action during the cycle.  
* **reactiveCA** : CA used as reactive Action during the cycle
* **lostProCA** : lost in case of fumble. Apply only to proactive action.
* **lostCA** : lost in case of fumble. Apply to all CA.
* **castCA** : CA counter needed to cast magic (casting time).
* **reloadCA** : CA counter needed to reload range weapon
* **turnStatus** : on, off, delay, out or disabled. 
  * (on, off) : Indicate wether the token has already taken is turn or not, 
  * (delay) : token has delayed it to keep a reactive action, 
  * (out) : token is out for this cycle (because is has no more remaining CA)
  * (disabled) : token can do nothing because is totally out of the combat : incapacitate, dead, etc.
* **activeTurn** : 1 if it is the turn of the token , 0 otherwise.
* **weaponReach** : indicate wether the token can strike or not.
  * **ok** : nothing special. Default value.
  * **outmanoeuvred** : the token can't attack nor take proactive action for this MR
  * **closed** : the token cannot parry because is weapon is to long, he can only attack with a damage of 1d3+1 (representing the pommel / hilt of his weapon)
  * **outranged** : the token can only attack the weapon of its opponent (or limb of the huge creature i.e a tentacle)
* **situationMod** : indicate situation Combat modifier which can change during a combat (no global situation like darkness, etc.).
  * **none** : nothing special. Default value.
  * **prone** : -20% malus for attack and parry
  * **blinded** : -80% malus for attack and parry
* **chargeStatus** :
  * **none** : default value. no charge declared
  * **prepareCharge** : charge has been declared, token is moving during one MR. 
  * **chargeReady** : token has been moving during one mr he must select a type of charge passage or crash at its first turn.
  * **passageDone** : token as done its charge and conitnue moving till end of the turn.
* **currWeaponNb** : current nb of weapon hold by the token (could not be <0). Use to manage the lost weapon vent during a combat
* **defWeaponNb** : def nb of weapon usually hold by the token (usually set during charchetr creation adn use to reste a token combat status before a new combat


### combatLog

- Store the last proactiveAction taken , the last reactiveAction taken and the last consequence (damage, status change etc.). It is prefixed with corresponding MR_Nb and Cycle_Nb

```
combatLog = {"lastProactiveAction":"","lastReactiveAction":"","lastTokenChange":"","turnDeclaration":""}
```
Example  : 
- lastProactiveAction : MR_1, C_1 tokenname has done attack 
- lastReactiveAction : MR_1, C_1 tokenname has done parry 
- lastTokenChange : MR_1, C_1 tokenname has lost 3pts in L_ARM

### commonSkills

```
{
    "Athletics": {
        "code": "STR+DEX",
        "subtype": "",
        "current": 53,
        "base": 23,
        "culture": 0,
        "profession": 0,
        "experience": 30
    },
    "Brawn": {
        "code": "STR+SIZ",
        "subtype": "",
        "current": 33,
        "base": 23,
        "culture": 0,
        "profession": 0,
        "experience": 10
    },
    "Culture (Own)": {
        "code": "INT*2",
        "subtype": "Jrusteli",
        "current": 50,
        "base": 20,
        "culture": 30,
        "profession": 0,
        "experience": 0
    },
    "Dance": {
        "code": "DEX+CHA",
        "subtype": "",
        "current": 21,
        "base": 21,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Drive": {
        "code": "DEX+POW",
        "subtype": "",
        "current": 23,
        "base": 23,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Evade": {
        "code": "DEX*2",
        "subtype": "",
        "current": 44,
        "base": 24,
        "culture": 0,
        "profession": 0,
        "experience": 20
    },
    "Evaluate": {
        "code": "INT+CHA",
        "subtype": "",
        "current": 49,
        "base": 19,
        "culture": 0,
        "profession": 0,
        "experience": 30
    },
    "First Aid": {
        "code": "INT+DEX",
        "subtype": "",
        "current": 22,
        "base": 22,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Influence": {
        "code": "CHA*2",
        "subtype": "",
        "current": 18,
        "base": 18,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Insight": {
        "code": "INT+POW",
        "subtype": "",
        "current": 21,
        "base": 21,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Lore (Regional)": {
        "code": "INT*2",
        "subtype": "Kethaela",
        "current": 50,
        "base": 20,
        "culture": 30,
        "profession": 0,
        "experience": 0
    },
    "Perception": {
        "code": "POW+INT",
        "subtype": "",
        "current": 31,
        "base": 21,
        "culture": 0,
        "profession": 0,
        "experience": 10
    },
    "Persistence": {
        "code": "POW*2",
        "subtype": "",
        "current": 52,
        "base": 22,
        "culture": 0,
        "profession": 0,
        "experience": 30
    },
    "Resilience": {
        "code": "CON*2",
        "subtype": "",
        "current": 48,
        "base": 28,
        "culture": 0,
        "profession": 0,
        "experience": 20
    },
    "Ride": {
        "code": "DEX+POW",
        "subtype": "",
        "current": 23,
        "base": 23,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Sing": {
        "code": "CHA+POW",
        "subtype": "",
        "current": 20,
        "base": 20,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Sleight": {
        "code": "DEX+CHA",
        "subtype": "",
        "current": 31,
        "base": 21,
        "culture": 0,
        "profession": 0,
        "experience": 10
    },
    "Stealth": {
        "code": "INT+DEX",
        "subtype": "",
        "current": 22,
        "base": 22,
        "culture": 0,
        "profession": 0,
        "experience": 0
    },
    "Swim": {
        "code": "STR+CON",
        "subtype": "",
        "current": 35,
        "base": 25,
        "culture": 0,
        "profession": 0,
        "experience": 10
    },
    "Unarmed": {
        "code": "STR+DEX",
        "subtype": "",
        "current": 33,
        "base": 23,
        "culture": 0,
        "profession": 0,
        "experience": 10
    }
}
```

### Weapons

* Manage using str property (not json) - because i start by using an example in rptool wiki ;)
* the NumWeapons property is used to manage a unique number for each weapon.
  * it is used in each weaponAttribute property fields : ```Weapon1Name = "Sabre"```
  * It is never decreased (otherwise each weapon must be renumbered when one is deleted !)
  

