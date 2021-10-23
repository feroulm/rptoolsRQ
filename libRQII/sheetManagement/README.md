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

