# PopulateChunkEvent

To use this event use the following import:
```groovy
import net.minecraftforge.event.terraingen.PopulateChunkEvent
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[ChunkGeneratorEvent](chunk_generator_event.md)

## Methods
```groovy
boolean isHasVillageGenerated()
```

```groovy
net.minecraft.world.World getWorld()
```

```groovy
int getChunkZ()
```

```groovy
int getChunkX()
```

```groovy
java.util.Random getRand()
```

# PopulateChunkEvent.Pre

To use this event use the following import:
```groovy
import net.minecraftforge.event.terraingen.PopulateChunkEvent.Pre
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PopulateChunkEvent](populate_chunk_event.md), [ChunkGeneratorEvent](chunk_generator_event.md)

## Methods
# PopulateChunkEvent.Post

To use this event use the following import:
```groovy
import net.minecraftforge.event.terraingen.PopulateChunkEvent.Post
```

## Sub-Classes
This event extends the following events and can use all their methods and fields: <br>
[PopulateChunkEvent](populate_chunk_event.md), [ChunkGeneratorEvent](chunk_generator_event.md)

## Methods
