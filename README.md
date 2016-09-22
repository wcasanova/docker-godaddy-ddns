# docker-godaddy-ddns
Docker image to provide a DDNS service for godaddy domains

## Running
First, get a GoDaddy developer key & secret from https://developer.godaddy.com/keys/. Log in with your GoDaddy account then generate the API key/secret. Note that the very first time you do this, it will be created as .Test. environment (seen at the time of writing). Go back to the same page again or click on the .Keys. top menu then generate a new .Production. API key/secret instead.

To update a subdomain (second-level domain i.e. subdomain.domain.com) instead of primary domain (top-level domain i.e. domain.com), set Type=CNAME and Name=subdomain where subdomain is your subdomain.domain.com as seen in the GoDaddy DNS setup page.

Update IPV4 address for single mydomain.com
```
sudo docker run -d --name=ddns --restart=always \
	-e "GODADDY_KEY=<YOUR_KEY>" \
	-e "GODADDY_SECRET=<YOUR_SECRET>" \
	-e "GODADDY_DOMAIN=mydomain.com" \
	peteward44/godaddy-ddns
```

Update IPV4 address for mysubdomain.mydomain.com
```
sudo docker run -d --name=ddns --restart=always \
        -e "GODADDY_KEY=<YOUR_KEY>" \
        -e "GODADDY_SECRET=<YOUR_SECRET>" \
        -e "GODADDY_DOMAIN=mydomain.com" \
        -e "GODADDY_TYPE=CNAME" \
        -e "GODADDY_NAME=mysubdomain" \
        peteward44/godaddy-ddns
```

For IPV6 domain mydomain.com
```
sudo docker run -d --name=ddns --restart=always \
        -e "GODADDY_KEY=<YOUR_KEY>" \
        -e "GODADDY_SECRET=<YOUR_SECRET>" \
        -e "GODADDY_DOMAIN=mydomain.com" \
        -e "GODADDY_TYPE=AAAA" \
        -e "GODADDY_NAME=@" \
        -e "GODADDY_IPV6=1" \
        peteward44/godaddy-ddns
```

For IPV6 subdomain mysubdomain.mydomain.com
```
sudo docker run -d --name=ddns --restart=always \
        -e "GODADDY_KEY=<YOUR_KEY>" \
        -e "GODADDY_SECRET=<YOUR_SECRET>" \
        -e "GODADDY_DOMAIN=mydomain.com" \
        -e "GODADDY_TYPE=AAAA" \
        -e "GODADDY_NAME=mysubdomain" \
        -e "GODADDY_IPV6=1" \
        peteward44/godaddy-ddns
```

## Building
sudo docker build --rm -t peteward44/godaddy-ddns .

## Credit
Uses modified script from http://teanazar.com/2016/05/godaddy-ddns-updater/
