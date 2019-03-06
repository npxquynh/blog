---
title: "Socat - host forwarding"
tags: ["network", "note"]
date: 2019-03-06T20:41:36+01:00
draft: false
---

So I have a situtation that there is MySQL instance running at `198.168.100.100:34357`. The host IP is difficult to remember, the port number is just something random.

It would be easier for me to receive all traffics for MySQL at some `localhost:3306` port. 3306 is the default port for MySQL.

And the fact that I'm using OSX makes things a bit harder, the `nc` netcat in OSX doesn't work the same way as Linux `nc`. The command that works for me finally is:

{{< highlight bash >}}
socat TCP-LISTEN:3306,fork TCP:192.168.100.100:34357
{{< /highlight >}}

What it does is that all traffic coming to `localhost:3306` will be forwarded to `192.168.100.100:34357`

The structure for the command is `socat [options] <address> <address>`

- `TCP-LISTEN:3306,fork` is one address. 
- `TCP:192.168.100.100:34357` is another address.
- `TCP-LISTEN` and `TCP` are address type keywords.
- `3306`, `192.168.100.100`, `34357` are address parameters.
- `fork` is an address option, and it follows the address parameters after a ','

What I realize is that it's so much helpful to go through the `man socat`, but don't look for details. It's useful in the beginning to read through the structure and understand the basic.

