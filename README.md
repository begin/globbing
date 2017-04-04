# globbing

> Cheatsheet and introduction to "globbing".

**TODO**

* [ ] cheatsheet
* [ ] what is globbing
* [ ] wildcards
* [ ] extglobs
* [ ] posix brackets
* [ ] braces
* [ ] options

## What is "globbing"?

Globbing, also referred to as "glob matching" or "filepath expansion", is a concept from Bash that is used for matching files using wildcards, including `*`, `?` and `[...]` (where `...` inside the brackets represents any characters to be matched - more about this in the [wildcards](#wildcards) section).

For example, given a directory with the files `foo`, `bar` and `baz`, the pattern `b*` will match `bar` and `baz`, but not `foo`.

## Wildcards

* 
## Extended globbing

* extglobs
* braces
* brackets
* regex

## extglobs

Extended globbing, as described by the bash man page:

| **pattern** | **regex equivalent** | **description** | 
| --- | --- | --- |
| `?(pattern-list)` | `(... | ...)?` | Matches zero or one occurrence of the given patterns |
| `*(pattern-list)` | `(... | ...)*` | Matches zero or more occurrences of the given patterns |
| `+(pattern-list)` | `(... | ...)+` | Matches one or more occurrences of the given patterns |
| `@(pattern-list)` | `(... | ...)` <sup>*</sup> | Matches one of the given patterns |
| `!(pattern-list)` | N/A | Matches anything except one of the given patterns |

<sup><strong>*</strong></sup> `@` isn't a RegEx character.

Powered by [extglob](https://github.com/jonschlinkert/extglob). Visit that library for the full range of options or to report extglob related issues.

See [extglob](https://github.com/jonschlinkert/extglob) for more information about extended globs.

### brace expansion

In simple cases, brace expansion appears to work the same way as the logical `OR` operator. For example, `(a|b)` will achieve the same result as `{a,b}`.

Here are some powerful features unique to brace expansion (versus character classes):

* range expansion: `a{1..3}b/*.js` expands to: `['a1b/*.js', 'a2b/*.js', 'a3b/*.js']`
* nesting: `a{c,{d,e}}b/*.js` expands to: `['acb/*.js', 'adb/*.js', 'aeb/*.js']`

Visit [braces](https://github.com/jonschlinkert/braces) to ask questions and create an issue related to brace-expansion, or to see the full range of features and options related to brace expansion.

### POSIX character classes

POSIX character classes, or "bracket expressions", provide a way of defining regular expressions using something closer to plain english.

**Example**

```js
mm.isMatch('a1', '[[:alpha:][:digit:]]');
//=> true
```

See [expand-brackets](https://github.com/jonschlinkert/expand-brackets) for more information about extended bracket expressions.

### regex character classes

With the exception of brace expansion (`{a,b}`, `{1..5}`, etc), most of the special characters convert directly to regex, so you can expect them to follow the same rules and produce the same results as regex.

For example, given the list: `['a.js', 'b.js', 'c.js', 'd.js', 'E.js']`:

* `[ac].js`: matches both `a` and `c`, returning `['a.js', 'c.js']`
* `[b-d].js`: matches from `b` to `d`, returning `['b.js', 'c.js', 'd.js']`
* `[b-d].js`: matches from `b` to `d`, returning `['b.js', 'c.js', 'd.js']`
* `a/[A-Z].js`: matches and uppercase letter, returning `['a/E.md']`

Learn about [regex character classes][character-classes].

### regex groups

Given `['a.js', 'b.js', 'c.js', 'd.js', 'E.js']`:

* `(a|c).js`: would match either `a` or `c`, returning `['a.js', 'c.js']`
* `(b|d).js`: would match either `b` or `d`, returning `['b.js', 'd.js']`
* `(b|[A-Z]).js`: would match either `b` or an uppercase letter, returning `['b.js', 'E.js']`

As with regex, parenthese can be nested, so patterns like `((a|b)|c)/b` will work. But it might be easier to achieve your goal using brace expansion.

## Options

* `brackets`: Enable matching with POSIX character classes and regex ranges
* `extglob`: Enable extended globs. In addition to the traditional globs (using wildcards: `*`, `*`, `?` and `[...]`), extended globs add (almost) the expressive power of regular expressions, allowing the use of patterns like `foo/!(a|b)*`
* `dotglob`: Allows files beginning with `.` to be included in matches. This option is automatically enabled if the glob pattern begins with a dot.
* `failglob`: report an error when no matches are found
* `globignore` allows you to specify patterns a glob should not match
* `globstar`: recursively match directory paths
* `ignore` alias for `globignore`
* `nocase` alias for `nocasematch`
* `nocaseglob` perform case-insensitive pathname expansion
* `nocasematch` perform case-insensitive matching
* `nullglob` when enabled, the pattern itself will be returned when no matches are found

## Related concepts

* regular expressions
* tilde expansion
* kleene
* ksh

## Resources

**Documentation**

* [bash](https://github.com/felixge/node-bash)

**Tools and software**

* [micromatch](https://github.com/jonschlinkert/micromatch) (JavaScript/node.js)
* [minimatch](https://github.com/isaacs/minimatch) (JavaScript/node.js)
* [braces](https://github.com/jonschlinkert/braces) (JavaScript/node.js)
* [brace-expansion](https://github.com/juliangruber/brace-expansion) (JavaScript/node.js)
* [expand-brackets](https://github.com/jonschlinkert/expand-brackets) (JavaScript/node.js)
* [bash-glob](https://github.com/jonschlinkert/bash-glob) (JavaScript/node.js)
* [glob](https://github.com/isaacs/node-glob) (JavaScript/node.js)