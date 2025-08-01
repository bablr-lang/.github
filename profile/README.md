# BABLR
[![come chat on Discord](https://img.shields.io/discord/1151914613089251388)](https://discord.gg/NfMNyYN6cX)

The BABLR organization's mission is to build a new ecosystem of next-generation developer tools to radically raise computer code literacy around the world.

We accomplish our goal by creating a new textual embedding for code that enhances syntax with metadata. For example if you had `true` as a snippet of code, one of our parsers might describe it like this: `<*BooleanLiteral> 'true' </>`

The goal of this is to be able to give people a window into code! To understand what we mean by a window into code it is useful to imagine two scenarios:

1. A room with one wall with a window in it
2. A room with no windows, but a painting of a window

If you were unable to move your head you might not be able to tell the difference between the two scenarios, but you would also only ever see one picture. If you're allowed to move around the room you will be able to construct a much more complete model of what is on the other side of the window. It is still possible to construct a fairly convincing simulation of a window if your window is really a computer screen and you use head tracking: a camera infers the looker's position in the room and uses it render onto the screen a picture of the outside as seen from the looker's position. If you want to see what this might really look like Hollywood has you covered with a brilliant imagination of [head tracking as spy subterfuge](https://www.youtube.com/watch?v=B7NLcB_iPQU) in Mission Impossible: Ghost Protocol.

I mention this because it shows us a more general kind of trick we can do: we can create dimensionality by responding to changes in the user's perspective. Especially on the internet snippets of example code have a tendency to be flat and unchanging, like you're seeing a painting of a window into code as opposed an actual window into the code.

To make a `<code>` element on a web page feel like window to another world the head tracking example is still instructive: we need a model of whatever is outside the window so that we can offer many different perspectives. It's a universal model of code made for this purpose that the BABLR project aims to define and popularize.

We know the extra-dimensional power of a universal data model from another technology that has made itself ubiquitous: the web browser. In addition to the 2D text of a web page browsers offer us the ability (I might even say freedom) to dive into a richer structure which is not normally visible. Browsers are even starting to help users conceive of that richer structure using actual extra dimensions, with Microsoft Edge [offering a 3D view into the structural model of a web page](https://youtu.be/BZAH8ZXhHZA?si=bvi-musXAi6TXhnb).

In addition to helping people be code literate we also aim to help tools be code-literate. Our structured data model can made semantic merging a reality, wildly reduce costs of maintaining software forks, create an explosion of new parsers, lint rules, templates, and semantic edit helpers. While this project was conceived of and executed with human ingenuity and human labor, we also expect that offering a first-of-its-kind streaming LR parser framework will be a tremendous boon to LLM providers looking to enforce structural constraints on code or other structured data being generated on the fly.

Overall we strive to make the most widely-usable technologies we can imagine so that we can be inclusive of the broadest group of users, core contributors, parser authors, tool developers... By welcoming pluralism and diversity we strengthen our community and make the strongest possible argument for its long term survival. If you want to be part of our community we welcome your involvement!

Our main portal for documentation and knowledge about the project is our website: [https://bablr.org](https://bablr.org). Our engineering and support discussions happen on [Discord](https://discord.gg/NfMNyYN6cX).

## Accessibility

Our biggest accessibility goal is to support a new generation of engineers and hackers writing code on phones, tablets, or even VR headsets.

We also believe a that the presence of a universal DOM in IDEs would be a boon for accessibility technologies as it is in the web. If you want to you can try [voice coding with Cursorless](https://www.cursorless.org/) for example, but as things are now you will have to switch to VSCode first.

Finally we wish to be able to offer our code accessibility experience to speakers of all human languages, not just English. This is why our grammars use the `-en` prefix. We welcome translations of our grammars to other natural languages.

## CLI

The easiest way to get started with BABLR is our node CLI: https://www.npmjs.com/package/@bablr/cli

```bash
bablr -l @bablr/language-en-cstml -p Node <<< '<*BooleanLiteral> "true" </>'
```

Try passing the `-v` flag to see a trace of the parser!

## Scope

The BABLR project has an extremely ambitious vision. If you were to track the growth of the project over time you would find that its abilities and ambitions have always evolved in tandem: implementation chasing imagination.

The vision is roughly to create a new web browser and a new IDE, and possibly to fuse the existing concepts of "web browser", "IDE" and "VCS" together completely and permanently. We want to show that there exists a math that can describe the inner workings of each of these frontends equally well. It's a bit like trying to find the perfect shape for a Lego brick. If we're successful it should be possible for you to use our digital building blocks to create [almost anything you can imagine](https://www.youtube.com/watch?v=aPO5JaShu2U).

Our biggest challenge is that we've chosen to use a new kind of data model which no other tool is using. This means we have to write new parsers for everything. Since this is potentially very onerous work, every attempt has been made to provide a high-level, polished well-tooled, tight-feedback-loop environment for defining parsers.

One advantage we have is that BABLR isn't defined using any code generation or other such weird tricks. It's just a bunch of highly composable immutable primitives and a lot of very flexible functional scripting. A system like this can be constructed in any language with basic lambda calculus, and once constructed you'll have exactly the tools you need to carry out such a cross-language program translation in practice! If you're intersted in taking on a new VM implementation, please get in touch to coordinate and we'll do anything we can to help.

## A word about repository structure

We like having a lot of small, highly focused and conceptually independent repos.

We don't like monorepos. We think that smashing all the repos together encourages people not to think carefully about where the system boundaries belong. Further more it tends to centralize all maintenance costs as users cannot easily fork and own a small part of a bigger system without forking and owning all of it. Owners cannot easily delegate trust because trust tends to become all-or-nothing: contributors either can't do anything without help or they are given the keys to the kingdom. Our "multi-repo" strategy ensures that we can build trust by giving trust -- but more limited kinds of trust, and in ways that we can readily verify that our trust is not being abused by bad actors.

We think this tends to create a healthy, sustainable open-source ecosystem in the same way a tree is strong when its trunk supports many branches, twigs, and leaves. A tree with only a trunk is probably a dead tree.

Our most important repositories are:

- **[agast-helpers](https://github.com/bablr-lang/agast-helpers)**: Contains utilities for working with our public data structures
- **[agast-vm](https://github.com/bablr-lang/agast-vm)**: The authority on what is a legal agAST tree
- **[boot](https://github.com/bablr-lang/boot)**: Helps us break dependency cycles as a system defined in terms of itself
- **[bablr-vm](https://github.com/bablr-lang/bablr-vm)**: The main BABLR implementation. Instructions are provided by a strategy
- **[bablr-vm-strategy-parse](https://github.com/bablr-lang/bablr-vm-strategy-parse)**: Implements text parsing using class-based grammars and `bablr-vm`
- **[bablr](https://github.com/bablr-lang/bablr)**: A thin wrapper around `bablr-vm` and `bablr-vm-strategy-parse`
- **[bablr-cli](https://github.com/bablr-lang/bablr-cli)**: A node CLI for evaluating BABLR grammars
- **[regex-vm](https://github.com/bablr-lang/regex-vm)**: A streaming regex engine which accepts BABLR-format parse trees. The oldest repo!
- **[language-en-cstml](https://github.com/bablr-lang/language-en-cstml)**: A BABLR grammar for parsing CSTML.

## We accept donations!

The first five years of initial development work on this project were full time without compensation. If you are excited about the direction of our work and you are in a position to be able, we would love support on [OpenCollective](https://opencollective.com/bablr). Such contributions would in a very practical sense ensure our skilled team's ability to continue to focus on shipping the best possible software for everyone, for free!

## Code of Conduct

We don't maintain a formal code of conduct. This does not mean that all behavior is permissible, but rather that we recognize that creating a welcoming community requires continuous effort and diplomacy. We ask for your help to create a friendly ["no wrong doors"](https://lethain.com/no-wrong-doors/) culture, and we ask for grace and guidance from our community if and when we do not live up to our own promises and principles.
