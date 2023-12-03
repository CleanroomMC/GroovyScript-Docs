# Blood Magic Entity Sacrifice Amount

Package:

```groovy
mods.bloodmagic.Sacrificial
```

!!! Note
    Affects the value of Entities sacrificed to the Blood Altar via Sacrificial Dagger or Well of Suffering.
    Amount gained is `value * HP`. If not set, the default value of `25` is used for the Sacrificial Dagger,
    and configurable via config with a default value of `25` for the Well of Suffering Ritual.

## Setting the Sacrificial value of Entities

Just like other recipe types, Sacrificial also uses a recipe builder. <br>
You don't know what a builder is? Check [this](https://groovyscript-docs.readthedocs.io/en/latest/groovy/builder/) out

```groovy
mods.bloodmagic.Sacrificial.recipeBuilder()
```

Set the target Entity.

```groovy
.entity(String)
.entity(ResourceLocation)
.entity(Entity)
```

Set the Blood amount per HP when Sacrificed:

```groovy
.value(int)
```

Register recipe:

```groovy
.register()
```

!!! example

    ```groovy
    mods.bloodmagic.Sacrificial.recipeBuilder()
        .entity("minecraft:enderman") // If the Entity is already registered, overrides the prior value.
        .value(1000)
        .register()
    ```

## Removing Recipes

!!! Danger "Warning"
    Some Entities are set to 0 by default to prevent exploits - for example, Vanilla's Armor Stand.
    Removing these Sacrificial values may introduce unintentional exploits.

Removes the recipe that matches the given catalyst item:

```groovy
mods.bloodmagic.Sacrificial.remove(String)
mods.bloodmagic.Sacrificial.remove(ResourceLocation)
mods.bloodmagic.Sacrificial.remove(Entity)
```

Removes all registed Entities, resetting them to the default value:

```groovy
mods.bloodmagic.Sacrificial.removeAll()
```

!!! example

    ```groovy
    // Removes the default Sacrificial value of a Villager.
    mods.bloodmagic.Sacrificial.remove("minecraft:villager")
    ```
