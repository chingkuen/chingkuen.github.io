---
layout: post
title: Python Virtual Enviroment
subtitle: Python Virtual Enviroment
categories: python
tags: [python]
---

# Python Virtual Enviroment

## Install Virtual Enviroment

- 1st way

```python
pip3 install virtualenv
```

- 2nd way

```python
apt install python3.10-venv
```

## Create the Virtual Enviroment

- 1st way

```python
virtualenv --python py <myenv>
```

- 2nd way

```python
python -m venv <Virtual Enviroment Name>
```

It will create a folder with the designated name.
Then go into this directory.

```python
source bin/activate
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
