---
layout: post
title: Python Virtual Enviroment
subtitle: Python Virtual Enviroment
categories: python
tags: [python]
---

# Python Virtual Enviroment

## Install Virtual Enviroment

```python
pip3 install virtualenv
```

## Create the Virtual Enviroment

```python
python -m venv <Virtual Enviroment Name>
```

It will create a folder with the designated name.
Then go into this directory.

```python
source <Virtual Enviroment Name>/bin/activate
```

It will add (Virtual Enviroment Name) in the beginning of the prompt.

Example: (venv)

Check package list

```python
pip3 list
```

## Export the package list

```python
pip3 freeze > requirement.txt
```

- Check the content of requirement.txt

```python
type requirement.txt
```

- Install the same packages to other enviroment

```python
pip3 install -r requirement.txt
```

## Quit the Virtual Enviroment

```python
deactivate
```
