<h1 align="center">Minishell</h1>

<p align="center">
  A small Unix shell in C focused on parsing, builtins, pipes, redirections and signal handling.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/School-42-black?style=for-the-badge" alt="42 badge" />
  <img src="https://img.shields.io/badge/Language-C-blue?style=for-the-badge" alt="Language badge" />
  <img src="https://img.shields.io/badge/Status-42_Project-brightgreen?style=for-the-badge" alt="Status badge" />
</p>

<p align="center">
  <strong>parsing, execve, pipes, redirections, heredoc, builtins, environment, signals</strong>
</p>

---

## 📌 Overview

Minishell is a project developed as part of the 42 curriculum.

This repository implements an interactive shell loop based on `readline`, a parsing layer that builds command and redirection structures, and an execution layer that dispatches builtins, external commands, pipes and redirections.

This project focuses on:
- interactive command reading and shell loop management
- quote-aware parsing and token organization
- process creation with `fork`, `execve` and `wait`
- file descriptor management for pipes, redirections and heredocs

---

## ✨ Features

- ✅ Interactive prompt with `readline` history support
- ✅ Builtins: `echo`, `cd`, `pwd`, `export`, `unset`, `env`, `exit`
- ✅ Pipe execution for chained commands
- ✅ Redirections: `<`, `>`, `>>` and `<<`
- ✅ Signal handling for interactive mode and heredoc interruption
- ⚠️ Current parser design only exposes command, pipe and redirection tokens, so control operators such as `&&`, `||` or subshells are not implemented in this repository

---

## 🧠 Concepts Covered

This project covers the following concepts:

- linked-list based token and redirection structures
- quote-aware string parsing
- environment duplication and mutation
- process lifecycle management
- file descriptor duplication with `dup` and `dup2`
- manual memory management and cleanup paths

---

## 🛠️ Build

Clone the repository and compile the project:

```bash
git clone git@github.com:Middle-555/minishell.git
cd minishell
make
```

Available Makefile rules:

```bash
make
make clean
make fclean
make re
```

Additional notes:
- The repository also provides a `make rapide` target for a quieter build.
- The build links against `readline` with `-lreadline`.

---

## 🚀 Usage

Run the program with:

```bash
./minishell
```

### Examples

```bash
./minishell
echo "hello from minishell"
ls -l | grep minishell > out.txt
cat << EOF
heredoc line
EOF
```

Usage notes:
- `main` expects no extra CLI arguments and exits immediately if `argc != 1`.
- `Ctrl-D` exits the shell and prints `exit`.
- Once the prompt is open, commands are entered interactively inside `minishell`.

---

## 📂 Project Structure

```text
.
├── Makefile
├── include/
│   ├── minishell.h
│   └── utils/
│       ├── ft_printf/
│       ├── gnl/
│       └── libft/
├── srcs/
│   ├── builtin/
│   ├── envp/
│   ├── exec/
│   ├── parsing/
│   └── main.c
├── LICENSE
├── template.md
└── README.md
```

### Structure Details

- `include/` : main project headers and shared declarations
- `srcs/` : application source files grouped by responsibility
- `srcs/builtin/` : builtin command implementations and builtin dispatching
- `srcs/parsing/` : tokenization, quote handling, expansion logic and redirection parsing
- `srcs/exec/` : command execution, pipes, redirections, heredocs and signal flow
- `include/utils/` : local utility libraries (`libft`, `ft_printf`, `get_next_line`)

---

## ⚙️ Project Constraints

This repository is clearly organized around the 42 Minishell project scope:
- written in C
- centered on an interactive shell executable named `minishell`
- structured around parsing, execution, environment handling and builtins
- relies on manual memory management
- uses GNU Readline for the prompt layer

---

## 🧪 Testing

Testing in this repository is mainly manual:
- interactive command execution checks
- builtin behavior checks
- pipeline and redirection scenarios
- heredoc and signal interruption scenarios
- environment mutation and exit status checks

### Manual test examples

```bash
./minishell
echo "test" | cat
cat << EOF
hello
EOF
```

### Memory checks

```bash
valgrind --leak-check=full --track-fds=yes ./minishell
```
---

## 📖 What I Learned

This kind of project helps improve in the following areas:
- separating parsing concerns from execution concerns
- reasoning about processes and file descriptors
- handling shell edge cases around quotes, pipes and redirections
- cleaning dynamic allocations reliably in error and exit paths

---

## 🚧 Possible Improvements

Although the project already covers the core minishell mechanics, several improvements are possible:
- replace Linux-specific headers with a more portable alternative
- add an automated regression test suite
- extend the parser to support more shell grammar features
- align edge-case behavior even more closely with Bash semantics

---

## 👤 Authors

- [Yoan Onieva](https://github.com/Yonieva)
- [Gauthier Esteve](https://github.com/gaesteve42)
- [Kévin Pourcel](https://github.com/Middle-555)
- [Adrien Cabarbaye](https://github.com/Demiaeuw)

## 📄 License

This project is distributed under the MIT license. See [LICENSE](LICENSE).
