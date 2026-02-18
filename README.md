
## Initial Dependencies
### 1) Configure Custom Drive (Optional)
If you would like to install your UV to another drive, you can specify the path to the drive in the UV_PYTHON_INSTALL_DIR environment variable.
```sh
nano ~/.bashrc
```
Insert the following lines into your ~/.bashrc file and replace MY_DRIVE with the path to your drive:
```sh
export MY_DRIVE="YOUR_DRIVE_HERE"
export UV_PYTHON_INSTALL_DIR="$MY_DRIVE/uv/python"
export UV_CACHE_DIR="$MY_DRIVE/uv/cache"
export UV_TOOL_DIR="$MY_DRIVE/uv/tools"
export UV_LINK_MODE="copy"
```
Activate your source
```sh
source ~/.bashrc
```
### 2) Install UV
```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```
### 3) Install Python
```sh
uv python install 3.14
```

## Initializing the Project
If you already have uv and python installed, navigate to the project directory and initialize the project:
```sh
npm run install:deps
```

If you would like to just go ahead and run the project on the web 
```sh
npm run web
```
If you would like to run the project on the web and electron, run the following command 
```sh
npm run start
```

## Setup if you would like to make a similar project
To your new project copy over the main.cjs.example main.py.example and the package.json to your new project directory. Then run the following command:
```sh
npm run init:project
```
