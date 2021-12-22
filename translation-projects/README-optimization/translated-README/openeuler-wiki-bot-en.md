openeuler-wiki-bot
==============

## Usage

```bash
usage: openeuler-wiki-bot.py [-h] [-l] [-r] [-s SIG] [-a]

openEuler wiki bot.

optional arguments:
  -h, --help         show this help message and exit
  -l, --list         List all sig info.
  -r, --report       Generate information report.
  -s SIG, --sig SIG  Specify sig group.
  -a, --all          Report information for all sig.
```

#### Example1: Get the sig list

```bash
./openeuler-wiki-bot.py -l
```

#### Example2: Get all issues and prs of sig-ai-big data

```bash
./openeuler-wiki-bot.py -r -s sig-ai-bigdata
```
