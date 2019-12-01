# only-classes

import json


# class hotel finder
class HotelFinder:

    hotels = [] # list of hotels

    def available_hotels(self):
        money = self.user_input_money()
        desiredStar = self.user_input_desiredStar()
        availableHotels = []
        for hotel in self.hotels:
            if int(money) >= int(hotel["single_room_price"]) and int(hotel["star_rating"]) == int(desiredStar):
                availableHotels.append(hotel)
        pass

    def __init__(self):
        # init hotels
        with open('hotels.json') as filename:
            self.hotels = json.load(filename)
        pass

    def user_input_desiredStar(self):
        ds = input("Insert your desired star from 1 to 5: ")
        while True:
            try:
                ds = int(ds)
                if ds < 1 or ds > 5:
                    ds = input("Star count of a hotel may not be less than zero and more than 5")
                else:
                    return ds
            except ValueError as e:
                print("Try again")
                ds = input("Insert your desired star from 1 to 5: ")
                continue

    def getTheBestChoise(self):
        money = self.user_input_money()
        star = 1
        bestHotel = None
        for h in self.hotels:
            if money >= int(h["single_room_price"]) and star < int(h["star_rating"]):
                star = int(h["star_rating"])
                bestHotel = h

        print(bestHotel)

    def getHotelByPhoneNumber(self):
        hotel_string = 0
        phoneNumber = input("Input the phone number in the following format (###) #######: ")
        for h in self.hotels:
            if phoneNumber == h["phone"]:
                hotel_string = "Hotel: {}, Stars: {}, Price: {}".format(h["hotel_name"], h["star_rating"],
                                                                        h["single_room_price"])
                print(hotel_string)
        if hotel_string == 0:
            print("No such Hotel exists with that phone number")
        pass

    def check(self):
        while True:
            checks = input("Do you wanna try again? yes/no: ")
            print(checks)
            if checks == "no":
                return False
            elif checks == "yes":
                return True
            else:
                print('Please enter yes/no: ')
        pass

    def user_input_money(self):
        money = input("Insert the initial balance above 0: ")
        while True:
            try:
                money = int(money)
                if money > 0:
                    return money
                elif money < 0:
                    money = input("not intereseted in your debts")
            except ValueError as e:
                print("Try again")
                ds = input("Insert your desired star from 1 to 5: ")
                continue

    def poll(self):
        flag = True
        while flag:
            action = int(input(
                "Please input what you want (1 - for search based on PhoneNumber, 2 - For gettingthe best hotel based on money, 3 - for search based on stars): "))
            if action == 1:
                self.getHotelByPhoneNumber()
            elif action == 2:
                self.getTheBestChoise()
            elif action == 3:
                self.available_hotels()
            else:
                print(" Wrong action")
            pass
            flag = self.check()


if __name__ == "__main__":
    print("This app is for finding hotels")

    hotel_finder = HotelFinder()
    hotel_finder.poll()
