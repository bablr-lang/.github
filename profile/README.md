# BABLR
![come chat on Discord](https://img.shields.io/discord/1151914613089251388)

The BABLR org exists to build a next-gen tooling and editor ecosystem to radically raise code literacy around the world.

The main repo is [bablr-vm](https://github.com/bablr-lang/bablr-vm), and you can also see [an example grammar](https://gist.github.com/conartist6/5adbbf28d11497467848f530756c1c2a).

This project redefines what a parser is, formalizing its role in classifying characters into typed tokens, and grouping typed tokens into nodes. A parser's output can now be represented in a new format, CSTML (Concrete Syntax Tree Markup Language), which looks like this:

```cstml
  <BinaryExpression [Expression]>
    <NumericLiteral [Expression] path='left'>
      <| Digits '2' |>
    </>
    <| Trivia ' ' |>
    <| Punctuator '+' path='operator' |>
    <| Trivia ' ' |>
    <[Expression] path='right'/>
  </>
```

Note that this tree includes not only information about what syntactic structures were found, but about those which could have been found. I also allows trees to be incomplete without being malformed (such as this fragment is). These are both crucial features in a system that supports the creation of semantic editors!





