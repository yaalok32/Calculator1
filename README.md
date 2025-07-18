# Calculator1
import tkinter as tk
from tkinter import messagebox

class CalculatorApp:
    def __init__(self, root):
        self.root = root
        self.root.title("🧮 Calculator")
        self.root.geometry("360x480")
        self.root.configure(bg="#1e1e1e")
        self.expression = ""

        self.input_text = tk.StringVar()
        self.result_text = tk.StringVar()

        self.create_widgets()

    def create_widgets(self):
        # Entry fields
        input_frame = tk.Frame(self.root, bg="#1e1e1e")
        input_frame.pack(pady=20)

        input_entry = tk.Entry(input_frame, textvariable=self.input_text, font=("Helvetica", 20),
                               bg="#2f2f2f", fg="white", bd=0, width=22, justify='right')
        input_entry.grid(row=0, column=0, padx=10, pady=5)

        result_entry = tk.Entry(input_frame, textvariable=self.result_text, font=("Helvetica", 16),
                                bg="#2f2f2f", fg="#00ff88", bd=0, width=22, justify='right')
        result_entry.grid(row=1, column=0, padx=10)

        # Buttons
        btns_frame = tk.Frame(self.root, bg="#1e1e1e")
        btns_frame.pack()

        buttons = [
            ('7', '8', '9', '/'),
            ('4', '5', '6', '*'),
            ('1', '2', '3', '-'),
            ('0', '.', '=', '+'),
            ('C',)
        ]

        for row_idx, row in enumerate(buttons):
            for col_idx, btn_text in enumerate(row):
                button = tk.Button(btns_frame, text=btn_text, font=("Helvetica", 16),
                                   width=6, height=2, bd=0, fg="white", bg="#333333",
                                   command=lambda txt=btn_text: self.on_button_click(txt))
                button.grid(row=row_idx, column=col_idx, padx=5, pady=5, sticky="nsew")

        # Stretch last row "C" button to full width
        btns_frame.grid_columnconfigure(0, weight=1)
        btns_frame.grid_columnconfigure(1, weight=1)
        btns_frame.grid_columnconfigure(2, weight=1)
        btns_frame.grid_columnconfigure(3, weight=1)

    def on_button_click(self, char):
        if char == "C":
            self.expression = ""
            self.input_text.set("")
            self.result_text.set("")
        elif char == "=":
            try:
                result = str(eval(self.expression))
                self.result_text.set(f"= {result}")
            except Exception:
                self.result_text.set("Error")
        else:
            self.expression += str(char)
            self.input_text.set(self.expression)

if __name__ == "__main__":
    root = tk.Tk()
    app = CalculatorApp(root)
    root.mainloop()
