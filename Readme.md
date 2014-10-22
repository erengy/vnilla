# Vnilla

Vnilla is a lightweight markup language for [visual novel](https://en.wikipedia.org/wiki/Visual_novel) translation projects. Its syntax results in almost plain-text files with no distractions. This enables translators, editors and other contributors to focus on the content they are most interested in, and makes that content modifiable in any environment.

## Structure

The file structure of Vnilla is divided into blocks, paragraphs and lines. A typical Vnilla file includes three blocks, all of which are optional:

### Introduction

The first block is a metadata block, which gives relevant information about the file. Each line is simply a key-value pair, separated by a colon:

    == Introduction
    
    Project: Hypothetical Story
    File: script01
    Route: Common
    Date: March 17

You can expand this section with automated statistics:

    Lines: 1337
    Size: 112KB (ja), 124KB (en)

...with the names of the contributors:

    Contributors: Translator-kun, Editor-chan

...or anything else such as translation status:

    Translation: ✓
    Editing: ✓
    QC: ✗

Vnilla files are typically encoded in UTF-8, hence it is okay to use Unicode symbols as above.

### Characters

The second block is a dramatis personæ, which lists all the characters engaging in a dialogue in the current script. Names are translated once in *Characters* block instead of each time they speak in *Story* block.

    == Characters
    
    鈴木
    Suzuki
    
    本田
    Honda
    
    川崎
    Kawasaki

### Story

This final block holds the main content. Each in-game text line is represented as a paragraph (i.e., separated by a blank line) and each paragraph consists of one or more lines.

By default, first line of a paragraph is the original text, and the following is its translation:

    == Story
    
    むかしむかし、あるところに…
    Once upon a time...

For convenience, multiple lines within a single in-game text line are described by the `line` command, instead of being separated by an escape sequence such as `\n`:

    =line 2
    Japanese line #1
    Japanese line #2
    English translation line #1
    English translation line #2

Speech is described by using the `character` command, so the person working on the file will know which line belongs to whom. Note that editing these names does not affect their actual translations in *Characters* block, but this behavior can be changed if required.

    =character 主人公
    「ただいまー」
    "I'm home!"

Choices begin with the `choice` command:

    =choice
    もう少し彼女と話す
    Talk with her for a bit longer

Each paragraph may include comments, starting with a `>` symbol. You can use it to hold a conversation, a la IRC:

    めでたしめでたし
    ...and they all lived happily ever after.
    > Translator-kun: This is a comment.
    > Editor-chan: This one's too!

It is also possible to type down stray comments to indicate important points such as a scene break, beginning of a new day, or change of perspective:

    >>>>> Brace yourselves, H-scene is coming. >>>>>

Note that the use of multiple comment symbols above was a stylistic choice, not a requirement.

If you ever need to comment out a line, you are advised to use the `ignore` command instead:

    =ignore
    俺も幼心にわかっていた。
    > Translator-kun: Merging with the line below.

## Supported engines

Vnilla is just a representation of a visual novel script and –in theory– it is compatible with most VN translation projects, if not all. However, it is up to you to handle the conversion from a VN engine's own format and vice versa.

If the project you are working on somehow requires more than standard character, choice and line translations, setting up additional blocks might be a good idea.

## Configuration

Different VN engines have different special characters for changing text style, issuing a wait command, etc. For this reason, Vnilla avoids using reserved characters as much as possible, while allowing you to change them if need be. By modifying the configuration file, you may use a different set of reserved characters, commands and blocks.

## Tools

Often in a visual novel translation project, a contributor needs to do some bulk actions such as examination, modification and calculation; and there are times the usual find-and-replace method falls short, even with the aid of regular expressions.

Vnilla Tools offers handy functions that you may use in such an endeavor. You can list all the lines spoken by a certain character, filter them down to include a certain set of words, mark any line that is too long to fit into the game's text box, handle line wrapping, get a list of all choices, or automatically calculate the overall translation progress. Of course, you can expand the functionality according to your project's needs.

## Notes

A list of things to keep in mind for further development:

- Vnilla's structure has been designed mostly with ADV-style games in mind. Large blocks of text associated with NVL-style games need to be tested.
- Vnilla Tools will be released once it reaches a reasonable point in maturity. However, its development can be sped up if there is evident interest in such a toolset.

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).