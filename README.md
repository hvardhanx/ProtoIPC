# ProtoIPC
Interprocess communication using Protocol Buffers

### Server:

 - The single-threaded pipe server uses asynchronous operations to service simultaneous connections to multiple pipe clients.
 - The named-pipe server creates fixed number of pipe instances.
 - Each pipe instance can be connected to a separate pipe client. 
 - If a pipe client has finished using its pipe instance, the server disconnects from the client and reuses the pipe instance to connect to a new client. 
 - Asynchronous operations make it possible for one pipe to read and write data simultaneously and for a single thread to perform simultaneous I/O operations on multiple pipe handles.
 - It also enables a single-threaded pipe server to handle communications with multiple pipe clients efficiently.
 - The proto file which contains the schema can be found in the server folder.
 - The server parses the serialized string received from the client and prints all of the information.

### Client:

 - The client opens a named pipe, sets the pipe handle to message-read mode.
 - It uses the WriteFile function to send a request to the server, and uses the ReadFile function to read the server's reply.
 - The client contains the implementations of asynchronous and synchronous operations.
 - For the asynchronous implementations, the read/write operation is issued and then we detect its completion.
 - Detecting completion of the operation involves waiting for the event handle, checking the overlapped result, and then handling the data.
 - The client uses the functions defined by the protobuf to add a person to the address book.
 - It then serializes the address book and sends it to the server, where the server gets the serialized string and prints all of the information.

#### Protobuf schema:
 - [Address book schema](IPCServerCpp/IPCServerCpp/addressbook.proto)

#### Executables:
 - [Asynchronous read/write from client](AsyncReadWriteClient)
 - [Synchronous read/write from client](SyncReadWriteClient)