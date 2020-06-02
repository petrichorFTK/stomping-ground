# stompingground
Stomping Ground - a personal lab that I will expand upon to meet my exploratory needs!

I needed a way to quickly add boxes to an ever expanding home 'virtualizes' lab to meet my needs. This is just a quick and dirty start that I will add too.

Things to note:
1. I do not use Vagrant's default key so I encourage you to generate your own keys and place them in the same directory where you are running Vagrant. 

2. This does not take care of any networking. Vagrant needs the first interface of everybox to be NAT'd so it can talk to it.

3. All these boxes come from Vagrant Cloud and there is ZERO checking for badness on them. Do not use these on production networks. I can testify that I did not put anything malicious on the boxes I use in the Vagrantfile but I also did nothing to harden them :)
