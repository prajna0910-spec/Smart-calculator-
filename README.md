# Smart-calculator
import tkinter as tk


def click(button):
    current = display.get()

    if button == "C":
        display.delete(0, tk.END)

    elif button == "DEL":
        display.delete(len(current) - 1, tk.END)

    elif button == "=":
        try:
            result = eval(current)
            display.delete(0, tk.END)
            display.insert(0, str(result))
        except:
            display.delete(0, tk.END)
            display.insert(0, "Error")

    else:
        display.insert(tk.END, button)


# Create window
window = tk.Tk()
window.title("Smart Calculator")
window.geometry("350x500")
window.resizable(False, False)

# Display
display = tk.Entry(
    window,
    font=("Arial", 28),
    justify="right",
    bd=10
)
display.pack(fill="both", padx=10, pady=20, ipady=10)

# Buttons
buttons = [
    ["7", "8", "9", "/"],
    ["4", "5", "6", "*"],
    ["1", "2", "3", "-"],
    ["0", ".", "%", "+"],
    ["C", "DEL", "="]
]

frame = tk.Frame(window)
frame.pack()

for row in buttons:
    row_frame = tk.Frame(frame)
    row_frame.pack(fill="both", expand=True)

    for button in row:
        tk.Button(
            row_frame,
            text=button,
            font=("Arial", 18),
            width=5,
            height=2,
            command=lambda b=button: click(b)
        ).pack(side="left", padx=3, pady=3)

# Run application
window.mainloop()