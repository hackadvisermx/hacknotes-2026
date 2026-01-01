# KDNU-3B

Category: Binary exploitation

## Description

NPLD analysts recovered a fragment of the KRAMPUS Syndicate’s KDNU-3B navigation firmware during a recent incident response sweep. The module appears to handle routing adjustments for mid-air course corrections, but most of its internal logic is inactive or stripped from the build. During static review, investigators identified a code path that is never reached during normal execution and does not align with any documented subsystem.

The firmware is designed to reject unexpected inputs immediately, a behavior that is consistent with hardened flight control software. To understand what the Syndicate was hiding, you will need to analyze how the controller processes incoming commands and determine how to reach the dormant functionality without triggering its shutdown behavior.

Your objective is to examine the recovered binary, map out the dispatcher flow, and extract whatever information the hidden subsystem contains.

Connect at `nc ctf.csd.lol 1001`

This challenge's remote instance utilizes a proof-of-work verification system to prevent brute forcing and from other bad actors.

After connecting to the remote instance using `nc`, you must complete a proof-of-work challenge by running the command given and entering the output as the solution.

If you are on Windows, please download the [solver](https://github.com/redpwn/pow/releases/latest) manually (named `redpwnpow-windows-amd64.exe`) and run it yourself, like this in PowerShell:

```
 'challenge' is given after connecting to nc
 (the part after '-s')
.\redpwnpow-windows-amd64.exe <challenge>
```
In any case, please review the [auto-download script](https://pwn.red/pow) and [solver](https://github.com/redpwn/pow) yourself before running untrusted code on your computer. For more protection, we recommend completing the challenge in a sandboxed environment, such as a virtual machine.

If you have any questions or concerns about this technology, please open a ticket in our [Discord server](https://discord.com/invite/cyberstudents-916144903686336513).

## Hints

### 1
The program lets you jump to any function in memory if you can find its address. One of those functions prints the hidden file.

### 2
That function looks like it needs an argument, but think carefully… do you REALLY need to pass one for this challenge to work?

## Solve





