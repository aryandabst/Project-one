import random
import datetime

# List Declaration
name = []
phno = []
add = []
checkin = []
checkout = []
room = []
price = []
rc = []
p = []
roomno = []
custid = []
day = []


i = 0

# Home Function
def Home():
    while True:
        print("\t\t\t\t WELCOME TO HOTEL ANCASA")
        print("\t\t\t 1 Booking")
        print("\t\t\t 2 Rooms Info")
        print("\t\t\t 3 Room Service(Menu Card)")
        print("\t\t\t 4 Payment")
        print("\t\t\t 5 Record")
        print("\t\t\t 0 Exit")
        
        ch = int(input("-> "))
        
        if ch == 1:
            Booking()
        elif ch == 2:
            Rooms_Info()
        elif ch == 3:
            restaurant()
        elif ch == 4:
            Payment()
        elif ch == 5:
            Record()
        elif ch == 0:
            print("Exiting Hotel AnCasa. Thank you!")
            break
        else:
            print("Invalid Choice! Please try again.")

# Date validation function
def date(c):
    if c[2] >= 2019 and c[2] <= 2026:
        if c[1] != 0 and c[1] <= 12:
            if c[1] == 2 and c[0] != 0 and c[0] <= 31:
                if c[2] % 4 == 0 and c[0] <= 29:
                    pass
                elif c[0] < 29:
                    pass
                else:
                    print("Invalid date")
                    Home()
            elif c[1] <= 7 and c[1] % 2 != 0 and c[0] <= 31:
                pass
            elif c[1] <= 7 and c[1] % 2 == 0 and c[0] <= 30 and c[1] != 2:
                pass
            elif c[1] >= 8 and c[1] % 2 == 0 and c[0] <= 31:
                pass
            elif c[1] >= 8 and c[1] % 2 != 0 and c[0] <= 30:
                pass
            else:
                print("Invalid date")
                Home()
        else:
            print("Invalid date")
            Home()
    else:
        print("Invalid date")
        Home()

# Booking Function
def Booking():
    global i
    print("\n---- BOOKING ROOMS ----\n")
    
    while True:
        n = str(input("Name: "))
        p1 = str(input("Phone No.: "))
        a = str(input("Address: "))
        if n != "" and p1 != "" and a != "":
            name.append(n)
            phno.append(p1)
            add.append(a)
            break
        else:
            print("Name, Phone no. & Address cannot be empty..!!")
    
    cii = str(input("Check-In (dd/mm/yyyy): "))
    checkin.append(cii)
    cii = cii.split('/')
    ci = [int(cii[0]), int(cii[1]), int(cii[2])]
    date(ci)

    coo = str(input("Check-Out (dd/mm/yyyy): "))
    checkout.append(coo)
    coo = coo.split('/')
    co = [int(coo[0]), int(coo[1]), int(coo[2])]

    # Check if Check-out is after Check-in
    d1 = datetime.datetime(ci[2], ci[1], ci[0])
    d2 = datetime.datetime(co[2], co[1], co[0])
    if d2 <= d1:
        print("\nCheck-Out date must fall after Check-In\n")
        Home()
    
    date(co)
    d = (d2 - d1).days
    day.append(d)

    print("\n----SELECT ROOM TYPE----")
    print(" 1. Standard Non-AC - Rs. 3500/day")
    print(" 2. Standard AC - Rs. 4000/day")
    print(" 3. 3-Bed Non-AC - Rs. 4500/day")
    print(" 4. 3-Bed AC - Rs. 5000/day")
    
    ch = int(input("-> "))
    
    if ch == 1:
        room.append('Standard Non-AC')
        price.append(3500)
    elif ch == 2:
        room.append('Standard AC')
        price.append(4000)
    elif ch == 3:
        room.append('3-Bed Non-AC')
        price.append(4500)
    elif ch == 4:
        room.append('3-Bed AC')
        price.append(5000)
    else:
        print("Wrong choice. Try again.")
        Home()
    
    rn = random.randrange(40) + 300
    cid = random.randrange(40) + 10
    
    while rn in roomno or cid in custid:
        rn = random.randrange(60) + 300
        cid = random.randrange(60) + 10
    
    roomno.append(rn)
    custid.append(cid)
    rc.append(0)
    p.append(0)
    
    print("\n*** ROOM BOOKED SUCCESSFULLY ***")
    print(f"Room No. - {rn}")
    print(f"Customer Id - {cid}")

# Rooms Info Function
def Rooms_Info():
    print("\n------ HOTEL ROOMS INFO ------\n")
    print("STANDARD NON-AC - Double Bed, TV, Telephone, Balcony, Washroom\n")
    print("STANDARD AC - Double Bed, TV, Telephone, Balcony, Washroom, AC\n")
    print("3-Bed NON-AC - 3 Beds, TV, Telephone, Balcony, Washroom\n")
    print("3-Bed AC - 3 Beds, TV, Telephone, Balcony, Washroom, AC\n")

# Restaurant Function
def restaurant():
    ph = int(input("Customer Id: "))
    global i
    f = 0
    r = 0
    for n in range(0, i):
        if custid[n] == ph and p[n] == 0:
            f = 1
            print("\n---- HOTEL ANCASA MENU ----")
            print("39 Masala Dosa - 130")
            print("32 Butter Naan - 20")
            print("40 Paneer Dosa - 130")
            print("Press 0 to end order")
            
            while True:
                ch = int(input("-> "))
                if ch == 39:
                    r += 130
                elif ch == 32:
                    r += 20
                elif ch == 40:
                    r += 130
                elif ch == 0:
                    break
                else:
                    print("Invalid choice.")
            
            print(f"\nTotal Restaurant Bill: Rs. {r}")
            rc[n] += r
            break
    if f == 0:
        print("Invalid Customer Id")

# Payment Function
def Payment():
    ph = str(input("Phone Number: "))
    global i
    f = 0
    
    for n in range(0, i):
        if ph == phno[n]:
            if p[n] == 0:
                f = 1
                print("\n---- PAYMENT ----")
                print("1- Credit/Debit Card")
                print("2- Paytm/PhonePe")
                print("3- Using UPI")
                print("4- Cash")
                _ = int(input("-> "))
                
                total_amt = (price[n] * day[n]) + rc[n]
                print(f"\nAmount to Pay: Rs. {total_amt}")
                
                ch = input("Confirm Payment? (y/n): ")
                if ch.lower() == 'y':
                    print("\n---- HOTEL ANCASA BILL ----")
                    print(f"Name: {name[n]}")
                    print(f"Phone No.: {phno[n]}")
                    print(f"Address: {add[n]}")
                    print(f"Check-In: {checkin[n]}")
                    print(f"Check-Out: {checkout[n]}")
                    print(f"Room Type: {room[n]}")
                    print(f"Room Charges: {price[n] * day[n]}")
                    print(f"Restaurant Charges: {rc[n]}")
                    print(f"Total Amount Paid: {total_amt}")
                    print("\nThank You. Visit Again!\n")
                    
                    p[n] = 1
                    roomno[n] = 0
                    custid[n] = 0
            else:
                print("Payment already done.")
            f = 1
            break
    if f == 0:
        print("Invalid Customer Id")

# Record Function
def Record():
    if phno:
        print("\n---- HOTEL RECORD ----")
        print("| Name | Phone No. | Address | Check-In | Check-Out | Room Type | Price/day |")
        print("-" * 90)
        for n in range(0, i):
            print(f"| {name[n]} | {phno[n]} | {add[n]} | {checkin[n]} | {checkout[n]} | {room[n]} | {price[n]} |")
    else:
        print("No Records Found")

Home()
