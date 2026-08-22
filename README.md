# pycal

A lightweight terminal calendar with per-day notes. Single Python file, no dependencies beyond the standard library.

```
                       ◄  July 2026  ►

  ┌───────┬───────┬───────┬───────┬───────┬───────┬───────┐
  │  Mon  │  Tue  │  Wed  │  Thu  │  Fri  │  Sat  │  Sun  │
  ├───────┼───────┼───────┼───────┼───────┼───────┼───────┤
  │-29-   │-30-   │- 1-   │- 2-   │- 3-   │- 4-   │- 5-   │
  ├───────┼───────┼───────┼───────┼───────┼───────┼───────┤
  │- 6-   │- 7-   │- 8-   │- 9-   │-10-·  │-11-   │-12-   │
  ├───────┼───────┼───────┼───────┼───────┼───────┼───────┤
  │-13-   │-14-   │-15-   │-16-·  │-17-   │-18-   │-19-   │
  │       │       │       │code … │       │       │       │
  ├───────┼───────┼───────┼───────┼───────┼───────┼───────┤
  │-20-   │-21-   │-22-   │-23-·  │-24-   │-25-   │-26-   │
  │       │       │       │denti… │       │       │       │
  ├───────┼───────┼───────┼───────┼───────┼───────┼───────┤
  │-27-   │-28-   │-29-   │-30-   │-31-   │- 1-   │- 2-   │
  │       │       │       │       │       │       │       │
  └───────┴───────┴───────┴───────┴───────┴───────┴───────┘
─────────────────────────────────────────────────────────────
  Thu 16 Jul 2026
  a:edit  d:del  c:copy  v:paste  [ ]  n/p  /  g  t  q:quit
  code review with backend team
```

Cells grow to fill the window, so a taller terminal shows more of each note.
The key hints adapt to the terminal width.

## Requirements

- Python 3.7+
- A terminal with UTF-8 and 256-colour support (ncursesw)
- Minimum terminal size: 43 columns × 21 rows (22 rows to show every week of a
  six-week month; below that the grid scrolls to keep the selected day in view)

## Installation

```sh
git clone https://github.com/simddev/pycal
chmod +x pycal/pycal
sudo ln -s "$PWD/pycal/pycal" /usr/local/bin/pycal
```

No pip, no virtualenv, no build step.

## Usage

```sh
pycal
```

### Navigation

| Key | Action |
|-----|--------|
| `h` `←` / `l` `→` | Move one day |
| `k` `↑` / `j` `↓` | Move one week |
| `[` / `]` | Previous / next month |
| `t` | Jump to today |
| `n` / `p` | Jump to next / previous noted day |
| `g` | Go to a specific date |
| `q` / `Esc` | Quit |

### Notes

| Key | Action |
|-----|--------|
| `a` / `Enter` | Edit note for selected day |
| `d` | Delete note (press `v` to undo) |
| `c` | Copy note |
| `v` | Paste copied note |
| `/` | Search across all notes |
| `r` | Reload notes from disk |

#### Date input formats (`g`)

`DD` · `DD/MM` · `DD.MM` · `DD/MM/YYYY` · `DD-MM-YYYY` · `DD.MM.YYYY` · `YYYY-MM-DD` · `YYYY/MM/DD` · `YYYY.MM.DD`

#### Editor controls

| Key | Action |
|-----|--------|
| `Enter` | New line |
| `Esc` | Save and close |
| `Ctrl+G` | Discard changes |

Notes are capped at 500 characters. The editor scrolls both ways, so notes longer or wider than the panel stay editable. A `·` marker appears on any day that has a note, including days from adjacent months shown in the grid.

## Notes storage

One plain-text file per day, stored at:

```
$XDG_DATA_HOME/cal-notes/YYYY-MM-DD.txt
```

Falls back to `~/.local/share/cal-notes/` when `$XDG_DATA_HOME` is not set. Files are written atomically and are safe to back up, sync, or read directly.

Deleting a note removes its file. An empty note on save is treated as a deletion.

## Portability

pycal runs on any POSIX system with Python 3.7+ and ncursesw. Tested on Arch Linux and Alpine Linux (musl). Terminals without colour support render correctly in monochrome.

---

Simon D. · simon.d.dev@proton.me
