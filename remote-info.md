# Remote Info

## Pet Remote

```lua
workspace.__REMOTES.Game.Pets
```

Format:

```lua
workspace.__REMOTES.Game.Pets:FireServer({ {func1}, {func2}, ... })
```

## Spawn

```lua
{ 'Spawn', Player: LocalPlayer, string: petID, }
```

The pet ID is a string and can contain leading zeroes.

## Pet Movement

```lua
{ 'Spawn', Player: LocalPlayer, string: petID, PartToOrbit, number: offset }
```

The offset is a number, not a `Vector3`.

## Open Egg

```lua
{
    string: 'Open',
    string: 'Egg',
    string: EggName,
    table: {
        table: {
            g = bool: is_golden_pet,
            dm = bool: is_dark_matter_pet,
            r = bool: is_rainbow_pet,
            n = number: pet_type_ID,
            l = number: level
        }
    }
}
```

Example: hatch a Tier 1 egg containing a Giant Cat:

```lua
workspace.__REMOTES.Game.Pets:FireServer({
    {
        'Open', 'Egg', 'Tier 1',
        {
            { g = true, dm = true, r = true, n = 90010, l = 9e18 }
        }
    }
})
```
