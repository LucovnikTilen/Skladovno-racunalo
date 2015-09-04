# Skladovno-racunalo
from tkinter import *
class Racunalo():#glej rpn calculator
    def __init__(self, master):


        


        nadime = Label(text = "Računalo")
        nadime.grid(row = 4, column = 0)

        
        self.vpis = DoubleVar(master, value=0)#to je število, ki ga vpišemo
        self.vpis2 = DoubleVar(master, value=0)
        self.vpis3 = DoubleVar(master, value=0)
        self.vpis4 = DoubleVar(master, value=0)

        vpisno_polje = Entry(master, textvariable = self.vpis)
        vpisno_polje.grid(row = 3, column = 0)
        ime = Label(text = " Y 2000")
        ime.grid(row = 5, column = 0)

        vpisno_polje2 = Entry(master, textvariable = self.vpis2)
        vpisno_polje2.grid(row = 2, column = 0)

        vpisno_polje3 = Entry(master, textvariable = self.vpis3)
        vpisno_polje3.grid(row = 1, column = 0)

        vpisno_polje4 = Entry(master, textvariable = self.vpis4)
        vpisno_polje4.grid(row = 0, column = 0)        
        
        gumbPlusMinus = Button(master, text = "     +/-      ", command = self.PlusMinus)
        gumbPlusMinus.grid(row = 2, column = 1)


        gumbPlus = Button(master, text = "       +        ", command = self.plus)
        gumbPlus.grid(row = 0, column = 1)

        gumbMinus = Button(master, text = "       -      ", command = self.minus)
        gumbMinus.grid(row = 0, column = 2)

        gumbKrat = Button(master, text = "       *         ", command = self.krat)
        gumbKrat.grid(row = 1, column = 1)

        gumbDeljeno = Button(master, text = "       /      ", command = self.deljeno)
        gumbDeljeno.grid(row = 1, column = 2)

        gumbPotenca = Button(master, text = "Potenca ", command = self.potenca)
        gumbPotenca.grid(row = 2, column = 2)

        gumbKvadrat = Button(master, text = " Kvadrat   ", command = self.kvadrat)
        gumbKvadrat.grid(row = 3, column = 1)

        gumbKoren = Button(master, text = "   Koren  ", command = self.koren)
        gumbKoren.grid(row = 3, column = 2)

        gumbObratna = Button(master, text = "    1 / x    ", command = self.obratna)
        gumbObratna.grid(row = 4, column = 2)

        gumbZamenjaj = Button(master, text = "Zamenjaj ", command = self.zamenjaj)
        gumbZamenjaj.grid(row = 4, column = 1)

        master.bind("<Return>", self.enter)
        vpisno_polje.bind("<Key>", self.pritisni_gumb)
        gumbEnter = Button(master, text = "    Enter     ", command = self.enter)
        gumbEnter.grid(row = 5, column = 1)

        gumbAc = Button(master, text = "    AC      ", command = self.ac)
        gumbAc.grid(row = 5, column = 2)

    def pritisni_gumb(self, event):
        if event.char == '+':
            self.plus()
            return "break"
        elif event.char == '-':
            self.minus()
            return "break"
        elif event.char == '*':
            self.krat()
            return "break"
        elif event.char == '/':
            self.deljeno()
            return "break"
        elif event.char == 'n':
            self.PlusMinus()
            return "break"
        elif event.char == 'r':
            self.koren()
            return "break"
        elif event.char == 's':
            self.kvadrat()
            return "break"
        elif event.char == 'c':
            self.ac()
            return "break"
        elif event.char == 'z':
            self.zamenjaj()
            return "break"
        elif event.char == 'o':
            self.obratna()
            return "break"
        elif event.char == 'p':
            self.potenca()
            return "break"   



    def plus(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        z = self.vpis3.get()
        u = self.vpis4.get()
        self.vpis.set(x + y)
        self.vpis2.set(z)
        self.vpis3.set(u)
        self.vpis4.set(0)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} + {1} = {2}".format(y, x, x+y),file=ut)

    def minus(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        z = self.vpis3.get()
        u = self.vpis4.get()
        self.vpis.set(y - x)
        self.vpis2.set(z)
        self.vpis3.set(u)
        self.vpis4.set(0)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} - {1} = {2}".format(y, x, y-x),file=ut)

    def krat(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        z = self.vpis3.get()
        u = self.vpis4.get()
        self.vpis.set(x * y)
        self.vpis2.set(z)
        self.vpis3.set(u)
        self.vpis4.set(0)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} * {1} = {2}".format(y, x, y*x),file=ut)

    def deljeno(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        z = self.vpis3.get()
        u = self.vpis4.get()
        if x == 0:
            self.vpis.set("Infinity")
            self.vpis2.set(z)
            self.vpis3.set(u)
            self.vpis4.set(0)
            with open("zgodovina.txt", "a",encoding="utf8") as ut:
                print ("{0} / {1} = Infinity".format(y, x),file=ut)
        else:
            self.vpis.set(y / x)
            self.vpis2.set(z)
            self.vpis3.set(u)
            self.vpis4.set(0)
            with open("zgodovina.txt", "a",encoding="utf8") as ut:
                print ("{0} / {1} = {2}".format(y, x, y/x),file=ut)

    def enter(self, *args):
        a = self.vpis.get()
        b = self.vpis2.get()
        c = self.vpis3.get()
        self.vpis2.set(a)
        self.vpis3.set(b)
        self.vpis4.set(c)
        self.vpis.set(0)

    def ac(self):
        self.vpis.set(0)
        self.vpis2.set(0)
        self.vpis3.set(0)
        self.vpis4.set(0)

    def PlusMinus(self):
        a = self.vpis.get()
        self.vpis.set(-a)

    def potenca(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        z = self.vpis3.get()
        u = self.vpis4.get()
        self.vpis.set(y ** x)
        self.vpis2.set(z)
        self.vpis3.set(u)
        self.vpis4.set(0)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} ^ {1} = {2}".format(y, x, y**x),file=ut)

    def kvadrat(self):
        x = self.vpis.get()
        self.vpis.set(x ** 2)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} ^ 2.0 = {1}".format(x, x ** 2),file=ut)

    def koren(self):
        x = self.vpis.get()
        self.vpis.set(x ** 0.5)
        with open("zgodovina.txt", "a",encoding="utf8") as ut:
            print ("{0} ^ 0.5 = {1}".format(x, x ** 0.5),file=ut)

    def obratna(self):
        x = self.vpis.get()
        if x == 0:
            self.vpis.set("Infinity")
            with open("zgodovina.txt", "a",encoding="utf8") as ut:
                print ("1.0 / {0} = Infinity".format(x),file=ut)
        else:
            self.vpis.set(1 / x)
            with open("zgodovina.txt", "a",encoding="utf8") as ut:
                print ("1 / {0} = {1}".format(x, 1 / x),file=ut)

    def zamenjaj(self):
        x = self.vpis.get()
        y = self.vpis2.get()
        self.vpis.set(y)
        self.vpis2.set(x)


    
root = Tk()

aplikacija = Racunalo(root)

root.mainloop
