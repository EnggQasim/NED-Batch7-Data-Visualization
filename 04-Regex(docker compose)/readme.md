To set up a Jupyter Notebook environment using Docker Compose with a Dockerfile, you can follow the steps below:

### 1. **Create a Directory for Your Project**
   First, create a directory for your project.

   ```bash
   mkdir jupyter-notebook-setup
   cd jupyter-notebook-setup
   ```

### 2. **Create a `Dockerfile`**
   Create a `Dockerfile` inside the project directory. This file will define the environment.

   ```Dockerfile
   # Dockerfile

   # Use the official Jupyter Notebook base image
   FROM jupyter/base-notebook:latest

   # Set environment variables for Jupyter
   ENV JUPYTER_ENABLE_LAB=yes

   # Expose the default Jupyter port
   EXPOSE 8888

   # Optionally, install additional Python packages
   RUN pip install --no-cache-dir \
       numpy \
       pandas \
       matplotlib \
       scikit-learn

   # Set the command to start Jupyter Notebook
   CMD ["start-notebook.sh"]
   ```

   This `Dockerfile` starts from a base image that includes Jupyter Notebook and allows you to install additional Python packages.

### 3. **Create a `docker-compose.yml` File**
   Create a `docker-compose.yml` file in the same directory to define the services and how they interact.

   ```yaml
   version: '3.8'

   services:
     jupyter:
       build: .
       ports:
         - "8888:8888"
       volumes:
         - ./notebooks:/home/jovyan/work
       environment:
         - JUPYTER_TOKEN=mysecuretoken
   ```

   - **build**: Specifies that Docker Compose should build the image using the Dockerfile in the current directory (`.`).
   - **ports**: Maps port 8888 on your local machine to port 8888 in the container.
   - **volumes**: Mounts the `notebooks` directory from your host to the Jupyter working directory inside the container. This ensures that your notebooks are stored on your local machine.
   - **environment**: Sets an environment variable to secure Jupyter Notebook with a token. You can replace `mysecuretoken` with a more secure token or password.

### 4. **Create a Directory for Notebooks**
   Create a directory where your Jupyter notebooks will be stored.

   ```bash
   mkdir notebooks
   ```

### 5. **Build and Run the Docker Container**
   Now, build the Docker image and start the container with Docker Compose.

   ```bash
   docker-compose up --build
   ```

   This command will build the Docker image and start the Jupyter Notebook server.

### 6. **Access Jupyter Notebook**
   Once the container is running, open your web browser and navigate to:

   ```
   http://localhost:8888/?token=mysecuretoken
   ```

   Replace `mysecuretoken` with the token you set in the `docker-compose.yml` file.

### 7. **Stop the Container**
   When you're done, you can stop the Jupyter Notebook container with:

   ```bash
   docker-compose down
   ```

This setup provides a reusable, isolated Jupyter Notebook environment that can be easily shared and deployed.


--------------
Here's a `README.md` template for teaching regular expressions (regex) in Python, based on the regex concepts from the Dataquest blog. This template includes explanations and examples for students.

---

# Regular Expressions in Python - Cheat Sheet and Examples

## Introduction

Regular Expressions (regex) are sequences of characters that define a search pattern. They are incredibly powerful tools used for string matching, manipulation, and extraction. In Python, the `re` module provides full support for Perl-like regular expressions.

This guide will walk you through the basic and advanced concepts of regex with Python code examples to help you understand and apply regex in your projects.

## Table of Contents

