from tkinter import *

import mysql.connector

class Tinder:

    def __init__(self):

        ()#database connection
        self.conn=mysql.connector.connect(host="localhost", user="root", password="", database="tinder")
        self.mycursor=self.conn.cursor()

        self.root=Tk()

        self.root.title("TINDER")

        self.root.minsize(600, 400)
        self.root.maxsize(600, 400)

        self.destroyWindow()
        Label(text="Already a member!!!Log In Here!", fg="green").grid(row=0, column=0)

        Label(text="Enter Email").grid(row=1,column=0)
        self.emailInput=Entry()
        self.emailInput.grid(row=1,column=1)

        Label(text="Enter Password").grid(row=2,column=0)
        self.passwordInput=Entry()
        self.passwordInput.grid(row=2,column=1)

        Button(text="Login", command=lambda : self.login()).grid(row=3,column=0)

        self.message=Label(text="", fg="red")
        self.message.grid(row=4,column=0)

        Label(text="Not a member?Register here!", fg="green").grid(row=5,column=0)
        Button(text="Register Here", command=lambda : self.launchRegWindow()).grid(row=6,column=0)


        self.root.mainloop()

    def login(self):

        self.mycursor.execute("""SELECT * FROM `user` WHERE `email` LIKE '{}' AND `password` LIKE '{}'""".format(self.emailInput.get(),self.passwordInput.get()))

        response = self.mycursor.fetchall()

        if len(response)>0:
            self.message.configure(text="Welcome User")
            Label(text="For user menu Click Here!!", fg="blue").grid(row=8,column=0)
            Button(text="User Menu", command=lambda : self.launchUserMenu()).grid(row=9,column=0)
            Label(text="To Log Out Click Here!!", fg="blue").grid(row=10, column=0)
            Button(text="LOG OUT", command=lambda : self.launchLogOut()).grid(row=11, column=0)
            self.current_user_id = response[0][0]

        else:
            self.message.configure(text="Incorrect email/password")

    def launchRegWindow(self):

        self.destroyWindow()
        Label(text="Register").grid(row=0,column=0)

        self.conn = mysql.connector.connect(host="localhost", user="root", password="", database="tinder")
        self.mycursor = self.conn.cursor()

        Label(text="Full Name").grid(row=1,column=0)
        self.nameReg = Entry()
        self.nameReg.grid(row=1,column=1)

        Label(text="Provide Email").grid(row=2,column=0)
        self.emailReg = Entry()
        self.emailReg.grid(row=2,column=1)

        Label(text="Provide Password").grid(row=3,column=0)
        self.passwordReg = Entry()
        self.passwordReg.grid(row=3,column=1)

        Label(text="Provide Gender").grid(row=4,column=0)
        self.genderReg = Entry()
        self.genderReg.grid(row=4,column=1)

        Label(text="Provide Age").grid(row=5,column=0)
        self.ageReg = Entry()
        self.ageReg.grid(row=5,column=1)

        Label(text="Provide City").grid(row=6,column=0)
        self.cityReg = Entry()
        self.cityReg.grid(row=6,column=1)

        Label(text="Provide hobbies").grid(row=7,column=0)
        self.hobbiesReg = Entry()
        self.hobbiesReg.grid(row=7,column=1)

        Button(self.root, text="Register", command=lambda : self.register()).grid(row=8,column=0)

        self.message = Label(text="", fg="red")
        self.message.grid(row=9,column=0)

        self.root.mainloop()

    def register(self):

        self.mycursor.execute("""INSERT INTO `user` (`user_id`, `name`, `email`, `password`, `gender`, `age`, `city`, `hobbies`) VALUES
                     (NULL, '{}', '{}', '{}', '{}', '{}', '{}', '{}')""".format(self.nameReg.get(),
                                                                                self.emailReg.get(),
                                                                                self.passwordReg.get(),
                                                                                self.genderReg.get(),
                                                                                self.ageReg.get(),
                                                                                self.cityReg.get(),
                                                                                self.hobbiesReg.get()))

        self.conn.commit()

        self.message.configure(text="Registration Successful")

        Label(text="To Log Out Click Here!!", fg="blue").grid(row=10, column=0)
        Button(text="LOG OUT", command=lambda: self.launchLogOut()).grid(row=11, column=0)

    def launchUserMenu(self):

        self.destroyWindow()
        Label(text="User Menu").grid(row=0, column=0)

        Label(text="To view all users Click Here!!", fg="blue").grid(row=1, column=0)
        Button(text="View Users", command=lambda : self.launchViewUsers()).grid(row=2, column=0)

        Label(text="To view whom you have proposed Click Here!!", fg="blue").grid(row=3, column=0)
        Button(text="Proposed Users", command=lambda : self.launchProposedUsers()).grid(row=4, column=0)

        Label(text="To view who have proposed you Click Here!!", fg="blue").grid(row=5, column=0)
        Button(text="Proposals", command=lambda : self.launchProposals()).grid(row=6, column=0)

        Label(text="To view all matches Click Here!!", fg="blue").grid(row=7, column=0)
        Button(text="Matches", command=lambda : self.launchMatches()).grid(row=8, column=0)

        Label(text="To Log Out Click Here!!", fg="blue").grid(row=9, column=0)
        Button(text="LOG OUT", command=lambda: self.launchLogOut()).grid(row=10, column=0)

        self.sb1 = Scrollbar()
        self.sb1.grid(row=0, column=1, rowspan=5)

        self.list1 = Listbox(height=7, width=40)
        self.list1.grid(row=0, column=2, rowspan=6, columnspan=4)

        self.list1.configure(yscrollcommand=self.sb1.set)
        self.sb1.configure(command=self.list1.yview)

        self.entry_value = StringVar()

    def launchViewUsers(self, i=0):

        self.list1.delete(0, END)
        self.view_users()

        for i in self.all_users_list:
            self.list1.insert(END, i)

        Label(text="enter the id of the user whom you would like to propose:", fg="blue").grid(row=12,column=0)
        self.juliet_id = Entry()
        self.juliet_id.grid(row=13, column=0)
        Button(text="Propose", command=lambda: self.propose()).grid(row=14, column=0)

    def propose(self):
        self.mycursor.execute(
        """INSERT INTO `proposals` (`proposal_id`, `romeo_id`, `juliet_id`) VALUES (NULL, '{}', '{}')"""
                    .format(self.current_user_id, self.juliet_id.get()))
        self.conn.commit()
        Label(text="Proposal sent successfully! Fingers crossed!", fg="green").grid(row=15,column=0)
        self.launchViewUsers()

    def view_users(self):

        self.mycursor.execute(
            """SELECT `user_id`,`name`,`gender`,`age`,`city`,`hobbies` FROM `user` WHERE `user_id` NOT LIKE '{}'""".format(
                self.current_user_id))
        self.all_users_list = self.mycursor.fetchall()

    def launchProposedUsers(self):

        self.list1.delete(0, END)
        self.view_proposed()

        for i in self.proposed_user_list:
            self.list1.insert(END, i)

    def view_proposed(self):
        self.mycursor.execute(
            """SELECT u.`name`,u.`gender`,u.`city`,u.`age`,u.`hobbies` FROM `proposals` p JOIN `user` u ON p.`juliet_id` = u.`user_id` 
            WHERE p.`romeo_id` LIKE '{}'""".format(self.current_user_id))
        self.proposed_user_list = self.mycursor.fetchall()

    def launchProposals(self):

        self.list1.delete(0, END)

        self.view_requests()

        for i in self.request_user_list:
            self.list1.insert(END, i)

    def view_requests(self):
        self.mycursor.execute(
            """SELECT u.`name`,u.`gender`,u.`city`,u.`age`,u.`hobbies` FROM `proposals` p JOIN `user` u ON p.`romeo_id` = u.`user_id` 
            WHERE p.`juliet_id` LIKE '{}'""".format(self.current_user_id))
        self.request_user_list = self.mycursor.fetchall()

    def launchMatches(self):

        self.list1.delete(0, END)

        self.view_matches()

        for i in self.matched_user:
            self.list1.insert(END, i)

    def view_matches(self):
        # tripple subquery
        self.mycursor.execute(
            """SELECT `name`,`gender`,`age`,`city`,`hobbies` FROM `user` WHERE `user_id` IN 
            (SELECT `juliet_id` FROM `proposals` WHERE `romeo_id` LIKE '{}' AND `juliet_id` IN (SELECT `romeo_id` FROM `proposals` 
            WHERE `juliet_id` LIKE '{}'))""".format(self.current_user_id, self.current_user_id))
        self.matched_user = self.mycursor.fetchall()

    def launchLogOut(self):

        self.destroyWindow()

        self.current_user_id = 0
        Label(text="!!Logged out successfully!!", fg="red").grid(row=0,column=0)

        Label(text="Already a member!!!Log In Here!", fg="green").grid(row=1, column=0)

        Label(text="Enter Email").grid(row=2, column=0)
        self.emailInput = Entry()
        self.emailInput.grid(row=2, column=1)

        Label(text="Enter Password").grid(row=3, column=0)
        self.passwordInput = Entry()
        self.passwordInput.grid(row=3, column=1)

        Button(text="Login", command=lambda: self.login()).grid(row=4, column=0)

        self.message = Label(text="", fg="red")
        self.message.grid(row=5, column=0)

        Label(text="Not a member?Register here!", fg="green").grid(row=6, column=0)
        Button(text="Register Here", command=lambda: self.launchRegWindow()).grid(row=7, column=0)

        self.root.mainloop()

    def destroyWindow(self):

        for i in self.root.grid_slaves():
            i.destroy()

obj=Tinder()
