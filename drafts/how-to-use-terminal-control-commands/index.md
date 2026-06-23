# How to Use Terminal Control Commands

Demonstration of how command-line based applications can use terminal control commands (terminal capabilities) to control what's displayed on the terminal.

## Content

Specify a simple command-line based application (or just a dummy component like a progress bar) and implement it with:

1. Raw terminal control commands (Bash script)
1. Terminfo codes (Bash script)
1. ncurses (C)
1. Maybe another terminal UI library in another programming library
    - Python
        - [curses](https://docs.python.org/3/howto/curses.html) (wrapper around the original C curses library)
        - [Urwid](http://urwid.org/index.html) (an alternative to curses)
    - Go
        - [goncurses](https://pkg.go.dev/github.com/rthornton128/goncurses) (wrapper around original C ncurses library)
        - [termbox](https://pkg.go.dev/github.com/nsf/termbox-go) (still working but unmaintained)
        - [tcell](https://pkg.go.dev/github.com/gdamore/tcell/v2) (based on termbox)

## Remarks

## Resources

- https://unix.stackexchange.com/questions/573410/how-to-interact-with-a-terminfo-database-in-c-without-ncurses
    - This StackOverflow answer states that terminfo isn't really an advantage anymore in terms of portability since virtually every terminal emulator is VT100/ANSI compatible.