1. [Basic Regex Syntax](#basic-regex-syntax)
2. [Character Classes](#character-classes)
3. [Anchors](#anchors)
4. [Quantifiers](#quantifiers)
5. [Groups and Capturing](#groups-and-capturing)
6. [Lookahead and Lookbehind](#lookahead-and-lookbehind)
7. [Common Regex Patterns](#common-regex-patterns)
8. [Examples](#examples)

## Basic Regex Syntax

### Literal Characters

Literal characters match exactly what they are. For example, the pattern `abc` will match the string "abc" exactly.

```python
import re

pattern = r"abc"
text = "abcde"
match = re.search(pattern, text)
print(match.group())  # Output: abc
```

### Metacharacters

Metacharacters are characters that have a special meaning in regex. Here are a few:

- `.`: Matches any single character except newline
- `^`: Matches the start of the string
- `$`: Matches the end of the string
- `\`: Escapes a metacharacter

Example:

```python
pattern = r"c.d"
text = "code"
match = re.search(pattern, text)
print(match.group())  # Output: cod
```

## Character Classes

Character classes allow you to match one of several characters. They are defined using square brackets `[]`.

- `[abc]`: Matches any one of `a`, `b`, or `c`
- `[a-z]`: Matches any lowercase letter
- `[^abc]`: Matches any character except `a`, `b`, or `c`

Example:

```python
pattern = r"[a-z]"
text = "Code123"
match = re.findall(pattern, text)
print(match)  # Output: ['o', 'd', 'e']
```

## Anchors

Anchors are used to specify the position of a match.

- `^`: Matches the start of the string
- `$`: Matches the end of the string

Example:

```python
pattern = r"^Hello"
text = "Hello World"
match = re.search(pattern, text)
print(match.group())  # Output: Hello
```

## Quantifiers

Quantifiers define how many times a character or group should be matched.

- `*`: 0 or more times
- `+`: 1 or more times
- `?`: 0 or 1 time
- `{n}`: Exactly `n` times
- `{n,}`: At least `n` times
- `{n,m}`: Between `n` and `m` times

Example:

```python
pattern = r"\d{2,4}"
text = "2023"
match = re.search(pattern, text)
print(match.group())  # Output: 2023
```

## Groups and Capturing

Groups are used to group part of a regex together. They can be referenced later in the regex or in the replacement string.

- `()`: Defines a group
- `(?:...)`: Non-capturing group
- `\1`, `\2`, etc.: Backreferences to groups

Example:

```python
pattern = r"(hello) (world)"
text = "hello world"
match = re.search(pattern, text)
print(match.group(1))  # Output: hello
print(match.group(2))  # Output: world
```

## Lookahead and Lookbehind

Lookahead and lookbehind assertions allow you to match a pattern only if it is followed or preceded by another pattern.

- `(?=...)`: Positive lookahead
- `(?!...)`: Negative lookahead
- `(?<=...)`: Positive lookbehind
- `(?<!...)`: Negative lookbehind

Example:

```python
pattern = r"hello(?= world)"
text = "hello world"
match = re.search(pattern, text)
print(match.group())  # Output: hello
```

## Common Regex Patterns

Here are some common regex patterns:

- `\d`: Matches any digit (equivalent to `[0-9]`)
- `\D`: Matches any non-digit
- `\w`: Matches any word character (alphanumeric + `_`)
- `\W`: Matches any non-word character
- `\s`: Matches any whitespace character
- `\S`: Matches any non-whitespace character

Example:

```python
pattern = r"\w+"
text = "Hello, World!"
match = re.findall(pattern, text)
print(match)  # Output: ['Hello', 'World']
```

## Examples

### Example 1: Validating an Email Address

```python
pattern = r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$"
text = "example@example.com"
match = re.match(pattern, text)
if match:
    print("Valid email")
else:
    print("Invalid email")
```

### Example 2: Extracting Dates

```python
pattern = r"\d{2}/\d{2}/\d{4}"
text = "Today's date is 09/08/2024."
match = re.search(pattern, text)
print(match.group())  # Output: 09/08/2024
```

### Example 3: Finding All Words in a String

```python
pattern = r"\b\w+\b"
text = "This is a test string."
matches = re.findall(pattern, text)
print(matches)  # Output: ['This', 'is', 'a', 'test', 'string']
```

## Conclusion

This guide provides a foundational understanding of regular expressions in Python. Practice these patterns and examples to become proficient in regex, and soon you'll be able to write complex expressions with ease.

Happy coding!

Match found:", match.group())  # Output: Match found: folder\file

# Example 3: Escaping parentheses
text = "(123) 456-7890"
match = re.search(r'\(\d{3}\) \d{3}-\d{4}', text)
if match:
    print("Match found:", match.group())  # Output: Match found: (123) 456-7890
```

## 10. Common Patterns

Some regex patterns are frequently used for validating input or parsing text.

```python
# Example 1: Email validation
text = "user@example.com"
pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
match = re.match(pattern, text)
if match:
    print("Valid email")  # Output: Valid email

# Example 2: URL validation
text = "https://www.example.com"
pattern = r'^(https?|ftp)://[^\s/$.?#].[^\s]*$'
match = re.match(pattern, text)
if match:
    print("Valid URL")  # Output: Valid URL

# Example 3: Phone number validation (US)
text = "(123) 456-7890"
pattern = r'^\(\d{3}\) \d{3}-\d{4}$'
match = re.match(pattern, text)
if match:
    print("Valid phone number")  # Output: Valid phone number
```

## Conclusion

This comprehensive guide covers the essential topics of the Python `re` module, providing three examples for each concept. Practice these examples and experiment with creating your own regular expressions to master regex in Python.

Happy coding!


