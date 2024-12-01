---
Body: 2
Mind: 2
Spirit: 2
Mortal_Health: 7
Surface_Health: 14
Stamina: 6
Mana: 5
Total_Health: 21
Strength: 1
Agility: 1
Will: 1
Intellect: 1
Connection: 1
Soul: 1
Stamina_Regen: 3
Mana_Regen: 1
B_Mana: 1
B_Stamina: 2
B_Health: 3
Dodge: 1
B_Dodge: 8
Block: 1
B_Block: 4
Dexterity: 6
Dexterity_Gifted: 1
Dexterity_SP: 0
Speed: 2
Speed_Gifted: 1
Speed_SP: 0
B_Move: 6
---
# Traits
- `VIEW[***Physicality:*** {Body}][text(renderMarkdown)]` 
	- **Strength:** `INPUT[number:Strength]`
	- **Agility:** `INPUT[number:Agility]`
		- *Dexterity:*
			- Gifted: `INPUT[toggle(onValue(2),offValue(1)):Dexterity_Gifted]`
			- Skill Points: `INPUT[number:Dexterity_SP]`
			- Skill Value Cap: `VIEW[{Agility}*{Dexterity_Gifted}][math]`
			- Total Skill Value: `VIEW[{Dexterity_SP}+2][math:Dexterity]`
		- *Speed:*
			- Gifted: `INPUT[toggle(onValue(2),offValue(1)):Speed_Gifted]`
			- Skill Points: `INPUT[number:Speed_SP]`
			- Skill Value Cap: `VIEW[{Agility}*{Speed_Gifted}][math]`
			- Total Skill Value: `VIEW[{Speed_SP}+2][math:Speed]`
- `VIEW[*Mentality:* {Mind}][text(renderMarkdown)]`
	- **Will:** `INPUT[number:Will]`
	- **Intellect:** `INPUT[number:Intellect]`
- `VIEW[*Spirituality:* {Spirit}][text(renderMarkdown)]`
	- **Connection:** `INPUT[number:Connection]`
	- **Soul:** `INPUT[number:Soul]`

# Derived Statistics
## Health Pools
- ***Base Health:*** `INPUT[number:B_Health]` 
- *Mortal Health:* `VIEW[{Body}+{Spirit}+{B_Health}][math:Mortal_Health]`
- *Surface Health:* `VIEW[2*{Mortal_Health}][math:Surface_Health]`
- *Total Health:* `VIEW[{Surface_Health}+{Mortal_Health}][math:Total_Health]`
## Resource Pools
- *Stamina (Regeneration):* `VIEW[{Body}+{Mind}+{B_Stamina}][math:Stamina]` (`VIEW[floor({Stamina}/2)][math:Stamina_Regen]` per rd)
- ***Base Stamina:*** `INPUT[number:B_Stamina]` 
---
- *Mana (Regeneration):* `VIEW[{Mind}+{Spirit}+{B_Mana}][math:Mana]` (`VIEW[floor({Mana}/4)][math:Mana_Regen]` per rd)
 - ***Base Mana:*** `INPUT[number:B_Mana]` 
## Defenses
- **Dodge**: `VIEW[(floor(({Mind}+{Spirit})/4))][math:Dodge]`d`VIEW[{B_Dodge}][text]`
	- ***Base Dodge:*** d`INPUT[inlineSelect(option(4), option(6), option(8),option(10),option(12)):B_Dodge]`
- **Block**: `VIEW[(floor(({Mind}+{Body})/4))][math:Block]`d`VIEW[{B_Block}][text]`
	- ***Base Block:*** d`INPUT[inlineSelect(option(4), option(6), option(8),option(10),option(12)):B_Block]`
## Move 
- ***Base Move:***`INPUT[number:B_Move]` 
- **Actual Movement**: `VIEW[{B_Move}+((floor({Speed}/5)*5)/5)][math:Dexterity]`

%%
Math Section
%%
`VIEW[{Strength} + {Agility}][math(hidden):Body]`
`VIEW[{Will} + {Intellect}][math(hidden):Mind]` 
`VIEW[{Soul} + {Connection}][math(hidden):Spirit]` 