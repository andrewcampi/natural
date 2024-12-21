# Natural

**Natural** is a command-line utility that converts natural language instructions into actual Ubuntu terminal commands by querying [Groq](https://groq.com) large language models. It then optionally executes those commands.

## Features

- Converts plain English prompts into single shell commands.
- Interactive mode: shows you the command first, asks for confirmation.
- Automated mode ("-y"): Skips confirmation (risky – be careful!).
- Saves your Groq API key securely in "~/.natural/config.ini".
- Lets you list and select different Groq models.

## Prerequisites

- "curl" must be installed on your system.
- A valid **Groq API Key**.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/andrewcampi/natural.git
cd natural
```

### 2. Build and install

We provide an example of building a ".deb" package and installing via "apt-get".  
*(You need "dpkg-deb" and some packaging tools installed.)*

```bash
# Inside the natural repo:
# 1) Make sure the script is executable
chmod +x natural

# 2) Build a Debian package (example only: you'd need to structure your debian/ folder).
mkdir -p build/usr/bin
cp natural build/usr/bin/natural

# Minimal DEBIAN control file
mkdir -p build/DEBIAN
cat <<EOF > build/DEBIAN/control
Package: natural
Version: 1.0.0
Section: utils
Priority: optional
Architecture: all
Essential: no
Maintainer: Andrew Campi <andrewcampi@example.com>
Description: Natural is a command-line utility to convert natural language into Ubuntu terminal commands
EOF

dpkg-deb --build build natural_1.0.0_all.deb

# 3) Install using apt-get or dpkg
sudo apt-get install ./natural_1.0.0_all.deb
```

**Alternatively**, you could just copy "natural" to "/usr/local/bin":

```bash
sudo cp natural /usr/local/bin
sudo chmod +x /usr/local/bin/natural
```

Now you can run "natural --help".

## Usage

"""bash
# Provide your API key
natural --auth YOUR_GROQ_API_KEY

# Check info about natural
natural --info

# Convert a prompt into a command (confirmation required)
natural copy "test.txt" and paste it to "/tmp/test.txt"

# Convert a prompt into a command and auto-execute (dangerous!)
natural -y delete everything in /tmp
"""

**Important**: If you have not set a valid API key, you will see an error message when trying to run normal prompts.

---

### "natural --help" Output

```bash
Usage: natural [options] [prompt]

Examples:
  natural copy "test.txt" and paste it to "/tmp/test.txt"
  natural --auth <API_KEY>
  natural --list-models
  natural --model <model_name>
  natural --info
  natural -y copy home folder to /mnt/backup

Options:
  --auth <API_KEY>      Provide your Groq API key. It is saved securely.
  --list-models         List the available models.
  --model <MODEL_NAME>  Select the model to use from Groq.
  --info                Show info about this Natural installation.
  -y                    Auto-accept the generation and execute immediately (dangerous).
  -h, --help            Show this help message and exit.

Description:
  "natural" is a CLI that uses Groq's LLM to interpret your natural language prompt
  and produce a single shell command. It then optionally executes that command for you.
  If you do not specify "-y", you will be shown the generated command and asked for confirmation.
  By default, the model used is "llama-3.3-70b-versatile".
```

## License

[MIT License](LICENSE).

---

### Disclaimer

**Use caution when auto-confirming or running any generated commands.** Large Language Models can produce unexpected results, and it is possible to execute destructive operations on your system if not careful.
