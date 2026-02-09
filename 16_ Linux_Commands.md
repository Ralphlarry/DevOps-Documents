PHASE 1: NETWORKING & ACCESS CHECKS (PRODUCTION BASICS)
IPs and interfaces (help confirm network is up):
  ip a

Default route (proves you can reach the internet via gateway):
  ip route

DNS resolution (proves name → IP works):
  dig pravinmishra.com +short
          (or)
  host pravinmishra.com

Connectivity test (quick packet-level check):
  ping -c 4 thecloudadvisory.com

Listening ports + owning process (what is actually exposed):
  sudo ss -tulpen

Firewall status (basic security signal, even if not configured):
  sudo ufw status

PHASE 2: SERVICE HEALTH + PROCESS VALIDATION (SYSTEMD STYLE)
This phase checks whether the service is healthy AND manageable like production.
Service status:
  systemctl status nginx --no-pager

Check enabled on boot (reliability):
  systemctl is-enabled nginx

Verify Nginx config is valid (prevents bad restarts):
  sudo nginx -t

Identify master/worker processes:
  ps aux | grep -E "nginx: master|nginx: worker" | grep -v grep

Confirm which PID is listening on port 80:
  sudo ss -lptn '( sport = :80 )'

Safe restart drill (simulate a routine deploy):
   sudo systemctl restart nginx
   systemctl status nginx --no-pager

PHASE 3: LOGS & REQUEST TRACE (REAL DEVOPS WORK)
In industry, “it’s working” is not enough. We check logs to confirm clean traffic and find hidden errors.
Generate a request so logs update (do this first):
  curl -s http://public> /dev/null
  curl -I http://public> /dev/null

Access logs (traffic proof):
  sudo tail -n 30 /var/log/nginx/access.log
  
Error logs (failures, misconfig, permission issues):
  sudo tail -n 30 /var/log/nginx/error.log

Systemd journal (service-level problems):
  sudo journalctl -u nginx --no-pager -n 50

PHASE 4: SYSTEM RESOURCE HEALTH (CAPACITY RED FLAGS)
Load and uptime:
  uptime

CPU/memory view (quick):
  free -h

Disk usage:
  df -h

Biggest consumers under /var (logs often fill disks in real life):
  sudo du -sh /var/* | sort -h

PHASE 5: CONFIGURATION & CONTENT INTEGRITY (RELEASE SAFETY)
Real teams verify config + content after deploy.
Confirm correct web root has build files:
  ls -lah /var/www/html | head -n 20

Confirm Nginx is serving your build (not default page):
  grep -R "Deployed by" -n /var/www/html 2>/dev/null | head

Confirm Nginx config has SPA routing:
  grep -n "try_files" /etc/nginx/sites-available/default

Task A (Recommended): Bad config deployed
Introduce a tiny syntax error:
  sudo nano /etc/nginx/sites-available/default

Confirm config is broken:
  sudo nginx -t (must fail)

Fix the config back
Validate and restart:
   sudo nginx -t
   sudo systemctl restart nginx
   curl -I http://publicIP

Task B: Web content missing after deployment
Break content safely (backup first):
  sudo mv /var/www/html /var/www/html_backup
  sudo mkdir -p /var/www/html
  sudo rm -rf /var/www/html
  sudo mv /var/www/html_backup /var/www/html
  sudo systemctl restart nginx
  curl -I http://publicIP

  access.log
  error.log
  journalctl -u nginx

