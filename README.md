import PySimpleGUI as sg
import openai
import keyboard
import os
import chardet
import pyperclip

openai.api_key = "Your_API_Key"

sg.theme('DarkTeal10')


def open_code_gen():
    code_generation()


def open_text_comp():
    text_completion()


def open_readme_gen():
    readme_generation()

def detect_encoding(filepath):
    with open(filepath, 'rb') as f:
        result = chardet.detect(f.read())
    return result['encoding']

keyboard.add_hotkey('ctrl+alt+c', open_code_gen)
keyboard.add_hotkey('ctrl+alt+t', open_text_comp)
keyboard.add_hotkey('ctrl+alt+r', open_readme_gen)


def code_generation():
    # code for code generation
    layout_text = [[sg.Text('Ask me about code!')],
                   [sg.InputText()],
                   [sg.Text("", key='-OUTPUT-')],
                   [sg.Text("Waiting...", key='-SPIN-')]
                   ]
    layout_text.append([sg.Button('Copy'), sg.Button('OK'), sg.Button('Cancel')])
    window_text = sg.Window('MultiAi Code Generation', layout_text)

    while True:
        event, values = window_text.read()
        if event in (None, 'Cancel'):
            break
        question = values[0]
        window_text['-OUTPUT-'].update('')
        window_text['-SPIN-'].update('Loading...')
        response = openai.Completion.create(
            engine="text-davinci-002",
            prompt=question,
            max_tokens=2048,
            n=1,
            stop=None,
            temperature=0.5,
        )
        if event == "Copy":
            sg.popup_ok('Code Copied to clipboard')
            pyperclip.copy(response["choices"][0]["text"])
        window_text['-OUTPUT-'].update(response["choices"][0]["text"])
        window_text['-SPIN-'].update('Compleate')
    window_text.close()


def text_completion():
    layout_text = [[sg.Text('Ask me a question')],
                   [sg.InputText()],
                   [sg.Text("", key='-OUTPUT-')],
                   [sg.Text('Wating...', key='-SPIN-')]
                   ]
    layout_text.append([sg.Button('Copy'), sg.Button('OK'), sg.Button('Cancel')])
    window_text = sg.Window('MultiAi Text Completion', layout_text)

    while True:
        event, values = window_text.read()
        if event in (None, 'Cancel'):
            break
        question = values[0]
        window_text['-OUTPUT-'].update('')
        window_text['-SPIN-'].update('Loading...')
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=question,
            max_tokens=2048,
            n=1,
            stop=None,
            temperature=0.5,
        )
        if event == "Copy":
            sg.popup_ok('Text Copied to clipboard')
            pyperclip.copy(response["choices"][0]["text"])
        window_text['-OUTPUT-'].update(response["choices"][0]["text"])
        window_text['-SPIN-'].update('Compleate')
    window_text.close()


def readme_generation():


    # code for readme generation
    layout_text = [[sg.Text('Enter the directory path:')],
                  [sg.InputText()],
                  [sg.Text("", key='-OUTPUT-')],
                  [sg.Text('Wating...', key='-SPIN-')]
                  ]
    layout_text.append([sg.Button('Copy'), sg.Button('OK'), sg.Button('Cancel')])
    window_text = sg.Window('MultiAi README Generation', layout_text)
    while True:
        event, values = window_text.read()
        if event in (None, 'Cancel'):
            break
        directory = values[0]
        files = os.listdir(directory)
        readme_text = ""
        for file in files:
            if file.endswith(".py"):
                encoding = detect_encoding(os.path.join(directory, file))
                with open(os.path.join(directory, file), "r", encoding=encoding) as f:
                    readme_text += f.read() + "\n\n"
        prompt = "Create a Readme.md for github about the following Code:\n\n" + readme_text
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=prompt,
            max_tokens=2048,
            n=1,
            stop=None,
            temperature=0.5,
        )
        directory_path = values[0]
        file_name = "README.md"
        file_path = os.path.join(directory_path, file_name)
        window_text['-OUTPUT-'].update('')
        window_text['-SPIN-'].update('Compleate...')

        # Code to generate the README content
        # ...

        with open(file_path, "w") as file:
            file.write(response["choices"][0]["text"])
            print("The README is done.")
            print("The README is located at: " + file_path)
        if event == "Copy":
            sg.popup_ok('Path Copied to clipboard')
            pyperclip.copy(file_path)
        window_text['-SPIN-'].update('')
        window_text['-OUTPUT-'].update("The README is located at: " + file_path)
        
        window_text['-SPIN-'].update('')
    window_text.close()


layout = [[sg.Text('Select the service you want')],
          [sg.Button('Code Generation', key='code_gen'), sg.Button(
              'Text Completion', key='text_comp'), sg.Button('README Generation', key='readme_gen')],
          ]

window = sg.Window('MultiAi Python Systems', layout)

while True:
    event, values = window.read()
    if event in (None, 'Exit'):
        break
    if event == 'code_gen':
        code_generation()
    if event == 'text_comp':
        text_completion()
    if event == 'readme_gen':
        readme_generation()

window.close()
