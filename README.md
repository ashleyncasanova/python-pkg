## [Packaging a Python Projects](https://packaging.python.org/en/latest/tutorials/packaging-projects/#packaging-python-projects)

### 1. Create a Basic Project Structure

```
packaging_tutorial/
└── src/
    └── example_package_YOUR_USERNAME_HERE/
        ├── __init__.py
        └── example.py
```

>Note: Do no suffix folders with `YOUR_USERNAME_HERE`.

>Note: We labeled both the `packaging_tutorial/` and  `example_package_YOUR_USERNAME_HERE/` directories with as `<package-name>`.

<span style="color:hotpink">The tutorial says to leave the `__init__.py` file empty, but with our modifications we needed to fill it with the following line of code:</span>

```python
from .example_package_YOUR_USERNAME_HERE import example_package_YOUR_USERNAME_HERE
```


### 2. Create Package Files Excluding `LICENSE` Directory

```
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── src/
│   └── example_package_YOUR_USERNAME_HERE/
│       ├── __init__.py
│       └── example.py
└── tests/
```
>Note: `tests/` is a placeholder for test files, so we can leave it empty.

### 4. Configure `project.toml` File with Metadata

```
[project]
name = "example_package_YOUR_USERNAME_HERE"
version = "0.0.1"
authors = [
  { name="Example Author", email="author@example.com" },
]
description = "A small example package"
readme = "README.md"
requires-python = ">=3.7"
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]

[project.urls]
"Homepage" = "https://github.com/pypa/sampleproject"
"Bug Tracker" = "https://github.com/pypa/sampleproject/issues"
```

### 5. Update `project.toml` with Hatchling Configuration
```
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"
```

>Note: Add contents to end of file.


### 5. Create `README.md`

Update `README.md` file with the following:

```
    ## Installation

    ```bash
    pip install packaging_tutorial
    ```
    
    ## Usage

    ```python
    from packaging_tutorial import packaging_tutorial
    ```
```

### 6. Generate `dist` Archives

<span style="color:hotpink">Added a .gitignore file</span>
```
touch .gitignore
```



Install [build](https://packaging.python.org/en/latest/key_projects/#build:~:text=Delivery%20Network%20(CDN).-,build%C2%B6,-Docs%20%7C%20Issues)
```
python -m pip install --upgrade build
```


Generate distribution archive
```
python -m build
```

<span style="color:hotpink">At this point I initialized the repo???</span>
 ```
 git init
 ```

### 7. Upload Distribution Archives

```
python -m pip install --upgrade twine
python -m twine upload dist/*
```

>Note: Omit `--repository testpypi` option (this example uploads packages to the pypi test registry).

<span style="color:hotpink">made intitial commit</span>

```
git commit -m "initial commit"
```


## Test Install Package:

### 1. Create a `test-<package-name>` dir and cd into it
```
mk dir test-package-name
cd test-package-name
```
### 2. Create a virtual environment and activate

```
python -m venv venv
source venv/bin/activate
```
### 3. Install package

```
pip install <package-name>
```

### 4. Test package in `main.py` file

Open directory in vscode

```ssh
code .
```

Add a main.py file
```
touch main.py
```

update main.py to contain the following
```python
from example_package_YOUR_USERNAME_HERE import example_package_YOUR_USERNAME_HERE

example_package_YOUR_USERNAME_HERE()
```

In integrated terminal run our main.py file
```
python main.py
```

## Updating a Package
### 1. Make source code changes

In our example, we added the following line of code to our `__init__.py` file:

```python
from .example_package_YOUR_USERNAME_HERE import example_package_YOUR_USERNAME_HERE
```

### 2. Update the `pyproject.toml` version number

We updated it 0.0.1 to 0.0.2 because we only had a minor patch.

### 3. Delete `dist` dir

We manually deleted the files relative to the 0.0.1 version.

><span style="color:hotpink">Note: You can delete the entire file and it will reload once you rebuild your distribution archives in the following step.</span>
### 4. Re-run build command

```
python -m build
```

## Test Package Update
### 1. Navigate to `test-<package-name>/` directory
```
cd test-<package-name>
```
### 2. Install update
```
pip install --upgrade <package-name>
```

<span style="color:hotpink">You may need to be explicit when updating 0.X.X versions. For example:</span>

```
pip install --upgrade <package-name>==0.0.2
```

### 3. Run `main.py` file

```
python main.py
```