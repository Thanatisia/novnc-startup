# NoVNC with Websockify 

## Information
### Background
```
NoVNC is a Web/browser-based VNC client that uses websockify as a dependency for Websocket capabilities.

Using websockify, it can essentially intercept the VNC server's display output and redirect it to NoVNC.

Additionally, 
    - NoVNC being a generic browser-based VNC client, it can be used with other mediums 
    - For example 
        + as the target for QEMU/KVM, as QEMU/KVM CLI utilities has VNC as a display output
```

### Project
- Repositories
    + NoVNC: https://github.com/novnc/novnc
    + Websockify: https://github.com/novnc/websockify
+ for more information, you may refer to my NoVNC documentation [here](https://github.com/Thanatisia/SharedSpace/tree/main/Docs/Home%20Lab/Services%20and%20Tools/VNC%20Clients/NoVNC) (WIP and still needs cleanup though)

## Setup
### Dependencies
- If using Docker
    + docker
    + docker-compose
- If using on Host system
    + novnc : A Web-based VNC client that connects to an existing VNC server and displays it on a browser using WebSocket
        - If installing using Package Manager
            - apt-based (Debian)
                ```console
                apt install novnc
                ```
        - Manual Build from Source
            + Just download the repository from [NoVNC GitHub](https://github.com/novnc/novnc) and place it in the folder '/usr/share/novnc'
    + websockify : A Websocket framework made in Javascript; Used with NoVNC to support the displaying of a VNC server on a browser
        - If installing using Package Manager
            - apt-based (Debian)
                ```console
                apt install websockify
                ```
        - Manual Build from Source
            + Clone from [GitHub - Websockify](https://github.com/novnc/websockify)

### Pre-Requisites
- Ensure the NoVNC client is installed
    + Take note of the path that contains the NoVNC client source
- If you are using `docker-compose`
    - Customize the docker-compose

## Documentation

### Using docker run
- Building Dockerfile image
    ```console
    docker build --tag thanatisia/novnc -f docker/Dockerfile .
    ```

- Starting up
    ```console
    docker run -itd --name novnc -p 8080:6080 -v "/path/to/novnc:/usr/share/novnc" -e VNC_WEB_CLIENT=/usr/share/novnc -e VNC_WEB_PORT=6080 -e VNC_SERVER_HOST_IP=localhost -e VNC_SERVER_HOST_PORT=5901 thanatisia/novnc
    ```

### Using docker-compose
- Starting up (WIP)
    + You can try, but there are some issues, please refer to [ISSUES](ISSUES.md) for the list
    ```console
    docker-compose up -d --build
    ```

### Bare-Metal
- Starting up
    - Explanations
        + novnc-webui-path       : The path to the NoVNC WebUI folder; Default: /usr/share/novnc
        + novnc-webui-port-number: The WebUI Port Number; Default: 6080
        + novnc-webui-host       : The WebUI Host IP address/name; Default: localhost
        + vnc-server-port-number : The VNC server port number; This port corresponds to the port used to connect to the VNC server you set up + display number; Default: 5901
    ```console
    websockify -D --web=[novnc-webui-path] [novnc-webui-port-number] [novnc-webui-host]:[vnc-server-port-number]
    ```

## Wiki
### Snippets and Examples
- Starting up NoVNC WebUI
    + Open up your browser
    + Access the URL `http(s)://[server-ip-address]:[vnc-web-port-number]/vnc.html`

## Configurations
### Docker
- Environment Variables
    + VNC_WEB_CLIENT      : The path to the VNC Web/browser-based client source file; Default '/usr/share/novnc'
    + VNC_WEB_PORT        : The WebUI HTTP port number; Default: 6080
    + VNC_SERVER_HOST_IP  : The VNC Server Host IP address/domain; Default: localhost
    + VNC_SERVER_HOST_PORT: The VNC server port number; This port is equivalent to the port used to connect to the VNC server you set up; Default: 5901
    + OTHER_OPTIONS       : The VNC Web/browser client other options; Default: '-D'

## Resources

## References

## Remarks

