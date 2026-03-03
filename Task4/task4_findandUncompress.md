# Task 4 - Find and Uncompress a File Named `research.*`

## Concept
In Linux files can be compressed in different formats like gzip, bzip2, zip etc.
We need to find a compressed file named `research` from anywhere in the system,
detect its compression type and uncompress it.

| Compression | Extension | Decompress Command |
|---|---|---|
| Gzip | `.gz` | `gunzip` |
| Bzip2 | `.bz2` | `bunzip2` |
| Zip | `.zip` | `unzip` |

---

## Steps Performed

### Step 1 - Create and Compress the File
```bash
echo "This is research data" > research.txt
gzip research.txt
```
> `gzip` compresses the file and automatically removes the original,
> creating `research.txt.gz`

### Step 2 - Move it to a Random Path (to simulate real scenario)
```bash
sudo mv research.txt.gz /var/log/research.txt.gz
```

### Step 3 - Find the File from Anywhere in the System
```bash
find / -name "research*" 2>/dev/null
```
> `2>/dev/null` hides permission error messages  
> Output:
```
/var/log/research.txt.gz
```

![find file screenshot](../images/findCommandzipfile.png)

### Step 4 - Check the Compression Type
```bash
file /var/log/research.txt.gz
```
> Output:
```
/var/log/research.txt.gz: gzip compressed data, was "research.txt"
```

![file type screenshot](../images/findCommandzipfile.png)

### Step 5 - Uncompress the File
```bash
gunzip /var/log/research.txt.gz
```

### Step 6 - Verify File is Uncompressed
```bash
find / -name "research*" 2>/dev/null
cat /var/log/research.txt
```
> Output:
```
/var/log/research.txt
This is research data
```

![verify screenshot](../images/unzipFileresearch.png)

---

## Result
- ✅ File was found at `/var/log/research.txt.gz`
- ✅ Compression type detected as **gzip**
- ✅ File successfully uncompressed to `research.txt`
- ✅ Content verified: `This is research data`
