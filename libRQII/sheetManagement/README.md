# sheetManagement
rpTools Macro for RuneQuest

*Purpose* : Viewing and editing human and monster sheet

Compose of two main window
- viewSheet
- editSheet

## editSheet
```
Logic - Mermaid Diagram
graph TD
    A(openSheetMgt) -->|tokenId| B[editSheet]
    B -->B1(refresh lnk)
    B1 -->A
    B -->B2(Equipment lnk)
    B2 -->C2(openSheetEquipementMgt)
    B -->B3[/Charac Frm/]
    B3 -->|tokenId,charac data|C3(updateCharac)
    B -->B4(Reset Charac lnk)
    B4 -->|tokenId|C4(resetCharacBase)
    B -->B5[/Ded POW Frm/]
    B -->B6[/Adv Skill FRM/]
    B -->B7[/Del Adv Skill lnk/]
    B7 -->|tokenId,skType,magic,...|C7(delTokenSkill)
```

![edit Sheet Mgt flow](../../assets/doc/editSheetFlow.png?raw=true)


### Fatigue level

#### Data Model
cf RQ_Human_Prop and RQ_Monster_Prop

Possible Values are taken from RQ_Lib/fatigueLevel prop,
We keep a json structure, in case we need to add malus management.
```
fatigue = {
    "level": "Fresh"
}
```

Sample to be copied on a token :
```
{"level":"Fresh"}
```

Can be called from editSheet (when managing a token) or from openHumCombatAttr (when modified during a combat)
```
Logic - Mermaid Diagram
graph TD
    A1(openSheetMgt) -->|tokenId| B1(editSheet)
	A2(openHumCombatAttr) -->|tokenId| B2(editHumCombatAttr)
    B1(editSheet) -->|tokenId, srcWindow| C[updateFatigue]
	B2(editHumCombatAttr) -->|tokenId| C[updateFatigue]
    C -->|srcWindow = openSheetMgt|Z1
    C -->|default|Z2
	Z1(openSheetMgt - callback)
	Z2(openHumCombatAttr - callback)
```

![Fatigue Mgt flow](../../assets/doc/fatigueMgtFlow.png?raw=true)

Principle :
- From the list box , select the fatigue level. The list box is filled using RQ:Lib/fatigueLevel property

### heroic Ability

#### Datamodel
```
heroicSkills = ["arrowCutting","awesomeSmash"]
```

Invoked whilst wielding a bludgeoning weapon or using Unarmed combat, you cause an automatic knockback of 1 metre per 2 points of rolled damage before it is reduced by parrying, armour or magic.
If the victim strikes any obstacle they smash into it, fall prone and automatically receive the attacker’s Damage Bonus to a random location, ignoring any protection.

Principle
- Heroic abilities are added from a template library : [RQ_Lib/heroicDb](../../dataModel/RQ_Lib.md)
- A token can have N heroic
- We only store on the token ability name, other values will be displayed from the template
- So it is managed in the same way as an advanced skill 

Its called from editSheet , for RUD , create is another dialog (same has adv skill) or from openHumCombatAttr (when modified during a combat)
```
Logic - Mermaid Diagram
graph TB
    A1[openSheetMgt] -->|tokenId| B1(editSheet)
	B1 -->|form| C1[/frm Update Heroic/]
    B1 -->|tokenId| C3>lnk Add heroic]
	C1 -->|tokenId,frmfields| D1(updateHeroic)
	D1 -->|tokenId|Z1
	C1 -->|tokenId,heroicId| D2(delHeroic)
	D2 -->|tokenId|Z1
    C3 -->|tokenId| D3[openAddHeroic]
    subgraph add Heroic
	    D3 --> |tokenId| E3(editAddHeroic)
	    E3 --> |tokenId,frm field|F3(addHeroic)
        F3 -->|tokenId|Z1
    end
	Z1(openSheetMgt - callback)
```

![Heroic Mgt flow](../../assets/doc/heroicMgtFlow.png?raw=true)