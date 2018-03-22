## RStudio in the cloud

Following [these notes from Matt
Strimas-Mackey](http://strimas.com/r/rstudio-cloud-1/), I was able to
get RStudio in a web browser using Amazon Web Services. (And then I
left it running for months. Oops.)

I want to get back and fire one up for my son to use on his chromebook
when he's at school. Instructions below.

But all this is basically made moot by the introduction of [RStudio
Cloud](https://rstudio.cloud), which basically does the same thing
better and easier, plus more, and at least for now it's free.

1. Log into the [AWS Console](https://console.aws.amazon.com)

2. Click on "EC2" under "Compute"

3. I'd previously created a security group ("SSH and HTTP for RStudio
   Server") and an SSH key pair.

4. Launch an instance

   - Click "Launch an instance"

   - Click on "Community AMIs" on the left

   - Search for "rstudio aslett"

   - Pick one (e.g. `RStudio-1.0.153_R-3.4.1...`) and click "Select"

   - Choose instance type (t2.micro free tier eligible)

   - Click "Configure instance details"

   - Under "Advanced Details" and add a script in the user data box

     ```shell
     #!/bin/bash
     apt-get update -y
     ```

     You could put installation of packages here, to save time later

   - Click "Next: Add storage" (10 GiB should be sufficient)

   - Click "Next: Add tags" (give your instance a name like "rstudio")

   - Click "Next: Configure Security Group"

   - Choose "Select an existing security group" and Select the "SSH
     and HTTP for RStudio Server"

   - Click "Review and Launch" and then "Launch"

   - Select the key pair made earlier ("Choose an existing key pair"
     and "aws")

   - You need to have access to the corresponding private key file,
     `aws.pem`. Mine's stored in my `~/.ssh1 directory. Acknowledge
     this and click "Launch instance".

5. Connect to the EC2 instance via SSH to change the password (user is
   `rstudio` and the default password is `rstudio`

   ```shell
   ssh -i ~/.ssh/aws.pem ubuntu@ec2-67-03-69-63.us-west-2.compute-amazonaws.com
   sudo passwd rstudio
   ```

6. Then go to that `ec2-...-us-west-2.compute-amazonaws.com` address
   in a web browser and enter `rstudio` as username and the password
   you created.

   Or use following to change that password within RStudio.

   ```r
   RStudioAMI::passwd()
   ```

---

I could connect to the instance from my work computer but not from my
laptop. It turns out that I'd restricted the inbound rules to be from
my IP address for my work desktop or at home.

It's possible to edit the security group while it's running:

- Go to the EC2 Dashboard
- Click on "Security Groups"
- Select the relevant group and then the "Action" button above, and
  then choose "Edit inbound rules"
- You could add additional lines that make it open from other IPs
