# Jupyter on EC2

## Setup

Set up an EC2 instance (free tier Amazon Linux AMI). Also, create and download a key pair.

Navigate to the directory that contains your private key file and then enter:
```bash
chmod 400 nameofyourprivatekey.pem
```

Connect to the machine via SSH:
```bash
ssh -i ./nameofyourprivatekey.pem ec2-user@your-ec2-public-ip
```

Ensure python3 and pip3 are installed on the machine. Since both python 2 and 3 were pre-installed on the ec2 instance, I added the following aliases to ~/.bashrc:
```bash
alias python=python3
alias pip=pip3
```

We can run the following commands to install Python 3 and pip (if not installed already):
```bash
sudo yum install -y python37
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py sudo python3 get-pip.py
```

And, install Jupyter:
```bash
pip install --user jupyter
```

## Connect to Jupyter on the EC2 machine

### Option 1 (Connect directly to the machine on port 8888)

Set up a firewall restriction so that we can connect directly to the machine on port 8888.

1. Select your EC2 instance
2. Under “Description”, select security groups
3. Click “Actions” -> “Edit Inbound Rules”
4. Add a new rule: change the port to 8888, select “My IP”
5. Click “Save”

Connect to Jupyter on the EC2 machine via the private IP:
```bash
jupyter notebook --ip your-private-ip
```

### Option 2 (Connect using SSH tunneling)

Reference: https://gist.github.com/jakechen/faf0500132d46d83517004bbfedbe5de

Ensure the instance is assigned to a security group with SSH access (usually assigned by a default security group inbound rule).

Open SSH Tunnel and start Jupyter Notebook:

1. Tunnel into your instance by adding -D -L localhost:8888:localhost:8888 to your SSH connection string. This should look like ssh -i "nameofyourprivatekey.pem" ec2-user@ec2-123-456-789-123.compute-1.amazonaws.com -D -L localhost:8888:localhost:8888 .
2. Start Jupyter Notebook in the background.
We recommend using something like screen, tmux, or nohup to keep your notebook in the background even if you lose connection to your instance. Otherwise you may lose your in-progress models.
Launch Jupyter Notebook using jupyter notebook --no-browser. The --no-browser flag prevents the server from launching a browser.
Tunnel into Notebook

Open up any web browser and point it to http://localhost:8888