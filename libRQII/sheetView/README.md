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