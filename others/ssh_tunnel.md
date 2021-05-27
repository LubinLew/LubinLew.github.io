# SSH隧道

> [SSH端口转发详解及实例 - 珂儿吖](https://www.cnblogs.com/keerya/p/7612715.html)



 B 无法直接访问 A, 但是 A 可以直接访问 B, 使用下面方法建立隧道, 则可以在 B 上访问 A。

```bash
# 客户端 A （与 B 建立 SSH连接，并要求 B 监听 2222 端口， 之后 2222端口的流量都转发到建立的SSh连接上）
ssh -NR 2222:localhost:22 root@192.168.12.62 -p 22  -o StrictHostKeyChecking=no

# 客户端 B（连接 2222 端口，就相当于ssh到可客户端A）
ssh root@127.0.0.1 -p 2222
```

## SSH 选项



-N      
        Do not execute a remote command.This is useful for just forwarding ports.

-R [bind_address:]port:host:hostport
-R [bind_address:]port:local_socket
-R remote_socket:host:hostport
-R remote_socket:local_socket
        Specifies that connections to the given TCP port or Unix socket on the remote (server) host are to be forwarded to the given host and port, or Unix socket, on the local
        side.  This works by allocating a socket to listen to either a TCP port or to a Unix socket on the remote side.  Whenever a connection is made to this port or Unix
        socket, the connection is forwarded over the secure channel, and a connection is made to either host port hostport, or local_socket, from the local machine.

        Port forwardings can also be specified in the configuration file.  
        Privileged ports can be forwarded only when logging in as root on the remote machine.
        IPv6 addresses can be specified by enclosing the address in square brackets.

        By default, TCP listening sockets on the server will be bound to the loopback interface only.
        This may be overridden by specifying a bind_address.  An empty bind_address, or the address ‘*’, 
        indicates that the remote socket should listen on all interfaces.
        Specifying a remote bind_address will only succeed if the server's GatewayPorts option is enabled (see sshd_config(5)).

        If the port argument is ‘0’, the listen port will be dynamically allocated on the server and 
        reported to the client at run time.  When used together with -O forward the
        allocated port will be printed to the standard output.

-p port
         Port to connect to on the remote host.  This can be specified on a per-host basis in the configuration file.

-I pkcs11
        Specify the PKCS#11 shared library ssh should use to communicate with a PKCS#11 token providing the user's private RSA key.

-i identity_file
        Selects a file from which the identity (private key) for public key authentication is read.  The default is ~/.ssh/identity for protocol version 1, and ~/.ssh/id_dsa,
        ~/.ssh/id_ecdsa, ~/.ssh/id_ed25519 and ~/.ssh/id_rsa for protocol version 2.  Identity files may also be specified on a per-host basis in the configuration file.  It is
        possible to have multiple -i options (and multiple identities specified in configuration files).  If no certificates have been explicitly specified by the
        CertificateFile directive, ssh will also try to load certificate information from the filename obtained by appending -cert.pub to identity filenames.

-o option
         Can be used to give options in the format used in the configuration file.  This is useful for specifying options for which there is no separate command-line flag.  For
         full details of the options listed below, and their possible values, see ssh_config(5).

    StrictHostKeyChecking
            If this flag is set to yes, ssh(1) will never automatically add host keys to the ~/.ssh/known_hosts file, and refuses to connect to hosts whose host key has changed.
            This provides maximum protection against trojan horse attacks, though it can be annoying when the /etc/ssh/ssh_known_hosts file is poorly maintained or when connections
            to new hosts are frequently made.  This option forces the user to manually add all new hosts.  If this flag is set to no, ssh will automatically add new host keys to the
            user known hosts files.  If this flag is set to ask (the default), new host keys will be added to the user known host files only after the user has confirmed that is
            what they really want to do, and ssh will refuse to connect to hosts whose host key has changed.  The host keys of known hosts will be verified automatically in all
            cases.