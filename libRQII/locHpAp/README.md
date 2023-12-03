# AP/HP - Heal / Damage Management

Usage: [xwiki - Damage Rules](https://www.inyanga.me/xwiki/bin/view/Rq/DamageRules)

## Data Model

Properties on the token (cf also dataModel/RQ_Human.md) :
- locNb : use to manage the number of item in 
- locHP : current value
- locHPorig : Initial value value before damage. Uses to compute Serious Wound & Major Wound
- locHPwound : Used to keep a wounded status. Enable custom rule and loose less CA when it is the 2nd wound of the same level.


This values are initiated during token creation : 
- cf [tokenPropertyManagement - init Token](../tokenPropertyManagement/RQ_Human.md).

They are modified by :
- [Sheet Management - updateHP.rqm](../sheetManagement/README.md) : recompute 

## updateAPHP.rqm

## Related issues
- #53 - Damage - Limit accumulation of lost CA