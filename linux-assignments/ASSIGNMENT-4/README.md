# Assignment 4 - otssh

## Overview

`otssh` is a Bash-based SSH connection management utility.

It provides a simple command-line interface to add, list, update, delete, and connect to saved SSH connections.

Connection details are stored in:

```text
~/.otssh.db
```

Each connection is stored using the following format:

```text
name|host|user|port|key
```

## Features

- Add an SSH connection
- List saved SSH connections
- Display detailed SSH connection commands
- Update an existing SSH connection
- Delete an SSH connection
- Connect to a saved SSH connection
- Support custom SSH ports
- Support SSH private keys with `-i`
- Validate required options and missing servers

## Requirements

- Linux / WSL
- Bash
- OpenSSH client

Verify SSH is available:

```bash
ssh -V
```

## Installation

Make the script executable:

```bash
chmod +x otssh
```

To use it directly from the current directory:

```bash
./otssh
```

After completing and testing the script, it can be installed as a system command:

```bash
sudo cp ./otssh /usr/local/bin/otssh
```

Then verify:

```bash
which otssh
```

## Usage

### 1. Add an SSH connection

Add a connection using the default SSH port 22:

```bash
./otssh -a -n server1 -h 192.168.21.30 -u kirti
```

Add a connection using a custom port:

```bash
./otssh -a -n server2 -h 192.168.42.34 -u kirti -p 2022
```

Add a connection using a private SSH key:

```bash
./otssh -a -n server3 -h 192.168.46.34 -u ubuntu -p 2022 -i ~/.ssh/id_rsa
```

### 2. List connections

```bash
./otssh ls
```

Example:

```text
server1
server2
server3
```

### 3. Display detailed connections

```bash
./otssh ls -d
```

Example:

```text
server1: ssh kirti@192.168.21.30
server2: ssh -p 2022 kirti@192.168.42.34
server3: ssh -i /home/syed/.ssh/id_rsa -p 2022 ubuntu@192.168.46.34
```

### 4. Update a connection

The update operation uses `-U`:

```bash
./otssh -U -n server1 -h 192.168.21.31 -u kirti -p 22
```

Verify the updated connection:

```bash
./otssh ls -d
```

### 5. Delete a connection

```bash
./otssh rm server3
```

Verify:

```bash
./otssh ls
```

### 6. Connect to a saved server

Use the saved connection name:

```bash
./otssh server1
```

The utility reads the saved details and constructs the appropriate SSH command.

For example:

```text
ssh kirti@192.168.21.30
```

For a custom port:

```text
ssh -p 2022 kirti@192.168.42.34
```

For a private key:

```text
ssh -i /home/syed/.ssh/id_rsa -p 2022 ubuntu@192.168.46.34
```

## Database

The utility stores connection information in:

```text
~/.otssh.db
```

Example database entries:

```text
server1|192.168.21.30|kirti|22|
server2|192.168.42.34|kirti|2022|
server3|192.168.46.34|ubuntu|2022|/home/syed/.ssh/id_rsa
```

The database is automatically created when the script runs.

## Command Reference

| Command | Description |
|---|---|
| `./otssh -a -n NAME -h HOST -u USER` | Add connection |
| `./otssh -a -n NAME -h HOST -u USER -p PORT` | Add with custom port |
| `./otssh -a -n NAME -h HOST -u USER -p PORT -i KEY` | Add with custom port and key |
| `./otssh ls` | List connections |
| `./otssh ls -d` | Display detailed SSH commands |
| `./otssh -U -n NAME -h HOST -u USER` | Update connection |
| `./otssh rm NAME` | Delete connection |
| `./otssh NAME` | Connect to saved server |

## Error Handling

The utility checks for invalid or incomplete operations.

Examples include:

```text
[ERROR]: Server information is not available, please add server first
```

and:

```text
[ERROR]: Server 'server-name' not found.
```

It also validates required options such as:

- `-n` for connection name
- `-h` for host
- `-u` for username

## Testing Performed

The following functionality was tested:

- Add server with default port
- Add server with custom port
- Add server with SSH private key
- List connections
- Display detailed SSH commands
- Update connection
- Delete connection
- Connect to a saved connection
- Error handling for unavailable connections

## Files

```text
otssh
README.md
```

## Learning Outcomes

Through this assignment, the following Linux and Bash concepts were practiced:

- Bash scripting
- Command-line argument parsing
- `getopts`
- Conditional statements
- File handling
- Text processing with `grep` and `cut`
- Temporary files with `mktemp`
- SSH command construction
- SSH ports and identity files
- Persistent data storage using a flat file
- Linux file permissions
