import tkinter as tk
import turtle
import time

# ------------------ TURTLE ANIMATION ------------------ #
def turtle_animation():
    wn = turtle.Screen()
    wn.bgcolor("black")
    wn.title("Welcome Animation")
    t = turtle.Turtle()
    t.pensize(3)
    colors = ["red", "orange", "yellow", "green", "blue", "purple"]

    t.speed(0)
    for i in range(36):
        t.color(colors[i % len(colors)])
        t.circle(100)
        t.left(10)

    t.hideturtle()
    time.sleep(2)
    wn.bye()  # Close turtle window

# Show animation before launching GUI
turtle_animation()

# ------------------ MAIN TKINTER GUI ------------------ #
root = tk.Tk()
root.title("Portfolio Website GUI")
root.geometry("1280x720")
root.configure(bg="#f4f4f4")
root.resizable(False, False)

# ------------------ HEADER ------------------ #
header = tk.Frame(root, height=10, bg="#282c34")
header.pack(fill="x")

tk.Label(header, text="MSPL WEBSITE",
         font=("Helvetica", 10, "bold"),
         fg="white", bg="#282c34").pack(pady=8)

# ------------------ NAVIGATION ------------------ #
nav = tk.Frame(root, bg="#61afef", height=20)
nav.pack(fill="x")

def create_nav_button(name):
    btn = tk.Label(nav, text=name, font=("Arial", 8,"bold"),
                   bg="#61afef", fg="white", padx=20, pady=10, cursor="hand2")
    btn.bind("<Button-1>", lambda e, n=name: show_page(n))
    btn.bind("<Enter>", lambda e: btn.config(bg="#528dcf"))
    btn.bind("<Leave>", lambda e: btn.config(bg="#61afef"))
    btn.pack(side="left", padx=2)

for name in ["Home", "About", "Projects", "Contact"]:
    create_nav_button(name)

# ------------------ PAGES ------------------ #
page_frame = tk.Frame(root, bg="white")
page_frame.pack(fill="both", expand=True)

home_page = tk.Frame(page_frame, bg="white")
about_page = tk.Frame(page_frame, bg="white")
projects_page = tk.Frame(page_frame, bg="white")
contact_page = tk.Frame(page_frame, bg="white")

# Home Page
tk.Label(home_page, text=" Welcome to My Portfolio", font=("Arial", 16, "bold"),
         fg="#333", bg="white").pack(pady=40)
tk.Label(home_page, text="Hi, I'm a passionate developer. This GUI is built with Tkinter!",
         font=("Arial", 10), fg="#555", bg="white").pack()

# About Page
tk.Label(about_page, text="About Me", font=("Arial", 16, "bold"),
         fg="#333", bg="white").pack(pady=40)
tk.Label(about_page, text="I'm a student learning Python and building projects with Tkinter.",
         font=("Arial", 10), fg="#555", bg="white").pack()

# Projects Page
tk.Label(projects_page, text="Projects", font=("Arial", 16, "bold"),
         fg="#333", bg="white").pack(pady=40)
tk.Label(projects_page, text="- Portfolio GUI with Tkinter\n- Calculator App\n- Snake Game",
         font=("Arial", 10), fg="#555", bg="white", justify="left").pack()

# Contact Page
tk.Label(contact_page, text="Contact Me", font=("Arial", 16, "bold"),
         fg="#333", bg="white").pack(pady=40)
tk.Label(contact_page, text="Email: demo@example.com\nPhone: +1234567890",
         font=("Arial", 10), fg="#555", bg="white").pack()

# Dictionary of Pages
pages = {
    "Home": home_page,
    "About": about_page,
    "Projects": projects_page,
    "Contact": contact_page
}

def show_page(name):
    for p in pages.values():
        p.pack_forget()
    pages[name].pack(fill="both", expand=True)

# ------------------ SHOW DEFAULT PAGE ------------------ #
show_page("Home")

# ------------------ MAINLOOP ------------------ #
root.mainloop()