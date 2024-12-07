# 🎚 pn-hud Documentation

This guide provides instructions on how to configure **pn-hud**.

---

## Table of Contents

1. [Dependencies](#dependencies)
2. [Drunkenness](#drunkenness)
   - [Events and Exports](#events-and-exports)
   - [How to configure drunkenness?](#how-to-configure-drunkenness)
3. [Stress](#stress)
   - [Events and Exports](#Events-and-Exports-Stress)

---

## Dependencies

- [ox_lib](https://github.com/overextended/ox_lib)

---

## Drunkenness

### Events and Exports

```lua
TriggerEvent("pn-hud:drunkenness:update", type, quantity)
```

- **type:** `string` - `"add"` or `"remove"`
- **quantity:** `number` - Value between 1 and 100

#### Example Usage
```lua
-- adds 50% drunkenness
TriggerEvent("pn-hud:drunkenness:update", "add", 50)
-- removes 50% drunkenness
TriggerEvent("pn-hud:drunkenness:update", "remove", 50)

-- gets drunkenness
print(exports["pn-hud"]:GetDrunkenness())
```
---

### How to Configure Drunkenness?

To configure drunkenness, follow these steps:

#### Step 1: Modify Your Inventory Script
⚠ **If you want to contribute your snippet, submit a Pull Request (PR).**

##### Example: [ox_inventory](https://github.com/overextended/ox_inventory)

1. Open `ox_inventory/client.lua`.
2. Navigate to **line 396**.
3. Replace this code:

```lua
if item.status then
    if client.setPlayerStatus then
        client.setPlayerStatus(item.status)
    end
end
```

with:

```lua
if item.status then
    local status = lib.table.deepclone(item.status)
    if status.drunkenness then
        TriggerEvent("pn-hud:drunkenness:update", "add", status.drunkenness)
        status.drunkenness = nil
    end
    if client.setPlayerStatus then
        client.setPlayerStatus(status)
    end
end
```

---

#### Step 2: Adding Drunkenness to an Item

Use the following format to add drunkenness to an item:

```lua
['burger'] = {
    label = 'Burger',
    weight = 220,
    client = {
        status = { hunger = 200000, drunkenness = 80 },
        anim = 'eating',
        prop = 'burger',
        usetime = 2500,
        notification = 'You ate a delicious burger'
    },
},
```

---

## Stress

### Events and Exports Stress

```lua
TriggerEvent("pn-hud:stress:update", type, quantity)
```

- **type:** `string` - `"add"` or `"remove"`
- **quantity:** `number` - Value between 1 and 100

#### Example Usage
```lua
-- adds 50% stress
TriggerEvent("pn-hud:stress:update", "add", 50)
-- removes 50% stress
TriggerEvent("pn-hud:stress:update", "remove", 50)

-- gets drunkenness
print(exports["pn-hud"]:GetStress())
```
