# JVM Memory Management

*Last Updated : 01/2024 - Java 21.*

### Summary

- [Structure](#structure)
    - [Heap Space](#heap-space)
    - [Stack Memory](#stack-memory)
    - [Young Generation](#young-generation)
    - [Old Generation](#old-generation)
    - [Permanent Generation](#permanent-generation)
- [Garbage Collection](#garbage-collection)

#
<br>

## Structure

```
      Minor GC                          Major GC

     ──────────               ────────────────────────────

    ┌──────────┬──────┬──────┬────────────────────────────┬────────────────┐
    │          │      │      │                            │                │
    │          │      │      │                            │                │
    │   Eden   │  S0  │  S1  │         Old memory         │      Perm      │
    │          │      │      │                            │                │
    │          │      │      │                            │                │
    └──────────┴──────┴──────┴────────────────────────────┴────────────────┘

     ─────────────────────────────────────────────────────
                           Heap

     ────────────────────────  ───────────────────────────

             Young Gen                   Old Gen
```
#
### Heap Space

- Used by the JVM to allocate memory to Objects (and not primitives).

- The GC runs in the Heap to free memory used by Objects with no reference.

- Any Object in the Heap has global access anywhere in the application.

#
### Stack Memory

- Contains methods-specific values and references to other Objects in the Heap used in the method.

- Primitives are stored here.

- Objects are stored in the Heap and referenced in the stack.

#
### Young Generation

- **Eden Memory** :
    - All new Objects are created there.
    - When Eden is filled, a minor GC is performed. All survivors Objects are moved into the **Survivor stack** (`S0`, `S1`).

- The survivors are always stacked inside one of the two stacks in order to gain performances. The other stays empty.

- Objects that survive many GC cycles are moved into the Old Generation Memory (threshold of age).

#
### Old Generation

- Contains long-lived Objects.

- GC is performed when the stack is full, but takes longer than the minor GC inside Eden.

#
### Permanent Generation

- Contains application metadata required by the JVM, SE libraries, classes, methods.
- Not a part of the **Heap**.

- Holds its own GC when full.

- Structure :

    - Method area : class structure (runtime constants, static variables), code for methods & constructors.
    - Memory pool :
        - Store immutable Objects, like Strings (ex: String pool).
        - Can belong to the Perm or Heap depending on the JVM implementation.
    - Stack memory.

<br>

## Garbage Collection

- Removes **non referenced** Objects.

- All GC event are "**Stop the world**" :

    - All application threads are stopped until completion.
    - Minor GC is fast and the stop is unnoticeable.
    - Major GC is long and may cause timeouts in highly responsive applications. the duration depends on the strategy used for GC.

***Steps*** :

1. **Marking**.
2. **Sweeping** (deletion).
3. **Compacting** (compact remaining Objects).

<br>

***GC Types*** :

1. *<u>Serial GC</u>*

    - Simple mark-sweep-compact with young and old gen structure.
    - Used for small standalone apps, small CPU or low memory footprint apps.

2. *<u>Parallel GC</u>*

    - Spawns N serial GC threads for Young Generation running in parallel for N CPU cores. Old GC is still single-threaded.

3. *<u>Parallel Old GC</u>*

4. *<u>Concurrent Mark Sweep (CMS) Collector</u>*

    - Runs GC concurrently with app threads for old GC, to minimize downtime.
    - Young Generation is in parallel, not concurrent.

5. *<u>G1 GC (Garbage First)</u>*

    - Will replace CMS.
    - Parallel, concurrent and incrementally compacting low-pause GC.
    - No Young or Old Generation, memory is divided into multiple equal-sized Heap regions.
    - First collects region with lesser live data.
    - Can meet a downtime target requirement specified by the developer, with high probability.
