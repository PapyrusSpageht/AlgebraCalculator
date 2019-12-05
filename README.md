from tkinter import * 
import random as r
import re
win = Tk()
win.geometry("425x350")

def solveAlgebra():
    try:
        equ=qEntry.get()
        if "." in equ:
            aAns.config(text="Please don't use decimals")
        elif "." not in equ:
            match = re.match(r"(\d+)x\+(\d+)=(\d+)", equ)
            m, c, y = match.groups()
            m, c, y = float(m), float(c), float(y) # Convert from strings to numbers
            x = (y-c)/m
            aAns.config(text="x = %f" % x)
            aAns.grid(row=3,column=1)
            fo=open("calculator.txt", "a")
            fo.write(qEntry.get() + "\n" + aAns.cget("text") + "\n"+ "\n")
            fo.close()
    except:
        aAns.config(text="ERROR. USE FORMAT (ax+b=c) \n WITH ONLY INTEGERS")
        print('ERROR. USE FORMAT (ax+b=c).')
    
        
def solveSimple():
    try:
        equ=qEntry.get()
        if "." in equ:
            aAns.config(text="Please don't use decimals")
        elif "." not in equ:
            match = re.match(r"(\d+)\+(\d+)", equ)
            m, c= match.groups()
            m, c= float(m), float(c)
            x=m+c
            aAns.config(text= m+c)
            fo=open("calculator.txt", "a")
            fo.write(qEntry.get() + " = " + str(aAns.cget("text")) + "\n" + "\n")
            fo.close()
    except:
        aAns.config(text="ERROR. USE FORMAT (a+b) \n WITH ONLY INTEGERS")
        print("ERROR. USE FORMAT (a+b)")
    

def randomFact():
    funFact.config(text=funFactList[r.randint(0,2)])

qLabel = Label(win,text="Question: ")
qLabel.grid(row=1,column=0,columnspan=1,sticky=E)
qLabel.config(font=("Papyrus",25),bg="#42f5ce")

qEntry = Entry(win)
qEntry.grid(row=1,column=1)
qEntry.config(font=("Helvetica",15),bg="#42f5ce")


aAns = Label(win, text="")
aAns.grid(row=3,column=1)
aAns.config(font=("Helvetica",15),bg="#42f5ce")


aLabel = Label(win,text="Answer: ")
aLabel.grid(row=3,column=0,columnspan=1,sticky=E)
aLabel.config(font=("Papyrus",25),bg="#42f5ce")
'''
goBtn = Button(win, text = "GO", command=solveAlgebra, highlightbackground='#34e1eb')
goBtn.grid(row=5,column=0,columnspan=2)
goBtn.config(height=5,width=20)
'''

funFactList=["Did you know that the favourite number \n of 10% of the population is 7?","Did you know that in a crowded room, 2 people \n probably share a birthday?", "The word hundred comes from the old Norse term, \n hundrath, which actually means 120 and not 100?"]

funFact=Label(win,text=funFactList[r.randint(0,2)])
funFact.grid(row=6,column=0,columnspan=2)
funFact.config(font=("Papyrus",15),bg="#42f5ce")


simpleBtn=Button(win,text="Simple",command = solveSimple, highlightbackground='#34e1eb')
simpleBtn.grid(row=7,column=0)
simpleBtn.config(height=5,width=20)


algebraBtn=Button(win,text="Algebra",command = solveAlgebra, highlightbackground='#34e1eb')
algebraBtn.grid(row=7,column=1)
algebraBtn.config(height=5,width=20)

funFactBtn=Button(win,text="Fun Fact",command = randomFact, highlightbackground='#34e1eb')
funFactBtn.grid(row=8,column=0)
funFactBtn.config(height=5,width=20)

quitBtn=Button(win,text="Quit",command = quit, highlightbackground='#34e1eb')
quitBtn.grid(row=8,column=1)
quitBtn.config(height=5,width=20)

win.configure(background='#42f5ce')

win.mainloop()
