# HACKMINDS LINUX CHALLENGE 003
## OPERATION: SHADOW VAULT


## Mission
Investigate a simulated Linux evidence package. Your main objectives are to retrieve a synthetic password hash, use John the Ripper to recover its password, and discover a hidden archive containing the final flag.

## Rules and safety
- Work only inside the supplied challenge folder and your own `participant_workspace`.
- All account records are synthetic training files, not live Linux system files.
- Never modify `/etc/passwd`, `/etc/shadow` or `/etc/sudoers`.
- Do not use `sudo` or attempt privilege escalation on your Kali machine.
- Do not upload challenge hashes or files to online services.
- You may ask your AI examiner for explanations and progressive hints. You must run the commands yourself and submit evidence.

## Stage 1 – Linux basics and workspace 
1. Open a terminal and enter the `HACKMINDS_CTF_003` directory.
2. Use `pwd` to show your current location.
3. Use `ls -la` to list ordinary and hidden entries.
4. Read `START_HERE.txt` and `case_files/system_profile.txt`.
5. Create `participant_workspace` with `passwords` and `recovered` subfolders.
6. Inspect `case_files/passwd.snapshot` and identify the simulated account names and UIDs.

Useful commands to learn: `pwd`, `ls -la`, `cat`, `mkdir -p`.

## Stage 2 – Password hash investigation and retrieval 
1. Read `case_files/shadow.snapshot`.
2. Identify the target account and its hash type.
3. Explain in your own words what a password hash is and why the supplied file is a simulation rather than a real `/etc/shadow` file.
4. Extract only the target hash value and save it to `participant_workspace/passwords/recovered_hash.txt`.
5. Check that the saved file contains the hash and no username, label or extra text.

Useful commands to learn: `cat`, `grep`, `cp`, `nano` or another text editor.

## Stage 3 – Password recovery with John the Ripper
1. Check whether John the Ripper is installed: `john --version`.
2. Locate and inspect `wordlists/challenge_words.txt`.
3. Explain what a wordlist does and what raw SHA-512 means. Do not confuse raw SHA-512 with Linux SHA-512 Crypt (`$6$`).
4. Run John using the supplied wordlist and your extracted hash file:

```bash
john --format=raw-sha512 --wordlist=wordlists/challenge_words.txt participant_workspace/passwords/recovered_hash.txt
```

5. Display the result:

```bash
john --show --format=raw-sha512 participant_workspace/passwords/recovered_hash.txt
```

6. Record the recovered password in your report. Submit terminal evidence showing the commands and result.

If John is unavailable, stop and tell your examiner/organiser. Do not install packages or use the internet during the timed challenge unless the organiser explicitly permits it. Do not claim success without running the tool.

## Stage 4 – Hidden archive discovery and flag recovery 
1. Search the challenge folder recursively, including hidden directories, for the archive.
2. Identify the suspected archive using `file`.
3. List its contents before extracting it using `tar -tzvf`.
4. Extract it into `participant_workspace/recovered` using `tar -xzvf <archive-path> -C participant_workspace/recovered`.
5. Locate the flag in the recovered files and record it in your report.

Useful commands to learn: `find`, `ls -la`, `file`, `tar`, `grep`.


