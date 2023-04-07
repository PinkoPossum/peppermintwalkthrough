# Peppermint Walkthrough

In Linode, at the top left - as pictured below - click create and then select "Linode" from the drop down.
![step one](https://user-images.githubusercontent.com/120178527/230673624-abd4d456-6dea-4bb9-a927-70de0ba447ca.png)

Once at the creation screen, select "Marketplace" as pictured below.
![step two](https://user-images.githubusercontent.com/120178527/230673823-f5b4e408-916b-436e-ba14-1ba1978a81a2.png)

Below "select an app" type "peppermint" into the search bar and you should select the option pictured below.
![step three](https://user-images.githubusercontent.com/120178527/230673951-8c8e072a-4337-4578-b14b-a226daa3aa01.png)

Now, scrolling down you will see "select an image", "region", and "linode plan". For the image I recommend Ubuntu due to the wide availability of documentation; however, as Ubuntu is based on Debian the documentation should translate over well if you'd rather use Debian. Next, for region, select whichever is closest to your physical location, for me it is Dallas, TX. Finally, pick your plan, if you're using this for friends and loved ones as I am, select a shared cpu plan as it is the most cost effective.
![step four](https://user-images.githubusercontent.com/120178527/230674281-20481aa9-c719-4d32-be44-7db27acf5d89.png)

Scrolling down again you'll find an entry field to name your server. If you only plan to run one you can just leave it as the default. Next create a secure but memorable password, this will be your root password when interfacing with the server.
![step five](https://user-images.githubusercontent.com/120178527/230674575-52edc51a-8548-4f18-b595-1778ec2552dd.png)

Finally, scroll down and press "Create".

On this page we will be accessing the LISH Console. As pictured below, click on "Launch LISH Console".
![step six](https://user-images.githubusercontent.com/120178527/230674748-6f3d90a1-3402-4494-9692-aa91b2195c31.png)

A console window will pop up and you'll see it populate with system information as the linode is setup. Once you are prompted to login you'll know it is complete.

Go ahead and enter root as the username and then your password.
![step seven](https://user-images.githubusercontent.com/120178527/230674817-dc555681-7c66-45db-b5b6-73deee28fc6b.png)

Once we're logged in, we'll type docker ps. After pressing return we will get an output that contains the port our linode is using, in this case 5001. 
![step eight](https://user-images.githubusercontent.com/120178527/230674863-d08b0ae1-bbc3-42db-a61d-2c2146ffd523.png)

Back on our control panel, go to "Network".
![step nine](https://user-images.githubusercontent.com/120178527/230674965-dea6b477-9ff3-4a64-8bc6-58c2ebbcdd02.png)

Scrolling down a bit to "IP Addresses" we are looking for the IP Address direclty below the "Reverse DNS" column. 
![step ten](https://user-images.githubusercontent.com/120178527/230675067-0cbd5e6a-7169-43f8-a686-253709ea3108.png)

to access the site, type your reverse dns followed by the port number into your browser.
![step eleven](https://user-images.githubusercontent.com/120178527/230675145-9b8e8957-0032-4e58-99b3-c698a601049f.png)
i.e. 000-00-000-237.ip.linodeusercontent.com:5001

If you entered it correctly you'll see this login screen.

Back to our linode console for a moment.
We're going to type in mkdir peppermint
![mkdir](https://user-images.githubusercontent.com/120178527/230675263-fe05dd83-b34d-4117-8251-ba0651c0fbf3.png)
Then type cd peppermint/
![cd](https://user-images.githubusercontent.com/120178527/230675282-e0585157-bbc0-49f0-817f-6f31e7e09062.png)
then nano docker-compose.yml
![nano](https://user-images.githubusercontent.com/120178527/230675305-65b4d0e9-933e-4cd8-965e-cc5b2d0c7ee2.png)

where we will then copy and paste the following text
```
version: "3.1"

 services:
  postgres:
    container_name: postgres
    image: postgres:latest
    restart: always
    volumes:
      - ./docker-data/db:/data/db
    environment:
      POSTGRES_USER: peppermint
      POSTGRES_PASSWORD: 1234
      POSTGRES_DB: peppermint
  client:
    container_name: peppermint
    image: pepperlabs/peppermint:latest
    ports:
      - 5000:5000
    restart: on-failure
    depends_on:
      - postgres
    environment:
      PORT: 5000
       DB_USERNAME: peppermint
       DB_PASSWORD: 1234
       DB_HOST: 'postgres'
       BASE_URL: "http://localhost:5000"
```

After which press CTRL+X, then press Y, and finally hit ENTER to save. This will set your port to 5000 by default. Now lets return to our login page and login with the user name and password we set with that yaml code.

admin@admin.com
1234

You should now be on the dashboard, which looks like this.
![done](https://user-images.githubusercontent.com/120178527/230675411-4d8e0d76-e78a-4886-9829-b92d9b00b6d6.png)







