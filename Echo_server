import socket

def start_server():
    # Create and configure the server socket
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.bind(('localhost', 5000))
    server.listen(1)
    
    print("Waiting for a connection...")
    connection, client_address = server.accept()
    print(f"Connection established with {client_address}")

    try:
        buffer = ""
        while True:
            # Receive data from the client
            data = connection.recv(1024)
            if not data:
                break

            # Decode and append to buffer
            buffer += data.decode()

            # Process complete messages
            while '\n' in buffer:
                # Split the buffer by newline characters
                parts = buffer.split('\n')
                for part in parts[:-1]:
                    message = part.strip()
                    if message.lower() == 'quit':
                        print("Client requested to quit. \n keep learning!!! ")
                        message = message + " \n\r Keep Learnig!!!!"
                        connection.sendall(message.encode())
                        return
                    print("Received:", message)
                    connection.sendall(f"echo > {message}\n\r".encode())
                buffer = parts[-1]  # Keep the remaining incomplete message
    finally:
        connection.close()
        server.close()

if __name__ == "__main__":
    start_server()
