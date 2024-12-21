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

### 2. Install

Simply copy "natural" to "/usr/local/bin" with the necessary permissions:

```bash
sudo cp natural /usr/local/bin
sudo chmod +x /usr/local/bin/natural
```

Now you can run "natural --help".

## Usage

```bash
# Provide your API key
natural --auth YOUR_GROQ_API_KEY

# Check info about natural
natural --info

# Convert a prompt into a command (confirmation required)
natural copy "test.txt" and paste it to "/tmp/test.txt"

# Convert a prompt into a command and auto-execute (dangerous!)
natural -y delete everything in /tmp
```

**Important**: If you have not set a valid API key, you will see an error message when trying to run normal prompts.

---

### "natural --help" Output

```bash
$ natural -h
usage: natural [-h] [--auth API_KEY] [--list-models] [--model MODEL_NAME] [--info] [-y] [prompt ...]

A natural language to terminal command interface using Groq.

positional arguments:
  prompt              Your natural language prompt. E.g. 'copy test.txt to /tmp'

options:
  -h, --help          show this help message and exit
  --auth API_KEY      Provide your Groq API key. It is saved securely.
  --list-models       List the available models.
  --model MODEL_NAME  Select the model to use from Groq.
  --info              Show info about this Natural installation.
  -y                  Auto-accept the generation and execute immediately.

```

## License

[MIT License](LICENSE).

---

### Disclaimer

**Use caution when auto-confirming or running any generated commands.** Large Language Models can produce unexpected results, and it is possible to execute destructive operations on your system if not careful.
