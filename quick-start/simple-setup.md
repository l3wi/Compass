# Simple Compass setup

- Freshly installed Ubuntu 18.04 LTS Server
- At least 8GB RAM, preferably 4 cores+ (the more cores the faster inital setup complete)
- At least 10GB SSD

## Dependencies install

First we install what we need for Bazel to install:

	sudo apt-get install pkg-config zip g++ zlib1g-dev unzip python


Next we retrieve the installer

	wget https://github.com/bazelbuild/bazel/releases/download/0.18.0/bazel-0.18.0-installer-linux-x86_64.sh

Next we need to make sure we can execute this script before we can actually run it:

	chmod +x bazel-0.18.0-installer-linux-x86_64.sh

After doing this we can install Bazel, we will install it under your currently active user using the `--user` flag:

	./bazel-0.18.0-installer-linux-x86_64.sh --user

Now that Bazel is installed we need to install Docker and jq:

	sudo apt install apt-transport-https ca-certificates curl software-properties-common
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
	sudo apt update
	sudo apt install docker-ce

That was Docker, First we need universe repo for jq:
	
	sudo add-apt-repository universe
	sudo apt install jq

## Cloning into Compass

    git clone https://github.com/iotaledger/compass.git
    cd compass

## Calculating the Merkle tree

Install it first:

	bazel run //docker:layers_calculator

Next we need to think of a depth, 2^depth, so a depth of 16 is 2^16 (65536), if you issue milestones every minute you can run 2^depth minutes of COO before you run out of Merkle tree, so the depth needs to be high enough, but on the other hand the higher the depth the longer the tree generation takes. 

For our demo purpose we'll use a depth of 16, this allows us to run compass for 45 days in a row at 1 minute milestone intervals. Calculating the tree for this will not take as long. 

For comparison: A depth of 24 would  allow you to run Compass for over 31 years but it will take a lot of CPU hours to generate that tree. 

Generate the seed for the COO:

	cat /dev/urandom |LC_ALL=C tr -dc 'A-Z9' | fold -w 81 | head -n 1 

Enter the docs dir for private tangle

	cd docs/private_tangle

	cp config.example.json config.json

Run the docker image for layers calculator (TODO: Check if this is still needed when installing Docker BEFORE building layers_calculator)

	sudo ~/compass/bazel-bin/docker/layers_calculator


	sudo ./01_calculate_layers.sh

This outputs:

	[main] INFO org.iota.compass.LayersCalculator - Calculating 65536 addresses.
	...
	[main] INFO org.iota.compass.LayersCalculator - Successfully wrote Merkle Tree with root: JMRTYHMGNZGNOLPSSBVLWRPMGIAMOXPLURNDIBKXIFTCJCLOYKH9FMVNKPBVFVMGSUFEYVUUIEARFQXAK

This took around 15 minutes on a 4-core VM at depth 16.

## Run IRI

	cp snapshot.example.txt snapshot.txt

Edit the `config.json`, add in the line `milestoneStart: 1` then run:

	sudo ./02_run_iri.sh


## Run COO

	bazel run //docker:coordinator

Run the COO docker image

	sudo ~/compass/bazel-bin/docker/coordinator


	sudo ./03_run_coordinator.sh -bootstrap -broadcast

