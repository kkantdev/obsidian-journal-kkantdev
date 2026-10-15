---
{"dg-publish":true,"permalink":"/documents/command/grafiphy/install-guide-for-mac/","dg-note-properties":{}}
---

 first dependency for the Mac, you have to install the Python for the graphite use
 
[python](https://www.python.org/downloads/macos/)

```
python3 --version

pip3 --version

```
note* when you install the Python in the Mac, you will be pre-installed the pipe three also, so you don't have to install, just install them, Python and check if both are install or not 

```
pip3 install graphifyy

```

----------------- 

### Step 1: Try running it through Python

Run:

```
python3 -m graphify --help
```

If that works, Graphify is installed correctly.

---

### Step 2: Find where the executable was installed

Run:

```
python3 -m site --user-base
```

It will probably print something like:

```
/Users/madankryadav/Library/Python/3.13
```

The executable is usually in:

```
/Users/madankryadav/Library/Python/3.13/bin
```

Check by running:

```
ls ~/Library/Python/3.13/bin
```

Do you see `graphify` listed there?

---

### Step 3: Add it to your PATH

If `graphify` is in that directory, add it to your PATH:

```
echo 'export PATH="$HOME/Library/Python/3.13/bin:$PATH"' >> ~/.zshrcsource ~/.zshrc
```

Now try:

```
graphify --help
```

---

## If `graphify` is NOT in that folder

Run these two commands and paste the output:

```
python3 -m graphify --help
```

and

```
ls ~/Library/Python/3.13/bin
```

I'll tell you exactly what to do next. We're very close.