# The TTY Subsystem (Theory)

How characters move from a terminal to an app and vice versa in UNIX/Linux.

Explain the TTY subsystem in high-level terms.

## Content

#todo Transform the follwing into Shelf notes

- History
    - A physical terminal could be either in line mode or character mode (see [Terminal Character Mode vs Line Mode](https://github.com/weibeld/weibeld-notes/blob/main/notes/terminal-character-mode-vs-line-mode.md))
    - The mode of the terminal could be set by the host through terminal control commands (see [Terminal Control Commands (Theory)](https://github.com/weibeld/nightingale/blob/main/drafts/terminals-2a-terminal-control-commands-theory/index.md))
        - TODO: verify
    - Line mode: the terminal buffers characters internally and only sends the entire string to the host when Enter is pressed
        - Note: this is the reason that the [Enter key is called Enter](https://en.wikipedia.org/wiki/Enter_key#History) (IBM 3270 and 5250 have separate Enter and  Return keys)
        - Line-based input applications like the shell used line mode
    - Character mode: the terminal sends every character to the host as it is pressed
        - Non-line based input applications, like vi, used character mdoe
    - In both cases, the input characters were sent from the device driver directly to the application
- TTY subsystem
    - Introduced by UNIX in the early 1970s (according to ChatGPT)
    - It's an intermediate processing layer for terminals in the kernel
    - The TTY subsystem intercepts and processes characters sent from the terminal before sending them to the application and vice versa
    - Its goal is to provide common functionality for terminals, such as line editing
    - The line editing feature menas that that all terminals can now run in character mode and the TTY subsystem emulates the line mode that was previously implemented by the terminals
        - This change is transparent to the application receiving the input, e.g. an application that expects the terminal to run in line mode
        - The advantage of offloading line editing to the TTY subsystem is that the line editing behaviour is identical across different terminal types
    - The line editing component of the TTY subsystem is called [line discipline](https://en.wikipedia.org/wiki/Line_discipline)
        - The line discipline also works in the other direction: characters sent by the application back to the terminal may be transformed by the line discipline
            - For example, LF (which is used in UNIX as a line separator) is transformed to CR+LF before being sent to the terminal (or whatever line separator the  terminal expects)
            - See [Carriage Return and Line Feed Line Separators](https://github.com/weibeld/weibeld-notes/blob/main/notes/carriage-return-and-line-feed-line-separators.md)
    - The TTY subsystem also provides other functionality, for example job and session control
        - This functionality is implemented in the TTY driver part of the TTY subsystem
        - The TTY driver component is a layer between the line discipline and the application
- Line discipline
    - Can be configured by the application or user
        - For example, it can be set to cooked (canonical) or raw mode
            - In raw mode, the line editing functionality is basically disabled and every character is sent to the application as it is entered
        - The line editing commands can also be customised
    - A user can configure the line discipline with the `stty` command
- Anatomy of the TTY subsystem
    - An instance of the TTY subsystem in the kernel looks as follows:
        - `[device driver] <--> [line discipline] <--> [tty driver]`
    - A single set of these components is called a "TTY device"
        - A UNIX system may have many TTY devices
            - In the case of physical terminals, as many as there are physical connectors to connect a terminal too
            - In the case of terminal emulators, an arbitrary number
    - The TTY driver part of a TTY device is exposed as a file under `/dev`, e.g. `/dev/tty1`
    - Applications may connect to a particular TTY device through the TTY driver (represented by files e.g. `/dev/tty1`)
    - A physical terminal is connected to a TTY device by connecting it to the physical socket managed by the device driver part of the TTY device
    - In the case of terminal emulators:
        - There may be an arbitrary number of TTY devices
        - A terminal emulator can connect to any TTY device (through the pseudo terminal, see below)
- Evolvement of TTY subsystem
    - Physical terminals:
        - `[terminal] <----> [host [kernel [device driver] <--> [line discipline] <--> [tty driver] kernel] <--> [application]  host]`
    - Built-in terminal emulators (built into the kernel), e.g. [Linux console](https://en.wikipedia.org/wiki/Linux_console):
        - `[host [kernel [terminal emulator] <--> [line discipline] <--> [tty driver] kernel] <--> [application]  host]`
    - User-space terminal emulators
        - [host [terminal emulator] <--> [kernel [pseudo terminal (pty)] <--> [line discipline] <--> [tty driver] kernel] <--> [application]  host]`

## Remarks

- Possible subtitle: how characters move between the terminal and an application

## Resources

- http://www.linusakesson.net/programming/tty/
