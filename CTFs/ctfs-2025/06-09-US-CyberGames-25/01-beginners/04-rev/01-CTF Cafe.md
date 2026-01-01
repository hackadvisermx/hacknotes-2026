
# CTF Cafe

Welcome to the CTF Cafe, where we serve only the finest menu items! We pride ourselves in our secret sauce, which is exclusive or something along those lines. At least, I think it is...

# Solucion

```
docker run --platform linux/amd64 -it --rm -v "$(pwd):/ctf" ubuntu:24.04 bash


```

```c

undefined8 main(void)

{
  int iVar1;
  int local_10;
  uint local_c;
  
LAB_004004ae:
  while( true ) {
    puts(&DAT_00401300);
    puts("1. View Menu");
    puts("2. Place Order");
    puts("3. View Total");
    puts("0. Exit");
    printf("Enter your choice: ");
    iVar1 = __isoc23_scanf(&DAT_00401371,&local_10);
    if (iVar1 == 1) break;
    clear_input();
    puts("Invalid input. Please enter a number.");
  }
  if (local_10 == 9) {
    puts("Oh, so you want the secret sauce recipe? Only if you have our proprietary key!");
    printf("Enter 8-byte hex key (e.g., 0x0123456789ABCDEF): ");
    iVar1 = __isoc23_scanf(&DAT_00401442,&key);
    if (iVar1 != 1) {
      puts("Invalid input.");
      return 1;
    }
    if (key == -0x642d38a5b63b1015) {
      puts("Congratulations! You have unlocked the secret sauce recipe!");
      printf("Secret Sauce: ");
      for (local_c = 0; local_c < 0x21; local_c = local_c + 1) {
        putchar((int)(char)(*(byte *)((long)&size + (long)((int)local_c % 8)) ^
                           secret_sauce[(int)local_c]));
      }
      putchar(10);
    }
    else {
      puts("Incorrect key! You can\'t have the secret sauce recipe.");
    }
  }
  else {
    if (9 < local_10) goto LAB_0040065f;
    if (local_10 == 3) {
      view_total();
      goto LAB_004004ae;
    }
    if (local_10 < 4) {
      if (local_10 == 2) {
        place_order();
        goto LAB_004004ae;
      }
      if (2 < local_10) goto LAB_0040065f;
      if (local_10 == 0) {
        puts("Thank you for dining with us!");
        return 0;
      }
      if (local_10 == 1) {
        print_menu();
        goto LAB_004004ae;
      }
    }
  }
LAB_0040065f:
  puts("Invalid choice. Try again.");
  goto LAB_004004ae;
}
```


```bash
root@e10a374a87d4:/ctf# ./ctf_cafe

===== 🍔 Welcome to the CTF Cafe! =====
1. View Menu
2. Place Order
3. View Total
4. Exit
Enter your choice: 9
Oh, so you want the secret sauce recipe? Only if you have our proprietary key!
Enter 8-byte hex key (e.g., 0x0123456789ABCDEF): -0x642d38a5b63b1015
Congratulations! You have unlocked the secret sauce recipe!
Secret Sauce: SVBGR{d3c0mp1l3rs_m4k3_l1f3_34sy}
Invalid choice. Try again.

===== 🍔 Welcome to the CTF Cafe! =====
1. View Menu
2. Place Order
3. View Total
4. Exit
Enter your choice: 0
Thank you for dining with us!
root@e10a374a87d4:/ctf#

```