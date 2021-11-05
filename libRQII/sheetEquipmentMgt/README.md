
## Equipment Management

### Data Model
cf RQ_Human_Prop and RQ_Monster_Prop
```
wealth = {
    "hold": {
        "gp": 50,
        "sp": 20,
		"cp": 30,
		"others" : "2 ruby, 1 diamond"
    },
	"hidden": {
        "gp": 300,
        "sp": 200,
		"cp": 100,
		"others" : "2 saphir, 2 diamond"
    }
}
```

Sample to be copied on a token :
```
{"hold":{"gp":50,"sp":20,"cp":30,"others":"2 ruby, 1 diamond"},"hidden":{"gp":300,"sp":200,"cp":100,"others":"2 saphir, 2 diamond"}}
```

```
equipmentDesc = {
  "hold": "Boots, Camping stuff, Torch (x2)",
	"hidden": "Rich Clothes, Secret Book"
}
```

Sample to be copied on a token :
```
{"hold":"Boots, Camping stuff, Torch (x2)","hidden":"Rich Clothes, Secret Book"}
```

```
magicItemDesc = {
  "hold": "crystal (2/8), spell matrix : protection (2)",
	"hidden": "Family talisman with a bound spirit"
}
```
Sample to be copied on a token :
```
{"hold":"crystal (2/8), spell matrix : protection (2)","hidden":"Family talisman with a bound spirit"}
```

### Principle

- wealth is managed using a specific property (_wealth_) , with two status Hold or Hidden (cf RQ_Human.md) and a structure for gp, sp, etc.

- equipement is managed using a simple text field  (_equipmentDesc_) with also two "status" Hold or Hidden (cf RQ_Human.md)

- Magic items are managed using a simple text field  (_magicItemDesc_) with also two "status" Hold or Hidden 

- Gold & Equipment are two different form in the same dialog each with its update button
- two different update action

Managed using another Dialog Windows, called from sheetManagement/editSheet
```
graph TD
    A(openEquipmentMgt) -->|tokenId| B[editEquipmentMgt]
    B --> C1[/Wealth Frm/] 
	  B --> C2[/Equipment Frm/]
    B --> C3[/Magic Item Frm/]
    C1 --> |tokenId| D1(updateWealth) 
	  C2 --> |tokenId| D2(updateEquipment) 
    C3 --> |tokenId| D3(updateMagicItem) 
	  D1 --> |tokenId| Z
	  D2 --> |tokenId| Z
    D3 --> |tokenId| Z
    Z(openEquipmentMgt - callback)
```

![Equipment Mgt flow](../../assets/doc/equipmentMgtFlow.png?raw=true)
