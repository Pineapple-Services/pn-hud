# 🎚 pn-hud Documentation

This guide provides instructions on how to configure **pn-hud**.

---

## Table of Contents

1. [Dependencies](#dependencies)
2. [Drunkenness](#drunkenness)
   - [Events and Exports](#events-and-exports)
   - [How to configure drunkenness?](#how-to-configure-drunkenness)
      - [Adding drunkenness to an item](#adding-drunkenness-to-an-item)
3. [How to Add New HUD Values?](#how-to-add-new-hud-values)

---

## Dependencies

- [ox_lib](https://github.com/overextended/ox_lib)

---

## Drunkenness

### Events and Exports

```lua
TriggerEvent("pn-hud:drunkness:updateStatus", type, quantity)
```

- **type:** `string` - "add" / "remove"
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
        TriggerEvent("pn-hud:drunkness:updateStatus", "add", item.status.drunkenness)
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

## How to Add New HUD Values?

To integrate new HUD values, follow these steps:

1. **Identify the Value**: Determine the HUD value you want to add (e.g., thirst, stamina).
2. **Update Your Script**:
   - Add the necessary logic to handle the new value.
   - Trigger an event to update the HUD, similar to how drunkenness is handled.
3. **Integrate with Inventory**:
   - If you use `ox_inventory`, update the `status` property of your items to include the new value.
   - Modify the inventory script to support the new value (e.g., as shown for drunkenness above).
4. **Test**: Ensure the new value appears and updates correctly in the HUD.

Example:
```lua
TriggerEvent("pn-hud:newValue:updateStatus", "add", 50)
``` 
