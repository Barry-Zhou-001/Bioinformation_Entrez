from Bio import Entrez
import tkinter as tk
import tkinter.messagebox
import os
from Bio import SeqIO
 
root = tk.Tk()
root.title("Entrez")
root.geometry('350x300')

var1 = tk.DoubleVar()
label1 = tk.Label(text="Database", width=40, height=2)
label1.pack()
entry1 = tk.Entry(width=40)
entry1.pack()

var2 = tk.StringVar()
label2 = tk.Label(text="Term", width=20, height=2)
label2.pack()
entry2 = tk.Entry(width=40,)
entry2.pack()

var3 = tk.DoubleVar()
label3 = tk.Label(text="ID", width=20, height=2)
label3.pack()
entry3 = tk.Entry(width=40)
entry3.pack()
 
def FindID():
    global var1
    global var2
    global var3
    var1 = entry1.get()
    var2 = entry2.get()
    handle = Entrez.esearch(db="%s"%var1, term="%s"%var2)
    record = Entrez.read(handle)
    global rlist
    rlist = record["IdList"]
    length = len(rlist)
    root2 = tk.Tk()
    root2.title("identity")
    text1 = tk.Text(root2,width=60,height=30)
    text1.insert(tk.INSERT,'共有序列%s个  \n'%length )
    text1.insert(tk.END,'%s'%rlist)
    text1.pack()
    root2.mainloop()
    
def FindContent():
    global var1
    global var3
    var1 = entry1.get()
    var3 = int(entry3.get())
    Content = Entrez.efetch(db="%s"%var1, id="%s"%var3, rettype="gb", retmode="gb")
    Content_Str = Content.read()
    root3 = tk.Tk()
    root3.title("content")
    text2 = tk.Text(root3,width=100,height=50)
    text2.insert(tk.INSERT,'%s'%Content_Str)
    text2.pack()
    root3.mainloop()

def download():
    var1 = entry1.get()
    var2 = entry2.get()
    handle = Entrez.esearch(db="%s"%var1, term="%s"%var2)
    record = Entrez.read(handle)
    rlist = record["IdList"]
    #Entrez.email = "A.N.Other@example.com" 
    filename = "id_%s.gbk" % rlist[0]
    filenames = [filename]
    for i in range (1,len(rlist)):
        filename = "id_%s.gbk" % rlist[i]
        filenames.append(filename)
    for i in range (0,len(rlist)):
        if not os.path.isfile(filenames[i]):
        # Downloading...
            net_handle = Entrez.efetch(db="%s"%var1,id=rlist[i],rettype="gb", retmode="gb")
            out_handle = open(filenames[i],"w",encoding='utf8')
            out_handle.write(net_handle.read())
            out_handle.close()
            net_handle.close()
            print("Saved%s"%i)
    tkinter.messagebox.showinfo('提示','下载完成')

button1 = tk.Button(text="查询ID" ,width=10, height=2, command=FindID)
button1.pack(padx=25, pady=10, side="left")
button2 = tk.Button(text="查询内容" ,width=10, height=2, command=FindContent)
button2.pack(padx=20, pady=10, side="left")
button3 = tk.Button(text="全部下载" ,width=10, height=2, command=download)
button3.pack(padx=20, pady=10, side="left")

root.mainloop()
