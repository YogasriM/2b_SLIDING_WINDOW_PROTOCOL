# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To perform the implementation of sliding window protocol.
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
SERVER :
      import socket
      server_socket = socket.socket()
      server_socket.bind(('localhost', 8000))
      server_socket.listen(1)
      
      print("Waiting for connection from client...")
      connection, addr = server_socket.accept()
      print(f"Connected to: {addr}")
      
      total_frames = int(input("Enter number of frames to send: "))
      frames = list(range(total_frames))
      window_size = int(input("Enter Window Size: "))
      
      start = 0  
      while start < len(frames):
          end = start + window_size
          frame_batch = frames[start:end]  
          connection.send(str(frame_batch).encode())
          ack = connection.recv(1024).decode()
          if ack:
              print(ack)
              start = end

CLIENT :
      import socket
      
      client_socket = socket.socket()
      client_socket.connect(('localhost', 8000))
      
      while True:
          data = client_socket.recv(1024).decode()
          if not data:
              break
          print(data)
          client_socket.send("Acknowledgement received from the client".encode())
## OUPUT

<img width="526" height="245" alt="image" src="https://github.com/user-attachments/assets/18d64eda-17a5-4b7a-bc89-3c24847609e3" />


<img width="615" height="113" alt="image" src="https://github.com/user-attachments/assets/638faae1-2c26-44ad-b374-c57f7234d5c9" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
