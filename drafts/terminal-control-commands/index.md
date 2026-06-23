# Terminal Control Commands

Demistify terminal control commands with a focus on the ANSI/VT100 commands (see below).

Part of the teminal series:

1. [[1.article-ideas.terminal-control-commands]]
2. [[1.article-ideas.the-tty-subsystem]]
3. [[1.article-ideas.how-to-configure-a-tty-device]]
4. [[1.article-ideas.how-to-use-terminal-control-commands]]

## Content

#todo Refactor this into notes in the Shelf.

- Terminal control commands are codes sent by the host to the terminal to control the behaviour of the terminal
- Today, there's a de-facto standard for such codes that's implemented by most terminal emulators (see below)
- Standards (the following standards are mostly equivalent)
    - [ECMA-48](https://www.ecma-international.org/publications/standards/Ecma-048.htm) (1976)
    - [ANSI X3.64](https://standards.globalspec.com/std/512717/ansi-x3-64) (1977)
    - [ISO 6429](https://www.iso.org/standard/12782.html) (1978)
- Alternative names
    - [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code)
    - VT100 escape codes
- VT100
    - The [VT100](https://en.wikipedia.org/wiki/VT100) (introduced in 1978) was [one of the first](https://en.wikipedia.org/wiki/VT100) terminals to implement the   ANSI escape codes (see above)
    - The VT100 is today the [de-facto standard](https://en.wikipedia.org/wiki/VT100) for terminal emulators to emulate
    - The ANSI escape codes are also described in the [VT100 User Guide](https://www.vt100.net/docs/vt100-ug/)
        - VT100 also implements proprietary control sequences, in addition to the ANSI ones, which are also described in the VT100 User Guide
- Types of control codes
    - [Control characters](https://www.vt100.net/docs/vt100-ug/chapter3.html#S3.3.1): single-character codes (non-alphanumeric)
    - [Control sequences](https://www.vt100.net/docs/vt100-ug/chapter3.html#S3.3.2): multi-character codes that start with a Control Sequence Introducer (CSI). In   the ANSI standard, the CSI is `ESC [`.
    - The VT100 User Guide also describes private (proprietary) control sequences which may either start with the ANSI CSI or a different CSI (e.g. `ESC #`).
- Text colour and formatting
    - The text colour and formatting is set with the SGR (Select Graphic Rendition) control sequence defined as `ESC [ ... m`
    - The VT100 User Guide [does not list](https://www.vt100.net/docs/vt100-ug/chapter3.html#SGR) the colour parameters for SGR
        - Probably because the [VT100 didn't support colours](https://lwn.net/Articles/751980/) by default
    - The colour parameters for SGR are however listed in the [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code#3-bit_and_4-bit) Wikipedia article
- Modern usage of terminal control commands
    - Libraries like ncurses, etc.
    - Just mention them, this is not the focus of this article

## Remarks

This is the first article of a three-part series about terminals:

1. Terminal control commands: how a terminal can be controlled by applications
1. TTY subsystem: how characters move from a terminal to an app and vice versa in UNIX/Linux
1. Bash line editing: clearing up some confusion about line editing

Further topics that might be covered in separate articles are:

1. Terminal input sequences: how some terminal control commands can also be entered through the keyboard (see [Terminal input sequenes](https://en.wikipedia.org/wiki/ANSI_escape_code#Terminal_input_sequences))
    - Is this still relevant today?
    - Maybe this just refers to the encoding of non-alphanumeric keys when they are sent from the terminal to the host?
1. Practical usage of terminal control commands
    - Termcap, terminfo
    - ncurses, etc.


## Resources

- https://github.com/weibeld/terminal-escape-sequences
    - There's an error in this document: terminal escape sequences are only sent from the host to the terminal, not entered by the user into the terminal
- https://github.com/weibeld/figures/tree/master/misc/terminal-control.graffle
    - There are errors in the "Example" and "Escape Sequences" figures: terminal control commands are not entered through the keyboard
- https://github.com/weibeld/figures/blob/master/misc/terminals.sketch
- [[2.box.overview-terminals]]
