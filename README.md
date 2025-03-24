# **Electronic Tax Document Invoicing**

The module provides the functionality to extends an electronic tax document with the following partners:

- Infile (Guatemala)

## **Author**

Jorge Alvarez <alvarez.jeap@gmail.com>

## **Requirements***

- [Odoo](https://github.com/odoo/odoo)
- Python 3+
- Pip3
- [direnv](https://direnv.net)
- [pyenv](https://github.com/pyenv/pyenv)

## **Setting Up the Environment**

- Install `virtualenv`

```sh
pip install virtualenv
```

- Download required **`odoo`** version

- Add extra `pip` dependencies

```sh
echo "watchdog\nautopep8\npylint\npyotp\npython-u2flib-server\nphonenumbers\nruamel.yaml\nGitPython\npyotp\nemail_validator\npython-u2flib-server\nresponses\npdbpp\n" >> requirements.txt
```

- Instal required python version

```sh
pyenv install 3.7.9
```

- Create required files

```sh
echo "3.7.9\n" > .python-version
echo "source .env/bin/activate\n\nunset PS1\n" > .envrc
echo "10\n" > .nvmrc
```

- Create virtual environment and install dependencies

```sh
virtualenv .env --python=$(cat .python-version)
source .env/bin/activate
direnv allow
pip install -r requirements.txt
```

- Improve `.gitignore`

```sh
echo ".DS_Store\n.env\nextra-addons\ncustom-addons\n" >> .gitignore
```

- Create `extra-addons` directory for external dependencies

```sh
mkdir extra-addons
touch extra-addons/__init__.py
```

- Create `custom-addons` directory for development

```sh
mkdir custom-addons
touch extra-addons/__init__.py
```

- Create `.vscode/launch.json` configuration file

```text
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
    "name": "Python: Current File",
    "type": "python",
    "request": "launch",
    "pythonPath": "${workspaceRoot}/.env/bin/python3",
    "program": "${workspaceRoot}/odoo-bin",
    "args": [
      "--dev", "all",
      "-c", "setup.cfg",
      "--db_host", "192.168.99.1",
      "--db_user", "odoo",
      "--db_password", "odoo",
      "--database", "odoo_v16",
      "--http-port", "1600",
      "--addons-path", "${workspaceRoot}/addons,${workspaceRoot}/extra-addons,${workspaceRoot}/custom-addons"
    ],
    "cwd": "${workspaceRoot}",
    "console": "integratedTerminal"
  }]
}
```

## **Runbook**

- Issues with `psycopg2`
  - For python 3.7+ replace with `psycopg2-binary`
