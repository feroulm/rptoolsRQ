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
    B --> C1[/Update Common Spell/] 
    B --> C2[/Update Divine Spell/] 
    B --> |tokenId, nameFilter,typeFilter| C3(editAddSpells)
    C1 --> |tokenId| D(updateSpells)
    C2 --> |tokenId| D(updateSpells)
```

