# Cloudflare RDP
Cloudflare RDP can be done by using Cloudflare Tunnel. Please first follow the [guide](../README.md) to setup your Cloudflare Tunnel

## Prerequisite
### Host
- XRDP (UBUNTU)
- cloudflared

### Client
- cloudflared

## Setup
Setting up cloudflare RDP is easy. All you need to do is have a Cloudflare Tunnel and add the following service to your tunnel config.yaml under your ingress:
```
- hostname: <WHERE DO YOU WANT TO HOST RDP PUBLICLY>
  service: rdp://localhost:3389 <WHERE IS YOUR THING HOSTED ON YOUR SERVER LOCALLY> 
```

Then add the hostname on your Cloudflare Dashboard with the following inputs:
| Parameter | Input     | Description                |
| :-------- | :------- | :------------------------- |
| `Type` | `CNAME`| Select A if you have static IP; dynamic IP select CNAME, `we have dynamic IP`|
| `Name` | `xrdp.honeydew.com`| Proper URL where you want to host ur RDP, only one level of SUBDOMAIN is allowed for free tier cloudflare.
|`Target`| `<YOUR API TUNNEL UUID>.cfargotunnel.com`| To point everything to CF argo tunnel which handles security for us

## Connection
Make sure your Host Tunnel is running else you won't be able to connect and also install cloudflare. [Installation Guide](../README.md)

Open a Terminal and run the following:
```
cloudflared access rdp --hostname <Your Hostname> --url rdp://localhost:4389 <where do you want to run your RDP session,can be anyport>
```

This will connect your client to the tunnel and do not close it. Now all you have to do is enter `localhost:4389` as address in your RDP software. Here are some examples:

- Remmina **(UBUNTU)**
- Remote Desktop Connection **(WINDOWS)**

## References
- [Cloudflare Docs - RDP](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/use-cases/rdp/)