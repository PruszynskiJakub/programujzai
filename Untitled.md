
Pointer/handler - method
Aby uniknąć przekazywania i obsługi dużych ilości informacji stanowiących odpowiedzi z narzędzi, możemy zastosować tzw wzorzec Pointer/Handler. 
Polega on na przekazywaniu dużych ilości nie za pomocą wartości a za pomocą referencji. 
Innymi słowy agent w takim scenariuszu przestaje być odpowiedzialny za przetwarzanie danych, dostaję natomiast ważną odpowiedzialność komunikacji i orkiestracji.

Ten wzorzec składa się tak naprawdę z trzech  składowych:
- pamięci Agenta przechowującej odpowiedzi narzędzi
- wrappera wokół narzędzi który decyduje o tym, że odpowiedź dane narzędzia należy przekazać przez referencję czy też treść jest na tyle krótka, że możemy jej używać bezpośrednio w kontekście
- narzędzia do pozyskiwania treści wpisu

``` typescript
interface StoredValue {
    data: unknown;
    metadata: Record<string, unknown>; // what the LLM sees
  }

class AgentMemory {
    private store = new Map<string, StoredValue>();

    set(path: string, data: unknown, metadata: Record<string, unknown>): string {
      this.store.set(path, { data, metadata });
      return path;
    }

    get(path: string): unknown {
      const entry = this.store.get(path);
      if (!entry) throw new Error(`Nothing at path: ${path}`);
      return entry.data;
    }

    describe(path: string): Record<string, unknown> {
      return this.store.get(path)?.metadata ?? {};
}

    // For hierarchical storage of dict results
    setDict(basePath: string, dict: Record<string, unknown>, metadata: Record<string,
   unknown>): string {
      for (const [key, value] of Object.entries(dict)) {
        this.store.set(`${basePath}/${key}`, { data: value, metadata: {} });
      }
      this.store.set(basePath, { data: dict, metadata });
      return basePath;
    }
  }
  
  
  function mirrorTool<T extends Record<string, unknown>>(
    name: string,
    originalTool: Tool<T>,
    memory: AgentMemory,
    opts: { outputThreshold?: number } = {},
  ): Tool<T> {
    const threshold = opts.outputThreshold ?? 500; // chars

    return tool({
      description: originalTool.description,
      parameters: originalTool.parameters,
      execute: async (input) => {
        // (1) Resolve pointers in input
        const resolved = resolvePointers(input, memory);

        // (2) Execute original tool
        const result = await originalTool.execute(resolved);

        // (3) Store large outputs, return pointer + metadata
        const serialized = JSON.stringify(result);

        if (serialized.length <= threshold) {
          return result; // Small enough, return directly
        }

        const path = `${name}/${crypto.randomUUID().slice(0, 8)}`;
        const metadata = extractMetadata(name, result);

        memory.set(path, result, metadata);

        return {
          _pointer: path,
          ...metadata,
          hint: `Full data stored at "${path}". Pass this path to other tools to use
  it.`,
        };
      },
    });
    
function resolvePointers(
    input: Record<string, unknown>,
    memory: AgentMemory,
): Record<string, unknown> {
const resolved: Record<string, unknown> = {};

for (const [key, value] of Object.entries(input)) {
  if (typeof value === "string" && memory.has(value)) {
	resolved[key] = memory.get(value);
  } else {
	resolved[key] = value;
  }
}

return resolved;
}
    
```



Scratchpad