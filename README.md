# basic_websocket
var app = require ('express') ();
var http = require('http').createServer (app);
var io = require('socket.io') (http);

app.get ('/', (req, res) => {
    res.sendFile(__dirname +'/index.html');
});

io.on ('connection', (socket) =>{
    // socket.broadcast.emit ('hi');
    socket.on('chat message', (msg) => {
        io.emit('chat message', msg);
    console.log('a user connected');
    });
    socket.on('disconnect', () => {
        console.log('user disconnected')
    })
});

http.listen(3000, () => {console.log('listening on * : 3000'); });
