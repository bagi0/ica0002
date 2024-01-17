## Backup Service Level Agreement (SLA)

# ICA0002 
# Rashad Baghiyev 214075IVSB

# Infrastructure Backup Overview
This SLA outlines the backup strategy for the critical components of our IT infrastructure developed and managed during the course. It ensures data integrity, availability, and swift recovery in case of data loss.

# Infrastructure Components Covered
Database Server: MySQL storage of structured data for agama application.
InfluxDB: Time-series data storage for monitoring and metrics.

# Recovery Point Objective (RPO)
Backup Frequency: Daily
Backup Window: 18:30 - 20:00 UTC+2 (Estonian time)
Acceptable Data Loss: Maximum of 24 hours.

# Restoration Criteria
Backups are considered for restoration in the following scenarios:
Extended Downtime: Service downtime exceeding 6 hours.
Data Corruption: Irrecoverable data loss or corruption impacting service functionality.
Disaster Recovery: In the event of critical system failures or cyber attacks.
