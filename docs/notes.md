https://github.com/JamesIves/github-pages-deploy-action/tree/dev#using-an-ssh-deploy-key-
Using an SSH Deploy Key 🔑
If you'd prefer to use an SSH deploy key as opposed to a token you must first generate a new SSH key by running the following terminal command, replacing the email with one connected to your GitHub account.

ssh-keygen -t rsa -m pem -b 4096 -C "youremailhere@example.com" -N ""
Once you've generated the key pair you must add the contents of the public key within your repository's deploy keys menu. You can find this option by going to Settings > Deploy Keys, you can name the public key whatever you want, but you do need to give it write access. Afterwards, add the contents of the private key to the Settings > Secrets menu as DEPLOY_KEY.

With this configured, you can then set the ssh-key part of the action to your private key stored as a secret.

- name: Deploy 🚀
  uses: JamesIves/github-pages-deploy-action@v4
  with:
    folder: site
    ssh-key: ${{ secrets.DEPLOY_KEY }}
You can view a full example of this here.
Alternatively, if you've already configured the SSH client within a previous step you can set the ssh-key option to true to allow it to deploy using an existing SSH client. Instead of adjusting the client configuration, it will simply switch to using GitHub's SSH endpoints.


target repo - public key - deploy key
source repo - private key - ssh-key DEPLOY_KEY - secret