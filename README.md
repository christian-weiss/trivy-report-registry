# Continous Vulnerability Monitoring
Instead of scanning docker images only once (directly after you build it), you may want to get informed when your image 
become insecure due to newly discovered vulnerabilities. 

If you want to install a docker image, which was build last 
week, you should have an up-to-date vulnerability report, to see if it is still safe to use that image. 

If a docker image is already used by you in e.g. a production system you may want to get notified when the docker image 
has become insecure. 

If you use immutable systems then you can safly offload that vulnerability scan with Trivy 
Report Registry. This ensures that the performance of your production system is not affected and that you do not 
need to open-up our network and system policies for a scanner.  
 
## A scan per day, keeps the attacker away
Trivy Report Registry starts to continous monitor your docker image release directly after Trivy gets triggered the very
first time about that specific docker image release. Trivy Report Registry ensures that this release is tested for new 
vulnerabilities every day. 

## Transparency for docker image status
Trivy Report Registry allows you (as a docker image vendor) to easily share security relevant reports with your 
community of users. Easy navigation from docker images to reports, to source code and combined with nice eyecatcher 
shield.io badges give you all the information at ease of use.

## Reports
Trivy Report Registry lists all vulnerability reports of each version of your docker image, for all your docker images.

## Easy Navigation between tools
You can easily navigate back to your source code, to your docker hub autobuild log and to autotest log. 
By adding a link e.g. in your README.md back to Trivy Report Registry you can enable navigation in both directions from 
github and docker hub. We recommend to link to the index page of your docker image at Trivy Report Registry. It is also 
possible to set a deep link specific or to the latest release.

## Badges
Trivy Report Registry also provides two badges for each docker image release:
 + Vuln Risk
 + Vuln Report Age

All badges are powered by shield.io so you can manage your style the same way as you do for most other badges from other vendors.

### Vuln Risk Badge
It shows the highest detected rating level (CVSS severity) in your vulnerability report and counts of all issues 
in that rating level. Depending on the rating level the badge is colored from green to red.

Severity Levels:
 + ![TRR Badge Risk CRITIAL](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnRisk_CRITICAL.json) 
 + ![TRR Badge Risk HIGH](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnRisk_HIGH.json) 
 + ![TRR Badge Risk MEDIUM](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnRisk_MEDIUM.json) 
 + ![TRR Badge Risk LOW](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnRisk_LOW.json) 
 + ![TRR Badge Risk NONE](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnRisk_NONE.json) 

 
### Vuln Report Age
It shows how old (in days) the report for that docker image release is. 

Colors:
- ![TRR Badge Age ok](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnCheck_1day.json) 0 day = green (less then 1 day) 
- ![TRR Badge Age problem](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnCheck_2days.json) 1+ days = orange (less then 7 days)
- ![TRR Badge Age outdated](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/christian-weiss/trivy-report-registry/master/examples/badges/VulnCheck_aged.json) 7+ days = red (more then 7 days) 

If the age count is > 1 day means that there is probably a problem with your pipeline. 
After 7 days even the most relaxed person should no longer trust in your image.
See troubleshooting section.

## Limitations of Trivy Report Registry (TRR)
Trivy Report Registy is to help open source and low budget projects to easily automate vulnerability 
scans without hosting costs or service plans. It is meant to scan your project images, but not to scan all
docker images on this planet, as you would avoid the terms of use of your docker hub account and risk being banned.

Trivy Report Registry helps you to setup a cross-service pipeline between:
+ Github
+ Docker Hub
+ Trivy Report Registry

## Install Trivy Report Registry (TRR)
See [how to install TRR](docs/INSTALL.md)

## Usage
See [how to use TRR](docs/USAGE.md)