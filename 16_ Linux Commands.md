PHASE 1: NETWORKING & ACCESS CHECKS (PRODUCTION BASICS)
1.	IPs and interfaces (help confirm network is up):
  ip a
2.	Default route (proves you can reach the internet via gateway):
ip route
3.	DNS resolution (proves name → IP works):
dig pravinmishra.com +short
(or)
host pravinmishra.com
4.	Connectivity test (quick packet-level check):
ping -c 4 thecloudadvisory.com
5.	Listening ports + owning process (what is actually exposed):
sudo ss -tulpen
6.	Firewall status (basic security signal, even if not configured):
sudo ufw status

PHASE 2: SERVICE HEALTH + PROCESS VALIDATION (SYSTEMD STYLE)
This phase checks whether the service is healthy AND manageable like production.
1.	Service status:
systemctl status nginx --no-pager
2.	Check enabled on boot (reliability):
systemctl is-enabled nginx
3.	Verify Nginx config is valid (prevents bad restarts):
sudo nginx -t
4.	Identify master/worker processes:
ps aux | grep -E "nginx: master|nginx: worker" | grep -v grep
5.	Confirm which PID is listening on port 80:
sudo ss -lptn '( sport = :80 )'
6.	Safe restart drill (simulate a routine deploy):
1.	sudo systemctl restart nginx
2.	systemctl status nginx --no-pager

PHASE 3: LOGS & REQUEST TRACE (REAL DEVOPS WORK)
In industry, “it’s working” is not enough. We check logs to confirm clean traffic and find hidden errors.
1.	Generate a request so logs update (do this first):
1.	curl -s http://public> /dev/null
2.	curl -I http://public> /dev/null
2.	Access logs (traffic proof):
sudo tail -n 30 /var/log/nginx/access.log
3.	Error logs (failures, misconfig, permission issues):
sudo tail -n 30 /var/log/nginx/error.log
4.	Systemd journal (service-level problems):
sudo journalctl -u nginx --no-pager -n 50

PHASE 4: SYSTEM RESOURCE HEALTH (CAPACITY RED FLAGS)
1.	Load and uptime:
uptime
2.	CPU/memory view (quick):
free -h
3.	Disk usage:
df -h
4.	Biggest consumers under /var (logs often fill disks in real life):
sudo du -sh /var/* | sort -h

PHASE 5: CONFIGURATION & CONTENT INTEGRITY (RELEASE SAFETY)
Real teams verify config + content after deploy.
1.	Confirm correct web root has build files:
ls -lah /var/www/html | head -n 20
2.	Confirm Nginx is serving your build (not default page):
grep -R "Deployed by" -n /var/www/html 2>/dev/null | head

3.	Confirm Nginx config has SPA routing:
grep -n "try_files" /etc/nginx/sites-available/default

Task A (Recommended): Bad config deployed
1.	Introduce a tiny syntax error:
sudo nano /etc/nginx/sites-available/default
2.	Confirm config is broken:
sudo nginx -t (must fail)
3.	Fix the config back
4.	Validate and restart:
1.	sudo nginx -t
2.	sudo systemctl restart nginx
3.	curl -I http://publicIP
Task B: Web content missing after deployment
1.	Break content safely (backup first):
1.	sudo mv /var/www/html /var/www/html_backup
2.	sudo mkdir -p /var/www/html
3.	sudo rm -rf /var/www/html
4.	sudo mv /var/www/html_backup /var/www/html
5.	sudo systemctl restart nginx
6.	curl -I http://publicIP

access.log
error.log
journalctl -u nginx

