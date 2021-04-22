(fcb-access-aspera)=
# How to download files with Aspera

+++
<br/>

----

````{panels}
:container: container-lg pb-3
:column: col-lg-3 col-md-4 col-sm-6 col-xs-12 p-1
:card: rounded

<i class="fa fa-qrcode fa-2x" style="color:#7e0038;"></i>
^^^
<h4><b>Recipe metadata</b></h4>
 identifier: <a href="">RX.X</a> 
 version: <a href="">v1.0</a>

---
<i class="fa fa-fire fa-2x" style="color:#7e0038;"></i>
^^^
<h4><b>Difficulty level</b></h4>
<i class="fa fa-fire fa-lg" style="color:#7e0038;"></i>
<i class="fa fa-fire fa-lg" style="color:#7e0038;"></i>
<i class="fa fa-fire fa-lg" style="color:lightgrey"></i>
<i class="fa fa-fire fa-lg" style="color:lightgrey"></i>
<i class="fa fa-fire fa-lg" style="color:lightgrey"></i>

---
<i class="fas fa-clock fa-2x" style="color:#7e0038;"></i>
^^^
<h4><b>Reading Time</b></h4>
<i class="fa fa-clock fa-lg" style="color:#7e0038;"></i> 15 minutes
<h4><b>Recipe Type</b></h4>
<i class="fa fa-laptop fa-lg" style="color:#7e0038;"></i> Hands-on
<h4><b>Executable Code</b></h4>
<i class="fa fa-play-circle fa-lg" style="color:#7e0038;"></i> Yes

---
<i class="fa fa-users fa-2x" style="color:#7e0038;"></i>
^^^
<h4><b>Intended Audience</b></h4>
<p> <i class="fa fa-user-md fa-lg" style="color:#7e0038;"></i> Principal Investigator </p>
<p> <i class="fa fa-database fa-lg" style="color:#7e0038;"></i> Data Manager </p>
<p> <i class="fa fa-wrench fa-lg" style="color:#7e0038;"></i> Data Scientist </p>  
````

---


## Main Objectives

This recipe is about documenting how to use the popular Aspera Fast Transfer Protocol.
This is part of a group of other related recipes about efficient files uploads and downloads .
While the Aspera protocol is used by major public repositories such as NCBI SRA and EMBL ENA, it is important to note that the communication protocol is **proprietary**.
The recipe will therefore also cover some of the implications of using a `closed protocol` in terms of FAIR compliance.



## Graphical overview

```{figure} aspera-mermaid.png
---
height: 1050px
name: Aspera Data Transfer Process
alt: Aspera Data Transfer Process
---
Aspera Data Transfer Process.
```

## Capability & Maturity Table

| Capability  | Initial Maturity Level | Final Maturity Level  |
| :------------- | :------------- | :------------- |
| Interoperability | minimal | repeatable |

----
## Obtain Aspering services

### Get Accounts Permissions:
* Apply for access
* Pay attention to the conditions
* Sign up if you are the appropriate person for this download/upload 
* Typically Aspera sites are locked down and need a username and password.
* For some sites, only one username is allowed per organisation, so it is worth making sure that that person is technically capable of uploading or downloading data, and also understands the data a little.
 
### Decide how you are going to access the data:
* A Web browser is great for initial browsing and downloading of small occasional files. It will automatically prompt you to download the Aspera broswer plugin to be able to do download any files.
* For heavy duty downloading an Aspera command line client is needed. e.g. to download gigabytes or even terrabytes of data.
 
### Decide on Software needed and get it installed:
 
* For linux:
  * Aspera ascp This can be downloaded from:  https://downloads.asperasoft.com/
  * Documentation:
    * General: https://download.asperasoft.com/download/docs/ascp/2.7/html/index.html
    * Examples https://download.asperasoft.com/download/docs/ascp/2.7/html/fasp/ascp-examples.html
 
#### Get the Firewall Configured as required to allow downloading and or uploading:
* You may need to have firewall exceptions raised to unblock ports 3301 and 22, with your organisation IT's network perimeter team. 
* Try connecting first in case they are already not blocked

#### Work out the appropriate command line options:
* For the Aspera command line, there are a large variety of options for downloading and uploading. See the download documentation above.
* Considerations:
  * Use the `-k {1,2,3}`  option to allow restarts without re-downloading all the data.
  * Run it using something like screen, so that it can be running in the background on a server
  * On the command line you can choose a preferred transfer rate. Please be careful to not hog the network bandwidth (we found up to about 100Mbps is okay).
 
#### Download Example command line:
* These are the download command options we used. (and both ports 3301 and 22 were unblocked)

```bash
#set the password variable corresponding to your Aspera account.
export ASPERA_SCP_FILEPASS="mypassword"
 
#example to download the files recursively from a specific directory on the Aspera server to
$ /hpc/apps/current/aspera/v3.9.6.app/bin/ascp -k 1 -P 33001  -o FileCrypt=decrypt aspera.myacc@aspera-immport.niaid.nih.gov:dir_to_download ./
```
 
* Ascp Version we used:
```bash
$ ascp --version
IBM Aspera Desktop Client version 3.9.6.176292
ascp version 3.9.6.176292
...
```

### Monitoring connections and file transfers

* Observe the  download/upload speed e.g. 100Mbs and then you can estimate the finish time
* Have some automated monitoring on the download process to  notify you if it  stops/finishes.  Even an hourly `du -sh` from a cron job
* Also typically you are pulling down many directories and files. On completion, it may be worth doing a recursive file listing to a file e.g. `ls -ltR > file_listing.txt` to give you and your "customers" a simple file catalogue.

### Considerations for uploading

* For uploading much of the above applies. The main differences are:
  * be aware of geographical zoning and which areas to upload to
  * prepare data for ease of tranfer, for instance, organize data in directories or consider data compression prior to transfer (note that this transfers a computational burden of decompression).

* Example command line for uploading
  * (Needed - no real example yet)

## Discussion

* Aspera is commercial software
* Is this still okay as part of FAIR principles? As long as the instution with the server has paid for the licence
* Action : ask EBI e.g. Tony or Fuqi (in the presentation)
* Action Philippe: will ask Mark Wilkinson if Aspera is compliant? and how it would work with his evaluator?
* Look at the dockerised version of the client?
* write a new recipe for uploading - probably update this.

### What to read next?

  - File transfer with FTP
  - FAIR Evaluation

---

## Authors

| Name           | Affiliation    | orcid          | CrediT role   |
| :------------- | :------------- | :------------- |:------------- |
| Peter Woollard  | GSK, metadata group in R&D Data and Computational Sciences  |  0000-0002-7654-6902 |  Writing - Original Draft |
| Philippe Rocca-Sera | Oxford University| | reviewer |
| | | | |



--- 

## License

This page is released under the Creative Commons 4.0 BY license.

<a href="https://creativecommons.org/licenses/by/4.0/"><img src="https://mirrors.creativecommons.org/presskit/buttons/80x15/png/by.png" height="20"/></a>