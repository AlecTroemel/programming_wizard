# Types
## primitives
```
	NUMBER: [all real integers]
	DIRECTION: [NORTH, SOUTH, EAST, WEST]
	LOCATION: ???
```

## elements
```
	FIRE
	WATER
	ICE
	EARTH
	WIND 
	ELECTRICITY
	NONE: does no damage, but is useful for more complex things
```

# Cast Reserved Word
```
	cast [lvl NUMBER] spell_name:
		input1 = TYPE
		input2 = TYPE
		input3 = TYPE
```

# Spell Reserved Word
```
	spell spell_name:
		CAST
		CAST
		CAST
```

# Base Spells

## Attacks 
- __ball__: Strike a single location
	```
		cast ball:
			element = ELEMENT
			[location = LOCATION] ... maybe get this from another cast like move
	```

- __beam__: Strike through a whole row
	```
		cast beam:
			element = ELEMENT
			direction = DIRECTION
	```

- __explode__: Strike a location and its adjacent locations
	```
		cast explode:
			element = ELEMENT
			[location = LOCATION]
	```


## Defense
- __armor__: apply an element to a target at a location
	```
		cast armor:
			element = ELEMENT
			location = LOCATION
	```

- __wall__: create an elemental wall at a location
	```
		cast wall:
			element = ELEMENT
			location = LOCATION
	```

## Status
- __cover__:  place an element on a location
	```
		cast cover:
			element = ELEMENT
			location = LOCATION
	```

- __move__:  move an target at a location in a direction 
	```
		cast move:
			element = ELEMENT
			direction = DIRECTION
	```

- __teleport__: teleport a target at a location to a new location
	```
		cast teleport:
			element = ELEMENT
			location = LOCATION
	```


## Helpers
- __input__: get and input from the parent cast	
	```
		cast input:
			word = string
	```

- __repeat__: do something multiple times
	```
		cast repeat:
			times = NUMBER
			do = CAST
	```

- __respond__: respond to contact with a spell element type
	```
		cast respond:
			element = ELEMENT | spell = SPELL_NAME
			do = CAST
	```

- probe

- addition/subtraction ? is there basic math?
- if-else statements?


# Examples
```
	spell move_two_spaces:
		cast lvl 2 move:
			direction = cast input
```

```
	spell exploding_earth_armor:
		cast armor:
			element = EARTH
		cast respond:
			element = EARTH
			do = cast explode:
				element = FIRE
```























---

# OLD
__primitaves are upper case for this document__
## data types
NUMBER // [all real integers]
LOCATION // [x, y]
OBJECT // an instantiated object in the game map
DIRECTION // [NORTH, SOUTH, EAST, WEST]
SPELL

## primatives spells
FIRE
WATER
ICE 
EARTH
WIND 
ELECTRICITY

### 2 elemental primatives add together to create new spells
fire + ice = water

## at the beginning of a fight, you must allocate crystals between
mana 
base types
mobility

// cast's do actions, but cost mana
// mana is a number
// every cast return's something
// All cast's in a spell inherit the level from the parent cast by default
// this can be manualy overriden

cast [lvl NUMBER] cast_name:
	[location:] // by default inharited from parent call 

default cast's

```
// returns spell
cast ball:
	[location:]
	spell:

// returns spell
cast strike: 
	[location:]
	spell:

// returns location of target at given location after movement
cast target: 
	[location:]

// returns spell
// when this spell is hit by a specific spell type, reactive with a spell
cast respond:
	spell: 
	spell:

// returns spell
// repeats x times, where x is the level of the cast
cast repeat:
	spell:

// returns spell
// effects area of radius x, where x is the level of the cast
cast area:
	spell:

// returns ???
// move object at location 1 in direction
//  level of cast == spaces moved
cast move:
	[location:]
	direction: 
```

## spells 
are like functions that take in a caster and the target

```
spell spell_name (caster, target, lvl):
	contents
```

### example spells

```
spell homing_firestrike:
	cast strike:
		location: 
			cast lvl 2 target:
		type: FIRE
```

```
spell area_water:
	cast area:
		spell: WATER

spell five_square_shroud:
	cast lvl 5 area:
		spell: AIR
```


you can nest spells

```
spell ice_ball:
	cast ball:
		location: target
		spell: ice

spell ice_ball_sweep:
	cast repeat:
		spell: ice_ball [target.x, target.y + count]
```





