import os
import sys
import socket
import datetime
import time

     
FILE = os.path.join(os.getcwd(), "networkinfo.log")
#creating log file in the currenty directiory
#FILE (variable name), ??getcwd?? get current directory, os function
#?? , ?? creating new file networkinfo.log, gets updated everytie code is run
#

def ping():    
#to ping a particular IP
        try:
            socket.setdefaulttimeout(3)
            #if data interruption occurs for 3 seconds, <except> part will be executed

            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            #AF_INET: address family
            #SOCK_STREAM: type for TCP

            host = "8.8.8.8"
            port = 53

            server_address = (host,port)
            s.connect(server_address)

        except OSError as error:
            return False
            #function returns false value after data interruption

        else:
            s.close()
            #cleaning the connection after the communication with the server is completed
            return True


def calculate_time(start, stop):
#time conversiion and calculating time difference

        difference = stop - start
        seconds = float(str(difference.total_seconds()))
        return str(datetime.timedelta(seconds=seconds)).split(".")[0]

def first_check():
#to check if the system was already connected to an internet connection

        if ping():
        #if ping returns true
            live = "\nCONNECTION AQUIRED\n"
            print(live)
            connection_aquired_time = datetime.datetime.now()
            aquiring_message = "connection aquired at: " + str(connection_aquired_time).split(".")[0]
            print(aquiring_message)

            with open(FILE, "a") as file:
            #writes into the log file
                file.write(live)
                file.write(aquiring_message)

            return True
            
        else:
        #if ping reutrns false
            not_live = "\nCONNECTION NOT AQUIRED\n"
            print(not_live)

            with open(FILE, "a") as file:
            #writes into the log file
                file.write(not_live)
            return False


def main():
#main function to call functions
        monitor_start_time = datetime.datetime.now()
        monitoring_date_time = "monitering started at: " + str(monitor_start_time).split(".")[0]

        if first_check():
        #if true
            print(monitoring_date_time)
            #monitoring will only start when the connection will be acquired

        else:
        #if false
            while True:
            #infinite loop to see if the connection is acquired
                if not ping():
                #if connection not acquired
                    time.sleep(1)
                else:
                #if connection is acquired
                    first_check()
                    print(monitoring_date_time)
                    break
                

        with open(FILE, "a") as file: #write into the file as a into networkinfo.log, ???"a" - append: opens file for appending, creates the file if it does not exist???
            file.write("\n")
            file.write(monitoring_date_time + "\n")

        

        while True: #infinite loop to run the code forever, as we are monetering the network connection till the machine is on
            if ping(): # <connected> goes to the //send_request function//, if true:: the loop will stop for 5 seconds and then continue
                time.sleep(5) #if sendrequest(false), sleep 5 sec


            else: # <disconnected> 
                down_time = datetime.datetime.now()
                fail_msg = "disconnected at: " + str(down_time).split(".")[0]
                print(fail_msg)


                with open(FILE, "a") as file: #<writing in the log>
                    file.write(fail_msg + "\n")

                    
                while not ping(): # inside disconnect, if send request return false, pinging again and again utill connected again after every 1 second
                    time.sleep(1)

                up_time = datetime.datetime.now() #<connected again time> if while loop breaks, and connected again
                uptime_message = "connected again: " + str(up_time).split(".")[0]
     
                down_time = calculate_time(down_time, up_time) #calling time calculating function, printing unavailability time
                unavailablity_time = "connection was unavailable for: " + down_time
     
                print(uptime_message)
                print(unavailablity_time)
     
                with open(FILE, "a") as file: #<log entry for connected again, and unavailability time>
                    file.write(uptime_message + "\n")
                    file.write(unavailablity_time + "\n")
main()



