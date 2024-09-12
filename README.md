import tkinter as tk
from tkinter import messagebox
from tkinter import ttk

class KidCalculator(tk.Tk):
    def __init__(self):
        super().__init__()
        self.title("Calculadora Divertida 🌟")
        self.geometry("350x450")
        self.configure(bg='lightpink')
        self.create_widgets()
        self.history = []

    def create_widgets(self):
        # Title
        title_label = tk.Label(self, text="¡Calculadora Genial! 🎈", font=('Comic Sans MS', 16, 'bold'), bg='lightpink', fg='purple')
        title_label.pack(pady=10)

        # Entry
        self.entry = tk.Entry(self, width=16, font=('Comic Sans MS', 24), borderwidth=2, relief='ridge', justify='right')
        self.entry.pack(pady=10)

        # Buttons
        button_texts = [
            ('7', '8', '9', '÷'),
            ('4', '5', '6', '×'),
            ('1', '2', '3', '-'),
            ('0', '.', '=', '+'),
            ('C', 'History', 'Fun', '🎲')
        ]

        for r, row in enumerate(button_texts):
            for c, text in enumerate(row):
                button = tk.Button(self, text=text, width=6, height=2, font=('Comic Sans MS', 14),
                                   bg='lightyellow', fg='black', relief='raised', command=lambda t=text: self.on_button_click(t))
                button.grid(row=r+1, column=c, padx=5, pady=5)

    def on_button_click(self, char):
        if char == 'C':
            self.entry.delete(0, tk.END)
        elif char == '🎲':
            self.entry.insert(tk.END, '5+5')  # Fun example
        elif char == 'Fun':
            self.show_message("¡Hola! 🎉", "¡Diviértete usando la calculadora!")
        elif char == 'History':
            self.show_history()
        elif char == '÷':
            self.entry.insert(tk.END, '/')
        elif char == '×':
            self.entry.insert(tk.END, '*')
        elif char == '=':
            try:
                result = eval(self.entry.get())
                self.entry.delete(0, tk.END)
                self.entry.insert(tk.END, str(result))
                self.add_to_history(self.entry.get() + ' = ' + str(result))
            except Exception:
                self.entry.delete(0, tk.END)
                self.entry.insert(tk.END, "Error")
        else:
            self.entry.insert(tk.END, char)

    def show_message(self, title, message):
        messagebox.showinfo(title, message)

    def show_history(self):
        if not hasattr(self, 'history'):
            self.history = []
        history_text = "\n".join(self.history) if self.history else "¡No hay historial aún!"
        self.show_message("Historial de Cálculos", history_text)

    def add_to_history(self, entry):
        if not hasattr(self, 'history'):
            self.history = []
        self.history.append(entry)

if __name__ == "__main__":
    app = KidCalculator()
    app.mainloop()
