This challenge comes with a zip file. Extracting the zip results in 2 files: “syslog” and “auth.json”.

Site: https://github.com/snovvcrash/usbrip

```console
kali@kali:~/HTB/Challenges/Forensic/USB_Ripper$ sudo usbrip events violations auth.json -f syslog

         _     {{4}}    {v2.2.1-2}
 _ _ ___| |_ ___[E]___
| | |_ -| . |  _[N] . |
|___|___|___|_| [S]  _|
               x[i]_|   https://github.com/snovvcrash/usbrip


[*] Started at 2020-05-06 03:27:11
[03:27:13] [INFO] Reading "/mnt/hgfs/HTB/Challenges/Forensic/USB_Ripper/syslog"
100%|██████████████████████████████| 900000/900000 [00:15<00:00, 56886.33line/s]
[03:27:29] [INFO] Opening authorized device list: "/mnt/hgfs/HTB/Challenges/Forensic/USB_Ripper/auth.json"
[03:27:30] [INFO] Searching for violations
100%|██████████████████████████████| 100000/100000 [00:00<00:00, 654345.76dev/s]
[?] How would you like your violation list to be generated?

    1. Terminal stdout
    2. JSON-file

[>] Please enter the number of your choice (default 1): 2
[>] Please enter the output file name (default is "viol.json"):
[03:27:45] [INFO] Generating violations list (JSON)
[03:27:45] [INFO] New violations list: "/mnt/hgfs/HTB/Challenges/Forensic/USB_Ripper/viol.json"
[*] Shut down at 2020-05-06 03:27:45
[*] Time taken: 0:00:34.483411
kali@kali:~/HTB/Challenges/Forensic/USB_Ripper$
kali@kali:~/HTB/Challenges/Forensic/USB_Ripper$ cat viol.json
[
    {
        "conn": "????-08-03 07:18:01",
        "host": "kali",
        "vid": "3993",
        "pid": "9324",
        "prod": "1F8ADAEE73D993944FC7C7783",
        "manufact": "884CCC9A3DF08F49C621373E",
        "serial": "71DF5A33EFFDEA5B1882C9FBDC1240C6",
        "port": "1-1",
        "disconn": "????-08-03 07:18:10"
    }
]kali@kali:~/HTB/Challenges/Forensic/USB_Ripper$
```
71DF5A33EFFDEA5B1882C9FBDC1240C6

It looks like hashcode
https://crackstation.net/

mychemicalromance
