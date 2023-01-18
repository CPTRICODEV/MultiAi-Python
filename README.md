# MultiAi - Python

MultiAi is a Python system that provides code generation, text completion, and README generation services. It uses the OpenAI API to generate code, text, and READMEs from user input. It also provides a graphical user interface for users to interact with the system.

## Getting Started

To use MultiAi - Python, you will need to install the required packages and set your - [OpenAi](https://beta.openai.com/account/api-keys) API key up, in the *MultiAi.py* file

### Prerequisites

The following packages are required to run MultiAi:

- PySimpleGUI
- OpenAI
- Keyboard
- OS
- Chardet
- Pyperclip
- py2app

### Installing

To install the packages, run the following command:

```
pip install -r requirements.txt
```

Once the packages are installed, you can run the MultiAi.py file to launch the application.

### Usage

#### Option 1 - Windows & MacOS
Once the application is launched, you will be presented with a window with three buttons: Code Generation, Text Completion, and README Generation. Select the service you want to use and follow the instructions on the screen.

#### Option 2 - MacOS
If you want to build this as a app for your mac, just go into your vscode terminal and paste this in: 
``` 
python3 setup.py py2app -A 
```
This is ONLY for MACOS.
Windows are comming soon.


#### Code Generation

When you select the Code Generation option, you will be asked to enter a question. The system will then generate code based on your question.

#### Text Completion

When you select the Text Completion option, you will be asked to enter a question. The system will then generate text based on your question.

#### README Generation

When you select the README Generation option, you will be asked to enter the directory path of the project you want to generate the README for. The system will then generate a README for the project.

## Built With

- [PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/) - A GUI framework for Python
- [OpenAI](https://openai.com/) - An AI platform
- [Keyboard](https://pypi.org/project/keyboard/) - A Python module for monitoring and controlling keyboard
- [OS](https://docs.python.org/3/library/os.html) - A Python module for interacting with the operating system
- [Chardet](https://pypi.org/project/chardet/) - A Python module for detecting character encoding
- [Pyperclip](https://pypi.org/project/pyperclip/) - A Python module for copying and pasting text

## Authors

- **[CPTRICODEV]** - *Initial work* - [CPTRICODEV](https://github.com/CPTRICODEV)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
