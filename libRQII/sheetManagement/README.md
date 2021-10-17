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

Composed of sub-windows for spellManagement
### spellManagement

principle :
- library of spells are defined on Lib RQII token using spellsDb property (cf Data Model/RQ_Lib.md)
- Then they are CRUD on a token using the spellManagement action.
- When added to a token the spell is copied to the token property (spells, divineSpells, sorcereySpells, draconicSpells, draconicPrepared)
- draconicPrepared & spiritSpell are not implemented yet

Logic - Mermaid diagram
```
graph TD
    A(openSheetSpellMgt) -->|tokenId, nameFilter,typeFilter| B[editSheetSpellMgt]
	B --> |tokenId, nameFilter,typeFilter| C1(editAddSpells)
    B --> C2[/Each Spell Frm/] 
	B --> C3[/Each Spell Del Lnk/] 
	B --> C4[/Drac. pre. lnk/]
    C2 --> |tokenId, spellType| D2(updateSpells) 
    C3 --> |tokenId, spellType, spellId| D3(delSpell)
	D3 --> |keyPrefix,Json| E4[[reindexJson]]
	C4 -->|tokenId, spellName, spellMagnitude|D4(addPreparedSpell)
    C1 --> E1[/Filter/]
    C1 --> E2[/Add Spell Frm/]
    C1 --> E3[/Create Spell Frm/]
	D2 --> |tokenId| Z
	D3 --> |tokenId| Z
	D4 --> |tokenId| Z
	E1 --> |tokenId| Z
    E2 --> |tokenId + All spell Fields| F1(addSpell)
    E3 --> |tokenId + All spell Fields| F2(createSpell)
    F1 --> |tokenId| Z
    F2 --> |tokenId| Z
    Z(openSheetSpellMgt -callback)
```

![spell Mgt flow](../../assets/doc/spellManagementFlow.png?raw=true)
