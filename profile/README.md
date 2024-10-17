# BABLR
[![come chat on Discord](https://img.shields.io/discord/1151914613089251388)](https://discord.gg/NfMNyYN6cX)

The BABLR organization's mission is to build a new ecosystem of next-generation developer tools to radically raise computer code literacy around the world. It aims to do this by creating a common "math-y" system for representing code to that unlocks new coding workflows for all developers while changing the way that language and tooling authors collaborate to deliver rich IDE functionality.

The current aim of the project is to grow to the size where its community is self sustaining. The ideal is that ease of defining languages should make many people want to define languages in terms of CSTML. Having many languages defined in CSTML will make it an attractive foundation on which to build language-aware tools. Once a critical threshhold is passed this should become a self-sustaining virtuous cycle where tools make it worth writing languages which make it worth writing tools.

It is worth noting that the technologies that are popular in this space (notably tree-sitter and LSP) are already benefactors of this dynamic so that the activation energy required for a new, original product to break into this market is exceedingly high.

## Developer Experience

Much current developer suffering arises from one of several main pain points:

- Our tools usually can't tell us what an individual piece of syntax actually means.
- Our tools can't usually help us discover what syntaxes are available to us.
- When we shift from a language we know well to one that is foreign, we often have to shift from using tools we know well and trust to tools we don't know or trust at all.
- Often your IDE loses track of your intent in editing code, causing it to produce bizarre results that are nevertheless not technically the result of any bug.
- Editing significant amounts of code by hand is so labor intensive that developers are trying to replace their brains with artificial brains just to not have to deal with it
- There is no universal target environment against which to evaluate queries and transformations, so queries and transformations are wildly underused in the development process.
- It is usually not easy to extend our tools *or* our languages.

## The solution

The solution, at its most general, is to create an embedding language for code documents: a language that's meant to store documents written in other (arbitrary) languages within it. Think of an embedding like a box that comes with a guarantee that you can safely put anything in it and then get that same thing back out again. HTML, XML, and JSON are the most commonly known and used embedding languages. 

In order to solve the problem of tracking developer intent in an IDE, though, our language will need some features not found in other embedding languages, most notably gaps. If you think of CSTML like a piece of paper on which you write, the existence of a gap in the CSTML (notated `<//>`) is sort of like having the ability to take your pencil and stab a hole straight through the piece of paper. Creating this kind of hole/gap is a wildly useful thing to be able to do: it's basically the purpose of any templating language. In JS you might write `console.log('Hello, %s', 'myself')`. In this case `%s` is the gap. But in Python it would be `print("Hello, {}".format("myself"))`, where `{}` is the gap.

Now take this one step further. You're inserting a new `if` statement into your code. A common edit to write in JS is adding an if statement like `if(condition) body` but if you type out `if()` you'll discover that the minimal text isn't valid JS syntax. The smallest valid syntax you can write is: `if(/**/);`, but this is still very language specific. What if instead we take our pencil and jab a hole in the paper resulting in something which, if it were expressed in a templating language, would look something like: `if(<gap>)<gap>`. Using the lego-y composability that comes with these "universal code templates" is how BABLR can allow you to build up syntactic programs with a drag and drop user experience that is currently possible only in a toy language like [Scratch](https://scratch.mit.edu/projects/editor/)

## Usage

All together it looks something like this:

```js
import { buildTag, Context, AgastContext } from 'bablr';
import { buildFullyQualifiedSpamMatcher } from '@bablr/agast-vm-helpers';
import * as language from '@bablr/language-en-es3';

const ctx = Context.from(AgastContext.create(), language);
const matcher = buildFullyQualifiedSpamMatcher({}, language.canonicalURL, 'Expression');

const js = buildTag(ctx, language, matcher);

const condition = js`true`;
const statement = js`sayHello();`;

js`if(${condition}) {
  ${statement}
}`;
```

Formatting is always preserved in these templating operations, so the result is:

```js
if (true) {
  sayHello();
}
```

## CSTML

Let's say we have a simple JSON expression like this:
```json
[1, true, "3"]
```

A CSTML represention of the same data will be much more verbose, and it will always contain the complete original text embedded inside it. This is not a format that you are likely to read directly (very often), instead more likely this data will be used to construct a much denser (literal) representation (like the one above) where the extra data is expressed as colorful syntax highlighting and other rich editor features which can enhance rendering and interactivity of the embedded code.

```cstml
<$>
  .:
  <$Array>
    openToken: <*Punctuator '[' balanced=']' />
    separators[]: []
    elements[]$: []
    elements[]$:
    <$Number span='Number'>
      wholePart:
      <$Integer>
        signToken: null
        value: <*UnsignedInteger '1' noDoubleZero />
      </>
      fractionalSeparatorToken: null
      fractionalPart: null
      exponentSeparatorToken: null
      exponentPart: null
    </>
    separators[]: <*Punctuator ',' />
    <#*Space:Space ' ' />
    elements[]$:
    <$Boolean>
      sigilToken: <*Keyword 'true' />
    </>
    separators[]: <*Punctuator ',' />
    <#*Space:Space ' ' />
    elements[]$:
    <$String>
      openToken: <*Punctuator '"' balanced='"' balancedSpan='String' />
      content: <*StringContent '3' />
      closeToken: <*Punctuator '"' balancer />
    </>
    closeToken: <*Punctuator ']' balancer />
  </>
</>
```
