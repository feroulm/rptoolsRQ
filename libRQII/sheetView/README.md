# Display PJ / PNJ / Monster Sheet

Called from :
- Campain/openSheet
```
Logic - Mermaid Diagram
graph LR
  A1(openSheet) -->|tab| B{Display Tab}
  B -->|main, tokenId| C[viewSheet]
  B -->|magic, tokenId| D[viewSheetMagic]
  B -->|skills, tokenId| E[viewSheetSkills]
  B -->|logs, logTypeFilter, logSessionNameFilter, tokenId| F[viewSheetLogs]
  C -->|tokenId|Z1
  D -->|tokenId|Z1
  E -->|tokenId|Z1
  F -->|tokenId|Z1
	Z1(openSheet - callback)
```

![other Attribute Mgt flow](../../assets/doc/sheetViewFlow.png?raw=true)

## Window Logic
Cf #73 for more details.
- This macro enable to open multiple sheet, one per token.
- But when it come to edition (cf Sheet Management), we reverted back to a single window principle. 
  - otherwise, with all the sub-windows, it became a mess.