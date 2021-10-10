# sheetManagement
rpTools Macro for RuneQuest

*Purpose* : Viewing and editing human and monster sheet

Compose of two main window
- viewSheet
- editSheet

## editSheet

Composed of sub-windows for spellManagement
### spellManagement

Logic - Mermaid diagram
```
graph TD
    A(openSheetSpellMgt) -->|tokenId, nameFilter,typeFilter| B[editSheetSpellMgt]
    B --> C1[/Common Spell Frm/] 
    B --> C2[/Divine Spell Frm/] 
    B --> |tokenId, nameFilter,typeFilter| C3(editAddSpells)
    C1 --> |tokenId, spellType| D(updateSpells)
    C2 --> |tokenId, spellType| D(updateSpells)
    C3 --> E1[/Filter/]
    C3 --> E2[/Add Spell Frm/]
    C3 --> E3[/Create Spell Frm/]
    E2 --> |tokenId + All spell Fields| F1(addSpell)
    E3 --> |tokenId + All spell Fields| F2(createSpell)
    D --> |tokenId| Z
    E1 --> |tokenId| Z
    F1 --> |tokenId| Z
    F2 --> |tokenId| Z
    Z(openSheetSpellMgt -callback)
```

![spell Mgt flow](../../assets/doc/spellManagementFlow.png?raw=true)
