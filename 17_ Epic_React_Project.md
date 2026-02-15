✅ Ubuntu VM 
✅ Nginx
✅ VM has internet access
✅ VM inbound rules allow HTTP (Port 80)

##  Run these commands and verify outputs:
    hostname
    lsb_release -a
    nginx -v
    sudo systemctl status nginx --no-pager

##  Unzip:
    unzip -o site.zip
    ls -la

##  Move files from Local to Vm:
    scp -i your-key.pem -r . ubuntu@<EC2_PUBLIC_IP>:/tmp/portfolio

##  Connect to Vm:
    ssh -i your-key.pem ubuntu@<EC2_PUBLIC_IP>
    sudo rm -rf /var/www/html/*
    sudo cp -r /tmp/portfolio/* /var/www/html/
    sudo nginx -t && sudo systemctl reload nginx

    




###########################################################################################################################################


##  Install Software & Application Modification:
    Install Node.js & npm
    sudo apt update  
    sudo apt install -y nodejs npm  
    node -v && npm -v
    
##  Install and Start Nginx
    sudo apt install -y nginx  
    sudo systemctl start nginx  
    sudo systemctl enable nginx
    
##  Clone the React App Repo
    git clone https://github.com/pravinmishraaws/my-react-app.git  
    cd my-react-app  

##  Open the App.js file
##  Navigate to your React app’s source folder:
    cd my-react-app/src
    
##  Open the App.js file in a text editor:
    nano App.js
    
##  (or use vi/vim if you prefer)
##  Modify the content

##  Build Application for Production:
##  Install Dependencies & Build App
    npm install  
    npm run build 
    
##  Serve React App via Nginx
    sudo rm -rf /var/www/html/*  
    sudo cp -r build/* /var/www/html/  
    sudo chown -R www-data:www-data /var/www/html  
    sudo chmod -R 755 /var/www/html 
    
##  Configure Nginx
##  Replace the default config:
```
1.	echo 'server {
2.	  listen 80;
3.	  server_name _;
4.	  root /var/www/html;
5.	  index index.html;
6.	 
7.	  location / {
8.	    try_files $uri /index.html;
9.	  }
10.	 
11.	  error_page 404 /index.html;
12.	}' | sudo tee /etc/nginx/sites-available/default > /dev/null

```

    sudo systemctl restart nginx
    
##  Get your public IP:
    curl ifconfig.me

