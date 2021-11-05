# Serializable
Fast and memory-safe\* table serialization library

\*Best effort was made to ensure proper handling of serializing and unserializing very large tables but for obvious reasons I can't guarantee that you won't run into out-of-memory errors, particularly when loading tables with size ≈ ½system memory
## Caveats
1. No cycles in table structure (nested tables are okay, but there's no cycle detection)
2. No userdata/coroutines/function as keys/values (only serializable values are strings, numbers, booleans and other tables)
3. Serialized format is (as of now) not as compact as it ought to be (i.e. there are some optimizations which could be made)

## Usage
You either need a stream (table which supports :write for using it with `serializable.serialize` or :read for `serializable.unserialize`, usually a file handle) or you can let the library do the file handling for you as well, with you only providing the filename:
```Lua
  local serializable = require("serializable")
  serializable.serializeToFile(table_to_serialize, "/home/serialized_table.txt")
  local loaded_table = serializable.unserializeFromFile("/home/serialized_table.txt")
```
