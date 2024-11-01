# Furblend
Furblend is a web app that lets you render blender projects remotely on your home pc when you are away. 

## Usage
After the server is up and running, a web interface will be accessible through port `5510`, or the one you specified in environment variable. \
\
Default username: `furblend` \
Defualt password: `000000` 

## Install
### Node.js runtime
Furblend uses node.js. If you already have node installed, you can skip this part. \
It's recommended to use the latest LTS version. \
If you have experience with programming, it's recommended to use a [package manager](https://nodejs.org/en/download/package-manager).\
If you are not comfortable with computers, you can use an [installer](https://nodejs.org/en/download/prebuilt-installer) to install the regular way.
### Install
Download and extract the latest release into a folder and copy the folder's path. \
Open terminal(if you are on windows, use powershell), and run these command in order
```
cd <folder path here>
npm install
```
After that, you can use `node build/app.js` to start the server. Press Ctrl-C to stop. \
\
It's recommended to use a process manager to manage the server. Here, we will use pm2. \
First, install pm2: \
If you are on windows, open powershell as administrator and run: \
`npm install -g pm2` \
\
If you are on mac or linux, run: \
`sudo npm install -g pm2` \
\
Afterwards, go back to the terminal you opened the folder in, and run: \
`pm2 start build/app.js` \
\
**Congratulations, you now have the server up n running!** \
You can then open `http://localhost:5510` in a web browser to access the dashboard. \
\
To access the dashboard through internet, you need to either setup port forwarding on your router, or use a port forwarding service.

## Configuration
There are two things thats configurable. Port number and access username & passwords. \
\
To change port number, edit the file named `.env` with a text editor. Restart the server after saving by: \
`pm2 restart 0`
\
To add/change username & password, open the file named `credentials.json` with a text editor and follow the following instructions: \
By default, the file should look like this:
```
{
  "furblend": "$2a$12$U50d2nTyfITrZ3HnUeXkaeHR2WehVwaMhxnG5b3Ml45SLnLkMCLPC"
}
```
To add a user, add a comma at the end of the second line and make new line. \
The key name is the username, and the value is the [bcrypt hash](https://bcrypt-generator.com) of the password. \
Here, we will add a user named "john", and their password is "superjohncafe"
```
{
  "furblend": "$2a$12$U50d2nTyfITrZ3HnUeXkaeHR2WehVwaMhxnG5b3Ml45SLnLkMCLPC",
  "john": "$2a$12$m3pzX9uiTiO1CdissBl2gOmFTK8BPG7TMxBQE3jLz4P1hj6CGcaou"
}
```
To change a username, simply replace the old key name with the new one. \
To change a password, simply replace the old hash with the new hash. \
\
Afterwards, save the file and restart the server (if server is managed through pm2, you can restart it by: \
`pm2 restart 0`\
\
If the server crashes afterwards, you likely have an extra comma or missing a double quote or comma. You can check if everything is correct using a [JSON checker](https://jsonchecker.com/)
