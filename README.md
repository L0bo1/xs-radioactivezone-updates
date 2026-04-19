# xs-radioactivezone

Premium radioactive zone system for FiveM with gas mask protection, persistent filter usage, oxygen filter refills, admin zone editor, blips, HUD, and configurable damage.

## Features

- Create, edit, delete, and preview radioactive zones in game.
- Admin NUI panel with zone editor, zone list, settings, and live coordinates.
- Radioactive zone damage when players enter without a gas mask.
- Gas mask item support for ESX and QB.
- Persistent gas mask filter durability.
- Oxygen filter item to refill mask durability.
- Configurable radius, damage, blip sprite, and blip color per zone.
- Filter HUD and radioactive zone alert.
- Optional GitHub update checker.

## Installation

1. Place the resource in your server resources folder:

```text
resources/[xs]/xs-radioactivezone
```

2. Add this to `server.cfg`:

```cfg
ensure xs-radioactivezone
```

3. Add admin ACE permission:

```cfg
add_ace group.admin xs.radioactivezone.admin allow
```

4. Add the inventory items.

ESX default item names:

```text
gas_mask
oxygen_filter
```

QB default item names:

```text
gasmask
oxygen_filter
```

## Commands

```text
/radmenu
```

Opens the admin zone editor.

```text
/radtp [zone_id]
```

Teleports an admin to a saved zone.

## Configuration

Main file:

```text
config.lua
```

Core values:

```lua
Config.MaskDuration = 1200
Config.DamageFrequency = 5000
Config.BaseDamage = 5
```

Item names:

```lua
Config.Items = {
    ESXGasMask = 'gas_mask',
    QBGasMask = 'gasmask',
    OxygenFilter = 'oxygen_filter'
}
```

Filter behavior:

```lua
Config.Filter = {
    PersistUsage = true,
    SaveFile = 'data/filters.json',
    RefillAmount = 1200,
    ConsumeRefillItem = true,
    DepleteOnlyInsideZone = false
}
```

`DepleteOnlyInsideZone = false` means the filter loses durability whenever the mask is equipped.

`DepleteOnlyInsideZone = true` means the filter only loses durability inside radioactive zones.

## Update Checker

Create a public GitHub repo for update metadata only:

```text
xs-radioactivezone-updates/
  version.txt
  changelog.txt
```

`version.txt` should contain only the latest version:

```text
1.1.0
```

Then set:

```lua
Config.UpdateChecker = {
    Enabled = true,
    VersionURL = 'https://raw.githubusercontent.com/YOUR_USER/xs-radioactivezone-updates/main/version.txt',
    CheckDelaySeconds = 12
}
```

The checker prints update status in the server console.

## Data Files

Zones are saved in:

```text
data/zones.json
```

Filter durability is saved in:

```text
data/filters.json
```

Do not delete `data/filters.json` unless you want to reset all player mask filter durability.
