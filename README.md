import mysql.connector;
from tkinter import *
gui = Tk()
gui.title('GUI')
gui.geometry("400x400")
#gui.attributes("-fullscreen",True)

btn = Button(gui,text="First Python Button",
             activebackground='Blue',
             activeforeground="white",
             borderwidth=10,
             relief=SOLID,
             font=('times new roman',10,'italic'),
             bg='gold',fg='red')
#gui.mainloop()


db = mysql.connector.connect(
    host = "127.0.0.1",
    user = "root",
    password = "admin"
    )
cur = db.cursor();
cur.execute("create database IF NOT EXISTS inventory_management");
cur.execute("use inventory_management")
cur.execute("create table if not exists inventory (id INT AUTO_INCREMENT PRIMARY KEY, Part_No VARCHAR(255), Item_Name VARCHAR(255), Item_Description VARCHAR(255), Total_Quantity VARCHAR(200), Balance_Quantity VARCHAR(200), Issue_To VARCHAR(200))")

def search(var1, var2):
    global cur
#    if var1 == "Part_No":
        
#         cur.execute("select * from inventory")
#     else:
    print(f"this is var1 {var1}")
    print(f"this is var2 {var2}")
    cur.execute(f"select * from inventory where {var1} = {var2}")
    
        
    for i in cur:
        print(i)
        print("yes")
    print("yes")
    

def show_inventory():
    res = input("Search Item by \na. ) Part_No \nb. ) Item_Name \nc. ) Description \nd. ) Issue_To \ne. ) All Items \n   ")
    if res == "a":
        no = input("Enter Part Number \n   ")
        part_no = "Part_No"
        search(part_no, no)
        print("a")
    elif res == "b":
        no = input("Enter Item Name \n   ")
        Name = "Item_Name"
        search(Name, no)
        print("b")
    elif res == "c":
        no = input("Enter Item Description \n   ")
        search(Description, no)
        print("c")
    elif res == "d":
        no = input("Enter Item Issued to \n   ")
        search(Issue_To, no)
        print("d")
    elif res == "e":
        search(0,0) 
    else:
        print("enter a valid command ")
#         

def add_item():
    global cur
    part_no = input("Enter Part Number \n   ");
    name = input("Enter Item Name \n   ");
    description = input("Enter Item Description \n   ");
    total = input("Enter Total Quantity \n   ");

    #cur.execute(f"INSERT INTO inventory (Part_No, Item_Name, Item_Description, Total_Quantity) VALUES ('{po}', '{description}', '{total}', '{name}')")
    cur.execute(f"INSERT INTO inventory (Part_No, Item_Name, Item_Description, Total_Quantity) VALUES ('{part_no}', '{name}', '{description}', '{total}')")    




while True:
    print()
    res = input("""1.) Show Inventory \n2.) ADD Item \n3.) Delete Item \n4.) Update Item \n   """);
    if res == "1":
        show_inventory();
        print("check")
    elif res == "2":
        add_item();

        db.commit();
        print("Data Successfully Added");
    elif res == "3":
        #delete_item();
        print("delete")
    elif res == "4":
        #update_item();
        print("update")
    


