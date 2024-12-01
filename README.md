# 🎚 pn-hud Documentation

This guide provides instructions on how to configure **pn-hud**.

---

## Table of Contents

1. [Dependencies](#dependencies)
2. [Drunkenness](#drunkenness)
   - [Events and Exports](#events-and-exports)
   - [How to configure drunkenness?](#how-to-configure-drunkenness)
      - [Adding drunkenness to an item](#adding-drunkenness-to-an-item)
3. [Events and Exports](#events-and-exports)

---

## Dependencies

- [ox_lib](https://github.com/overextended/ox_lib)

---

## Drunkenness

### Events and Exports

```lua
TriggerEvent("pn-hud:drunkness:updateStatus", type, quantity)
```

- **type:** `string` - `"add"` or `"remove"`
- **quantity:** `number` - Value between 1 and 100

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
    if item.status.drunkenness then 
        TriggerEvent("pn-hud:drunkenness:update", "add", item.status.drunkenness)
        return true
    end
    if client.setPlayerStatus then
        client.setPlayerStatus(item.status)
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

## Events and Exports

### Updating Drunkenness

```lua
-- client side
TriggerEvent("pn-hud:drunkenness:update", type, quantity)
```
- **type:** `string` - `"add"` or `"remove"`
   - `"add"`: Increases the value.
   - `"remove"`: Decreases the value.
- **quantity:** `number` - A numeric value that specifies how much to add or remove.

#### Example Usage
```lua
-- adds 50% drunkenness
TriggerEvent("pn-hud:drunkenness:update", "add", 50)
-- removes 50% drunkenness
TriggerEvent("pn-hud:drunkenness:update", "remove", 50)
```
---
