# hp-cups-fix
### Attemps to reconfigure CUPS to work with my HP LaserJet 3015 All-In-One (not P3015)

I have an old, but reliable, HP LaserJet 3015 All-in-One printer for which I still have toner.  But this particular printer did not have the ethernet port option on it.  So, just USB-B. But I want it to work as a network printer, thus I connected it to a old netbook on which I installed Ubuntu Server 24.04 with CUPS.

However that presented a new issue.  I recall with older Ubuntu and Zorin systems that I had directly connected...printing worked great.  But with newer Ubuntu versions, the symptoms I'm getting are it will only print the first page of what I put in the queue.  And it will print a second page that has the following on it:

```
ERROR:
typecheck
OFFENDING COMMAND:
idiv
STACK:
50000
--nostringval--
--nostringval--
-mark-
-mark-
-mark-
-mark-
```

After a huge amount of searching I finally stumbled upon this advice:

[https://www.bloovis.com/posts/2014-05-12-fixing-printing-problems-with-hp-laserjet-3015/](https://www.bloovis.com/posts/2014-05-12-fixing-printing-problems-with-hp-laserjet-3015/)

# Fix Issue 1: rendering error

They identify the root cause of the above error being: "This problem started when Ubuntu switched the PDF to PostScript renderer in the print system from Poppler to GhostScript"

Find the name of your printer:
```
lpstat -v
```

Change the printer's renderer:
```
lpadmin -p <PRINTER> -o pdftops-renderer-default=pdftops
```

This change is persistent.

# Fix Issue 2: printing is crazy slow

The driver that is "recommended", but does not work very well:<br>
<img width="306" height="18" alt="image" src="https://github.com/user-attachments/assets/708fd35a-196c-4f6f-87a1-8ba608bf64a0" />

The driver that seems to work quickly and correctly:<br>
HP LaserJet 3015 pcl3, hpcups 3.23.12 (grayscale, 2-sided printing)

Change your driver to this second one.

