# BEST PRACTICES.

ALWAYS CHECK .agents/rules.

## File Management.

- /common/ - Contains all config files, either JSON/JSON5.
  - /common/<category_key>/
- /core/framework/ - Client business logic.
- /core/server/ - Backend business logic.
- /core/ui/ - Frontend code.
  - /core/ui/components/ - Composable components used in UI.
  - /core/ui/<interface_key>/
    - bottombar/ - UI anchored bottom.
    - leftbar/ - UI anchored left.
    - map/ - UI attached to map/scene.
    - rightbar/ - UI anchored right.
    - topbar/ - UI anchored top.
- /docs/ - Typedoc/Doxygen for the current project.
- /localisation/ - User-facing localisation (EN-GB, FR, DE)
- /tests/ - Temporary testing files. DO NOT USE /scratch/. IMPORTANT: clean up temporary testing files if use has clearly expired.
- autobuild.bat/autobuild.sh - Builds program for distribution.
- autodoc.bat/autodoc.sh - Produces documentation.
- autorun.bar/autorun.sh - Starts current program.

## Requirements.

1. All files are snake_case.<extension>. Only class files are CamelCase.<extension>.
2. Do not repeat yourself (DRY). Two or more, use a function or a for. If something is a config, it must exist in /common/.
3. Files not mentioned or used anywhere should be deleted unless they exist for API/pipeline purposes.
4. If logical flow, must be strongly preserved, i.e. data pipelines, prefix each step with a letter, i.e. A\_<function_key>, etc.
5. Your files should be compatible with Doxygen/Typedoc.

## Writing.

Use non-Oxford British English (EN-GB). Avoid run-on verbiage, prioritise brevity and human writing. All strings should be localised into EN-GB, FR, DE; variable delimiters in localisation use the £ sign, i.e. £1£. Timezones are GMT+0.

Numbers use European decimals: 58,88. Use semantic abbreviations for numbers: k, M, B, T.

# CODE FORMATTING.

## 1. Structure and maintainability

- 2-space indentation, except for markup and schema.
- Alphabetise code paragraphs, declaration groups and labelled foldable blocks without changing execution order.
- Separate functions with double line breaks; use these elsewhere for readability.
- Code files: limit to 1000 lines; one class declaration. Split larger files logically.
- For repeated operations, use a function or `for` loop. Store configuration in `/common/`; prefer JSON5 and composable patterns over magic numbers.

## 2. Naming and variables

- Classes: CamelCase.
- Functions/methods: camelCase.
- Variables: snake_case.
- DOM/HTML-facing attributes: kebab-case.
- Parameters: `arg<#>_<parameter_name>`; options: `arg<#>_options`.
- Use precise names. Prefer options object for more than one optional parameter or 4+ arguments.
- Declare variables inside functions, except libraries/dependencies. Use `let` for non-globals; never `const`.
- Alphabetise declarations, separating related groups with double line breaks. Parameter conversions follow parameter order instead.

Variable conventions:

- `all_`: array of object keys or class instances.
- `do_not_`: negative boolean/display option.
- `local_`: variable scoped below function level.
- `options`: always an object.
- `ot_`: second counterpart.
- `_array`: array; legacy `_string` may denote a UI-string-building array.
- `_obj`: object.

Use `//Format <variable>` before pushing formatted-string elements.

## 3. Comments

- CSS: `/* -- Comment -- */`.
- HTML: `<!-- Comment -->`.
- JS: `//Comment`.
- JS multiline: opening `/*`, comment body and closing `*/` on separate lines.
- JSDoc: opening `/**`, ` *`-prefixed lines and closing ` */`.
- No mid-sentence newlines: write naturally, word wrap does its job.

## 4. Function contract

Except startup/init functions, functions must belong to an object or class namespace, not the global namespace.

Alphabetise function declarations. Put a space before definition parameter lists, but not call parameter lists. Separate functions with double line breaks.

For functions with parameters or returns, provide multiline JSDoc directly above the definition, documenting parameters, optional defaults, returns and aliases where applicable.

Use this section order:

1. `//Convert from parameters`. Strip parameter prefixes into internal variables, in parameter order. Include only parameter-derived declarations. Convert options with an inline ternary, falling back to `{}`.
2. Optional: `//Initialise options`. Set default subobject options only when undefined.
3. Optional: `//Declare local instance variables.`. Alphabetise function-wide declarations, including aliases of `this`.
4. Guard clauses. May appear anywhere after parameter conversion, but never after the main body begins.
5. Function body. Optional: begin after a double line break. Keep processing here, separate from declarations and returns.
6. `//Return statement` above each non-guard return. Use a ternary for two alternatives or an if–else chain otherwise.

## 5. Conditionals

- Group complex boolean expressions with parentheses across indented lines.
- Invalid input: skip operation and call `console.error()`; do not throw.
- Pre-ES6 nested-property checks: chain indented conditions. In supported ES6+ environments, prefer nullish coalescing.
- Standalone one-line `if`: omit braces. Multiline `if` and all if–else statements: use braces.
- Never use `switch`; use if–else chains.
- Keep ternaries inline during parameter conversion; otherwise place them below assignments. Never nest, chain or use three-line ternaries.

## 6. Loops and timers

- For large inputs, keep complexity at `O(n^2)` or better.
- Loop-letter order: `i`, `x`, `y`, `z`, `a`, `b`, `c`, …
- Omit `for` braces for one-line bodies. Avoid `while`.
- For `setInterval()` and `setTimeout()`, use an arrow callback followed by delay and callback arguments.
- Store interval handles locally for later `clearInterval()`.
- Use `setTimeout()` for delayed execution.

## 7. Maths

- Space only `+` and `-` in equations: `5*9 + 4`.
- Clamp ranges with `Math.min()` and `Math.max()`, not one-line conditions.