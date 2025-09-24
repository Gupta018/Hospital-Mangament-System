from tkinter import *
from tkinter import ttk, messagebox
import mysql.connector

class Hospital:
    def __init__(self, root):
        self.root = root
        self.root.title("Hospital Management System")
        self.root.geometry("1540x800+0+0")   

        # Variables
        self.Nameoftablets=StringVar()
        self.ref=StringVar()
        self.Dose=StringVar()
        self.NumberOfTablets=StringVar()
        self.Lot=StringVar()
        self.Issuedate=StringVar()
        self.ExpDate=StringVar()
        self.DaliyDose=StringVar()
        self.sideEffect=StringVar()
        self.FurtherInformation=StringVar()
        self.StorageAdvice=StringVar()
        self.DrivingUsingMachine=StringVar()
        self.HowToUseMedine=StringVar()
        self.PatientId=StringVar()
        self.nhsNumber=StringVar()
        self.PatientName=StringVar()
        self.DateOfBirth=StringVar()
        self.PatientAddress=StringVar()

        # Title
        lbtitle = Label(self.root, bd=20, relief=RIDGE,
                        text="HOSPITAL MANAGEMENT SYSTEM", fg="red", bg="white",
                        font=("times new roman", 50, "bold"))
        lbtitle.pack(side=TOP, fill=X)

        # DataFrame
        Dataframe = Frame(self.root, bd=20, relief=RIDGE)
        Dataframe.place(x=0, y=130, width=1530, height=400)  
        
        DataframeLeft=LabelFrame(Dataframe, bd=10, relief=RIDGE, padx=10,
                                 font=("times new roman", 12, "bold"), text="Patient Information")
        DataframeLeft.place(x=0, y=5, width=980, height=350)

        DataframeRight=LabelFrame(Dataframe, bd=10, relief=RIDGE, padx=10,
                                  font=("times new roman", 12, "bold"), text="Prescription")
        DataframeRight.place(x=990, y=5, width=450, height=350)

        # Buttons Frame
        Buttonframe = Frame(self.root, bd=20, relief=RIDGE)
        Buttonframe.place(x=0, y=530, width=1530, height=70)

        # Details Frame (Table)
        Detailsframe = Frame(self.root, bd=20, relief=RIDGE)
        Detailsframe.place(x=0, y=600, width=1530, height=190)

        # -------- DataFrameLeft Widgets --------
        Label(DataframeLeft, text="Name of Tablet", font=("times new roman", 12, "bold")).grid(row=0, column=0)
        comNametablet=ttk.Combobox(DataframeLeft, textvariable=self.Nameoftablets, state='readonly',
                                   font=("times new roman", 12, "bold"), width=33)
        comNametablet["values"]=("Nice","Corona Vaccine","Acetaminophen","Adderall","Amlodipine","Ativen")
        comNametablet.grid(row=0,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Reference No:").grid(row=1,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.ref,width=35).grid(row=1,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Dose:").grid(row=2,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.Dose,width=35).grid(row=2,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="No Of Tablets:").grid(row=3,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.NumberOfTablets,width=35).grid(row=3,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Lot:").grid(row=4,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.Lot,width=35).grid(row=4,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Issue Date:").grid(row=5,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.Issuedate,width=35).grid(row=5,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Exp Date:").grid(row=8,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.ExpDate,width=35).grid(row=8,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Daily Dose:").grid(row=6,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.DaliyDose,width=35).grid(row=6,column=1)

        Label(DataframeLeft,font=("arial",12,"bold"),text="Side Effect:").grid(row=7,column=0,sticky=W)
        Entry(DataframeLeft,font=("arial",12,"bold"),textvariable=self.sideEffect,width=35).grid(row=7,column=1)

        # -------- DataFrameRight (Prescription Box) --------
        self.txtPrescription=Text(DataframeRight,font=("arial",12,"bold"),width=45,height=16)
        self.txtPrescription.grid(row=0,column=0)

        # -------- Buttons --------
        Button(Buttonframe, text="Prescription", bg="green", fg="white", font=("arial", 12, "bold"),
               width=24, height=2, command=self.generate_prescription).grid(row=0,column=0)
        Button(Buttonframe, text="Prescription Data", bg="green", fg="white", font=("arial", 12, "bold"),
               width=24, height=2, command=self.iPrescriptionData).grid(row=0,column=1)
        Button(Buttonframe, text="Update", bg="green", fg="white", font=("arial", 12, "bold"),
               width=24, height=2, command=self.update_data).grid(row=0,column=2)
        Button(Buttonframe, text="Delete", bg="green", fg="white", font=("arial", 12, "bold"),
               width=23, height=2, command=self.delete_data).grid(row=0,column=3)
        Button(Buttonframe, text="Clear", bg="green", fg="white", font=("arial", 12, "bold"),
               width=24, height=2, command=self.clear_data).grid(row=0,column=4)
        Button(Buttonframe, text="Exit", bg="green", fg="white", font=("arial", 12, "bold"),
               width=24, height=2, command=self.root.destroy).grid(row=0,column=5)

        # -------- Table with Scrollbars --------
        scroll_x=ttk.Scrollbar(Detailsframe,orient=HORIZONTAL)
        scroll_y=ttk.Scrollbar(Detailsframe,orient=VERTICAL)
        self.hospital_table=ttk.Treeview(Detailsframe,column=("nameoftablets","ref","dose","nooftablets","lot","issuedate",
                                              "expdate","dailydose","storage","nhsnumber","pname","dob","address"),
                                         xscrollcommand=scroll_x.set, yscrollcommand=scroll_y.set)

        scroll_x.pack(side=BOTTOM, fill=X)
        scroll_y.pack(side=RIGHT, fill=Y)
        scroll_x.config(command=self.hospital_table.xview)
        scroll_y.config(command=self.hospital_table.yview)

        self.hospital_table.heading("nameoftablets", text="Name of Tablets")
        self.hospital_table.heading("ref", text="Reference No")
        self.hospital_table.heading("dose", text="Dose")
        self.hospital_table.heading("nooftablets", text="No of Tablets")
        self.hospital_table.heading("lot", text="Lot")
        self.hospital_table.heading("issuedate", text="Issue Date")
        self.hospital_table.heading("expdate", text="Exp Date")
        self.hospital_table.heading("dailydose", text="Daily Dose")
        self.hospital_table.heading("storage", text="Storage")
        self.hospital_table.heading("nhsnumber", text="NHS Number")
        self.hospital_table.heading("pname", text="Patient Name")
        self.hospital_table.heading("dob", text="DOB")
        self.hospital_table.heading("address", text="Address")
        self.hospital_table["show"]="headings"

        for col in self.hospital_table["columns"]:
            self.hospital_table.column(col, width=100)
        self.hospital_table.pack(fill=BOTH,expand=1)

        self.fetch_data()

    # ---------- Functionalities -----------

    def iPrescriptionData(self):
        if self.Nameoftablets.get() == "" or self.ref.get() == "":
            messagebox.showerror("Error", "All fields are required")
            return
        conn = mysql.connector.connect(host="127.0.0.1", user="root", password="Gupta@123", database="myData")
        my_cursor = conn.cursor()
        my_cursor.execute("""
            INSERT INTO hospital 
            (nameoftablets, ref, dose, nooftablets, lot, issuedate, expdate, dailydose, storage, nhsnumber, pname, dob, address)
            VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)
        """, (
            self.Nameoftablets.get(),
            self.ref.get(),
            self.Dose.get(),
            self.NumberOfTablets.get(),
            self.Lot.get(),
            self.Issuedate.get(),
            self.ExpDate.get(),
            self.DaliyDose.get(),
            self.StorageAdvice.get(),
            self.nhsNumber.get(),
            self.PatientName.get(),
            self.DateOfBirth.get(),
            self.PatientAddress.get()
        ))
        conn.commit()
        conn.close()
        self.fetch_data()
        messagebox.showinfo("Success", "Record has been inserted successfully")

    def fetch_data(self):
        conn = mysql.connector.connect(host="127.0.0.1", user="root", password="Gupta@123", database="myData")
        my_cursor = conn.cursor()
        my_cursor.execute("SELECT * FROM hospital")
        rows = my_cursor.fetchall()
        if len(rows) != 0:
            self.hospital_table.delete(*self.hospital_table.get_children())
            for row in rows:
                self.hospital_table.insert("", END, values=row)
        conn.close()

    def clear_data(self):
        self.Nameoftablets.set("")
        self.ref.set("")
        self.Dose.set("")
        self.NumberOfTablets.set("")
        self.Lot.set("")
        self.Issuedate.set("")
        self.ExpDate.set("")
        self.DaliyDose.set("")
        self.sideEffect.set("")
        self.StorageAdvice.set("")
        self.nhsNumber.set("")
        self.PatientName.set("")
        self.DateOfBirth.set("")
        self.PatientAddress.set("")
        self.txtPrescription.delete("1.0", END)

    def generate_prescription(self):
        self.txtPrescription.delete("1.0", END)
        self.txtPrescription.insert(END, f"Tablet Name: {self.Nameoftablets.get()}\n")
        self.txtPrescription.insert(END, f"Reference No: {self.ref.get()}\n")
        self.txtPrescription.insert(END, f"Dose: {self.Dose.get()}\n")
        self.txtPrescription.insert(END, f"No of Tablets: {self.NumberOfTablets.get()}\n")
        self.txtPrescription.insert(END, f"Lot: {self.Lot.get()}\n")
        self.txtPrescription.insert(END, f"Issue Date: {self.Issuedate.get()}\n")
        self.txtPrescription.insert(END, f"Exp Date: {self.ExpDate.get()}\n")
        self.txtPrescription.insert(END, f"Daily Dose: {self.DaliyDose.get()}\n")
        self.txtPrescription.insert(END, f"Storage Advice: {self.StorageAdvice.get()}\n")
        self.txtPrescription.insert(END, f"Patient Name: {self.PatientName.get()}\n")
        self.txtPrescription.insert(END, f"DOB: {self.DateOfBirth.get()}\n")
        self.txtPrescription.insert(END, f"Address: {self.PatientAddress.get()}\n")

    # Optional: Implement delete & update
    def delete_data(self):
        selected = self.hospital_table.focus()
        values = self.hospital_table.item(selected, 'values')
        if not selected:
            messagebox.showerror("Error", "Select a record to delete")
            return
        conn = mysql.connector.connect(host="127.0.0.1", user="root", password="Gupta@123", database="myData")
        my_cursor = conn.cursor()
        my_cursor.execute("DELETE FROM hospital WHERE ref=%s", (values[1],))
        conn.commit()
        conn.close()
        self.fetch_data()
        messagebox.showinfo("Success", "Record deleted successfully")

    def update_data(self):
        selected = self.hospital_table.focus()
        values = self.hospital_table.item(selected, 'values')
        if not selected:
            messagebox.showerror("Error", "Select a record to update")
            return
        conn = mysql.connector.connect(host="127.0.0.1", user="root", password="Gupta@123", database="myData")
        my_cursor = conn.cursor()
        my_cursor.execute("""
            UPDATE hospital SET 
            nameoftablets=%s, dose=%s, nooftablets=%s, lot=%s, issuedate=%s, expdate=%s, dailydose=%s, storage=%s, nhsnumber=%s, pname=%s, dob=%s, address=%s
            WHERE ref=%s
        """, (
            self.Nameoftablets.get(),
            self.Dose.get(),
            self.NumberOfTablets.get(),
            self.Lot.get(),
            self.Issuedate.get(),
            self.ExpDate.get(),
            self.DaliyDose.get(),
            self.StorageAdvice.get(),
            self.nhsNumber.get(),
            self.PatientName.get(),
            self.DateOfBirth.get(),
            self.PatientAddress.get(),
            self.ref.get()
        ))
        conn.commit()
        conn.close()
        self.fetch_data()
        messagebox.showinfo("Success", "Record updated successfully")


# Run the application
root = Tk()
ob = Hospital(root)
root.mainloop()
