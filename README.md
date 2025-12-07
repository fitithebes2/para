# para
# urok 1

import tkinter as tk

root = tk.Tk()
root.title("First Window")
root.geometry("600x400+500+200")
#root.iconbitmap("bomb.ico")

Label_1 = tk.Label(font= ("Arial",100,"bold"),text = "Hello\nThere", bg="red",fg="yellow", width=10,height=3, padx=85, pady=50)
Label_1.pack()

root.mainloop()



#Urok 2

import tkinter as tk
from tkinter import filedialog
def file_new():
    save_or_not = tk.Tk()
    save_or_not.geometry("150x70+700+550")
    save_or_not.resizable(False, False)
    save_or_not.grid_columnconfigure(0, minsize=75)
    save_or_not.grid_columnconfigure(1, minsize=75)
    saving_label = tk.Label(save_or_not, text="Save file?")
    saving_label.grid(columnspan=2)
    def without_saving():
        save_or_not.destroy()
        global text
        text.delete('1.0', tk.END)
    def saving():
        file_save()
        save_or_not.destroy()
        global text
        text.delete('1.0', tk.END)
    yes_button = tk.Button(save_or_not, text="Yes", command=saving, width=8)
    no_button = tk.Button(save_or_not, text="No", command=without_saving, width=8)
    yes_button.grid(column=0, row=1)
    no_button.grid(column=1, row=1)

def file_open():
    file_name = filedialog.askopenfilename(initialdir='/', title='Open file', filetypes=(('Text Documents','*.txt'),('allfiles','*.*')))
    if file_name:
        with open(file_name, 'r') as f:
            text_open = f.read()
            if text_open!= tk.NONE:
                text.delete(1.0, tk.END)
                text.insert(tk.END, text_open)
            else:
                text.delete(1.0, tk.END)

def file_save():
    file_name = filedialog.asksaveasfilename(initialdir='/', title='Select file', filetypes=(('Text Documents','*.txt'),('allfiles','*.*')))
    if file_name:
        with open(file_name+".txt", 'w') as f:
            text_save = str(text.get(1.0, tk.END))
            f.write(text_save+'\n')

def file_exit():
    root.destroy()

def help_function():
    help_window = tk.Tk()
    help_window.geometry("300x70+700+550")
    help_window.resizable(False, False)
    help_label = tk.Label(help_window, text="Link to instructions\nhttps://www.wikihow.com/Use-Notepad")
    help_label.pack()
    def back():
        help_window.destroy()
    back_button = tk.Button(help_window, text="Back", command=back, width=10)
    back_button.pack()

def about():
    about_window = tk.Tk()
    about_window.geometry("300x70+700+550")
    about_window.resizable(False, False)
    help_label = tk.Label(about_window, text="ItStep\nThanks for using!")
    help_label.pack()
    def back():
        about_window.destroy()
    back_button = tk.Button(about_window, text="Back", command=back, width=10)
    back_button.pack()

root = tk.Tk()
root.geometry("600x400+500+400")
root.title("Magician's diary")
#root.iconbitmap("Note.ico")
root.minsize(200, 100)
root.maxsize(1920,1080)
menu = tk.Menu(root)
root.config(menu=menu)
file_menu = tk.Menu(menu, tearoff=0)
file_menu.add_command(label='New', command = file_new)
file_menu.add_command(label='Open.', command = file_open)
file_menu.add_command(label='Save as.', command = file_save)
file_menu.add_command(label='Exit', command = file_exit)
menu.add_cascade(label='File', menu=file_menu)
help_menu = tk.Menu(menu, tearoff=0)
help_menu.add_command(label='Help', command=help_function)
help_menu.add_command(label='About', command =about)
menu.add_cascade(label='Help', menu=help_menu)
text = tk.Text(root)
text.pack(expand=tk.YES, fill=tk.BOTH)
root.mainloop()








# part 2














import tkinter as tk
bomb = 100
score = 0
press_return = True
root = tk.Tk()
root.title("Game")
root.geometry("600x600+500+400")
root.iconbitmap("bomb.ico")
label = tk.Label(root, text='Press [enter] to start the game', font=('Comic Sans MS', 12))
label.pack()
fuse_label = tk.Label(root, text=f'Fuse: {str(bomb)}', font=('Comic Sans MS', 14))
fuse_label.pack()
score_label = tk.Label(root, text=f'Score: {str(score)}', font=('Comic Sans MS', 14))
score_label.pack()
img_1 = tk.PhotoImage(file="1.gif")
img_2 = tk.PhotoImage(file="2.gif")
img_3 = tk.PhotoImage(file="3.gif")
img_4 = tk.PhotoImage(file="4.gif")

bomb_label = tk.Label(image=img_1)
bomb_label.pack()
def update_display():
    global bomb
    global score
    if bomb >= 80:
        bomb_label.config(image=img_1)
    elif 50 <= bomb < 80:
        bomb_label.config(image=img_2)
    elif 0 < bomb < 50:
        bomb_label.config(image=img_3)
    else:
        bomb_label.config(image=img_4)
    fuse_label.config(text='Fuse: ' + str(bomb))
    score_label.config(text='Score: ' + str(score))
    fuse_label.after(100, update_display)

def is_alive():
    global bomb
    global press_return
    if bomb <= 0:
        bomb = 0
        label.config(text='Bang! Bang! Bang!')
        press_return = True
        return False
    else:
        return True

def update_bomb():
    global bomb
    bomb -= 5
    if is_alive():
        fuse_label.after(400, update_bomb)
def update_score():
    global score
    if is_alive():
        score += 1
        score_label.after(3000, update_score)

def start(event):
    global press_return
    if not press_return:
        pass
    else:
        update_bomb()
        update_score()
        update_display()
        label.config(text='')
        press_return = False

def click():
    global bomb
    if is_alive():
        bomb += 1

click_button = tk.Button(root, text='Click me',
bg='black', fg='white', width=15, font=('Comic Sans MS', 14), command=click)
click_button.pack()
root.bind('<Return>', start)
root.mainloop()





































