This interactive simulator helps you understand how firewalls protect different network zones. Click on any connection between zones to configure firewall rules.

The network consists of:

- **Internet**: The external world
- **DMZ (Demilitarized Zone)**: Public-facing servers like web and email
- **Internal Network**: Protected corporate network
- **Workstations**: Employee computers
- **Cloud Services**: External cloud resources

**Internet to DMZ:** Allow only HTTP and HTTPS traffic
**DMZ to Internal:** Allow HTTP, HTTPS, and SSH traffic
**Internal to DMZ:** Allow HTTP, HTTPS, and SSH traffic
**Internal to Cloud:** Allow HTTP, HTTPS, SSH, and SMTP traffic
**Internal to Workstations:** Allow all traffic types
