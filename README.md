# Bit-Sync

### Full documentation [here](https://docs.google.com/document/d/1TKeq-kEQOR1TsG7wWaypIJgA0GZmNLL65sJjs1Dwkxc/edit?usp=sharing)
### Prerequisites:

1. G++ compiler
    
    `sudo apt-get install g++`
    
2. “libssl-dev” library for SHA-1 hashing
    
    `sudo apt-get install libssl-dev`
    

### How to compile project:

1. go to client directory
    
    `make`
    
2. go to tracker directory
    
    `make`
    
3. To clean solution
    
    `make clean`
    

### How to Run project:

### To run the Tracker

`./tracker <MY_TRACKER_IP>:<PORT> <OTHER_TRACKER_IP>:<PORT> <SEEDERLIST_FILE> <TRACKER_LOG_FILE>
eg : ./tracker 127.0.0.1:5000 127.0.0.1:6000 seederlist serverlog1`

### To run the Client

`./client <CLIENT_IP>:<UPLOAD_PORT> <TRACKER_IP_1>:<PORT_1> <TRACKER_IP_2>:<PORT_2> <client_log_file>`

- creating client1 on new terminal with socket : 127.0.0.1:8800
    
    eg : `./client 127.0.0.1:8800 127.0.0.1:5000 127.0.0.1:6000 clientlog1`
    
- creating client2 on another terminal with socket : 127.0.0.1:8810
    
    eg : `./client 127.0.0.1:8810 127.0.0.1:5000 127.0.0.1:6000 clientlog2`
    

### Command/Functionality on Client side

1. **To Share the file over network :**
    
    `share <LOCAL_FILE_PATH> <FILENAME>.<FILE_EXTENSION>.mtorrent
     eg : share /home/rog/1gb.test 1gb.test.mtorrent`
    
- It will generate .mtorrent file and send data to tracker that I(client/seeder) have this file. Now other client/leecher can download this file using .mtorrent file.
1. **To Download the file :**
    
    `get <FILENAME.mtorrent> <DESTINATION_PATH>
     eg : get 1gb.test.mtorrent /home/rog/new_1gb.test`
    
- It will send request to tracker to know about available seeders and then randomly choose one seeder and make connection with it to get chunk of data.
1. **Show Downloading status**
    
    `show_downloads`
    
- It will list out files which are downloading(D), successfully downloaded(S).
1. **To Stop sharing of file over network :**
    
    `remove <FILENAME.mtorrent>
    Eg : remove 1gb.test.mtorrent`
    
- It will stop sharing of that file over network by removing .mtorrent file and metadata of that file from tracker.
1. **Close client :**
    
    `close`
    
- It will shutdown client and remove all metadata of files which have been shared by this client from tracker.
  
 #### Note

* seederlist file must be present on tracker folder for tracker to run. If not then create empty seederlist file.
* whenever client starts, it scans current working directory for .mtorrent file and update/inform tracker about it.
* Client(seeder/leecher) and tracker implemented by multithreading thus also support parallel downloads and uploads.
