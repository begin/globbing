# Globbing cheatsheet

WIP

## Basic globbing

| **Character** | **Description** | 
| --- | --- | 
| `*` | Matches any character zero or more times, except for `/` | 
| `**` | Matches any character zero or more times, including `/` | 
| `?` | Matches any character except for `/` one time | 
| `[abc]` | Matches any characters inside the brackets. For example, `[abc]` would match the characters `a`, `b` or `c`, and nothing else. | 

Notes:

- `*` typically does not match dotfiles (file names starting with a `.`) unless explicitly enabled by the user [via options](#common-options) 
- `?` also typically does not match the leading dot
- More than two stars in a glob path segment are typically interpreted as _a single star_ (e.g. `/***/` is the same as `/*/`)

## Extended globbing

### brace expansion

TODO

### extglob

| **pattern** | **regex equivalent** | **description** | 
| --- | --- | --- | 
| `?(pattern-list)` | `(...|...)?` | Matches zero or one occurrence of the given patterns | 
| `*(pattern-list)` | `(...|...)*` | Matches zero or more occurrences of the given patterns | 
| `+(pattern-list)` | `(...|...)+` | Matches one or more occurrences of the given patterns | 
| `@(pattern-list)` | `(...|...)` <sup>*</sup> | Matches one of the given patterns | 
| `!(pattern-list)` | N/A | Matches anything except one of the given patterns | 

### POSIX character classes 

TODO

## Globbing options

Options that are commonly available on various globbing implementations.

| **Option name** | **Description** | 
| --- | --- | 
| `extglob` | Enable extended globs. In addition to the traditional globs (using wildcards: `*`, `*`, `?` and `[...]`), extended globs add (almost) the expressive power of regular expressions, allowing the use of patterns like `foo/!(a|b)*` | 
| `dotglob` | Allows files beginning with `.` to be included in matches. This option is automatically enabled if the glob pattern begins with a dot. Aliases: `dot` (supported by: [minimatch][], [micromatch][]) | 
| `failglob` | report an error when no matches are found | 
| `globignore` allows you to specify patterns a glob should not match  Aliases: `ignore` (supported by: [minimatch][], [micromatch][]) | 
| `globstar` | recursively match directory paths (enabled by default in [minimatch][] and [micromatch][], but not in [bash][]) | 
| `nocaseglob` | perform case-insensitive pathname expansion | 
| `nocasematch` | perform case-insensitive matching. Aliases: `nocase` (supported by: [minimatch][], [micromatch][]) | 
| `nullglob` | when enabled, the pattern itself will be returned when no matches are found. Aliases: `nonull` (supported by: [minimatch][], [micromatch][]) | 
