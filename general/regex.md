# REGULAR EXPRESSIONS (REGEX)

- Regular expressions (or regex for short) is a syntax that allows you to match strings with specific patterns

## How to Read and Write Regexes

### Quantifiers

Regex **quantifiers** check to see how many times you should search for a character. Below is a list of quantifiers:

- `a|b` - match either "a" or "b"
- `?` - zero or one
- `+` - one or more
- `*` - zero or more
- `{N}` - exactly 'N' number of times, where N is a number
- `{N, }` - N or more number of times
- `{N, M}` - between N and M number of times, where N & M are numbers and N < M
- `*?` - zero or more times, but stop after first match

### Pattern Collections

**Pattern collections** allow you to search for a collection of characters to match against. Below is a list of common pattern collections:

- `[A-Z]` - match any uppercase character from "A" to "Z"
- `[a-z]` - match any lowercase chatacter from "a" to "z"
- `[0-9]` - match any number
- `[asdf]` - match any character that is either "a", "s", "d" or "f"
- `[^asdf]` - match any character that is not any of the following: "a", "s", "d" or "f"

These can be combined together,for example:

- `[0-9A-Z]` – match any character that’s either a number or a capital letter from “A” to “Z”
- `[^a-z]` – match any non-lowercase letter

### General Tokens

- `.` – any character
- `\n` – newline character
- `\t` – tab character
- `\s`– any whitespace character (including \t, \n and a few others)
- `\S` – any non-whitespace character
- `\w`– any word character (Uppercase and lowercase Latin alphabet, numbers 0-9, and \_)
- `\d` - any digit
- `\D` - any non-digit
- `\W`– any non-word character (the inverse of the \w token)
- `\b`– word boundary: The boundaries between \w and \W, but matches in-between characters
- `\B`– non-word boundary: The inverse of \b
- `^` – the start of a line
- `$` – the end of a line
- `\`– the literal character “\”

## How to Use a Regex

Regular expressions aren’t simply useful for finding strings. You can also use them in other methods to help modify or work with strings. The following examples use JavaScript as an example, but many languages have similar methods.

### Creating and Searching Using Regex

- First we consider how Regex strings are constructed.
- In JavaScript (along with many other languages), we place Regex inside of // blocks.
- The regex to search for a lower case letter looks like this:
  ```JavaScript
  /[a-z]/
  ```
- The above syntax generates a `RegExp object` which we can use with built in methods such as `exec` to match against strings. For example:
  ```JavaScript
  /[a-z]/.exec("a"); // Returns ["a"]
  /[a-z]/.exec("01234") // Returns null
  ```
- We can then use 'truthiness' to determined if the regex matched.

### Replacing Strings with Regex

- You can also use a regex to search and replace a file’s contents as well.
- Suppose we wanted to replace any greeting with a message of “goodbye”. We could do something like the following:
  ```JavaScript
    function youSayHelloISayGoodbye(str) {
        str = str.replace(/[Hh]ello|[Hh]i|[Hh]ey/, "Goodbye");
        return str;
        }
  ```
- This is much faster than something like the following (i.e., without using Regex):
  ```JavaScript
  function youSayHelloISayGoodbye(str) {
    str = str.replace("Hello", "Goodbye");
    str = str.replace("Hi", "Goodbye");
    str = str.replace("Hey", "Goodbye");  str = str.replace("hello", "Goodbye");
    str = str.replace("hi", "Goodbye");
    str = str.replace("hey", "Goodbye");
    return str;
    }
  ```

### Flags

- Consider the previous example of trying to find and replace greetings with goodbye. We would expect the regex to match both `Hello` and `Hi` in `Hello, Hi there`, but it doesn't - it will only match the first instance.
- To match more than once we need to use **Regex Flags**.
- A **flag** is a modifier to an existing regex.
- **Flags** are always appended after the last forward slash in a regex expression.
- Here is a list of some useful flags:
  - `g` – Global, match more than once
  - `m` – Force $ and ^ to match each newline individually
  - `i` – Make the regex case insensitive
- Thus, if we modify our regex in the previous example to:

  ```JavaScript
  function youSayHelloISayGoodbye(str) {
      str = str.replace(/[Hh]ello|[Hh]i|[Hh]ey/g, "Goodbye");
      return str;
      }
  ```

  then both `Hello` and `Hi` are matched in the string `Hello, Hi there`

### Groups

- When searching with a regex, it can be useful to search for more than one matched item at a time.
- This is where **groups** come into play.
- **Groups** allow us to search for more than a single item at a time.
- For example, to match against both `Testing 123` and `Tests 123` without duplicating the “123” matcher in the regex we can do the following:
  ```JavaScript
  /(Testing|Tests) 123/
  ```
- Groups are defined by brackets

### Lookahead and Lookbehind Groups

- Lookahead and behind groups are extremely powerful
- There are four different types of lookahead and behinds:
  - `(?!)` – negative lookahead
  - `(?=)` – positive lookahead
  - `(?<=)` – positive lookbehind
  - `(?<!)` – negative lookbehind
- Lookahead looks to see that something is after the lookahead group or is not after the lookahead group, depending on if it’s positive or negative. For example:
  ```JavaScript
  /B(?!A)/
  ```
  will allow us to match `BC` but not `BA`.
- We can combine these groups with `^` and `$` tokens to try and match full strings. For example, the following regex will match any string that does not start with 'Test':
  ```JavaScript
  /^(?!Test)*$/gm
  ```
