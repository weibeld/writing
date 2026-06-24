# Bash Command Line Editing (Theory)

The Bash [command-line editing](https://www.gnu.org/software/bash/manual/bash.html#Command-Line-Editing) functionality is provided by [GNU Readline](https://tiswww.cwru.edu/php/chet/readline/rltop.html). 

The idea of this article is to present the full line editing features of Bash, by however making it clear that these features are provided by Readline. Thus, a focus is put on clearly distinguishing which facilities are provided by Readline and which are provided by Bash.

The article should also stress that, since Readline is used by various applications, the line editing features just learned also work for other applications that use Readline (see [Applications That Use GNU Readline](https://github.com/weibeld/weibeld-notes/blob/main/notes/applications-that-use-gnu-readline.md)).

## Content

- Reference [The TTY Subsystem (Practice)](https://github.com/weibeld/nightingale/blob/main/drafts/terminals-3b-the-tty-subsystem-practice/index.md) which states that by default Bash sets the TTY to raw mode and does the line editing itself
- Introduce GNU Readline
- List Readline features (see [GNU Readline Line Editing Commands](https://github.com/weibeld/weibeld-notes/blob/main/notes/gnu-readline-line-editing-commands.md)) and how they're used in Bash
    - Line editing
        - Default key sequences
        - Mention command arguments
        - Mention keyboard macros
    - Completion
        - Readline side
            - Key sequences (`Meta-?`, etc.)
        - Bash side:
            -`complete`, `compgen`, `compopt` (reference to https://www.gnu.org/software/bash/manual/bash.html#Command-Line-Editing)
    - History
        - Readline side: 
            - Different types, key sequences
            - History library (https://tiswww.cwru.edu/php/chet/readline/history.html)
                - History expansion (https://www.gnu.org/software/bash/manual/bash.html#History-Interaction)
        - Bash side:
            - `fc`, `history`, `$HIST*` variables (https://www.gnu.org/software/bash/manual/bash.html#Bash-History-Facilities)
        - The Bash history facilities and the Readline history can interact (e.g. when deleting the history with `history -c`, the history in Readline is deleted too)
            - This works presumably through the [History library](https://tiswww.cwru.edu/php/chet/readline/history.htm)
        - This makes history a quite large topic. Maybe include only the basic history provided by Readline and cover advanced history features in a separate article?
    - Editing modes
        - Readline side
            - `set editing-mode vi|emacs`
        - Bash side:
            - `set -o vi|emacs`
    - Configuration
        - Readline side
            - [Init file](https://www.gnu.org/software/bash/manual/bash.html#Readline-Init-File)
        - Bash side
            - `bind` (see [Bash bind Builtin](https://github.com/weibeld/weibeld-notes/blob/main/notes/bash-bind-builtin.md))
- Useful configurations
- Demonstrate difference between using `bind` and using a Readline init file
    - With `bind`, settings apply only to Bash, with Readline init file, settings apply to all apps that use Readline

## Remarks

<!-- Further remarks about the article -->

## Resources

General:

- [GNU Readline Line Editing Commands](https://github.com/weibeld/weibeld-notes/blob/main/notes/gnu-readline-line-editing-commands.md)
- [Applications That Use GNU Readline](https://github.com/weibeld/weibeld-notes/blob/main/notes/applications-that-use-gnu-readline.md)

Completion: 

- https://medium.com/itnext/programmable-completion-for-bash-on-macos-f81a0103080b
- https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion.html
- https://www.gnu.org/software/bash/manual/html_node/Programmable-Completion-Builtins.html

History:

- https://www.gnu.org/software/bash/manual/html_node/Using-History-Interactively.html
