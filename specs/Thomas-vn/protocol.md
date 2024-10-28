## 1. Overview 

This Server/Client application is implemented for performing basic arithmetics (ADDITION, SUBSTRACTION, MULTIPLICATION, DIVISION) on two integers. The client sends requests with a certain format and the server responds with the result. 

## 2. Transport Layer Protocol

- Protocol Type : TCP

- IP Address: The client connects to the server using the following command : nc -kl <port_number>. I personly used the localhost (127.0.0.1), because I did the project alone.

- Port : any available port

- Connection Handling:
    -> Server : Listens for connections and remains open to handle additional client requests.
    -> Client: Initiates the connection and can send multiple requests within the same session.

## 3. Messages 

Communication Order: The client sends a message first; the server responds with the result or an error.

Message Syntax:
Client to Server:
    COMMAND ARG1 ARG2
        COMMAND: Operation type (ADD or MULTIPLY).
        ARG1, ARG2: Integer values for the operation.
    Termination: EXIT to end the session.

Server to Client:
    Successful Result: Returns the integer result of the computation.
    Error Message: Returns ERROR: description_of_issue if an error occurs.

Message Directions:
    Client → Server: Sends requests (ADD, MULTIPLY, EXIT).
    Server → Client: Sends responses (result or error).

Required Message Sequence:
    1. Client: Initiates connection and sends a computation request.
    2. Server: Processes the request, sends the result or an error.
    3. Client: May send additional requests or EXIT to close the connection.
    4. Server: Closes the connection upon receiving EXIT.

## 4. Specific Elements

Error Handling:
    Invalid Commands: The server responds with ``ERROR: Invalid command`` if it receives an unsupported command.

    Malformed Inputs: The server responds with ``ERROR input if the message format is incorrect.

    Extensibility: New operations (e.g., SUBTRACT, DIVIDE) could be added by expanding the COMMAND options and adjusting server handling accordingly.
5. Example Dialogs
Valid Request (Addition):

Client: ADD 10 20
Server: 30
Valid Request (Multiplication):

Client: MULTIPLY 5 4
Server: 20
Invalid Command:

Client: SUBTRACT 10 5
Server: ERROR: Invalid command
Session Termination:

Client: EXIT
Server: Closes connection