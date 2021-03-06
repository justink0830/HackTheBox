The .zip file comes with one file: password.

```console
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ cat password
[...]

▒U▒͈3▒▒6▒3▒U▒▒▒▒▒▒7▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒(c▒▒▒7▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒[~▒▒▒▒▒▒▒▒▒▒▒▒ы▒▒▒▒▒▒$▒▒▒j▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒
[...]
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ file password
password: data
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$
```

```console
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ xxd password
00000000: afb4 fcfb ebff f7ff f7ff 2863 aab1 ffff  ..........(c....
00000010: ffff ffff ffff ffff ffff f3ff efff 8f9e  ................
00000020: 8c8c 8890 8d9b d18b 878b aaa7 f3ff 24bb  ..............$.
00000030: 90a3 6abb 90a3 0afe ebff 0cf7 8e55 c9cd  ..j..........U..
00000040: 8833 8d8c 36d1 33cb d308 551a fdff afb4  .3..6.3...U.....
00000050: f8f7 b237 01c1 ebff ffff edff ffff afb4  ...7............
00000060: fefd eafc ebff f7ff f7ff 2863 aab1 b237  ..........(c...7
00000070: 01c1 ebff ffff edff ffff f3ff f3ff ffff  ................
00000080: ffff ffff ffbf 5b7e ffff ffff 8f9e 8c8c  ......[~........
00000090: 8890 8d9b d18b 878b aaa7 f7ff 24bb 90a3  ............$...
000000a0: 6abb 90a3 afb4 faf9 ffff ffff feff feff  j...............
000000b0: b9ff ffff a1ff ffff ffff                 ..........
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$
```

We see that the file contains several octets with f, so it looks the previously there were 0x00 bytes and were xored with 0xff, and as a result we got the result as the image above.
We would need to XOR the file with 0xff. 

Code site: https://github.com/dirtbags/fluffy/blob/master/xor.c

```c
/*
 * xor filter -- 2017 Neale Pickett <zephyr@dirtbags.net>
 *
 * This file is in the public domain.  I make no promises about the functionality
 * of this program. 
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int
main(int argc, char *argv[])
{
	int start = 1;
	int base = 0;
	int arg;

	if (argv[start] && (0 == strcmp(argv[start], "-x"))) {
		base = 16;
		start += 1;
	}

	if (start + 1 > argc) {
		fprintf(stderr, "Usage: %s [-x] m1 [m2 ...]\n", argv[0]);
		return 1;
	}

	arg = start;

	while (1) {
		int c = getchar();
		unsigned char mask;

		if (!argv[arg]) {
			arg = start;
		}
		mask = strtol(argv[arg++], NULL, base);

		if (EOF == c) {
			break;
		}

		c ^= mask;
		putchar(c);
	}

	return 0;
}
```

```console
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ cat password | ./xor 0xff > bin
[...]
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ unzip bin
Archive:  bin
  inflating: password.txt
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ ls
bin  MemoryLeaks-TooktheByte.pdf  password  password.txt  Took_the_Byte.zip  xor  xor.c
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$ cat password.txt
HTB{27AjFDkqi1wJ}
kali@kali:~/HTB/Challenges/Forensic/Took_the_byte$
```
HTB{27AjFDkqi1wJ}
