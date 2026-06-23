# How to Configure a TTY Device

Take a closer look at the options for configuring a TTY device and how this plays together with line editing, in particular in Bash.

## Content

- For line-based applications, there are three locations where line editing can happen:
    1. In the terminal (if the terminal is in line mode; this is relevant only historically)
    2. In the line discipline of the TTY subsystem on UNIX/Linux
    3. In the application itself
- How is the TTY pipeline configured?
    - Show current configuration for a specific TTY device: `stty -f /dev/tty[x] -a`
        - Don't use `stty -a` because this shows the configuration for the `stty` process
    - The configuration is a combination of options that can either be on or off
    - There are some named combinations:
        - raw: don't perform any input/output processing (most options are turned off)
            - Enable with `stty raw`
        - sane (a.k.a. cooked): 
            - Enable with `stty sane`: the default settings, perform input and output processing, in particular using the default line discipline
    - The option `icanon` controls the line buffering, i.e. whether a line discipline is applied or not. If `icanon` is on, then lines are buffered in the TTY system and the control characters that are relate to erasing and killing characters (see `stty -a` output) are applied. If `icanon` is off, then lines are not buffered, the control characters ar not applied, and all characters are sent as is to the process (signalling characters like `Ctrl-C` are still interpreted).
        - By default, Bash disables `icanon` in the TTY device settings and also disables `echo` and `icrnl` (this is still less disablement of features than setting the TTY to raw mode with `stty raw`). This is because, by default, Bash wants to do the line editing itself. This is implemented with GNU Readline.
            - Artificially enabling line editing in the TTY when Bash expects no line editing:
                - In another terminal window do: `stty -f /dev/<tty> icanon echo icrnl`, where `<tty>` is the TTY to which Bash is connected
                - Type something in the terminal with Bash and try editing the command line with the common control characters, e.g. `Ctrl-C` and `Ctrl-U`. They work. However, try now some of the Bash specific control characters, such as `Meta-B`, `Meta-F`, `Ctrl-K`, the arrow keys, the history search (`Ctrl-R`) or command completion (`Tab`). They don't work. This is because all line editing happens in the TTY now. Until you hit `Enter`, Bash does not receive any data.
                - Then hit `Enter`. At this moment, the entire command is sent to Bash, where it is processed. The command is executed and the result is printed. However, besides the result, the command itself is also printed again. This is because Bash normally expects that `echo` in the TTY is turned off, and thus that Bash needs to echo every typed character (so that you can see what you type). So Bash echos everything it gets before executing it, not knowing that the TTY already echoed all the characters (since Bash doesn't know that we artifically changed the settings in the TTY).
                - After each command, Bash resets the TTY to its expected settings, so when you execute the next command, everything will be back to normal. To test it again, you need to execute the above `stty` command again.
                - The same can be achieved by setting the TTY to sane mode: `stty -f /dev/<tty> sane`
            - Artificially disabling TTY line editing for Bash without built-in line editing
                - Start Bash with `bash --noediting`. This disables the built-in line editing of Bash and Bash expects the line editing to be done in the TTY.
                - Disable `icanon` with `stty -f /dev/<tty> -icanon`
                - Type a command and try editing it with _any_ line editing command (Backspace, `Ctrl-W`, `Ctrl-U`, etc.). Nothing works. Every character that is typed is now sent immediately to Bash. The TTY does no line buffering and editing and Bash does also no line editing (since it expects the TTY to do it). It's now still possible to execute commands, however, it's impossible to edit the line.                    
- GNU Readline features
    - Emulates many of the TTY default line editing commands, such as `Ctrl-W` and `Ctrl-U`
    - Adds advanced commands such as `Meta-B`, `Meta-F`, or `Ctlr-K`
    - Provides completely distinct line editing modes, such as the vi or emacs mode  
        - Can be enabled with `set -o vi` or `set -o emacs`
    - Provides command completion (by pressing `Tab`)
    - Provides an interactive command history interface (by pressing `Ctrl-R`)

## Remarks

- TODO: find complete list of GNU Readline editing commands 

## Resources

- https://www.gnu.org/software/bash/manual/html_node/Command-Line-Editing.html
- https://blog.sanctum.geek.nz/vi-mode-in-bash/
- https://en.wikipedia.org/wiki/Terminal_mode
- http://uw714doc.xinuos.com/en/SDK_sysprog/_TTY_in_Canonical_Mode.html
- http://uw714doc.xinuos.com/en/SDK_sysprog/_TTY_in_Raw_Mode.html
- https://stackoverflow.com/questions/358342/canonical-vs-non-canonical-terminal-input
- GNU Readline:
    - https://en.wikipedia.org/wiki/GNU_Readline
    - https://tiswww.case.edu/php/chet/readline/rltop.html
    - https://web.mit.edu/gnu/doc/html/rlman_2.html
