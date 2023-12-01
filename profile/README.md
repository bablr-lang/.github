# BABLR
[![come chat on Discord](https://img.shields.io/discord/1151914613089251388)](https://discord.gg/NfMNyYN6cX)

The BABLR organization's mission is to build next-gen tooling ecosystem to radically raise computer code literacy around the world. It aims to do this by creating standard structural representations of computer code. Much current developer suffering comes from the fact that developers use a wide variety of tools in their work, and these tools interoperate poorly with each other. The particular problem is the absence of any format for code (other than plain text) that all tools share. BABLR aims to define a single representation for code that will be as useful as possible to the broadest group of individuals, then to capitialize on the existance of such a format to build the most richly integrated developer experiences in the world.

There are several closely related technologies under development to solve the problem: CSTML (a serialization format for parsed code), agAST (a JS in-memory sturcture for storing parsed code), and Spamex (a regex-like langauge with structural matching). Each of these technologies is designed to be larger than the BABLR organization and would likely be subject to formal standardization if they are informally successful, as is often the way of things with the web. Instead of writing a formal specification for these technologies, I have instead opted to define them in terms of a reference VM built in Javascript: [bablr-vm]([bablr-vm](https://github.com/bablr-lang/bablr-vm)). This newly-developed streaming parser core which parses code into agAST trees, CSTML documents, or CSTML-ish streams. Because the formats are defined by `bablr-vm` (and `bablr-vm` is in alpha), the formats should also be considered to be in alpha and are subject to change at any time up until `bablr-vm@1.0.0` (which is being worked towards with all possible haste).

Let's say we have a simple JSON expression like this ([playground](https://codesandbox.io/p/sandbox/blissful-sky-sgvdpz?file=%2Fsrc%2Fjson.grammar.js%3A34%2C47)):
```json
[1,true,"3"]
```

A CSTML represention of the same data will be much more verbose, and it will always contain the complete original text embedded inside it. This is not a format that you are likely to read directly (very often), instead more likely this data will be used to construct a much denser (literal) representation (like the one above) where the extra data is expressed as colorful syntax highlighting and other rich editor features which can enhance rendering and interactivity of the embedded code.

```cstml
<Array>
  open:
  <Punctuator balanced=']'>
    '['
  </>
  elements[]:
  <Number>
    digits:
    <Digit>
      '1'
    </>
  </>
  separators[]:
  <Punctuator>
    ','
  </>
  elements[]:
  <Boolean>
    value:
    <Keyword>
      'true'
    </>
  </>
  separators[]:
  <Punctuator>
    ','
  </>
  elements[]:
  <String>
    open:
    <Punctuator balanced='"' innerSpan='String'>
      '"'
    </>
    content:
    <StringContent>
      '3'
    </>
    close:
    <Punctuator balancer>
      '"'
    </>
  </>
  close:
  <Punctuator balancer>
    ']'
  </>
</>
```
