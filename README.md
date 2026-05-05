# BG3 Mod Junction Setup

Setup scripts that bridge a Baldur's Gate 3 mod Git repository with the BG3
Toolkit's Data directory using Windows junction points. Lets a team work in
the toolkit and use Git normally on the same files.

## What This Is

The BG3 Toolkit reads and writes mod files inside the game's Data directory,
but Git tracks files inside whatever folder you cloned into. These two
locations are different, and the toolkit has no setting to redirect where it
looks for files.

These scripts solve that by creating Windows junctions (a kind of symbolic
link) between your Git repository and the BG3 Data directory. The toolkit
keeps reading and writing to its normal location; the Git repo sees those
same files through the junction. No manual file copying, no duplicate state.

## What's In This Repo

- `SETUP.bat` — Launcher that auto-elevates to Administrator and runs the
  PowerShell script. This is the file teammates double-click.
- `setup-junctions.ps1` — The PowerShell script that does the actual work:
  copies the four mod folders into the BG3 Data path, deletes the originals
  from the repo, and creates junctions in their place.

## Who This Is For

Teams using SourceControlGenerator (or a similar workflow) to version-control
a BG3 mod project. If you're working solo and never plan to share the repo,
you don't need these scripts.

## How To Use

These scripts are part of a larger setup process. The full walkthrough lives
in the **Project Setup Guide** for the originating course. The short version:

1. Use SourceControlGenerator to create a Git repo from your BG3 mod project.
2. Drop `SETUP.bat` and `setup-junctions.ps1` into the repo root.
3. Add the `Public/` folder manually (SCG doesn't include it).
4. Commit and push.
5. Each teammate runs `SETUP.bat` once after cloning.

See the Project Setup Guide for full context, including troubleshooting and
lessons learned.

## Requirements

- Windows (the scripts use NTFS junctions and `mklink /J`).
- Administrator privileges (required to create junctions).
- Baldur's Gate 3 with the unlocked BG3 Toolkit installed.
- A mod project already created in the toolkit.

## Origin

Originally written for IGME-424: Game Modification at Rochester Institute of
Technology, by Carter Manion (team MF Tadpoles, Spring 2026), as part of the
"A Song For The Ages" mod project.

## License

MIT. See `LICENSE` for details.

## Acknowledgments

Conceptually built on top of LaughingLeader's
[SourceControlGenerator](https://github.com/LaughingLeader/SourceControlGenerator),
which handles the initial repo creation step that these scripts complement.
