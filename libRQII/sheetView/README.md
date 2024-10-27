# Display PJ / PNJ / Monster Sheet

Called from :
- Campain/openSheet
```
Logic - Mermaid Diagram
graph LR
  subgraph Menu
    Z1(openSheet - callback)
    Z2(openAPHP)
    Z3(openHumCombatAttr)
    Z4@{ shape: braces, label: "Idem pour chaque tab (mais non représenté)" }
  end
  A1(openSheet) -->|tab| B{Display Tab}
  B -->|main, tokenId| C[viewSheet]
  B -->|magic, tokenId| D[viewSheetMagic]
  B -->|skills, tokenId| E[viewSheetSkills]
  B -->|logs, logTypeFilter, logSessionNameFilter, tokenId| F[viewSheetLogs]
  C -->|tokenId|Menu

	
```

![other Attribute Mgt flow](../../assets/doc/sheetViewFlow.png?raw=true)

## Window Logic
Cf #73 for more details.
- This macro enable to open multiple sheet, one per token.
- But when it come to edition (cf Sheet Management), we reverted back to a single window principle. 
  - otherwise, with all the sub-windows, it became a mess.