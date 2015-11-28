# miniproject
#submitted by "suyash makhloga"
from tkinter import *
from tkinter import ttk
import tkinter.messagebox
import csv
import tkinter.scrolledtext as tkst
import matplotlib.pyplot as plt
#####################################################################################
def fetch_names():
    x=variable.get()
    loc='Baby Names 1944-2013//'+x
    loc=loc+'_cy'+y_1_e.get()+'_top.csv'
    file=open(loc,'r')
    j=0
    a='\nLIST OF TOP '
    a=a+(s_1_e.get()).upper()+' '+x.upper()+' NAMES IN THE YEAR '+y_1_e.get()+'\n\n'
    list_fetch.insert(INSERT,a)
    for i in file:
        if j==0:
            j=j+1
            continue
        elif j<=int(s_1_e.get()):
            j=j+1
            x=i.split(',')
            x1=x[0]
            x2=x[1]
            x1=x1.split('"')[1]
            x2=x2.split('"')[1]
            z=str(j-1)+'   '+x1+'   '+x2+'   '+'\n'
            list_fetch.insert(INSERT,z)
        else:
            break
    file.close()
def extract():
    cl=0
    cl2=0
    
    if y_1_e.get()=='':
        messagebox.showinfo(message='enter a year')
    elif int(y_1_e.get())<1944 and (y_1_e.get()>2013):
        messagebox.showinfo(message='year record not present')
    else:
        cl=1
        
    if s_1_e.get()=='':
        messagebox.showinfo(message='enter the number of names in show')
    else:
        cl2=1

    if cl==1 and cl2==1:
        fetch_names()
def plot():
    x=variable2.get()
    loc='Baby Names 1944-2013//'+x
    y=int(y_2_e.get())
    j=0
    year=[] 
    amount=[]
    while y<=2013:
        year.append(y)
        loc2=loc+'_cy'+str(y)+'_top.csv'
        file=open(loc2,'r')
        file_read=csv.reader(file)
        count=0
        for i in file_read:
            if i[0]==n_2_e.get().upper():
                count=1
                ip=i[1]
                amount.append(int(ip))
                break
        y=y+1
    plt.title('POPULARITY GRAPH OF "%s" FROM THE YEAR %d TO 2013' %(n_2_e.get().upper(),int(y_2_e.get())))
    plt.xlabel('NO. OF CHILDREN')
    plt.ylabel('YEAR')
    plt.plot(year,amount)
    plt.show()
def graph():
    cl=0
    cl2=0
    
    if y_2_e.get()=='':
        messagebox.showinfo(message='enter a year')
    elif int(y_2_e.get())<1944 and (y_2_e.get()>2013):
        messagebox.showinfo(message='year record not present')
    else:
        cl=1
        
    if n_2_e.get()=='':
        messagebox.showinfo(message='enter the number of names in show')
    else:
        cl2=1

    if cl==1 and cl2==1:
        plot()
def res():
    list_fetch.delete("1.0",END)
    empty=0
#####################################################################################  
root=Tk()
root.resizable(0,0)
a=''
lst_year=[]
lst_count=[]
lst_count2=[]
g_1=Label(root, text='Check for', font='bold')
variable = StringVar(root)
variable.set("male")
g_1_o = OptionMenu(root, variable, "male", "female")
y_1=Label(root, text='Year', font='bold')
y_1_e=Entry(root)
s_1=Label(root, text='Show', font='bold')
s_1_e=Entry(root)
sub_1=Button(root, text='Submit', command=extract, font='bold')
rst=Button(root, text='RESET', command=res, font='bold')
list_fetch = tkst.ScrolledText(master=root, wrap=WORD, width=50, height=10, font='bold')
g_2=Label(root, text='Check for', font='bold')
variable2 = StringVar(root)
variable2.set("male")
g_2_o = OptionMenu(root, variable, "male", "female")
y_2=Label(root, text='Year', font='bold')
y_2_e=Entry(root)
n_2=Label(root, text='Name', font='bold')
n_2_e=Entry(root)
s_2=Button(root, text='Submit', command=graph, font='bold')

g_1.grid(row=0, column=0, pady=10, sticky=E)
g_1_o.grid(row=0, column=1)
y_1.grid(row=0, column=2, pady=10, sticky=E)
y_1_e.grid(row=0, column=3, pady=10, padx=20)
s_1.grid(row=0, column=4, pady=10, sticky=E)
s_1_e.grid(row=0, column=5, pady=10, padx=20)
sub_1.grid(row=0, column=6, pady=10, padx=10, sticky=E)
rst.grid(row=0, column=7)
list_fetch.grid(row=1, column=0, columnspan=7, rowspan=10)
g_2.grid(row=12, column=0, pady=10, sticky=E)
g_2_o.grid(row=12, column=1)
y_2.grid(row=12, column=2, pady=10, sticky=E)
y_2_e.grid(row=12, column=3, pady=10, padx=20)
n_2.grid(row=12, column=4, pady=20, sticky=E)
n_2_e.grid(row=12, column=5)
s_2.grid(row=12, column=6)
