

Examine the source and determine how to get the flag to print with the remote service.

Download the source [here](https://rsac-picoctf-files.picoctf.net/c_rsac_challenges/e63388685d6eefbe71215aac9c79ad038aeb9337c8bb2b6233b22394ba26f0eb/frajilay.c)

## Solve

```
nc rsac-challenges.picoctf.net 65232

Enter your age: HOLA
[DEBUG] Error parsing input: 'HOLA
'
[DEBUG] Stack Trace: main -> get_input -> parse_input
[DEBUG] FLAG: picoCTF{7urn_d38u991n9_0ff_ccab7f02}
```



```bash
#!/usr/bin/vibethon

ANSI_RESET = "\x1b[0m"
ANSI_GREEN = "\x1b[1;32m"
ANSI_BLUE = "\x1b[1;34m"

HOSTNAME = "vibe-vm"
USERNAME = input(HOSTNAME + " login: ").strip()


def prompt(path):
    return input(ANSI_GREEN + USERNAME + "@" + HOSTNAME + ANSI_RESET + ":" + ANSI_BLUE + path + ANSI_RESET + "$ ")


def canonicalize(path):
    parts = []
    for split in path.split("/"):
        if split == "" or split == ".":
            pass
        elif split == "..":
            if len(parts) > 0:
                parts.pop()
        else:
            parts.append(split)
    return "/" + "/".join(parts)


def concat_path(cwd, path):
    if path.startswith("/"):
        ncwd = path
    else:
        ncwd = cwd + "/" + path
    return canonicalize(ncwd)


def listdir_str(cwd, path, append_path):
    try:
        res = "  ".join(listdir(concat_path(cwd, path)))
        if append_path:
            res = path + ":\n" + res
    except:
        res = "ls: cannot access '" + path + "': No such file or directory"
    return res


def is_secret(path):
    return path.endswith(".secret")


cwd = "/"
while True:
    cmd = prompt(cwd).strip().split()
    if len(cmd) > 0:
        if cmd[0] == "ls":
            if len(cmd) == 1:
                print(listdir_str(cwd, "", False))
            elif len(cmd) == 2:
                print(listdir_str(cwd, cmd[1], False))
            else:
                s = []
                for i in range(1, len(cmd)):
                    s.append(listdir_str(cwd, cmd[i], True))
                print("\n".join(s))

        elif cmd[0] == "cd":
            if len(cmd) == 1:
                ncwd = "/"
            else:
                ncwd = concat_path(cwd, cmd[1])
            try:
                listdir(ncwd)
                cwd = ncwd
            except:
                print("vash: cd: " + cmd[1] + ": No such file or directory / Permission denied")

        elif cmd[0] == "cat":
            if len(cmd) == 1:
                while True:
                    print(input())
            else:
                for i in range(1, len(cmd)):
                    path = concat_path(cwd, cmd[i])
                    if is_secret(path):
                        print("cat: " + cmd[i] + ": Permission denied (.secret)")
                    else:
                        try:
                            content = readfile(path)
                            write(content)
                        except:
                            print("cat: " + cmd[i] + ": No such file or directory / Permission denied")
        elif cmd[0] == "exit":
            break
        else:
            print(cmd[0] + ": command not found")
```