# Haven
This vagrant file was created to allow developers run ansible deploy scripts between servers running on their own machine.
This vagrant file creates a private network of 2 centos machines , ansible is installed on one called the appDeployer.
The keys for the deployer are also transferred across to the appserver host so that appDeployer machine can execute ansible scripts on it.



# Setup
git clone https://github.com/hennesb/haven.git

Run `vagrant up` , this should start both servers

To test 

Run `vagrant ssh appDeployer` when you get the shell run `ansible -m ping all` . You should get a response similar to

172.28.128.4 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}


# Corporate Proxies
If your running this behind a corporate proxy download the vagrant-proxy conf and modify the Vagrantfile with

config.proxy.http=x.x.x.x:80
config.proxy.https=x.x.x.x:443
