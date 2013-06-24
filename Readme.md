# Vnilla #

Vnilla is a lightweight markup language for [visual novel](http://en.wikipedia.org/wiki/Visual_novel) translation projects. Its syntax results in almost plain-text files with no distractions. This enables translators, editors and other contributors to focus on the content they are most interested in, and to modify it in any environment.

## Structure ##

The file structure of Vnilla is divided into blocks, paragraphs and lines. A typical Vnilla file includes three blocks, all of which are optional:

### Introduction ###

The first block gives relevant information about the file. Each line is simply a key-value pair, separated by a colon. By default, these lines are assumed to exist, even if they don't:

    Blocks: Introduction, Characters, Story
    Languages: ja, en

You can expand this section with some general information:

    Project: Hypothetical Story
    File: script01
    Route: Common
    Date: March 17

...with statistics:

    Lines: 1337
    Size: 112KB (ja), 124KB (en)

...or anything else such as translation status:

    Translated: Yes
    Edited: Yes
    QCed: No

### Characters ###

This block lists all characters engaging in a dialogue in the current script. Names are translated once in Characters block instead of each time they speak in Story block.

    鈴木
    Suzuki
    
    本田
    Honda
    
    川崎
    Kawasaki

### Story ###

This final block includes the main text. Each in-game text line is represented as a paragraph (i.e., separated by a blank line) and each paragraph consists of one or more lines.

By default, first line of a paragraph is the original text, and the following is its translation:

    むかしむかし、あるところに…
    Once upon a time...

Multiple lines within a single in-game text line are either separated by a literal `\n`, or marked with `[Lines]` notation.

Speech is described by putting the character's name between `【` and `】` symbols at the beginning of a line, so the person working on the file knows which line belongs to whom. Note that editing these names does not affect their actual translations in Characters block.

    【主人公】
    「ただいまー」
    "I'm home!"

Choices begin with an indicator too:

    [Choice](1-A)
    もう少し彼女と話す
    Talk with her for a bit longer

Each paragraph may include comments, starting with a `>` symbol. You can use it to hold a conversation:

    めでたしめでたし
    ...and they all lived happily ever after.
    > Translator-kun: This is a comment.
    > Editor-chan: This one's too!

It is also possible to type down stray comments to indicate important points such as a scene break, beginning of a new day, or change of perspective:

    >>>>> Brace yourselves, H-scene is coming. >>>>>

## Supported engines ##

Vnilla is just a representation of a visual novel script and, in theory, it is compatible with most VN translation projects, if not all. However, it is up to you to handle the conversion from a VN engine's own format and vice versa.

If the project you are working on somehow requires more than standard character, choice and line translations, setting up additional blocks might be a good idea.

## Tools ##

Often in a visual novel translation project, a contributor needs to do some bulk actions such as examination, modification and calculation; and there are times the usual find & replace method falls short even with the aid of regular expressions.

Vnilla Tools offers handy functions that you may use in such an endeavor. You can list all the lines spoken by a certain character, filter them down to include a certain set of words, mark any line that is too long to fit into the game's text box, handle line wrapping, or automatically calculate the overall translation progress. And of course, you can write your own lines of code according to your needs.

Vnilla Tools will be released once it reaches a reasonable point in maturity.

## Notes ##

A list of things to keep in mind for further development:

- Vnilla should avoid using reserved characters as much as possible. It is supposed to be compatible with all VN engines, and different engines have different special characters for changing text style, issuing a wait command, etc.
- Vnilla's structure has been designed mostly with ADV-style games in mind. While this is not tested, large blocks of text associated with NVL-style games might not fit very well in it, if they are spreading to multiple lines.