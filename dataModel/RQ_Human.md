## RQ_Human

### combatStatus
Used on each token during a combat to track various status

```
combatStatus = {"activeCA":0,"ccCA":0,"baseCA":0,"bonusCA":0,"weaponCA":0,"magicCA":0,"proactiveCA":0,"reactiveCA":0,"lostProCA":0,"lostCA":0,"castCA":0,"turnStatus":"disabled","activeTurn":0}
```

TST_WARRIOR1 (two weapon + magCA + bon CA + activeTur = 1) : 
```
 {"activeCA":5,"ccCA":5,"baseCA":2,"bonusCA":1,"weaponCA":1,"magicCA":1,"proactiveCA":0,"reactiveCA":0,"lostProCA":0,"lostCA":0,"castCA":0,"turnStatus":"on","activeTurn":1}
```
TST_WARRIOR2 (one weapon + magCA) :
```
{"activeCA":3,"ccCA":3,"baseCA":2,"bonusCA":0,"weaponCA":0,"magicCA":1,"proactiveCA":0,"reactiveCA":0,"lostProCA":0,"lostCA":0,"castCA":0,"turnStatus":"on","activeTurn":0}
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
* **turnStatus** : on, off, delay, out or disabled. 
  * (on, off) : Indicate wether the token has already taken is turn or not, 
  * (delay) : token has delayed it to keep a reactive action, 
  * (out) : token is out for this cycle (because is has no more remaining CA)
  * (disabled) : token can do nothing because is totally out of the combat : incapacitate, dead, etc.
* **activeTurn** : 1 if it is the turn of the token , 0 otherwise.
* **currWeaponNb** : current nb of weapon hold by the token (could not be <0). Use to manage the lost weapon vent during a combat
* **defWeaponNb** : def nb of weapon usually hold by the token (usually set during charchetr creation adn use to reste a token combat status before a new combat






