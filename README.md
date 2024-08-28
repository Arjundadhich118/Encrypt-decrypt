# Encrypt-decrypt
Encryption and Decription is a cryptographic tool used by cyber security experts to confuse or to astray the user who wants to crack the 
passwords. Basically it is used to convert the passwords in cryptographic form which is only crack by owner.

# Encrypt-Decrypt:
# Import the module for GUI
import tkinter as tk


# Initialising the font type and size
FONT = ("timesnewroman", 25, "bold")



class CaesarCypherGUI:
    def __init__(self, master):


        # Title for the window
        master.title("Encode and decode messages")


        # String type for plaintext and cyphertext
        self.plaintext = tk.StringVar(master, value="")
        self.cyphertext = tk.StringVar(master, value="")


        # Integer value for the key
        self.key = tk.IntVar(master)


        # Plaintext GUI and controls
        self.plain_label = tk.Label(master, text="Plaintext", fg="green", font=FONT).grid(row=0, column=0)
        self.plain_entry = tk.Entry(master, textvariable=self.plaintext, width=40, font=FONT)
        self.plain_entry.grid(row=0, column=1, padx=20)


        # Button constructs a button
        self.encrypt_button = tk.Button(master, text="Encrypt", command=lambda: self.encrypt_callback(), font=FONT).grid(row=0, column=2)
        self.plain_clear = tk.Button(master, text="Clear", command=lambda: self.clear('Plain'), font=FONT).grid(row=0, column=3)


        # Key controls
        self.key_label = tk.Label(master, text="Key", font=FONT).grid(row=1, column=0)
        self.key_entry = tk.Entry(master, textvariable=self.key, width=10, font=FONT).grid(row=1, column=1, sticky=tk.W, padx=20)


        # Cyphertext controls
        self.cypher_label = tk.Label(master, text="Cyphertext", fg="red", font=FONT).grid(row=2, column=0)
        self.cypher_entry = tk.Entry(master, textvariable=self.cyphertext, width=40, font=FONT)
        self.cypher_entry.grid(row=2, column=1, padx=20)
        self.decrypt_button = tk.Button(master, text="Decrypt", command=lambda: self.decrypt_callback(), font=FONT).grid(row=2, column=2)
        self.cypher_clear = tk.Button(master, text="Clear", command=lambda: self.clear('Cypher'), font=FONT).grid(row=2, column=3)


    # Defination of clear function
    def clear(self, str_val):
        if str_val == 'cypher':
            self.cypher_entry.delete(0, 'end')
        elif str_val == 'plain':
            self.plain_entry.delete(0, 'end')


    # Defination of key function
    def get_key(self):
        try:
            key_val = self.key.get()
            return key_val
        except tk.TclError:
            pass


    # Encryption method
    def encrypt_callback(self):
        key = self.get_key()
        cyphertext = encrypt(self.plain_entry.get(), key)
        self.cypher_entry.delete(0, tk.END)
        self.cypher_entry.insert(0, cyphertext)


    # Decryption method
    def decrypt_callback(self):
        key = self.get_key()
        plaintext = decrypt(self.cypher_entry.get(), key)
        self.plain_entry.delete(0, tk.END)
        self.plain_entry.insert(0, plaintext)


# Encryption formula of Caeser cipher
def encrypt(plaintext, key):
    cyphertext = ""
    for char in plaintext.upper():
        if char.isalpha():
            cyphertext += chr((ord(char) + key - 65) % 26 + 65)
        else:
            cyphertext += char
    return cyphertext


# Decryption formula of Caser cipher
def decrypt(cyphertext, key):
    plaintext = ""
    for char in cyphertext.upper():
        if char.isalpha():
            plaintext += chr((ord(char) - key - 65) % 26 + 65)
        else:
            plaintext += char
    return plaintext


# Run the program
if __name__ == "__main__":
    root = tk.Tk()
    caesar = CaesarCypherGUI(root)
    root.mainloop()
    root.mainloop()
