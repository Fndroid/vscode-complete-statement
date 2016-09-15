Complete Statement with semicolon or brace in vscode.

Mimic IntelliJ's complete statement.
In other words, append `;` and move to line end.

Works with languages with a C style syntax.

Key binding
-----------

This extension uses `ctrl+;` (`cmd+;` on mac)
since vscode already uses `ctrl+shift+enter`.

You can rebind `extension.complete-statement` to `ctrl+shift+enter`.

BTW, `ctrl+;` is easier to remember and type than `ctrl+shift+enter`.
I myself use `ctrl+enter` since `ctrl+;` is hard to type in dvorak.

Example
-------

We use `][` to represent cursor.

```typescript
][
let a_number = 2][ # deside to specify type
let a_number: number][ = 2
// press `ctrl+;` (`cmd+;` on mac)
let a_number: number = 2;][
let semicolon: string][ = "already exist";
// press `ctrl+;`, just move cursor to the end
let semicolon: string = "already exist";][
function works_too(para: number][)
// `ctrl+;`
function works_too(para: number) {][

}
// `down` arrow key
function works_too(para: number) {
    ][
}
// Respects `tabSize` setting. If `tabSize` unset, use 4 spaces.
function works_too(para: number) {
    if (a_number == 1][)
}
// `ctrl+;`
function works_too(para: number) {
    if (a_number == 1) {][

    }
}
```

Bugs
----

- As mentioned above, complete structure (if, for, etc) requires `down` arrow key.

    It will not auto moves to the start of next line like IntelliJ.
    Read the source code or [#11841] for more information.

- This extension does not understand semantics of programming languages.
  So complete structure may not work as you expected.

    For example, it cannot completes `if` with multiple line conditions.
    Also it cannot complete functions in C.
    The "parsing" is *very naive*, it does not even use regex.
    The naive "parsing" is probably good at performance,
    at the cost of only covering limited conditions.

- Indented with tab is not supported yet. Pull request is welcome.

[#11841]: https://github.com/Microsoft/vscode/issues/11841

License
-------

0BSD
