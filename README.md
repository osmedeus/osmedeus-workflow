<p align="center">
  <img alt="Osmedeus" src="https://raw.githubusercontent.com/osmedeus/assets/main/logo-transparent.png" height="140" />
  <br />
  <strong>Osmedeus - A Workflow Engine for Offensive Security</strong>

  <p align="center">
  <a href="https://docs.osmedeus.org/"><img src="https://img.shields.io/badge/Documentation-0078D4?style=for-the-badge&logo=Google-Chrome&logoColor=39ff14&labelColor=black&color=black"></a>
  <a href="https://docs.osmedeus.org/donation/"><img src="https://img.shields.io/badge/Sponsors-0078D4?style=for-the-badge&logo=GitHub-Sponsors&logoColor=39ff14&labelColor=black&color=black"></a>
  <a href="https://twitter.com/OsmedeusEngine"><img src="https://img.shields.io/badge/%40OsmedeusEngine-0078D4?style=for-the-badge&logo=Twitter&logoColor=39ff14&labelColor=black&color=black"></a>
  <a href="https://discord.gg/gy4SWhpaPU"><img src="https://img.shields.io/badge/Discord%20Server-0078D4?style=for-the-badge&logo=Discord&logoColor=39ff14&labelColor=black&color=black"></a>
  </p>
</p>

***

## Osmedeus Workflow

Workflow is the core of the Osmedeus Engine which represents your methodology as YAML files.


## Installation

> NOTE that you need some essential tools like `curl, wget, git, zip` and login as **root** to start

```shell
bash -c "$(curl -fsSL https://raw.githubusercontent.com/osmedeus/osmedeus-base/master/install.sh)"
```

## Anatomy of Public Community methodology

![community-workflow](https://raw.githubusercontent.com/osmedeus/documentation/main/src/static/workflow/community-workflow.png)

## Usage

Check out [this page](https://docs.osmedeus.org/installation/usage#scan-actually-start-a-scan-based-on-predefined-workflow) to see how this workflow can be use to scan

```shell
# Practical Scan Usage:

## Start a simple scan with default 'general' flow
osmedeus scan -t sample.com

## Start a general scan but exclude some of the module
osmedeus scan -t sample.com -x screenshot -x spider

## Start a simple scan with other flow
osmedeus scan -f vuln -t sample.com

## Scan for CIDR with file contains CIDR with the format '1.2.3.4/24'
osmedeus scan -f cidr -t list-of-cidrs.txt
osmedeus scan -f cidr -t '1.2.3.4/24' # this will auto convert the single input to the file and run

## Directly run the vuln scan and directory scan on list of domains
osmedeus scan -f vuln-and-dirb -t list-of-domains.txt

## Directly run the general but without subdomain enumeration scan on list of domains
osmedeus scan -f domains -t list-of-domains.txt

## Use a custom wordlist
osmedeus scan -t sample.com -p 'wordlists={{.Data}}/wordlists/content/big.txt' -p 'fthreads=40'

## Scan list of targets
osmedeus scan -T list_of_targets.txt

## Get target from a stdin and start the scan with 2 concurrency
cat list_of_targets.txt | osmedeus scan -c 2

```


## 👨‍💻 Contribute

If you have found some valuable tool or suggest to use the tool in each module better feel free to open an issue for just DM me via [@j3ssiejjj](https://twitter.com/j3ssiejjj).


## 💬 Community & Discussion

Join Our Discord server [here](https://discord.gg/gy4SWhpaPU)

## 💎 Donation

Please check out [this page](https://docs.osmedeus.org/donation/) for couple donation methods here

## License

`Osmedeus` is made with ♥ by [@j3ssiejjj](https://twitter.com/j3ssiejjj) and it is released under the MIT license.
