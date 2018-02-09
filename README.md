
## Usage

1. Place app in `./app`

2. Create Heroku-style `./app/Procfile`

3. Create `ansible/local.yaml` and customize it based on `ansbile/default.yaml`

4. Install Vagrant and https://github.com/cogitatio/vagrant-hostsupdater

5. Run vagrant up

6. Inside the vagrant box:

a. Place Heroku-style environ file at `/srv/app/conf/environ`

b. Install requirements in the virtual env: `sudo -u django /srv/app/env/bin/pip install -r /srv/app/releases/current/requirements.txt`

b. Run `sudo systemctl restart app`

7. Go to http://django.local/
