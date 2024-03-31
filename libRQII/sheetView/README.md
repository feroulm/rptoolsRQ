# Display PJ / PNJ / Monster Sheet

Called from :
- Campain/openSheet
```
Logic - Mermaid Diagram
graph LR
    A1(openSheet) -->|tokenId| B1(viewSheet)
    B1 -->|tokenId, params| C[updateOtherAttr]
    C -->|tokenId|Z1
	Z1(openSheetMgt - callback)
```

![other Attribute Mgt flow](../../assets/doc/otherAttrMgtFlow.png?raw=true)

## Window Logic
Cf #73 for more details.
- This macro enable to open multiple sheet, one per token.
- But when it come to edition (cf Sheet Management), we reverted back to a single window principle. 
  - otherwise, with all the sub-windows, it became a mess.