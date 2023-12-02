
### spiritManagement
Usage : cf [xwiki - MapTool - Pnj Manager](https://www.inyanga.me/xwiki/bin/view/Rq/MapTool/PnjManager/)

Principle :
  - spirits are managed as token, the ref library of all spirits is a specific map named (_Spirit_Lib) with all the token on it.
  - on the character token, in the spiritSpells property, we store a json structure containing (described also in DataModel/RQ_Human.md)
  
```
spiritSpells = {
    "spirit1": {
        "spiritTokenId": "",
        "spiritBaseName": "Soul Eater",
		"spiritCustomName" : "My Soul Eater",
		"spiritLibMapName" : "_Spirit_Lib"
    },
	"spirit2": {
        "spiritTokenId": "",
        "spiritBaseName": "Wolf Spirit",
		"spiritCustomName" : "My Wolf Spirit",
		"spiritLibMapName" : "_Spirit_Lib"
    }
}
```
  - spiritID is managed the same way we manage preparedDraconicSpellId (so we need a renumbering in case of suppression & it's not ordered

CRUD
  -  to add a spirit on a sheet, with provide a list of all the token that are the map _Spirit-Lib 
     - we build a list box with the spirit name / icone (like in the summonMacro of bag of trick)
	 
  - If we want to change the carac of the invocated spirit we use the monster default edit sheet as with normal token.
  - If we want ot change the carac of the template, we edit the token on _Spirit_Lib map. It will not update existing instance on othermap.

Display - On the Edit Sheet
  - list with just a name, a link to delete the spirit, a link to display the spirit Sheet in a another window (Prio 2 ?)

Display - on the Viewing Sheet
   - the player click on the spirit name, it open another window with the spirit sheet
   - The spirit sheet display a summon button, the spirit is summoned using its baseName (cf #25)
   - This button will copy an instance of the spirit from the _Spirit_Lib map to the current sheet, next to the token.
     - It serch the map using the baseName so they must be unique on this Map

```
graph TD
    A(openSheetSpiritMgt) -->|tokenId| B[editSheetSpiritMgt]
	B --> |tokenId| C1(editAddSpirit)
    B --> C2[/Spirit lst Frm/] 
	B --> C4[/Spirit View lnk/]
    B --> C3[/Each Spirit Del Lnk/] 
    C2 --> |tokenId| D2(updateSpirit) 
    C3 --> |tokenId, spiritId| D3(delSpirit)
	D3 --> |keyPrefix,Json| E3[[reindexJson]]
	C4 -->|spiritTokenId|D4(openSummonSpirit)
    C1 --> E2[/Add Spirit Frm/]
    D4 --> |tokenId| E4(viewSummonSpirit)
    D3 --> |tokenId| Z
	D2 --> |tokenId| Z
    E2 --> |tokenId + All spell Fields| F1(addSpirit)
    F1 --> |tokenId| Z
    E4 --> |tokenId| F4(summonSpirit)
    F4 --> |tokenId| Z
    Z(openSheetSpiritMgt -callback)
```

![spirit Mgt flow](../../assets/doc/spiritMgtFlow.png?raw=true)
