## OTP GENERATOR TO VERIFY THE USER

- def verify_otp(entered_otp):
            if entered_otp == user_otp:
                messagebox.showinfo("OTP Verification", "OTP verification Successful.")
                c.execute(f"INSERT INTO sign_up values('{n}','{g}','{p}','{re}',{m},'{gender_value}','{image}') ")
                conn.commit()
                print("Value Stored in the sign_up table")
                root.configure(bg="lightgreen")
                head_top.configure(bg="lightgreen")
                heading1.configure(bg="green")
                heading2.configure(bg="green")
                name.configure(bg="lightgreen")
                gmail_name.configure(bg="lightgreen")
                password.configure(bg="lightgreen")
                re_password.configure(bg="lightgreen")
                mobile_no.configure(bg="lightgreen")
                btn.configure(bg="green", fg="white")
                Label(root, text="Submitted", bg="lightgreen").place(x = 500, y = 440)
                root.destroy()
                def extract_lyrics():
                    song_name = song_entry.get()
                    artist_name = artist_entry.get()
                    genius = lyricsgenius.Genius("AIzaSyAjxGRJlw3vH6V2nUvjgtEnvSFah8A4wH8")  # Replace with your own Genius API key
                    song = genius.search_song(song_name, artist_name)
                    lyrics_text.delete("1.0", END)  # Clear previous lyrics
                    if song is not None:
                        lyrics_text.insert(END, song.lyrics)
                        c.execute("INSERT INTO search_history (Name, Gmail, Searched_Song, Searched_Artist) VALUES (%s, %s, %s, %s)", (n, g, song_name, artist_name))
                        conn.commit()
                    else:
                        lyrics_text.insert(END, "Lyrics not found.")
                window = Tk()
                window.title("Lyrics Extractor")
                window.geometry("400x300+600+200")
                window.configure(bg="#8ECDDD")
                song_label = Label(window, text="Song:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
                song_label.pack(pady=10)
                song_entry = Entry(window, font=("Arial", 16))
                song_entry.pack()
                artist_label = Label(window, text="Artist:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
                artist_label.pack(pady=10)
                artist_entry = Entry(window, font=("Arial", 16))
                artist_entry.pack()
                extract_button = Button(window, text="Extract Lyrics", command=extract_lyrics, font=("cambria", 16, "bold"), bg="#071952", fg="white")
                extract_button.pack(pady=10)
                spacing = 15
                lyrics_text = Text(window, height=80, width=120, font=("cambria", 15, "bold"), spacing1=spacing)
                lyrics_text.pack(pady=15, padx=30)
    # Set the text alignment to center
                lyrics_text.tag_configure("center", justify='center')
    # Insert the text and apply the "center" tag to center-align it
                lyrics_text.insert("1.0", "Your lyrics text here...", "center")
                window.mainloop()
            else:
                messagebox.showerror("OTP Verification", "Invalid OTP, Please try Again")

## SEND OTP
def send_otp(email):
      port = 465 #For SSL
      smtp_server = "smtp.gmail.com"
      sender_email = "shashanktripathi1703@gmail.com"
      password = "ymll luhd vuqm ardq"

    #   otp = generate_otp()
      otp = ''.join([str(random.randint(0, 9)) for i in range(6)])
      message = f"""\
      Subject: One Time Password for Music App Login
      Your OTP is {otp}.
      This password will be valid for 5 minutes only. Please use it to login into your account & Do not share it with anyone"""

      context = ssl.create_default_context()
      with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:
          server.login(sender_email, password)
          server.sendmail(sender_email, email, message)
      return otp

## Whole Code
from tkinter import *
import random
import email.utils
import smtplib
import ssl
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from tkinter import filedialog
from tkinter import messagebox
import mysql.connector as msl
import lyricsgenius
root = Tk()

conn = msl.connect(host = "localhost", port = 3307, user = "root", password = "")
print("Database Connected")
c = conn.cursor()
c.execute("CREATE DATABASE if not exists Lyrics_User")
print("Database Created")
conn = msl.connect(host = "localhost", port = 3307, user = "root", password = "", database = "Lyrics_User")
c = conn.cursor()
c.execute('''CREATE TABLE if not exists sign_up (
            Name varchar(20), 
            Gmail varchar(50) PRIMARY KEY, 
            Password varchar(20), 
            Re_Password varchar(20),
            Mob_No int, 
            Gender ENUM('Male', 'Female'), 
            Image_Path varchar(100)
        )''')
print("Table Created")
c.execute('''CREATE TABLE if not exists search_history (
             Id INT AUTO_INCREMENT PRIMARY KEY,
             Name VARCHAR(20),
             Gmail VARCHAR(50),
             Searched_Song VARCHAR(100),
             Searched_Artist VARCHAR(100)
           )''')
print("Song History Saved")

def upload_image():
    image_path = filedialog.askopenfilename(initialdir="/", title="Select Image", filetypes=(("Image Files", "*.jpg *.jpeg *.png *.gif"),))
    return image_path


# def generate_otp():
#     return random.randint(1000, 9999)  # Generate a random 4-digit OTP
      

def validate_email(user_gmail):
    if "@" in user_gmail and "." in user_gmail[user_gmail.index("@"):]:
        return True
    return False

def send_otp(email):
      port = 465 #For SSL
      smtp_server = "smtp.gmail.com"
      sender_email = "example@gmail"
      password = "example-password"

    #   otp = generate_otp()
      otp = ''.join([str(random.randint(0, 9)) for i in range(6)])
      message = f"""\
      Subject: One Time Password for Music-Extractor App Login
      Your OTP is {otp}.
      This password will be valid for 5 minutes only. Please use it to login into your account & Do not share it with anyone"""

      context = ssl.create_default_context()
      with smtplib.SMTP_SSL(smtp_server, port, context=context) as server:
          server.login(sender_email, password)
          server.sendmail(sender_email, email, message)
      return otp


def fun():
    n = n_text.get()
    g = gmail_text.get()
    p = password_text.get()
    re = re_password_text.get()
    m = mobile_text.get()
    gender_value = gender.get()
    image = upload_image()
    if validate_email(g):
        c.execute("SELECT * FROM sign_up WHERE Gmail = %s", (g,))
        existing_user = c.fetchone()
        
        if existing_user:
            messagebox.showerror("Sign-Up Error", "This email is already registered. Please use a different email.")
            verify_window.destroy()
        else:
            user_otp = send_otp(g)
            def verify_otp(entered_otp):
                if entered_otp == user_otp:
                    messagebox.showinfo("OTP Verification", "OTP verification Successful.")
                    verify_window.destroy()
                    c.execute("INSERT INTO sign_up (Name, Gmail, Password, Re_Password, Mob_No, Gender, Image_Path) VALUES (%s, %s, %s, %s, %s, %s, %s)",(n, g, p, re, m, gender_value, image))
                    conn.commit()
                    print("Value Stored in the sign_up table")
                    root.configure(bg="lightgreen")
                    head_top.configure(bg="lightgreen")
                    heading1.configure(bg="green")
                    heading2.configure(bg="green")
                    name.configure(bg="lightgreen")
                    gmail_name.configure(bg="lightgreen")
                    password.configure(bg="lightgreen")
                    re_password.configure(bg="lightgreen")
                    mobile_no.configure(bg="lightgreen")
                    btn.configure(bg="green", fg="white")
                    Label(root, text="Submitted", bg="lightgreen").place(x = 500, y = 440)
                    root.destroy()
                    def extract_lyrics():
                        song_name = song_entry.get()
                        artist_name = artist_entry.get()
                        genius = lyricsgenius.Genius("AIzaSyAjxGRJlw3vH6V2nUvjgtEnvSFah8A4wH8")  # Replace with your own Genius API key
                        song = genius.search_song(song_name, artist_name)
                        lyrics_text.delete("1.0", END)  # Clear previous lyrics
                        if song is not None:
                            lyrics_text.insert(END, song.lyrics)
                            c.execute("INSERT INTO search_history (Name, Gmail, Searched_Song, Searched_Artist) VALUES (%s, %s, %s, %s)", (n, g, song_name, artist_name))
                            conn.commit()
                        else:
                            lyrics_text.insert(END, "Lyrics not found.")
                    window = Tk()
                    window.title("Lyrics Extractor")
                    window.geometry("400x300+600+200")
                    window.configure(bg="#8ECDDD")
                    song_label = Label(window, text="Song:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
                    song_label.pack(pady=10)
                    song_entry = Entry(window, font=("Arial", 16))
                    song_entry.pack()
                    artist_label = Label(window, text="Artist:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
                    artist_label.pack(pady=10)
                    artist_entry = Entry(window, font=("Arial", 16))
                    artist_entry.pack()
                    extract_button = Button(window, text="Extract Lyrics", command=extract_lyrics, font=("cambria", 16, "bold"), bg="#071952", fg="white")
                    extract_button.pack(pady=10)
                    spacing = 15
                    lyrics_text = Text(window, height=80, width=120, font=("cambria", 15, "bold"), spacing1=spacing)
                    lyrics_text.pack(pady=15, padx=30)
    # Set the text alignment to center
                    lyrics_text.tag_configure("center", justify='center')
    # Insert the text and apply the "center" tag to center-align it
                    lyrics_text.insert("1.0", "Your lyrics text here...", "center")
                    window.mainloop()
    else:
        messagebox.showerror("OTP Verification", "Invalid OTP, Please try Again")

    def submit_otp():
        entered_otp = otp_entry.get()
        if entered_otp == user_otp:  # Compare the entered OTP with the generated OTP
            verify_otp(entered_otp)
        else:
            messagebox.showerror("Invalid OTP", "The OTP entered is incorrect. Please try again.")
    verify_window = Tk()
    verify_window.title("Verify OTP")
    verify_window.geometry("600x300+500+200")
    verify_window.configure(bg = "#D895DA")
    f_heading = ("cambria", 20, "bold")

    Label(verify_window, text="Enter the OTP sent to your Email",font = f_heading, fg="#D20062", bg = "#D895DA").place(x=80, y=50)
    otp_entry = Entry(verify_window, show="*", font = ("cambria", 15, "bold"), fg="#D20062")
    otp_entry.place(x=170, y=130)

    Button(verify_window, text="Submit", command=submit_otp, font = f_heading, fg="#D895DA", bg = "#D20062").place(x=240, y=180)
    verify_window.mainloop()

    
def login():
    root.destroy()
    win = Tk()
    def verify():
        un = user_n_text.get()
        ug = user_g_text.get()
        up = user_pass_text.get()
        c.execute("SELECT * FROM sign_up WHERE Name = %s AND GMAIL = %s AND Password = %s", (un, ug, up))
        result = c.fetchone()
        if result:
            Label(win, text = "Login Succesfully", font = ("cambria", 12, "bold"), bg="orange", fg = "white").place(x = 380, y = 350)
            win.destroy()
            def extract_lyrics():
                        song_name = song_entry.get()
                        artist_name = artist_entry.get()
                        genius = lyricsgenius.Genius("AIzaSyAjxGRJlw3vH6V2nUvjgtEnvSFah8A4wH8")  # Replace with your own Genius API key
                        song = genius.search_song(song_name, artist_name)
                        lyrics_text.delete("1.0", END)  # Clear previous lyrics
                        if song is not None:
                            lyrics_text.insert(END, song.lyrics, "center")
                            c.execute("INSERT INTO search_history (Name, Gmail, Searched_Song, Searched_Artist) VALUES (%s, %s, %s, %s)", (un, ug, song_name, artist_name))
                            conn.commit()
                        else:
                                lyrics_text.insert(END, "Lyrics not found.", "center")
            window = Tk()
            window.title("Lyrics Extractor")
            window.geometry("400x300+600+200")
            window.configure(bg="#8ECDDD")
            song_label = Label(window, text="Song:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
            song_label.pack(pady=10)
            song_entry = Entry(window, font=("Arial", 16))
            song_entry.pack()
            artist_label = Label(window, text="Artist:", font=("Arial", 16, "bold"), bg="#8ECDDD", fg="#071952")
            artist_label.pack(pady=10)
            artist_entry = Entry(window, font=("Arial", 16))
            artist_entry.pack()
            extract_button = Button(window, text="Extract Lyrics", command=extract_lyrics, font=("cambria", 16, "bold"), bg="#071952", fg="white")
            extract_button.pack(pady=10)
            spacing = 15
            lyrics_text = Text(window, height=80, width=120, font=("cambria", 16, "bold"), spacing1=spacing)
            lyrics_text.pack(pady=15, padx=30)
            # Set the text alignment to center
            lyrics_text.tag_configure("center", justify='center')

            # Insert the text and apply the "center" tag to center-align it
            lyrics_text.insert("1.0", "Your lyrics text here...", "center")
            window.mainloop()

        else:
            win.configure(bg="red")
            head_top.configure(bg="red",fg="black")
            user_name.configure(bg="red",fg="black")
            user_gmail.configure(bg="red",fg="black")
            user_pass.configure(bg="red",fg="black")
            btn_submit.configure(fg="white")
            Label(win, text="Login UnSuccesfully", font=("cambria", 12, "bold"), bg="red", fg="white").place(x=380,
                                                                                                                y=350)
    win.title("LOGIN-FORM")
    win.geometry("600x400+500+200")
    win.resizable(0, 0)
    win.configure(bg = "#46C2CB")
    f_login = ("cambria", 35, "bold")
    head_top = Label(win, font=f_login, text = "LOGIN-FORM", bg="#15133C", fg="#FFE15D")
    head_top.place(x=170, y=10)
    f_login_text = ("cambria", 20, "bold")
    user_name = Label(win, font=f_login_text, text = "USER-NAME", bg="#46C2CB", fg="#15133C")
    user_name.place(x = 40, y = 110)
    user_n_text = Entry(win, font=f_login_text)
    user_n_text.place(x = 210, y = 110)
    user_gmail = Label(win, font=f_login_text, text="GMAIL", bg="#46C2CB", fg="#15133C")
    user_gmail.place(x = 40, y = 180)
    user_g_text = Entry(win, font=f_login_text)
    user_g_text.place(x = 210, y = 180)
    user_pass = Label(win, font=f_login_text, text = "PASSWORD", bg="#46C2CB", fg="#15133C")
    user_pass.place(x = 40, y = 250)
    user_pass_text = Entry(win, font=f_login_text)
    user_pass_text.place(x = 210, y = 250)
    btn_submit = Button(win, font = f_text, text="SUBMIT", bg="#15133C", fg="#FFE15D", command=verify)
    btn_submit.place(x=250, y=320)
    win.mainloop()


root.title("REGISTRATION-FORM")
root.configure(bg="#D8B4F8")
root.geometry("600x550+500+150")
root.resizable(0,0) 


f_heading = ("cambria", 35, "bold")
heading1= Label(root, text="SIGN-UP", font = f_heading, bg="#900C3F")
heading1.place(x=205, y=15)
heading1= Label(root, text="SIGN-UP", font = f_heading, bg="#900C3F")
heading1.place(x=215, y=5)
heading2= Label(root, text="SIGN-UP", font = f_heading, bg="#900C3F")
heading2.place(x=205, y=5)
heading2= Label(root, text="SIGN-UP", font = f_heading, bg="#900C3F")
heading2.place(x=215, y=15)
head_top = Label(root, text = "SIGN-UP", font = f_heading, bg="#3B185F", fg="white")
head_top.place(x=210,y=10)

f_text = ("cambria", 20, "bold")
name = Label(root, text = "Name", font = f_text, bg="#D8B4F8", fg="#3B185F")
name.place(x = 40, y = 100)
n_text = Entry(root, font = f_text)
n_text.place(x = 150, y = 100)

gmail_name= Label(root, text = "Gmail", font = f_text, bg="#D8B4F8", fg="#3B185F")
gmail_name.place(x = 40, y = 150)
gmail_text = Entry(root, font = f_text)
gmail_text.place(x = 150, y = 150)

password = Label(root, text="Pass", font=f_text, bg="#D8B4F8", fg="#3B185F")
password.place(x=40, y=200)
password_text = Entry(root, font=f_text, show="*")
password_text.place(x=150, y=200)

re_password = Label(root, text="Re-Pass", font=f_text, bg="#D8B4F8", fg="#3B185F")
re_password.place(x=40, y=250)
re_password_text = Entry(root, font=f_text, show="*")
re_password_text.place(x=150, y=250)

mobile_no= Label(root, text = "Mob_No", font = f_text, bg="#D8B4F8", fg="#3B185F")
mobile_no.place(x = 40, y = 300)
mobile_text = Entry(root, font = f_text)
mobile_text.place(x = 150, y = 300)

gender = StringVar()
gender.set('Male')
gender_label = Label(root, text='Gender:', font=f_text, bg="#D8B4F8", fg="#3B185F")
gender_label.place(x=40, y=350)  

male_radiobutton = Radiobutton(root, text='Male', font=f_text,
                               bg="#D8B4F8", fg="#3B185F", variable=gender, value='Male')
male_radiobutton.place(x=150, y=350) 

female_radiobutton = Radiobutton(root, text='Female', font=f_text,
                                 bg="#D8B4F8", fg="#3B185F", variable=gender, value='Female')
female_radiobutton.place(x=250, y=350)  

upload_button = Button(root, font=f_text, text="Upload Image", bg="#3B185F", fg="white", command=upload_image)
upload_button.place(x=220, y=402)

btn = Button(root, font = f_text, text="SUBMIT", bg="#3B185F", fg="white", command=fun)
btn.place(x=180,y=470)
btn_login = Button(root, font = f_text, text="LOGIN", bg="#3B185F", fg="white", command=login)
btn_login.place(x=350,y=470)
root.mainloop()