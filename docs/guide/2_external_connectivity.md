---
title: External connectivity
tags:
  - documentation
---
#### Why?
The home assistant can run quite well on the local network. You will see all the devices, integrate them and control when at home. This might be sufficient until you leave for a 14 day vacation or need to change some setting from work. With Solax cloud app, these setting are easily accessible.  When you switch to HA, you would probably want to replicate this. If you do not need or want to feel free to skip to next chapter.

This section is mainly pointer to relevant docs, that are quite nice.

#### Adding site to CF

1. Get a domain. Either https://www.cloudflare.com/products/registrar/ / Namecheap.com or similar.
2. Please create an account and add your domain. https://developers.cloudflare.com/fundamentals/manage-domains/add-site/.

#### Tunneling

=== "Port Forwarding"
	Based on using a static ip adress and setting up your router to take a certain port and any traffic to that port will go to device running HA. This will allow anybody with your ip address and port to access the HA.

=== "Tunneling"
	Requires you to setup a CF account and register your domain with CF. You connect to the CF and that connection is instead of sending data of a another websites, sends you requests of people who want to see your website and your HA respond with the data.

I prefer the tunneling as it allows simple connection of your HA.

Advantages:

- simpler to setup than port forwarding on your router
- You do not need to have public static IP address
- Usable in situations where you behind NAT (you in an enclosed network of your internet provider) or your IP address  changes often. Please figure this out with your provider.
- You can secure your Home assistant with google account.

Requirements:

- Cloudflare account
- Domain (DNS by Cloudflare)

Addon used: https://github.com/brenner-tobias/addon-cloudflared

1. Start by adding the Cloudflared and following the advanced addon setup. Please selected something like m.ha.your_domain.com.
2.  You are now probably in CF Zero Trust, go back into you domain dashboard and click SSL/TSL -> Client certificates.
3. First in the hosts you want to protect input the m.ha.your_domain.com, second click the Create Certificate. Select the Validity you want, and let the CF generate the cert for you by clicking Create. Copy the certificate into a client.pem and private key to client.key.
4.  run
```
openssl pkcs12 -export -out client_cert.pfx --passout pass:your_pass -inkey client.key -in client.pem
```
1. send the client_cert.pfx to your mobile phone and install the certificate by adding it.
2. If you want to use it from windows, install again by double clicking and installing. You will need to also disable QUIC protocol at eg. chrome:://flags
   https://support.eset.com/en/kb6757-disable-quic-protocol-in-google-chrome-browser
3. Now you will need the certificate to connect.
4. But this is not quite nice to always carry around.
5. We will create a second domain with different protection.
6. Go to CF Zero Trust -> Network -> Tunnels -> select your tunnel -> Edit ->Public hostnames. At this page add subdomain like desktop.ha.your_domain.com.
7. Stay at Zero Trust -> Access -> Applications -> Add application.
8. Select Self Hosted, Input your name and Add Hostname you just created.
9. Below you can find Policies, click create new policy. Input Name and In the Add Rules section select emails and input your mail. More about access https://developers.cloudflare.com/cloudflare-one/policies/access/. Save the new policy and go back to the Application creation form. Now select existing policy and save.
10. Upon visiting the domain you should see a window asking for an email. You will get a pin sent to your mail and will be access your instance from anywhere.


You can also add google as identity provider, meaning you will login into Google instead of sending a pin.

Google Identity - https://developers.cloudflare.com/cloudflare-one/identity/idp-integration/google/
One Time pin -	https://developers.cloudflare.com/cloudflare-one/identity/one-time-pin/
