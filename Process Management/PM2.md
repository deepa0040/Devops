- PM2 is a production process manager for Node.js applications.  

- Here's a summary of key concepts and commands:
<br>
<br>

  **Key Features:**
  
- Process Management: Keeps apps running, auto-restarts on crashes.
- Load Balancing: Cluster mode for multi-core CPUs.
- Zero-Downtime Deployment: Updates without service interruption.
- Process Monitoring: CPU, memory usage, etc.
- Log Management: Centralized log viewing and rotation.
- Startup on Boot: Automatic app launch on server restart.
<br>
<br>

**Installation:**
<br>

Bash
```
npm install -g pm2
```

Basic Commands:

Start:

```
pm2 start app.js (Start app)
pm2 start app.js --name "My App" (Named app)
pm2 start app.js -i max (Cluster mode, max cores)
pm2 start app.js -i 4 (Cluster mode, 4 instances)
pm2 start ecosystem.config.js (Start using config file)
```

List:

```
pm2 list or pm2 ls (List running apps)
```

Stop:

```
pm2 stop "My App" (Stop by name)
pm2 stop app.js (Stop by filename)
pm2 stop all (Stop all apps)
```

Restart:

```
pm2 restart "My App"
pm2 restart all
```

Delete:

```
pm2 delete "My App"
pm2 delete all
```

Monitor:

```
pm2 monit (Real-time monitoring)
pm2 logs "My App" (View logs)
```

Logs:

```
pm2 logs (All logs)
pm2 flush (Clear logs)
pm2 reloadLogs (Reload log configuration)
```

Startup on Boot:

```
pm2 startup (Generate startup script)
pm2 save (Save process list for startup)
pm2 unstartup (Disable startup)
```

Zero-Downtime Deployment: (using ecosystem.config.js)

```
pm2 deploy ecosystem.config.js <environment> setup
pm2 deploy ecosystem.config.js <environment> update
```

Reference:

- https://tn710617.github.io/pm2/
- https://pm2.io/docs/runtime/overview/
