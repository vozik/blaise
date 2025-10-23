documentation for the PSION (Program Structure Interface Object Notation) grammar file:

---

## 1️⃣ Goals

**Purpose of the PSION-based system:**

1. **Define a language declaratively** using JSON, including:

   * Syntax rules (`alternatives`)
   * Field mapping (`where`)
   * PSI and UAST nodes (`into`)

2. **Generate a runtime parser** automatically from the grammar.

3. **Build PSI nodes** that:

   * Contain full source info (positions, comments, whitespace)
   * Map 1:1 to language grammar

4. **Create lazy UAST nodes** from PSI for semantic analysis:

   * UAST nodes are simplified, universal
   * Each UAST node references its PSI source

5. **Enable runtime execution** from declarative executor definitions:

   * Each node can optionally define an `"executor"`
   * Provides a fast, flexible runtime for evaluation or code generation

6. **Support IDE tooling** features:

   * Syntax highlighting
   * Refactoring
   * Formatting
   * Multi-language extensibility

---

## 2️⃣ PSION Grammar File Structure

### Top-Level Sections

```text
comments        - list of runtime comment patterns
whitespace      - list of ignored characters
types           - builtin types (Integer, String, Boolean)
enums           - enumerations (e.g., statement_enum)
constants       - fixed values (operator_list)
grammar         - language rules
```

---

### Grammar Rules

Each rule has the following structure:

```json
"rule_name": {
  "alternatives": [ "literal token sequence(s)" ],
  "where": {
    "field_name": "@type" | "$builtin" | "optional" | "list of ... separated by ','" | "single/multiple from @enum" | "choice of ..."
  },
  "into": {
    "psi": "PsiNodeType",
    "fields": { "field_name": "where_field" },
    "executor": { ... } // optional runtime execution descriptor
  }
}
```

**Notes:**

1. **`alternatives`** contains only literal sequences or token patterns.
2. **`where`** defines the **semantic meaning and type** of each field.
3. **`into`** maps the parsed data to **PSI nodes**, UAST nodes, and optionally a runtime executor.
4. Built-in types (`$Integer`, `$String`) and enums (`single from @enum`) enforce type safety.
5. Lists and optional fields are fully declarative, e.g., `list of @argument separated by ','` or `optional`.

---

### Example Sections

**Comments & Whitespace**

```json
"comments": ["'//'..'\\n'", "'//'..'\\0'", "'{'..'}'", "'(*'..'*)'"],
"whitespace": [" ", "\\t", "\\r", "\\n"]
```

**Builtin Types**

```json
"types": {
  "Integer": { "type": "builtin_type", "value": "int32" },
  "String": { "type": "builtin_type", "value": "utf16" },
  "Boolean": { "type": "builtin_type", "value": "bool" }
}
```

**Grammar Rule Example**

```json
"function_definition": {
  "alternatives": ["'function' name '(' arguments ')' ':' return_type ';'"],
  "where": {
    "name": "@identifier",
    "arguments": "list of @argument separated by ',', optional",
    "return_type": "$Integer, optional"
  },
  "into": {
    "psi": "PsiFunction",
    "fields": { "name": "name", "parameters": "arguments", "return_type": "return_type" },
    "executor": { "type": "function_call", "args": ["parameters"] }
  }
}
```

**Key Points:**

* The grammar is **declarative**: everything needed to parse, create PSI/UAST, and run code is in the JSON.
* Supports **lazy UAST mapping** from PSI.
* Designed for **runtime parsing, analysis, and code generation**.

---

This PSION file and design form a **complete high-level starting point** for a **parser generator, runtime interpreter, and code generator**, all from one declarative specification.
