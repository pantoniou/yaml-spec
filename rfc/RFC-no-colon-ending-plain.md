RFC-000
=======

Plain-scalars cannot end with a colon character


| Key | Value |
| --- | --- |
| Target | 1.3 |
| Status | 0 |
| Requires | |
| Related | |
| Discuss | [Issue 0](../../issues/0) |
| Tags | [plain]() [scalar]() |


## Problem

A colon at the end of a plain scalar can appear to be ambiguous.
Its true meaning according to the spec is often surprising.


## Proposal

Forbid colons at the end of plain scalars.


## Explanation

In flow style, a colon at the end of a plain scalar can look ambiguous:
```
{foo:}
```

Generally, any YAML node should be able to be moved around, for example
if a linter wants to line up all keys and values in a mapping:
```
a: value
bc: value
cde: value
defg:: value
```

and suddenly this becomes invalid:
```
a     : value
bc    : value
cde   : value
defg: : value
```

libyaml already outputs such scalars with quotes, even if the event is
created with plain style.

OK:
```
"key:": value
```

Error:
```
key:: value
```
