This setup allows simple connection of your HA to Cloudflare via a tunnel. Tunnels is initiated by a outbound connection to Cloudflare, once established allows any traffic to be send over to your instance. 

Advantages:
- simpler to setup than port forwarding on your router
- You do not need to have public static IP address
- Usable in situations where you behind NAT (you in an enclosed network of your internet provider) or your IP address  changes often. Please figure this out with your provider.
- You can secure your Home assistant with google account.

Requirements:
- Cloudflare account
- Domain (DNS by Cloudflare)

Addon used: https://github.com/brenner-tobias/addon-cloudflared
The installation process is described quite well in the documentation. Here I will just share the  

For the identity provider i choose:
	https://developers.cloudflare.com/cloudflare-one/identity/idp-integration/google/