# Auto-Scaling

## Monitoring and Responding to load/traffic

### Worst to Best Practices
- Manual Monitoring: This requires constant human intervention and is prone to errors.
- Threshold-Based Alerts: This provides basic monitoring but lacks scalability and responsiveness. 
- Autoscaling: This automatically adjusts resources based on predefined thresholds, making sure that performance and resource utilisation is optimal.
- Predictive Scaling: This uses historical data and machine learning algorithms to anticipate traffic spikes and scale resources proactively.

## How you setup a dashboard

- Go to Azure portal > Overview > Monitoring tab. 
- Select desired performance metrics.
- Click "Show more charts" to see more.
- Pin the metrics to a new shared dashboard. 
  
  <img src="../assets/img35.png">
  <img src="../assets/img36.png">

- Create "Create new" > Type: choose "Shared" > Specify Dashboard name, Subscription and Resource group.
- Click "Create and pin".
- Optionally, add existing dashboards to the shared dashboard. 
- Search for "Dashboard hub" in the portal to access the dashboard.
  
  <img src="../assets/img37.png">

     *Note: You can also edit these by changing the rate from daily to hourly or every 30 minutes etc.*

## Load Testing
Get VMs to run the app and load test them:

- SSH into the application VM and install Apache Bench: 
  ```
  sudo apt-get install apache2-utils -y
  ```
- Perform load testing with Apache Bench by sending requests with specified concurrency levels:
  ```
  ab -n 1000 -c 100 http://172.166.125.223
  ```
    <img src="../assets/img38.png">


Key takeaway(s):
- Combining load testing and theerformance metrics on the dashboard helps to monitor resource usage and application response.
- Therefore, you can load testing data to set thresholds for alerts and trigger notifications for high CPU load.

## Setting Up CPU usage alert

- On Azure Portal, go to the Virtual Machine.
- Click 'Overview'
- Go to Monitoring > Alerts > New alert rule. 
- Choose the appropriate metric (e.g., CPU usage). 
- Set the condition to trigger the alert (e.g., average CPU usage exceeds a certain threshold). 
- Define the criteria for the alert (e.g., average CPU usage for each minute).
- Specify the action group to notify (e.g., email notification). 
- Review and Create.
- Click "Create" to save the alert rule.

Note: the threshold is low enough that the CPU utilisation will trigger an alert when you do heavy load testing and you get an email notification.

### Email Notification

- Wait for the alert condition to be met (e.g., CPU usage exceeds the threshold).
- Check your email inbox for the notification sent by Azure Alert.

