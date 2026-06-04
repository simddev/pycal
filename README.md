# pycal

A minimal terminal calendar with per-day notes, built with Python's `curses`.

```
        ◄  June 2026  ►
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ Mon │ Tue │ Wed │ Thu │ Fri │ Sat │ Sun │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  1  │  2  │  3  │  4 ·│  5  │  6  │  7  │
│     │     │     │ mtg │     │     │     │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┤
...
─────────────────────────────────────────────
  Thu 04 Jun 2026   a:edit  d:del  [:prev-mo ...
  team meeting at 10
```

## install

```sh
git clone https://github.com/simddev/pycal
chmod +x pycal/pycal
sudo ln -s "$PWD/pycal/pycal" /usr/local/bin/pycal   # optional
```

No dependencies beyond Python 3.6+ stdlib.

## usage

```
pycal
```

| key | action |
|-----|--------|
| `h` `l` `←` `→` | move one day |
| `k` `j` `↑` `↓` | move one week |
| `[` `]` | previous / next month |
| `t` | jump to today |
| `a` / `Enter` | edit note for selected day |
| `d` | delete note |
| `n` / `p` | jump to next / previous noted day |
| `/` | search note content |
| `g` | go to date |
| `r` | refresh notes from disk |
| `q` / `Esc` | quit |

The inline editor uses `Enter` for new lines and `Esc` to save.

## notes storage

Notes are plain text files, one per day:

```
$XDG_DATA_HOME/cal-notes/YYYY-MM-DD.txt
# falls back to ~/.local/share/cal-notes/
```

Max 500 characters per note. Deleting a note removes the file.
