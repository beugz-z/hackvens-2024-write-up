
# Write Up : Hackvens 2024 <br>  <br>

*Author : $beugz<br>*
*Challenge Type : Forensic <br>*
*Challenge Name : Analyse Me <br> <br>*

We've one .pcapng file whose md5 checksum is : *65cc809ee91597a1ff9a19db520fde5f* 

When opened with tshark we can see there are only USB captures with some URB_INTERRUPT in 

`tshark -r challenge.pcapng`

After searching on the web for is URB_INTERRUPT we can conclude that the capture is representing a keyboard input 

I choose to export the hexadecimal data and to make things easier, i output it in an output file : 

`tshark -r challenge.pcapng -T fields -e usb.capdata > hex_data`

Then i've got to translate the haxedecimal data into ASCII format with a python script
The script returned me this : 

```
Texte déchiffré :
cssh h4ck3r0rree'ottee6[Backspace]6servveer6ssh.hhqqckvveenens.ffrr 6p 2222
yes
p00sszz0r[Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace]ch4'p12[Backspace]0n
cqt /flq
```

The text is obsfucate like a qwerty keyboard and whe can see some Backspace. Some command may be thinking to a ssh connexion.
After deobfuscating the output, i got this for the ssh command : 

```
ssh h4ck3r0@remote-server-ssh.hackvens.fr -p 2222
yes
p00sszz0r[Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace][Backspace]ch4'p12[Backspace]0n
cqt /flq
```

For the password, we can see several [Backspace] so after removing the [Backspace], that is remaining : 

`ch4'p10n` 

After some  try, i found the password which is : cH4mp10n

And finally we got the flag by using the command : cat flag
