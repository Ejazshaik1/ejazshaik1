import json
class food_ord_app:
    def __init__(self):
        self.admin=[]
        self.count=0
        self.item_details={}

    def admin_login(self,item_num):
        self.count=self.count+1
        item_name=input("Enter item name:")
        item_quantity=input("Enter item quantity:")
        item_price=input("Enter item price:")
        item_discount=input("Enter item discount:")
        item_stock=input("Enter item in stock:")
        item_Data={"item_name":item_name,"item_quantity":item_quantity,"item_price":item_price,"item_discount":item_discount,"item_stock":item_stock}
        self.item_details[self.count] = item_Data
        with open("add_items.json","w") as f:
            json.dump(self.item_details,f,indent = 4)
        return self.item_details
    
    def item_edit(self):
        item_editnum=int(input("Enter number of the item to be edited:"))
        for key in self.item_details:
            print(type(item_editnum))
            print(type(key))
            if (item_editnum) is (key):
                item_name=input("Enter item name:")
                item_quantity=input("Enter item quantity:")
                item_price=input("Enter item price:")
                item_discount=input("Enter item discount:")
                item_stock=input("Enter item in stock:")
                item_Data={"item_name":item_name,"item_quantity":item_quantity,"item_price":item_price,"item_discount":item_discount,"item_stock":item_stock}
                self.item_details[key] = item_Data
                with open("add_items.json","w") as f:
                    json.dump(self.item_details,f,indent = 4)
                return self.item_details
            else:
                print("Entered ID is wrong")
                return self.item_details
            
    def item_remove(self):
        item_editnum=int(input("Enter number of the item to be edited:"))
        for key in self.item_details:
            print(type(item_editnum))
            print(type(key))
            if (item_editnum) is (key):
                del self.item_details[key]
                with open("add_items.json","w") as f:
                    json.dump(self.item_details,f,indent = 4)
                return self.item_details
            else:
                print("Entered ID is wrong")
                return self.item_details
 ###############     ###############      ############### ###############
class user:
    def __init__(self,Full_name, phone_number, email, Address, Password):
        self.full_name = Full_name
        self.phone_number = phone_number
        self.email = email
        self.address = Address
        self.password = Password
        self.user_details=[]
        self.user_cnt=0
    def register_user(self, Full_name,phone_number,email,Address,Password):
        new_user = user(Full_name,phone_number,email,Address,Password)
        self.user_details.append(new_user)

    def login_user(self, email, password):
        for user in self.user_details:
            if user.email == email and user.password == password:
                return user
        return None
                
            
    def itemlist(self):
        print("1.place order")
        print("2.for order history")
        print("3.Update profile")
        option=int(input("Enter your option number(select 1/2/3):"))
        item_data=[{"1":"Tandoori Chicken","quantity":"4 pieces","INR":"240"},
                    {"2":"Vegan Burger","quantity":"1 pieces","INR":"320"},
                    {"3":"Truffle Cake","quantity":"500gm","INR":"900"}]
        food_order=[]
        
        if option==1:
            print(item_data)
            user_input=int(input("select food item to be added(1/2/3):"))
            if user_input==1:
                food_order.append(item_data[0])
            elif user_input==2:
                food_order.append(item_data[1])
            elif user_input==3:
                food_order.append(item_data[2])
            else:
                print("You have choosen wrong")
            print("enter 1 for confirm \n enter 2 for delete")
            select=int(input("Enter the choice:"))
            if select == 1:
                print("Order placed successfully")
            else:
                print("order cancelled")
            return food_order
        elif option==2:
            return food_order
        elif option==3:
            user_number=int(input("Enter the number of user to be edited(like:0 or 1 etc.):"))
            user_data = self.user_details[user_number]
            for k,v in items(user_data):
                data=input("Enter data for {k}:")
                user_data[k]=data
            self.user_details[user_number]=user_data
        return self.user_details

x=food_ord_app()
y=user("jaju",55,"jaj@gmail.com",456,123)
login=int(input("enter login number(1 for admin,2 for user):"))
if 1 == login:
    item_num=int(input("Enter the number of items to be added into menu:"))
    for i in range(item_num):
        y=(x.admin_login(item_num))
    print("list of items added:\n",y)
    edit=input("if item list need to edited(Y/N):")
    if edit=="Y":
        edition=x.item_edit()
        print(edition)
    elif edit == "N":
        print("The food list:\n",y)
    else:
        print("selected option is wrong")

    remove=input("Any item to be removed from list(Y/N):")
    if remove=="Y":
        remove=x.item_remove()
        print("Updated food list:\n",remove)
    elif remove == "N":
        print("The food list:\n",y)
    else:
        print("selected option is wrong")
        pass
elif 2==login:
    Full_name=input("Enter your name:")
    phone_number=int(input("Enter your number:"))
    email=input("Enter your Email id:")
    Address=input("Enter your Address:")
    Password=input("Enter your password:")
    user_name=input("Enter user name:")
    reg_user=y.register_user(Full_name,phone_number,email,Address,Password)
    
    again=input("if you want to register another user.select(Y/N):")
    if again=="Y":
        Full_name=input("Enter your name:")
        phone_number=int(input("Enter your number:"))
        email=input("Enter your Email id:")
        Address=input("Enter your Address:")
        Password=input("Enter your password:")
        user_name=input("Enter user name:")
        reg_user=y.register_user(Full_name,phone_number,email,Address,Password)
    elif again!="N":
        print("selection is wrong")
        pass
    email=input("enter email:")
    password=input("enter password:")
    login_user=y.login_user(email,password)
    itemlist=y.itemlist()
    pass
