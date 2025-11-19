# Gamemode
This guide explains how to configure a gamemode to your liking, using the provided gamemode configuration module. A gamemode is used to control how the game works during a match's runtime. The format of a gamemode is **callbacks** (*called on an event*), **conditions** (*returns a boolean for processing*), and **variables** (*used to simply control basic settings*). Let's dive into how to configure a gamemode.

## Seekers
### Variable
```lua
Seekers = 1,
```
Determines how many players will start in the round as a **seeker**
* Example: \
`Seekers = 1` → One random player becomes the `Seeker` \
`Seekers = 3` → Three random players will become the `Seeker`

------------------------------------------------------------------------

## OnPlayerAdded(Player, Role)
### Callback
```lua
OnPlayerAdded = function(Player: Player, Role: string)
    -- Example code here
end,
```
Called when a player joins an active round
### Parameters
* `Player` → The player who joined the active match
* `Role` → `"Seeker"` or `"Hider"`
### Usage
The callback is used to apply gameplay effects, features, or more for a player when they join an ongoing match
### Common Examples:
* Give a `Seeker` a special tool or weapon (ex. slap tool, as used in `Slap` gamemode)
* Give hiders a short speed boost or forcefield
* Apply role based abilities
* Insert GUI elements
* Create tracking values or statistics

------------------------------------------------------------------------

## OnHit
### Condition & Callback
```lua
OnHit = function(Player: Player): boolean
    -- Example code here
end,
```
Called when a player attempts to **hit/tag/seek** (done via *main game configuration hit settings*)
### Parameters
* `Player` → The player who attempted to **hit/tag/seek** (done via *main game configuration hit settings*)
### Must Return
* `true` → The hit is processed, further action is taken
* `false` → Halt further action, the hit isn't processed
### Usage
* The condition is used to check whether or not a hit can be processed, allowing either further click action, or halting the current task
* The condition can also be used as a callback and condition, such as adding values or tracking an object (check **Common Examples**)
### Common Examples:
* Adding hit statistics (ex. hidden leaderstats)
* Playing an animation
* Debouncing attacks (**already done in pre-created gamemodes**)
* Triggering visual or sounds effects

------------------------------------------------------------------------

## OnTagged
### Callback
```lua
OnTagged = function(Player: Player, Target: Player)
    -- Example code here
end,
```
Called when a `Seeker` tags a `Hider`
### Parameters
* `Player` → The player who tagged the target (aka. the `Seeker`)
* `Target` → The player who was tagged by the `Seeker` (aka. the `Hider`)
### Usage
The callback is used to apply an event to a `Hider` or `Seeker` when somebody is tagged
### Common Examples:
* Classic (*built-in gamemode*)
* Elimination
* Infection (turn a `Hider` into a `Seeker`)

------------------------------------------------------------------------

## RoundOverCondition
### Condition
```lua
RoundOverCondition = function(TotalActive: number, Hiders: number, Seekers: number): boolean
    -- Example code here
end,
```
Called on information update to check if the round should be `completed`, or if it should be `continued`
### Parameters
* `TotalActive` → The total amount of players active in an ongoing match
* `Hiders` → The total amount of hiders in an ongoing match
* `Seekers` → The total amount of seekers in an ongoing match
### Must Return
* `true` → The game is over, return everybody to the lobby
* `false` → The round is still going, continue as normal
### Usage
The condition is used to check if the round should be `completed`, or if it should be `continued`
### Common Examples:
* No hiders remain (`Hiders <= 0`, *built into `classic`*)
* Seekers outnumber hiders (`Seekers >= Hiders`)
* Only seekers remain (`Seekers >= TotalActive`, can be used for infection)