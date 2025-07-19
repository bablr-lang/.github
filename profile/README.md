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

In addition to helping people be code literate we also aim to help tools be code-literate. Our structured data model can made semantic merging a reality, wildly reduce costs of maintaining software forks, create an explosion of new parsers, lint rules, templates, and semantic edit helpers. While this project was conceived of and executed with human ingenuity and human labor, we also expect that offering a first-of-its-kind streaming LR parser framework will be a tremendous boon to LLM providers looking to enforce structural constraints on code or other structured data being generated on the fly.

Overall we strive to make the most widely-usable technologies we can imagine so that we can be inclusive of the broadest group of users, core contributors, parser authors, tool developers... By welcoming pluralism and diversity we strengthen our community and make the strongest possible argument for its long term survival. If you want to be part of our communitty we welcome involvement through any and all channels.

Our main portal for documentation and knowledge about the project is our website: [https://bablr.org](https://bablr.org).

## CLI

The easiest way to get started with BABLR is our node CLI: https://www.npmjs.com/package/@bablr/cli

```bash
bablr -l @bablr/language-en-cstml -p Node <<< '<BooleanLiteral> "true" </>'
```

Try passing the `-v` flag to see a trace of the parser!

## A word about repository structure

We like having a lot of small, highly focused and conceptually independent repos.

We don't like monorepos. We think that smashing all the repos together encourages people not to think carefully about where the system boundaries belong. Further more it tends to centralize all maintenance costs as users cannot easily fork and own a small part of a bigger system without forking and owning all of it. Owners cannot easily delegate trust because trust tends to become all-or-nothing: contributors either can't do anything without help or they are given the keys to the kingdom. Our "multi-repo" strategy ensures that we can build trust by giving trust -- but more limited kinds of trust, and in ways that we can readily verify that our trust is not being abused by bad actors.

We think this tends to create a healthy, sustainable open-source ecosystem in the same way a tree is strong when its trunk supports many branches, twigs, and leaves. A tree with only a trunk is probably a dead tree.

## Code of Conduct

We don't maintain a formal code of conduct. This does not mean that all behavior is permissible, but rather that we recognize that creating a welcoming community requires continuous effort and diplomacy. We ask for your help to create a friendly ["no wrong doors"](https://lethain.com/no-wrong-doors/) culture, and we ask for grace and guidance from our community if and when we do not live up to our own promises and principles.
